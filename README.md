# Домашнее задание к занятию "`Название занятия`" - `Фамилия и имя студента`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

Задание 1
Выполните действия, приложите файлы с плейбуками и вывод выполнения.

Напишите три плейбука. При написании рекомендуем использовать текстовый редактор с подсветкой синтаксиса YAML.

Плейбуки должны:

1 Скачать какой-либо архив, создать папку для распаковки и распаковать скаченный архив. Например, можете использовать официальный сайт и зеркало Apache Kafka. При этом можно скачать как исходный код, так и бинарные файлы, запакованные в архив — в нашем задании не принципиально.
2 Установить пакет tuned из стандартного репозитория вашей ОС. Запустить его, как демон — конфигурационный файл systemd появится автоматически при установке. Добавить tuned в автозагрузку.
3 Изменить приветствие системы (motd) при входе на любое другое. Пожалуйста, в этом задании используйте переменную для задания приветствия. Переменную можно задавать любым удобным способом.

Выполнение
1.
```
---
- name: Download and extract Kafka archive
  hosts: all
  become: yes
  vars_prompt:
    - name: "ansible_become_pass"
      prompt: "Enter your sudo password:"
      private: true
  vars:
    archive_url: https://dlcdn.apache.org/kafka/3.4.0/kafka_2.13-3.4.0.tgz
    target_dir: /opt/kafka
  tasks:
    - name: Create directory for extracted files
      file:
        path: "{{ target_dir }}"
        state: directory

```
<img width="1591" height="317" alt="p1" src="https://github.com/user-attachments/assets/21fe1896-19e7-4a09-a08f-a80c9617e1a3" />
<img width="624" height="621" alt="1-1" src="https://github.com/user-attachments/assets/d496964c-2d39-42b1-9994-4042ad2f3b9f" />
<img width="702" height="673" alt="1-12" src="https://github.com/user-attachments/assets/45695185-9086-4d19-958f-a35081dfd5a9" />

2.

```
---
- name: Install and start tuned service
  hosts: all
  become: true
  vars_prompt:
    - name: "ansible_become_pass"
      prompt: "Please enter your sudo password"
      private: true
  tasks:
    - name: Ensure tuned package is installed
      yum:
        name: tuned
        state: present

    - name: Start and enable tuned service
      service:
        name: tuned
        enabled: true
        state: started

```
<img width="1639" height="1183" alt="p2" src="https://github.com/user-attachments/assets/2279d824-2d17-4837-9f7a-103cc4c04f72" />
<img width="1419" height="486" alt="1-1-2" src="https://github.com/user-attachments/assets/34264e6d-5358-4a85-9fda-b85885dd9fe5" />
<img width="1424" height="597" alt="1-1-3" src="https://github.com/user-attachments/assets/3432935a-6f8d-450a-a868-8c5dc4e5dd43" />
3.

```
---
- name: Change MOTD message dynamically
  hosts: all
  become: true
  become_method: sudo
  gather_facts: true
  tasks:
    - name: Set dynamic MOTD with IP address and hostname
      block:
        - name: Generate custom MOTD message
          set_fact:
            motd_message: |
              Welcome to {{ inventory_hostname }}!
              Your IP Address: {{ ansible_default_ipv4.address }}
              Have a great day, Sysadmin!

        - name: Update MOTD with custom greeting
          copy:
            content: "{{ motd_message }}\n"
            dest: /etc/motd
            owner: root
            group: root
            mode: '0644'
```
<img width="1552" height="1030" alt="P3" src="https://github.com/user-attachments/assets/445150f4-34f1-4cfd-ae71-a58049eb6a1b" />
<img width="505" height="118" alt="p1-3" src="https://github.com/user-attachments/assets/4ea4a46a-0975-4c48-a317-2b27588945d7" />
<img width="499" height="111" alt="p1-31" src="https://github.com/user-attachments/assets/88192bb9-aecf-4452-9e78-21076ce3142c" />

Задание 2
Выполните действия, приложите файлы с модифицированным плейбуком и вывод выполнения.

Модифицируйте плейбук из пункта 3, задания 1. В качестве приветствия он должен установить IP-адрес и hostname управляемого хоста, пожелание хорошего дня системному администратору.
Выполнение
```
--
- name: Change MOTD message dynamically
  hosts: all
  become: true
  become_method: sudo
  gather_facts: true
  tasks:
    - name: Set dynamic MOTD with IP address and hostname
      block:
        - name: Generate custom MOTD message
          set_fact:
            motd_message: |
              Приветствую вас на сервере {{ inventory_hostname }}!
              Его IP-адрес: {{ ansible_default_ipv4.address }}

        - name: Update MOTD with custom greeting
          copy:
            content: "{{ motd_message }}\n"
            dest: /etc/motd
            owner: root
            group: root
            mode: '0644'
```
<img width="2183" height="316" alt="Screenshot_22" src="https://github.com/user-attachments/assets/3d1b6d2c-24c8-474e-9a1b-4771f9fd512f" />
<img width="509" height="98" alt="p2-2" src="https://github.com/user-attachments/assets/17f94e4d-f6d2-4f98-8928-0763b58feedc" />
<img width="526" height="94" alt="p2-11" src="https://github.com/user-attachments/assets/5278d7e8-673a-445f-84cb-79b6ffb825b7" />

Задание 3
Выполните действия, приложите архив с ролью и вывод выполнения.

Ознакомьтесь со статьёй «Ansible - это вам не bash», сделайте соответствующие выводы и не используйте модули shell или command при выполнении задания.

Создайте плейбук, который будет включать в себя одну, созданную вами роль. Роль должна:

Установить веб-сервер Apache на управляемые хосты.
Сконфигурировать файл index.html c выводом характеристик каждого компьютера как веб-страницу по умолчанию для Apache. Необходимо включить CPU, RAM, величину первого HDD, IP-адрес. Используйте Ansible facts и jinja2-template. Необходимо реализовать handler: перезапуск Apache только в случае изменения файла конфигурации Apache.
Открыть порт 80, если необходимо, запустить сервер и добавить его в автозагрузку.
Сделать проверку доступности веб-сайта (ответ 200, модуль uri).
В качестве решения:

предоставьте плейбук, использующий роль;
разместите архив созданной роли у себя на Google диске и приложите ссылку на роль в своём решении;
предоставьте скриншоты выполнения плейбука;
предоставьте скриншот браузера, отображающего сконфигурированный index.html в качестве сайта.

`Приведите ответ в свободной форме........`

```
Поле для вставки кода...
....
....
....
....
```

```
Поле для вставки кода...
....
....
....
....
```
```
Поле для вставки кода...
....
....
....
....
```
```
Поле для вставки кода...
....
....
....
....
```
```
Поле для вставки кода...
....
....
....
....
```
```
Поле для вставки кода...
....
....
....
....
```
```
Поле для вставки кода...
....
....
....
....
```
```
Поле для вставки кода...
....
....
....
....
```
```
Поле для вставки кода...
....
....
....
....
```

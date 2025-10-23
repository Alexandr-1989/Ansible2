Задание 1
Выполните действия, приложите файлы с плейбуками и вывод выполнения.

Напишите три плейбука. При написании рекомендуем использовать текстовый редактор с подсветкой синтаксиса YAML.

Плейбуки должны:

1 Скачать какой-либо архив, создать папку для распаковки и распаковать скаченный архив. Например, можете использовать официальный сайт и зеркало Apache Kafka. При этом можно скачать как исходный код, так и бинарные файлы, запакованные в архив — в нашем задании не принципиально.
2 Установить пакет tuned из стандартного репозитория вашей ОС. Запустить его, как демон — конфигурационный файл systemd появится автоматически при установке. Добавить tuned в автозагрузку.
3 Изменить приветствие системы (motd) при входе на любое другое. Пожалуйста, в этом задании используйте переменную для задания приветствия. Переменную можно задавать любым удобным способом.


[playbook-kafka.yml](https://github.com/Alexandr-1989/Ansible2/blob/main/playbook-kafka.yml)

<img width="1591" height="317" alt="p1" src="https://github.com/user-attachments/assets/21fe1896-19e7-4a09-a08f-a80c9617e1a3" />
<img width="624" height="621" alt="1-1" src="https://github.com/user-attachments/assets/d496964c-2d39-42b1-9994-4042ad2f3b9f" />
<img width="702" height="673" alt="1-12" src="https://github.com/user-attachments/assets/45695185-9086-4d19-958f-a35081dfd5a9" />

2.
[playbook-tuned.yml](https://github.com/Alexandr-1989/Ansible2/blob/main/playbook-tuned.yml)
<img width="1639" height="1183" alt="p2" src="https://github.com/user-attachments/assets/2279d824-2d17-4837-9f7a-103cc4c04f72" />
<img width="1419" height="486" alt="1-1-2" src="https://github.com/user-attachments/assets/34264e6d-5358-4a85-9fda-b85885dd9fe5" />
<img width="1424" height="597" alt="1-1-3" src="https://github.com/user-attachments/assets/3432935a-6f8d-450a-a868-8c5dc4e5dd43" />
3.
  [playbook-motd.yml](https://github.com/Alexandr-1989/Ansible2/blob/main/playbook-motd.yml)
<img width="1552" height="1030" alt="P3" src="https://github.com/user-attachments/assets/445150f4-34f1-4cfd-ae71-a58049eb6a1b" />
<img width="505" height="118" alt="p1-3" src="https://github.com/user-attachments/assets/4ea4a46a-0975-4c48-a317-2b27588945d7" />
<img width="499" height="111" alt="p1-31" src="https://github.com/user-attachments/assets/88192bb9-aecf-4452-9e78-21076ce3142c" />

Задание 2
Выполните действия, приложите файлы с модифицированным плейбуком и вывод выполнения.

Модифицируйте плейбук из пункта 3, задания 1. В качестве приветствия он должен установить IP-адрес и hostname управляемого хоста, пожелание хорошего дня системному администратору.

[playbook-motd2.yml](https://github.com/Alexandr-1989/Ansible2/blob/main/playbook-motd2.yml)
<img width="2183" height="316" alt="Screenshot_22" src="https://github.com/user-attachments/assets/3d1b6d2c-24c8-474e-9a1b-4771f9fd512f" />
<img width="509" height="98" alt="p2-2" src="https://github.com/user-attachments/assets/17f94e4d-f6d2-4f98-8928-0763b58feedc" />
<img width="526" height="94" alt="p2-11" src="https://github.com/user-attachments/assets/5278d7e8-673a-445f-84cb-79b6ffb825b7" />

Задание 3
Выполните действия, приложите архив с ролью и вывод выполнения.

Ознакомьтесь со статьёй «Ansible - это вам не bash», сделайте соответствующие выводы и не используйте модули shell или command при выполнении задания.

Создайте плейбук, который будет включать в себя одну, созданную вами роль. Роль должна:

   1 Установить веб-сервер Apache на управляемые хосты.
   2 Сконфигурировать файл index.html c выводом характеристик каждого компьютера как веб-страницу по умолчанию для Apache. Необходимо включить CPU, RAM, величину первого HDD, IP-адрес. Используйте Ansible facts и jinja2-template. Необходимо реализовать handler: перезапуск Apache только в случае изменения файла конфигурации Apache.
   3 Открыть порт 80, если необходимо, запустить сервер и добавить его в автозагрузку.
   4 Сделать проверку доступности веб-сайта (ответ 200, модуль uri).
В качестве решения:

предоставьте плейбук, использующий роль;
разместите архив созданной роли у себя на Google диске и приложите ссылку на роль в своём решении;
предоставьте скриншоты выполнения плейбука;
предоставьте скриншот браузера, отображающего сконфигурированный index.html в качестве сайта.

<img width="1099" height="579" alt="p3" src="https://github.com/user-attachments/assets/21a6e290-efd1-4999-9934-dfce6d302ec6" />

<img width="1111" height="268" alt="Screenshot_6" src="https://github.com/user-attachments/assets/e3fd069a-624f-4e8b-8fbe-0a2cb5ee34a2" />
<img width="1095" height="231" alt="Screenshot_7" src="https://github.com/user-attachments/assets/53bc82c7-0402-4938-ab37-9eb62c728692" />


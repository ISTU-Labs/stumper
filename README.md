# Система автоматизации нанесения авторских логотипов на фотографии "Stamper"

## Цели и задачи

 - Целью разработки является создание WEB-приложения для нанесения на фотографии авторских логотипов;

 Для достижения цели решены следующие задачи:
 - ...

## Архитектура приложения

*Модель приложения* представляет собой вариант шаблона проектирования объектно-ориентированных приложений Model-View-Controller.

 <Архитектура>

A WEB-application to make authors' logos in their photos

## Программное обеспечение

Система разрабатывается согласно руководству с https://docs.pylonsproject.org/projects/pyramid/en/latest/tutorials/wiki2/

 1. Язык программирования - Python-3.6.5 https://python.org;
 2. Среда разработки веб-приложений - Pyramid https://trypyramid.com/;
 3. Шаблоны HTML-страниц Chameleon https://chameleon.readthedocs.io/en/latest/;
 4. Шаблон HTML-сайта Vali Admin https://www.npmjs.com/package/vali-admin;
 6. Библиотека обработки изображений https://pillow.readthedocs.io/en/5.1.x/handbook/tutorial.html;
 7. Библиотека отображения реляционных баз данных на объектную структуру Python https://www.sqlalchemy.org/download.html;
 9. Хранилище данных, включая изображения, реализована при помощи Percona Server (MySQL) https://www.percona.com/software/mysql-database/percona-server;



## Заключение

Во время производственной практики решены следующие задачи:

 1.
 2.

## Приложения

### Запуск сервера Percona

Для того, чтобы запустить виртуальную машину с сервером Percona необходимо выплонить следующую команду:

```shell
$ docker run --name stamper -e MYSQL_ROOT_PASSWORD=stamperpsw -d percona
```

Здесь `-d` обозначает, что запуск виртуальной машины осуществляется в режиме демона.

### Администрирование сервера Percona

MySQL - это программное обеспечение с открытым исходным кодом для управления базами данных, которое помогает пользователям хранить, организовывать и осуществлять доступ к информации. Оно имеет множество вариантов тонкой настройки прав доступа к таблицам и базам данных для каждого пользователя. Данное руководство представит вам краткий обзор некоторых из этих вариантов [....].

#### Создание нового пользователя

Разработанное приложение требует более жестких ограничений, есть способы создания пользователей с особыми наборами прав доступа.

Создание нового пользователя осуществляется в консоли MySQL:

```sql
CREATE USER 'stamper'@'172.%' IDENTIFIED BY 'stamperpsw';
```

К сожалению, на данном этапе пользователь "newuser" не имеет прав делать что-либо с базами данных. На самом деле, даже если если пользователь "newuser" попробует залогиниться (с паролем "stamperpsw"), он не попадет в консоль MySQL.

Таким образом, первое, что нам необходимо сделать, это предоставить пользователю доступ к информации, которая ему потребуется.

```sql
GRANT ALL PRIVILEGES ON *.* TO 'stamper'@'172.%';
```

Звездочки в этой команде задают базу и таблицу, соответственно, к которым у пользователя будет доступ. Конкретно эта команда позволяет пользователю читать, редактировать, выполнять любые действия над всеми базами данных и таблицами.

Поле завершения настройки прав доступа новых пользователей, убедитесь, что вы обновили все права доступа:

```
FLUSH PRIVILEGES;
```

Проверка подключения:

```shell
mysql -h 172.17.0.2 -u stamper -pstamperpsw mysql
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MySQL connection id is 3
Server version: 5.7.21-21 Percona Server (GPL), Release '21', Revision '2a37e4e'

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MySQL [mysql]>
```

Командная строка MySQL запустилась, следовательно, аутентификация пользователя прошла успешно.



## Список использованных источников

 1.

 2.
 10. Создание нового пользователя и настройка прав доступа в MySQL | DigitalOcean URL:https://www.digitalocean.com/community/tutorials/mysql-ru .

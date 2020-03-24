#Локальный пользователь по-умолчанию
```
snuffy@linux-learn:~$ sudo vim /etc/mysql/my.cnf
```
[mysql]
user=root

password=karramba
```
snuffy@linux-learn:~$ chmod 0600 ~/my.cnf
```
#Необходимость делать ДЗ удаленно, для подключения со смартфона
```
snuffy@linux-learn:~$ sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
```
[mysqld]
port = 3306

bind_address = 0.0.0.0 # Changed to allow remote connections
```
snuffy@linux-learn:~$ sudo systemctl restart mysql
```
```
snuffy@linux-learn:~$ sudo mysql
```
```
#Создаём пользователя для удалённых подключений (DBeaver/Workbench client с хост машины win7,
#RemoDB client on Android со смартфона) c полным доступом ко всем БД (как root)
mysql> CREATE USER 'snuffy'@'%' IDENTIFIED BY 'my_own_password';
mysql> GRANT ALL ON *.* TO 'snuffy'@'%';
mysql> FLUSH PRIVILEGES;

#Создаем БД
mysql> DROP DATABASE IF EXIST example;
mysql> CREATE DATABASE example;
mysql> USE example;

#Создаем Таблицу
mysql> DROP TABLE IF EXIST users;
mysql> CREATE TABLE users (
id SERIAL PRIMARY KEY,
name VARCHAR(255)
) COMMENT = 'Пользователи';

mysql>/q

#Создаем дамп БД example
mysqldump example > example_db_dump.sql

#Разворачиваем дамп в БД sample
mysql sample < example_db_dump.sql

#Создаем дамп первых 100 строк таблицы help_keyword БД mysql
snuffy@linux-learn:~$ mysqldump --where="true limit 100" mysql help_keyword > /home/snuffy/sandbox_dump.sql

######## sql файлы будут приложены ближе к уроку как буду дома, на удалённой тачке пропал инет (-

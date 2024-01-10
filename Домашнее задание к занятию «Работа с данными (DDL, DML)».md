# Домашнее задание к занятию «Работа с данными (DDL/DML)» Мальков Григорий

### Инструкция по выполнению домашнего задания

1. Сделайте fork [репозитория c шаблоном решения](https://github.com/netology-code/sys-pattern-homework) к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
2. Выполните клонирование этого репозитория к себе на ПК с помощью команды `git clone`.
3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
   - впишите вверху название занятия и ваши фамилию и имя;
   - в каждом задании добавьте решение в требуемом виде: текст/код/скриншоты/ссылка;
   - для корректного добавления скриншотов воспользуйтесь инструкцией [«Как вставить скриншот в шаблон с решением»](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md);
   - при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в [инструкции по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md).
4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`).
5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
6. Любые вопросы задавайте в чате учебной группы и/или в разделе «Вопросы по заданию» в личном кабинете.

Желаем успехов в выполнении домашнего задания.

---

Задание можно выполнить как в любом IDE, так и в командной строке.

### Задание 1
1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

1.2. Создайте учётную запись sys_temp. 

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)

1.4. Дайте все права для пользователя sys_temp. 

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

1.6. Переподключитесь к базе данных от имени sys_temp.

Для смены типа аутентификации с sha2 используйте запрос: 
```sql
ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
1.6. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

1.7. Восстановите дамп в базу данных.

1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

*Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.*

### Ответ:
1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.
```sh
sudo apt update
sudo apt install gnupg
wget https://dev.mysql.com/get/mysql-apt-config_0.8.22-1_all.deb
sudo dpkg -i mysql-apt-config_0.8.22-1_all.deb
sudo apt update
sudo apt install mysql-client mysql-server
```

1.2. Создайте учётную запись sys_temp. 
```sql
mysql -u root -p 
create user 'sys_temp'@'localhost' identified by '7rgi4Pj3RR';
exit
```

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)
```sql
mysql -u root -p 
select user from mysql.user;
exit
```
![Снимок экрана от 2024-01-10 20-20-57](https://github.com/Gr1ck01/homework-12-netology/assets/56309750/3505f2b6-6bfa-4fea-942b-6fc6001dc298)

1.4. Дайте все права для пользователя sys_temp. 
```sql
mysql -u root -p 
grant all privilegies on *.* to 'sys_temp'@'localhost';
```

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)
```sql
mysql -u root -p 
show grants for 'sys_temp'@'localhost';
```
![Снимок экрана от 2024-01-10 20-26-17](https://github.com/Gr1ck01/homework-12-netology/assets/56309750/e565e66d-d0f2-4e3f-9138-ecbddb6d76b7)

1.6. Переподключитесь к базе данных от имени sys_temp.

Для смены типа аутентификации с sha2 используйте запрос: 
```
ALTER USER 'sys_temp'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
### запрос:
```sql
mysql -u sys_temp -p 
alter user 'sys_temp'@'localhost' IDENTIFIED with mysql_native_password by '7rgi4Pj3RR';
exit
```

1.6. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.
```sh
wget -c https://downloads.mysql.com/docs/sakila-db.zip
unzip sakila-db.zip
cd sakila-db
```

1.7. Восстановите дамп в базу данных.
```sql
mysql -u sys_temp -p
show databases;
create database SakilaDB;
show databases;
use SakilaDB;
show tables;
source sakila-schema.sql;
source sakila-data.sql;
show tables;
exit
```

1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)
```sql
mysql -u sys_temp -p
show databases;
use SakilaDB;
show tables;
exit
```
![Снимок экрана от 2024-01-10 20-45-33](https://github.com/Gr1ck01/homework-12-netology/assets/56309750/b9100e28-869a-4435-87f6-98298f87c1e9)

![Снимок экрана от 2024-01-10 20-50-41](https://github.com/Gr1ck01/homework-12-netology/assets/56309750/a6ddd343-2c3a-47ed-b566-a1c73061e9f1)


### Задание 2
Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц. Пример: (скриншот/текст)
```
Название таблицы | Название первичного ключа
customer         | customer_id
```

![изображение](https://github.com/Gr1ck01/homework-12-netology/assets/56309750/de867d11-0722-4f1d-b156-05e0361cb909)



## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### Задание 3*
3.1. Уберите у пользователя sys_temp права на внесение, изменение и удаление данных из базы sakila.

3.2. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

*Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.*

### Ответ

3.1. Уберите у пользователя sys_temp права на внесение, изменение и удаление данных из базы sakila.
```sql
mysql -u root -p 
show grants for 'sys_temp'@'localhost';
grant ALL PRIVILEGES on sakila.* to 'sys_temp'@'localhost';
revoke INSERT, UPDATE, DELETE on sakila.* from 'sys_temp'@'localhost';
show grants for 'sys_temp'@'localhost';
```
3.2. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)
```sql
mysql -u root -p 
show grants for 'sys_temp'@'localhost';
exit
```

![изображение](https://github.com/Gr1ck01/homework-12-netology/assets/56309750/3494adb7-df50-49c9-82e0-ed44ba370865)




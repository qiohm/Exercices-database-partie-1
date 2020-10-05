# Exercices-database-partie-1
rendu en README.md d'exercices de créeation de DataBase avec psql


postgres=> CREATE DATABASE db_1;
CREATE DATABASE

postgres=> \list
                          List of databases
   Name    |  Owner  | Encoding | Collate | Ctype | Access privileges
-----------+---------+----------+---------+-------+-------------------
 db_1      | db_user | UTF8     | C       | C     |
 postgres  | qiohm   | UTF8     | C       | C     |
 template0 | qiohm   | UTF8     | C       | C     | =c/qiohm         +
           |         |          |         |       | qiohm=CTc/qiohm
 template1 | qiohm   | UTF8     | C       | C     | =c/qiohm         +
           |         |          |         |       | qiohm=CTc/qiohm
(4 rows)

postgres=> \c db_1
You are now connected to database "db_1" as user "db_user".


postgres=> \c db_1
You are now connected to database "db_1" as user "db_user".
db_1=> CREATE TABLE users (id SERIAL PRIMARY KEY, name VARCHAR(30), password VARCHAR(30));
CREATE TABLE

db_1=> INSERT INTO users (name, password) VALUES ('alice', '123'), ('bob', '456'), ('charlie','789');
INSERT 0 3
db_1=> SELECT * FROM users;
 id |  name   | password
----+---------+----------
  1 | alice   | 123
  2 | bob     | 456
  3 | charlie | 789
(3 rows)

db_1=> INSERT INTO users (name, password) VALUES ('dan', '101112'), ('eve', '131415'), ('faythe', '161718');
INSERT 0 3
db_1=> SELECT * FROM users;
 id |  name   | password
----+---------+----------
  1 | alice   | 123
  2 | bob     | 456
  3 | charlie | 789
  4 | dan     | 101112
  5 | eve     | 131415
  6 | faythe  | 161718
(6 rows)

db_1=> SELECT * FROM users WHERE LENGTH(password) > 3;
 id |  name  | password
----+--------+----------
  4 | dan    | 101112
  5 | eve    | 131415
  6 | faythe | 161718
(3 rows)

db_1=> ALTER TABLE users ADD COLUMN bio TEXT DEFAULT 'Hello World!';
ALTER TABLE
db_1=> SELECT * FROM users;
 id |  name   | password |     bio
----+---------+----------+--------------
  1 | alice   | 123      | Hello World!
  2 | bob     | 456      | Hello World!
  3 | charlie | 789      | Hello World!
  4 | dan     | 101112   | Hello World!
  5 | eve     | 131415   | Hello World!
  6 | faythe  | 161718   | Hello World!
(6 rows)

db_1=> UPDATE users SET bio = 'hello,i am '||(name);
UPDATE 6
db_1=> SELECT * FROM users;
 id |  name   | password |        bio
----+---------+----------+--------------------
  1 | alice   | 123      | hello,i am alice
  2 | bob     | 456      | hello,i am bob
  3 | charlie | 789      | hello,i am charlie
  4 | dan     | 101112   | hello,i am dan
  5 | eve     | 131415   | hello,i am eve
  6 | faythe  | 161718   | hello,i am faythe
(6 rows)

db_1=> SELECT * FROM users ORDER BY id DESC LIMIT 2;
 id |  name  | password |        bio
----+--------+----------+-------------------
  6 | faythe | 161718   | hello,i am faythe
  5 | eve    | 131415   | hello,i am eve
(2 rows)

db_1=> SELECT * FROM users WHERE id%2=1;
 id |  name   | password |        bio
----+---------+----------+--------------------
  1 | alice   | 123      | hello,i am alice
  3 | charlie | 789      | hello,i am charlie
  5 | eve     | 131415   | hello,i am eve
(3 rows)

db_1=> DELETE FROM users WHERE id%2=0;
DELETE 3
db_1=> SELECT * FROM users;
 id |  name   | password |        bio
----+---------+----------+--------------------
  1 | alice   | 123      | hello,i am alice
  3 | charlie | 789      | hello,i am charlie
  5 | eve     | 131415   | hello,i am eve
(3 rows)

db_1=> DROP TABLE users;
DROP TABLE

db_1=> \c postgres
You are now connected to database "postgres" as user "db_user".
postgres=> DROP DATABASE db_1;
DROP DATABASE

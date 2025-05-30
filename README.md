# sql_assignment
C:\Users\Minfy>psql -U postgres
Password for user postgres:

psql (17.5)
WARNING: Console code page (850) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

postgres=# CREATE DATABASE mydb;
CREATE DATABASE
postgres=# \c mydb
You are now connected to database "mydb" as user "postgres".
mydb=# CREATE TABLE users (
mydb(#     id SERIAL PRIMARY KEY,
mydb(#     name VARCHAR(100),
mydb(#     email VARCHAR(100)
mydb(# );
CREATE TABLE
mydb=# INSERT INTO users (name, email) VALUES ('Shybash', 'shybash@example.com');
INSERT 0 1
mydb=# SELECT * FROM users;
 id |  name   |        email
----+---------+---------------------
  1 | Shybash | shybash@example.com
(1 row)


mydb=# \l
                                                            List of databases
   Name    |  Owner   | Encoding | Locale Provider |      Collate       |       Ctype        | Locale | ICU Rules |   Access privileges
-----------+----------+----------+-----------------+--------------------+--------------------+--------+-----------+-----------------------
 mydb      | postgres | UTF8     | libc            | English_India.1252 | English_India.1252 |        |           |
 postgres  | postgres | UTF8     | libc            | English_India.1252 | English_India.1252 |        |           |
 template0 | postgres | UTF8     | libc            | English_India.1252 | English_India.1252 |        |           | =c/postgres          +
           |          |          |                 |                    |                    |        |           | postgres=CTc/postgres
 template1 | postgres | UTF8     | libc            | English_India.1252 | English_India.1252 |        |           | =c/postgres          +
           |          |          |                 |                    |                    |        |           | postgres=CTc/postgres
(4 rows)


mydb=# \q

C:\Users\Minfy>psql -U postgres
Password for user postgres:

psql (17.5)
WARNING: Console code page (850) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

postgres=# create user shybash_admin with password "shybash";
ERROR:  syntax error at or near ""shybash""
LINE 1: create user shybash_admin with password "shybash";
                                                ^
postgres=# create database university_db owner shybash_admin;
ERROR:  role "shybash_admin" does not exist
postgres=# create user shybash_admin with password 'shybash';
CREATE ROLE
postgres=# create database university_db owner shybash_admin;
CREATE DATABASE
postgres=# grant all privileges on database university_db to shybash_admin
postgres-# \q

C:\Users\Minfy>psql -u shybash_admin -d university_db;
psql: illegal option -- u
psql: hint: Try "psql --help" for more information.

C:\Users\Minfy>psql -u shybash_admin -d university_db;
psql: illegal option -- u
psql: hint: Try "psql --help" for more information.

C:\Users\Minfy>psql -U shybash_admin -d university_db;
Password for user shybash_admin:

psql: error: connection to server at "localhost" (::1), port 5432 failed: FATAL:  password authentication failed for user "shybash_admin"

C:\Users\Minfy>psql -U shybash_admin -d university_db;
Password for user shybash_admin:

psql: error: connection to server at "localhost" (::1), port 5432 failed: FATAL:  password authentication failed for user "shybash_admin"

C:\Users\Minfy>psql -U shybash_admin -d university_db;
Password for user shybash_admin:

psql: error: connection to server at "localhost" (::1), port 5432 failed: FATAL:  database "university_db;" does not exist

C:\Users\Minfy>psql -U shybash_admin -d university_db;
Password for user shybash_admin:

psql: error: connection to server at "localhost" (::1), port 5432 failed: FATAL:  database "university_db;" does not exist

C:\Users\Minfy>psql -U shybash_admin -d university_db;
Password for user shybash_admin:

psql: error: connection to server at "localhost" (::1), port 5432 failed: FATAL:  password authentication failed for user "shybash_admin"

C:\Users\Minfy>psql -U shybash_admin -d university_db;
Password for user shybash_admin:

psql: error: connection to server at "localhost" (::1), port 5432 failed: FATAL:  database "university_db;" does not exist

C:\Users\Minfy>psql -U postgres
Password for user postgres:

psql: error: connection to server at "localhost" (::1), port 5432 failed: FATAL:  password authentication failed for user "postgres"

C:\Users\Minfy>psql -U shybash_admin -d university_db;
Password for user shybash_admin:

psql: error: connection to server at "localhost" (::1), port 5432 failed: FATAL:  database "university_db;" does not exist

C:\Users\Minfy>psql -U shybash_admin -d university_db
Password for user shybash_admin:

psql (17.5)
WARNING: Console code page (850) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

university_db=> CREATE TABLE students (
university_db(>     student_id INTEGER,
university_db(>     first_name VARCHAR(50),
university_db(>     last_name VARCHAR(50),
university_db(>     email VARCHAR(100),
university_db(>     date_of_birth DATE
university_db(> );
CREATE TABLE
university_db=> \d
             List of relations
 Schema |   Name   | Type  |     Owner
--------+----------+-------+---------------
 public | students | table | shybash_admin
(1 row)


university_db=> ALTER TABLE students ADD COLUMN enrollment_date DATE;
ALTER TABLE
university_db=> ALTER TABLE students DROP COLUMN enrollment_date;
ALTER TABLE
university_db=> ALTER TABLE students ALTER COLUMN email TYPE VARCHAR(150);
ALTER TABLE
university_db=> ALTER TABLE students RENAME COLUMN date_of_birth TO dob;
ALTER TABLE
university_db=> ALTER TABLE students ADD CONSTRAINT unique_email UNIQUE (email);
ALTER TABLE
university_db=> -- Re-create students table if previously dropped in activity
university_db=> CREATE TABLE students (
university_db(>     student_id INTEGER,
university_db(>     first_name VARCHAR(50),
university_db(>     last_name VARCHAR(50),
university_db(>     email VARCHAR(100),
university_db(>     dob DATE
university_db(> );
ERROR:  relation "students" already exists
university_db=>
university_db=> -- insert your best frnd names
university_db=>
university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob)
university_db-> VALUES (1, 'Alice', 'Smith', 'alice.smith@example.com', '2003-05-15');
INSERT 0 1
university_db=>
university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob)
university_db-> VALUES (2, 'Bob', 'Johnson', 'bob.johnson@example.com', '2002-08-22'),
university_db->        (3, 'Charlie', 'Brown', 'charlie.brown@example.com', '2003-01-10');
INSERT 0 2
university_db=> SELECT first_name, last_name, email FROM students;
 first_name | last_name |           email
------------+-----------+---------------------------
 Alice      | Smith     | alice.smith@example.com
 Bob        | Johnson   | bob.johnson@example.com
 Charlie    | Brown     | charlie.brown@example.com
(3 rows)


university_db=> SELECT * FROM students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(3 rows)


university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob)
university_db-> VALUES (4, 'pulice', 'Smith', pulice.smith@example.com', '2003-05-15');
university_db'> SELECT * FROM students;
university_db'> SELECT first_name, last_name, email FROM students;
university_db'> INSERT INTO students (student_id, first_name, last_name, email, dob)
university_db'> VALUES (4, 'Pulice', 'Smith', 'pulice.smith@example.com', '2003-05-15');
university_db'> INSERT INTO students (student_id, first_name, last_name, email, dob)
university_db'> VALUES (5, 'Aarav', 'Patel', 'aarav.patel@example.com', '2002-11-23');
university_db'> SELECT * FROM students;
university_db'> \q

C:\Users\Minfy>psql -U shybash_admin -d university_db;
Password for user shybash_admin:

psql: error: connection to server at "localhost" (::1), port 5432 failed: FATAL:  password authentication failed for user "shybash_admin"

C:\Users\Minfy>psql -U shybash_admin -d university_db
Password for user shybash_admin:

psql (17.5)
WARNING: Console code page (850) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

university_db=> select *from students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(3 rows)


university_db=> select *from students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(3 rows)


university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob)
university_db-> VALUES (4, 'Pulice', 'Smith', 'pulice.smith@example.com', '2003-05-15');
INSERT 0 1
university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob)
university_db-> VALUES (5, 'Aarav', 'Patel', 'aarav.patel@example.com', '2002-11-23');
INSERT 0 1
university_db=> select *from students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | Pulice     | Smith     | pulice.smith@example.com  | 2003-05-15
          5 | Aarav      | Patel     | aarav.patel@example.com   | 2002-11-23
(5 rows)


university_db=> SELECT * FROM students WHERE student_id = 1;
 student_id | first_name | last_name |          email          |    dob
------------+------------+-----------+-------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com | 2003-05-15
(1 row)


university_db=> SELECT * FROM students WHERE student_id = 1;
 student_id | first_name | last_name |          email          |    dob
------------+------------+-----------+-------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com | 2003-05-15
(1 row)


university_db=>
university_db=> SELECT first_name, last_name FROM students WHERE last_name = 'Smith';
 first_name | last_name
------------+-----------
 Alice      | Smith
 Pulice     | Smith
(2 rows)


university_db=>
university_db=> SELECT * FROM students WHERE dob >= '2003-01-01'; -- Students born in or after 2003
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | Pulice     | Smith     | pulice.smith@example.com  | 2003-05-15
(3 rows)


university_db=>
university_db=> SELECT * FROM students WHERE dob BETWEEN '2002-01-01' AND '2002-12-31'; -- Born in 2002
 student_id | first_name | last_name |          email          |    dob
------------+------------+-----------+-------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com | 2002-08-22
          5 | Aarav      | Patel     | aarav.patel@example.com | 2002-11-23
(2 rows)


university_db=>
university_db=> SELECT * FROM students WHERE first_name LIKE 'A%';
 student_id | first_name | last_name |          email          |    dob
------------+------------+-----------+-------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com | 2003-05-15
          5 | Aarav      | Patel     | aarav.patel@example.com | 2002-11-23
(2 rows)


university_db=>
university_db=> SELECT * FROM students WHERE email ILIKE '%.com'; -- Case-insensitive ends with .com
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | Pulice     | Smith     | pulice.smith@example.com  | 2003-05-15
          5 | Aarav      | Patel     | aarav.patel@example.com   | 2002-11-23
(5 rows)


university_db=>
university_db=> SELECT * FROM students WHERE first_name = 'Alice' AND last_name = 'Smith';
 student_id | first_name | last_name |          email          |    dob
------------+------------+-----------+-------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com | 2003-05-15
(1 row)


university_db=>
university_db=> SELECT * FROM students WHERE student_id = 1 OR student_id = 3;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(2 rows)


university_db=>
university_db=> SELECT * FROM students WHERE student_id IN (1, 3, 5);
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          5 | Aarav      | Patel     | aarav.patel@example.com   | 2002-11-23
(3 rows)


university_db=> -- Add a student with a NULL email to test IS NULL
university_db=>
university_db=> INSERT INTO students (student_id, first_name, last_name, dob) VALUES (4, 'Diana', 'Prince', '2001-11-01');
INSERT 0 1
university_db=>
university_db=> SELECT * FROM students WHERE email IS NULL;
 student_id | first_name | last_name | email |    dob
------------+------------+-----------+-------+------------
          4 | Diana      | Prince    |       | 2001-11-01
(1 row)


university_db=>
university_db=> SELECT * FROM students WHERE email IS NOT NULL;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | Pulice     | Smith     | pulice.smith@example.com  | 2003-05-15
          5 | Aarav      | Patel     | aarav.patel@example.com   | 2002-11-23
(5 rows)


university_db=> select *from student desc;
ERROR:  syntax error at or near "desc"
LINE 1: select *from student desc;
                             ^
university_db=> select *from students desc;
ERROR:  syntax error at or near "desc"
LINE 1: select *from students desc;
                              ^
university_db=> select *from students order by last_name desc;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          4 | Pulice     | Smith     | pulice.smith@example.com  | 2003-05-15
          4 | Diana      | Prince    |                           | 2001-11-01
          5 | Aarav      | Patel     | aarav.patel@example.com   | 2002-11-23
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(6 rows)


university_db=> select *from students order by dob desc;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          4 | Pulice     | Smith     | pulice.smith@example.com  | 2003-05-15
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          5 | Aarav      | Patel     | aarav.patel@example.com   | 2002-11-23
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          4 | Diana      | Prince    |                           | 2001-11-01
(6 rows)


university_db=> select *from students order by last_name  asc,first_name des;
ERROR:  syntax error at or near "des"
LINE 1: ...elect *from students order by last_name  asc,first_name des;
                                                                   ^
university_db=> select *from students order by last_name ,first_name;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          5 | Aarav      | Patel     | aarav.patel@example.com   | 2002-11-23
          4 | Diana      | Prince    |                           | 2001-11-01
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          4 | Pulice     | Smith     | pulice.smith@example.com  | 2003-05-15
(6 rows)


university_db=> select *from students order by first_name offset 2;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | Diana      | Prince    |                           | 2001-11-01
          4 | Pulice     | Smith     | pulice.smith@example.com  | 2003-05-15
(4 rows)


university_db=> select *from students order by first_name offset 2 limit;
ERROR:  syntax error at or near ";"
LINE 1: select *from students order by first_name offset 2 limit;
                                                                ^
university_db=> select *from students order by first_name offset 2 limit 2;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(2 rows)


university_db=> select *from students order by first_name limit 2 offset 2;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(2 rows)


university_db=> select *from students order by dob desc limit 2;
 student_id | first_name | last_name |          email           |    dob
------------+------------+-----------+--------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com  | 2003-05-15
          4 | Pulice     | Smith     | pulice.smith@example.com | 2003-05-15
(2 rows)


university_db=> select *from students order by dob asc limit 2;
 student_id | first_name | last_name |          email          |    dob
------------+------------+-----------+-------------------------+------------
          4 | Diana      | Prince    |                         | 2001-11-01
          2 | Bob        | Johnson   | bob.johnson@example.com | 2002-08-22
(2 rows)


university_db=> select *from students order by student_id limit 2 offset 1;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(2 rows)


university_db=> select distinct last_name from university_db;
ERROR:  relation "university_db" does not exist
LINE 1: select distinct last_name from university_db;
                                       ^
university_db=> select distinct last_name from students;
 last_name
-----------
 Smith
 Patel
 Johnson
 Prince
 Brown
(5 rows)


university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob)
university_db-> VALUES (4, 'Pulice', 'Smith', 'pulice.smith@example.com', '2003-05-15');
ERROR:  duplicate key value violates unique constraint "unique_email"
DETAIL:  Key (email)=(pulice.smith@example.com) already exists.
university_db=> select distinct last_name from students;
 last_name
-----------
 Smith
 Patel
 Johnson
 Prince
 Brown
(5 rows)


university_db=> select SELECT COUNT(*) AS total_students FROM students;
ERROR:  syntax error at or near "SELECT"
LINE 1: select SELECT COUNT(*) AS total_students FROM students;
               ^
university_db=> SELECT COUNT(*) AS total_students FROM students;
 total_students
----------------
              6
(1 row)


university_db=> SELECT MIN(dob) AS oldest_student_dob FROM students;
 oldest_student_dob
--------------------
 2001-11-01
(1 row)


university_db=> SELECT MAX(dob) AS youngest_student_dob FROM students;
 youngest_student_dob
----------------------
 2003-05-15
(1 row)


university_db=> select count(*) as students_email with email from students;
ERROR:  syntax error at or near "with"
LINE 1: select count(*) as students_email with email from students;
                                          ^
university_db=> select count(*) as students_email  from students;
 students_email
----------------
              6
(1 row)


university_db=> select distinct count(*) from students;
 count
-------
     6
(1 row)


university_db=> select distinct count(*) as number of students from students
university_db-> group by \q

C:\Users\Minfy>psql -u shybash_admin -d university_db;
psql: illegal option -- u
psql: hint: Try "psql --help" for more information.

C:\Users\Minfy>psql -U shybash_admin -d university_db;
Password for user shybash_admin:

psql: error: connection to server at "localhost" (::1), port 5432 failed: FATAL:  database "university_db;" does not exist

C:\Users\Minfy>psql -U shybash_admin -d university_db
Password for user shybash_admin:

psql (17.5)
WARNING: Console code page (850) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

university_db=> select last_name ,count(*) as number_of_students
university_db-> from students
university_db-> group by last_name
university_db-> order by desc
university_db-> ;
ERROR:  syntax error at or near "desc"
LINE 4: order by desc
                 ^
university_db=> select last_name ,count(*) as number_of_students
university_db-> from students
university_db-> group by last_name
university_db-> order by desc;
ERROR:  syntax error at or near "desc"
LINE 4: order by desc;
                 ^
university_db=> select last_name ,count(*) as number_of_students
university_db-> from students
university_db-> group by last_name
university_db-> order by last_name desc;
 last_name | number_of_students
-----------+--------------------
 Smith     |                  2
 Prince    |                  1
 Patel     |                  1
 Johnson   |                  1
 Brown     |                  1
(5 rows)


university_db=> select last_name,count(*) as number_of_students
university_db-> from students
university_db-> group last_name
university_db-> group last_name
university_db-> ;
ERROR:  syntax error at or near "last_name"
LINE 3: group last_name
              ^
university_db=> select last_name,count(*) as number_of_students
university_db-> from students
university_db-> group by last_name
university_db-> having count(*)>1
university_db-> order by number_of_students desc;
 last_name | number_of_students
-----------+--------------------
 Smith     |                  2
(1 row)


university_db=> select first_name,count(*) as number_of_students
university_db-> from students
university_db-> group by first_name
university_db-> order by number_of_students desc;
 first_name | number_of_students
------------+--------------------
 Pulice     |                  1
 Alice      |                  1
 Bob        |                  1
 Aarav      |                  1
 Charlie    |                  1
 Diana      |                  1
(6 rows)


university_db=> drop table if exist students;
ERROR:  syntax error at or near "exist"
LINE 1: drop table if exist students;
                      ^
university_db=> drop table if exists students;
DROP TABLE
university_db=> create table students(student_id INTEGER primary key,
university_db(> first_name varchar(50) NOT NULL,
university_db(> last_name varchar(50) NOT NULL,
university_db(> email varchar(50) unique,
university_db(> dob DATE,
university_db(> enrollment_status varchar(10) check (enrollment_status IN('enrolled','graduated','dropped')));
CREATE TABLE
university_db=> select *from students;
 student_id | first_name | last_name | email | dob | enrollment_status
------------+------------+-----------+-------+-----+-------------------
(0 rows)


university_db=> INSERT INTO students (student_id, last_name, email, dob) VALUES (1, 'shybash', 'shybash@gmail.com', '2000-01-01')
university_db-> ;
ERROR:  null value in column "first_name" of relation "students" violates not-null constraint
DETAIL:  Failing row contains (1, null, shybash, shybash@gmail.com, 2000-01-01, null).
university_db=> INSERT INTO students (student_id, first_name,last_name, email, dob) VALUES (1, 'shybash','shaik', 'shybash@gmail.com', '2000-01-01');
INSERT 0 1
university_db=> INSERT INTO students (student_id, first_name,last_name, email, dob) VALUES (1, 'shybash','shaik', 'shybash@gmail.com', '2000-01-01');
ERROR:  duplicate key value violates unique constraint "students_pkey"
DETAIL:  Key (student_id)=(1) already exists.
university_db=> INSERT INTO students (student_id, first_name,last_name, email, dob) VALUES (2, 'revi','ree', 'revi@gmail.com', '2000-01-01');
INSERT 0 1
university_db=> select *from students;
 student_id | first_name | last_name |       email       |    dob     | enrollment_status
------------+------------+-----------+-------------------+------------+-------------------
          1 | shybash    | shaik     | shybash@gmail.com | 2000-01-01 |
          2 | revi       | ree       | revi@gmail.com    | 2000-01-01 |
(2 rows)


university_db=> INSERT INTO students (student_id, first_name,last_name, email, dob) VALUES ('shybash','shaik', 'sybash@gmail.com', '2000-01-01');
ERROR:  INSERT has more target columns than expressions
LINE 1: ...tudents (student_id, first_name,last_name, email, dob) VALUE...
                                                             ^
university_db=> INSERT INTO students (first_name,last_name, email, dob) VALUES ('shybash','shaik', 'sybash@gmail.com', '2000-01-01');
ERROR:  null value in column "student_id" of relation "students" violates not-null constraint
DETAIL:  Failing row contains (null, shybash, shaik, sybash@gmail.com, 2000-01-01, null).
university_db=> create table courses(
university_db(> course_id SERIAL primary key,
university_db(> course_name varchar(100) not null unique,
university_db(> credits integer check (credits >0 and credits<10));
CREATE TABLE
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Introduction to SQL', 3);
INSERT 0 1
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Database Design', 4);
INSERT 0 1
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Web Development', 3);
INSERT 0 1
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Data Structures', 4);
INSERT 0 1
university_db=> select *from courses;
 course_id |     course_name     | credits
-----------+---------------------+---------
         1 | Introduction to SQL |       3
         2 | Database Design     |       4
         3 | Web Development     |       3
         4 | Data Structures     |       4
(4 rows)


university_db=> CREATE TABLE enrollments (
university_db(>     enrollment_id SERIAL PRIMARY KEY,
university_db(>     student_id INTEGER NOT NULL,
university_db(>     course_id INTEGER NOT NULL,
university_db(>     enrollment_date DATE DEFAULT CURRENT_DATE, -- Sets default if not specified
university_db(>     grade CHAR(1) CHECK (grade IN ('A', 'B', 'C', 'D', 'F', 'W', NULL)), -- W for withdraw, NULL if not graded
university_db(>
university_db(>     -- Foreign Key constraint for student_id
university_db(>     CONSTRAINT fk_student
university_db(>         FOREIGN KEY (student_id)
university_db(>         REFERENCES students(student_id)
university_db(>         ON DELETE CASCADE, -- If a student is deleted, their enrollments are also deleted.
university_db(>                            -- Other options: ON DELETE RESTRICT, ON DELETE SET NULL, ON DELETE SET DEFAULT
university_db(>
university_db(>     -- Foreign Key constraint for course_id
university_db(>     CONSTRAINT fk_course
university_db(>         FOREIGN KEY (course_id)
university_db(>         REFERENCES courses(course_id)
university_db(>         ON DELETE RESTRICT, -- (Default if not specified) Prevent deleting a course if students are enrolled.
university_db(>
university_db(>     -- Ensure a student cannot enroll in the same course multiple times (if semester isn't a factor)
university_db(>     UNIQUE (student_id, course_id)
university_db(> );
CREATE TABLE
university_db=> select *from enrollments;
 enrollment_id | student_id | course_id | enrollment_date | grade
---------------+------------+-----------+-----------------+-------
(0 rows)


university_db=> INSERT INTO enrollments (student_id, course_id, grade) VALUES (1, 1, 'A');
INSERT 0 1
university_db=> INSERT INTO enrollments (student_id, course_id) VALUES (1, 2); -- Grade will be NULL
INSERT 0 1
university_db=> select *from enrollments;
 enrollment_id | student_id | course_id | enrollment_date | grade
---------------+------------+-----------+-----------------+-------
             1 |          1 |         1 | 2025-05-30      | A
             2 |          1 |         2 | 2025-05-30      |
(2 rows)


university_db=> INSERT INTO enrollments (student_id, course_id, grade) VALUES (2, 1, 'B');
INSERT 0 1
university_db=> SELECT * FROM students WHERE student_id = 1;
student_id | first_name | last_name |       email       |    dob     | enrollment_status
------------+------------+-----------+-------------------+------------+-------------------
          1 | shybash    | shaik     | shybash@gmail.com | 2000-01-01 |

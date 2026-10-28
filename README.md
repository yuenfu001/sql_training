Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| abdurrahman        |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.11 sec)

mysql> use abdurrahman;
Database changed
mysql> show tables;
+-----------------------+
| Tables_in_abdurrahman |
+-----------------------+
| info                  |
| profile               |
| registration          |
+-----------------------+
3 rows in set (0.02 sec)

mysql> select * from info;
+----+-----------------------+------------+--------+----------+
| id | user                  | department | salary | rev_gen  |
+----+-----------------------+------------+--------+----------+
|  1 | abdurrahman@gmail.com | IT         | 250000 |  1000000 |
|  2 | ammaarliu@gmail.com   | Sales      | 300000 |  2000000 |
|  3 | liuyuenfu@gmail.com   | Legal      | 100000 | 12000000 |
|  4 | mahmud2027@gmail.com  | Legal      | 500000 |  1200000 |
|  5 | something@gmail.com   | Sales      | 700000 |   120000 |
+----+-----------------------+------------+--------+----------+
5 rows in set (0.05 sec)

mysql> select department, SUM(rev_gen) AS total_rev_gen from info GROUP BY department ORDER BY total_rev_gen DESC;
+------------+---------------+
| department | total_rev_gen |
+------------+---------------+
| Legal      |      13200000 |
| Sales      |       2120000 |
| IT         |       1000000 |
+------------+---------------+
3 rows in set (0.01 sec)

mysql> select * from info order by salary DESC;
+----+-----------------------+------------+--------+----------+
| id | user                  | department | salary | rev_gen  |
+----+-----------------------+------------+--------+----------+
|  5 | something@gmail.com   | Sales      | 700000 |   120000 |
|  4 | mahmud2027@gmail.com  | Legal      | 500000 |  1200000 |
|  2 | ammaarliu@gmail.com   | Sales      | 300000 |  2000000 |
|  1 | abdurrahman@gmail.com | IT         | 250000 |  1000000 |
|  3 | liuyuenfu@gmail.com   | Legal      | 100000 | 12000000 |
+----+-----------------------+------------+--------+----------+
5 rows in set (0.00 sec)

mysql> select * from info order by salary DESC LIMIT 1;
+----+---------------------+------------+--------+---------+
| id | user                | department | salary | rev_gen |
+----+---------------------+------------+--------+---------+
|  5 | something@gmail.com | Sales      | 700000 |  120000 |
+----+---------------------+------------+--------+---------+
1 row in set (0.00 sec)

mysql> show tables;
+-----------------------+
| Tables_in_abdurrahman |
+-----------------------+
| info                  |
| profile               |
| registration          |
+-----------------------+
3 rows in set (0.00 sec)

mysql> select * from registration;
+-----------+-------------+------------+---------------+-----------------------+
| username  | first_name  | last_name  | password      | email                 |
+-----------+-------------+------------+---------------+-----------------------+
| abdul007  | Abdurrahman | Muhammad   | abdulmah1230  | abdurrahman@gmail.com |
| ammaar001 | Ammaar      | abdussamad | ammaar2026    | ammaarliu@gmail.com   |
| liu001    | Chiko       | Abdulsamad | liuchiko9321  | liuyuenfu@gmail.com   |
| mah007    | Mahmud      | Muhammad   | mahmudmah1230 | mahmud2027@gmail.com  |
| moh001    | Mahmud      | Muhammad   | mahmudmah1230 | something@gmail.com   |
+-----------+-------------+------------+---------------+-----------------------+
5 rows in set (0.03 sec)

mysql> select * from registration r JOIN info i ON r.email=i.user;
+-----------+-------------+------------+---------------+-----------------------+----+-----------------------+------------+--------+----------+
| username  | first_name  | last_name  | password      | email                 | id | user                  | department | salary | rev_gen  |
+-----------+-------------+------------+---------------+-----------------------+----+-----------------------+------------+--------+----------+
| abdul007  | Abdurrahman | Muhammad   | abdulmah1230  | abdurrahman@gmail.com |  1 | abdurrahman@gmail.com | IT         | 250000 |  1000000 |
| ammaar001 | Ammaar      | abdussamad | ammaar2026    | ammaarliu@gmail.com   |  2 | ammaarliu@gmail.com   | Sales      | 300000 |  2000000 |
| liu001    | Chiko       | Abdulsamad | liuchiko9321  | liuyuenfu@gmail.com   |  3 | liuyuenfu@gmail.com   | Legal      | 100000 | 12000000 |
| mah007    | Mahmud      | Muhammad   | mahmudmah1230 | mahmud2027@gmail.com  |  4 | mahmud2027@gmail.com  | Legal      | 500000 |  1200000 |
| moh001    | Mahmud      | Muhammad   | mahmudmah1230 | something@gmail.com   |  5 | something@gmail.com   | Sales      | 700000 |   120000 |
+-----------+-------------+------------+---------------+-----------------------+----+-----------------------+------------+--------+----------+
5 rows in set (0.00 sec)

mysql> select CONCAT(r.first_name," ",r.last_name) AS fullname,i.department,i.salary from registration r JOIN info i ON r.email=i.user;
+----------------------+------------+--------+
| fullname             | department | salary |
+----------------------+------------+--------+
| Abdurrahman Muhammad | IT         | 250000 |
| Ammaar abdussamad    | Sales      | 300000 |
| Chiko Abdulsamad     | Legal      | 100000 |
| Mahmud Muhammad      | Legal      | 500000 |
| Mahmud Muhammad      | Sales      | 700000 |
+----------------------+------------+--------+
5 rows in set (0.00 sec)

mysql> SELECT * FROM (select CONCAT(r.first_name," ",r.last_name) AS fullname,i.department,i.salary from registration r JOIN info i ON r.email=i.user) AS new_table;
+----------------------+------------+--------+
| fullname             | department | salary |
+----------------------+------------+--------+
| Abdurrahman Muhammad | IT         | 250000 |
| Ammaar abdussamad    | Sales      | 300000 |
| Chiko Abdulsamad     | Legal      | 100000 |
| Mahmud Muhammad      | Legal      | 500000 |
| Mahmud Muhammad      | Sales      | 700000 |
+----------------------+------------+--------+
5 rows in set (0.00 sec)

mysql> SELECT * FROM (select CONCAT(r.first_name," ",r.last_name) AS fullname,i.department,i.salary from registration r JOIN info i ON r.email=i.user) AS new_table ORDER BY salary DESC LIMIT 3;
+-------------------+------------+--------+
| fullname          | department | salary |
+-------------------+------------+--------+
| Mahmud Muhammad   | Sales      | 700000 |
| Mahmud Muhammad   | Legal      | 500000 |
| Ammaar abdussamad | Sales      | 300000 |
+-------------------+------------+--------+
3 rows in set (0.00 sec)

mysql> UPDATE registration SET first_name="Ammaar", last_name="Abdussamad" WHERE email="something@gmail.com";
Query OK, 1 row affected (0.03 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM (select CONCAT(r.first_name," ",r.last_name) AS fullname,i.department,i.salary from registration r JOIN info i ON r.email=i.user) AS new_table ORDER BY salary DESC LIMIT 3;
+-------------------+------------+--------+
| fullname          | department | salary |
+-------------------+------------+--------+
| Ammaar Abdussamad | Sales      | 700000 |
| Mahmud Muhammad   | Legal      | 500000 |
| Ammaar abdussamad | Sales      | 300000 |
+-------------------+------------+--------+
3 rows in set (0.00 sec)

mysql> WITH ADAM AS (select CONCAT(r.first_name," ",r.last_name) AS fullname,i.department,i.salary from registration r JOIN info i ON r.email=i.user) SELECT * FROM ADAM;
+----------------------+------------+--------+
| fullname             | department | salary |
+----------------------+------------+--------+
| Abdurrahman Muhammad | IT         | 250000 |
| Ammaar abdussamad    | Sales      | 300000 |
| Chiko Abdulsamad     | Legal      | 100000 |
| Mahmud Muhammad      | Legal      | 500000 |
| Ammaar Abdussamad    | Sales      | 700000 |
+----------------------+------------+--------+
5 rows in set (0.01 sec)

mysql> WITH ADAM AS (select CONCAT(r.first_name," ",r.last_name) AS fullname,i.department,i.salary from registration r JOIN info i ON r.email=i.user) SELECT * FROM ADAM ORDER BY salary DESC LIMIT 2;
+-------------------+------------+--------+
| fullname          | department | salary |
+-------------------+------------+--------+
| Ammaar Abdussamad | Sales      | 700000 |
| Mahmud Muhammad   | Legal      | 500000 |
+-------------------+------------+--------+
2 rows in set (0.00 sec)

mysql> ALTER TABLE info ADD COLUMN tax DECIMAL;
Query OK, 0 rows affected (0.04 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM info;
+----+-----------------------+------------+--------+----------+------+
| id | user                  | department | salary | rev_gen  | tax  |
+----+-----------------------+------------+--------+----------+------+
|  1 | abdurrahman@gmail.com | IT         | 250000 |  1000000 | NULL |
|  2 | ammaarliu@gmail.com   | Sales      | 300000 |  2000000 | NULL |
|  3 | liuyuenfu@gmail.com   | Legal      | 100000 | 12000000 | NULL |
|  4 | mahmud2027@gmail.com  | Legal      | 500000 |  1200000 | NULL |
|  5 | something@gmail.com   | Sales      | 700000 |   120000 | NULL |
+----+-----------------------+------------+--------+----------+------+
5 rows in set (0.00 sec)

mysql> UPDATE info SET tax=(.075*salary);
Query OK, 5 rows affected (0.01 sec)
Rows matched: 5  Changed: 5  Warnings: 0

mysql> SELECT * FROM info;
+----+-----------------------+------------+--------+----------+-------+
| id | user                  | department | salary | rev_gen  | tax   |
+----+-----------------------+------------+--------+----------+-------+
|  1 | abdurrahman@gmail.com | IT         | 250000 |  1000000 | 18750 |
|  2 | ammaarliu@gmail.com   | Sales      | 300000 |  2000000 | 22500 |
|  3 | liuyuenfu@gmail.com   | Legal      | 100000 | 12000000 |  7500 |
|  4 | mahmud2027@gmail.com  | Legal      | 500000 |  1200000 | 37500 |
|  5 | something@gmail.com   | Sales      | 700000 |   120000 | 52500 |
+----+-----------------------+------------+--------+----------+-------+
5 rows in set (0.00 sec)

mysql> SELECT *, (salary-tax) AS net_salary FROM info;
+----+-----------------------+------------+--------+----------+-------+------------+
| id | user                  | department | salary | rev_gen  | tax   | net_salary |
+----+-----------------------+------------+--------+----------+-------+------------+
|  1 | abdurrahman@gmail.com | IT         | 250000 |  1000000 | 18750 |     231250 |
|  2 | ammaarliu@gmail.com   | Sales      | 300000 |  2000000 | 22500 |     277500 |
|  3 | liuyuenfu@gmail.com   | Legal      | 100000 | 12000000 |  7500 |      92500 |
|  4 | mahmud2027@gmail.com  | Legal      | 500000 |  1200000 | 37500 |     462500 |
|  5 | something@gmail.com   | Sales      | 700000 |   120000 | 52500 |     647500 |
+----+-----------------------+------------+--------+----------+-------+------------+
5 rows in set (0.00 sec)

mysql> SELECT *, (salary-tax) AS net_salary, ((salary-tax)/salary) AS "% net" FROM info;
+----+-----------------------+------------+--------+----------+-------+------------+--------+
| id | user                  | department | salary | rev_gen  | tax   | net_salary | % net  |
+----+-----------------------+------------+--------+----------+-------+------------+--------+
|  1 | abdurrahman@gmail.com | IT         | 250000 |  1000000 | 18750 |     231250 | 0.9250 |
|  2 | ammaarliu@gmail.com   | Sales      | 300000 |  2000000 | 22500 |     277500 | 0.9250 |
|  3 | liuyuenfu@gmail.com   | Legal      | 100000 | 12000000 |  7500 |      92500 | 0.9250 |
|  4 | mahmud2027@gmail.com  | Legal      | 500000 |  1200000 | 37500 |     462500 | 0.9250 |
|  5 | something@gmail.com   | Sales      | 700000 |   120000 | 52500 |     647500 | 0.9250 |
+----+-----------------------+------------+--------+----------+-------+------------+--------+
5 rows in set (0.00 sec)

mysql> SELECT *, (salary-tax) AS net_salary, ((salary-tax)/salary)*100 AS "% net-salary" FROM info;
+----+-----------------------+------------+--------+----------+-------+------------+--------------+
| id | user                  | department | salary | rev_gen  | tax   | net_salary | % net-salary |
+----+-----------------------+------------+--------+----------+-------+------------+--------------+
|  1 | abdurrahman@gmail.com | IT         | 250000 |  1000000 | 18750 |     231250 |      92.5000 |
|  2 | ammaarliu@gmail.com   | Sales      | 300000 |  2000000 | 22500 |     277500 |      92.5000 |
|  3 | liuyuenfu@gmail.com   | Legal      | 100000 | 12000000 |  7500 |      92500 |      92.5000 |
|  4 | mahmud2027@gmail.com  | Legal      | 500000 |  1200000 | 37500 |     462500 |      92.5000 |
|  5 | something@gmail.com   | Sales      | 700000 |   120000 | 52500 |     647500 |      92.5000 |
+----+-----------------------+------------+--------+----------+-------+------------+--------------+
5 rows in set (0.00 sec)

mysql> SELECT *, (salary-tax) AS net_salary, ROUND(((salary-tax)/salary)*100,2) AS "% net-salary" FROM info;
+----+-----------------------+------------+--------+----------+-------+------------+--------------+
| id | user                  | department | salary | rev_gen  | tax   | net_salary | % net-salary |
+----+-----------------------+------------+--------+----------+-------+------------+--------------+
|  1 | abdurrahman@gmail.com | IT         | 250000 |  1000000 | 18750 |     231250 |        92.50 |
|  2 | ammaarliu@gmail.com   | Sales      | 300000 |  2000000 | 22500 |     277500 |        92.50 |
|  3 | liuyuenfu@gmail.com   | Legal      | 100000 | 12000000 |  7500 |      92500 |        92.50 |
|  4 | mahmud2027@gmail.com  | Legal      | 500000 |  1200000 | 37500 |     462500 |        92.50 |
|  5 | something@gmail.com   | Sales      | 700000 |   120000 | 52500 |     647500 |        92.50 |
+----+-----------------------+------------+--------+----------+-------+------------+--------------+
5 rows in set (0.00 sec)

mysql> SELECT *, (salary-tax) AS net_salary, ROUND(((salary-tax)/salary)*100,1) AS "% net-salary" FROM info;
+----+-----------------------+------------+--------+----------+-------+------------+--------------+
| id | user                  | department | salary | rev_gen  | tax   | net_salary | % net-salary |
+----+-----------------------+------------+--------+----------+-------+------------+--------------+
|  1 | abdurrahman@gmail.com | IT         | 250000 |  1000000 | 18750 |     231250 |         92.5 |
|  2 | ammaarliu@gmail.com   | Sales      | 300000 |  2000000 | 22500 |     277500 |         92.5 |
|  3 | liuyuenfu@gmail.com   | Legal      | 100000 | 12000000 |  7500 |      92500 |         92.5 |
|  4 | mahmud2027@gmail.com  | Legal      | 500000 |  1200000 | 37500 |     462500 |         92.5 |
|  5 | something@gmail.com   | Sales      | 700000 |   120000 | 52500 |     647500 |         92.5 |
+----+-----------------------+------------+--------+----------+-------+------------+--------------+
5 rows in set (0.00 sec)

mysql> SELECT department, COUNT(*) AS total_staff from info GROUP BY department order by total_staff DESC;
+------------+-------------+
| department | total_staff |
+------------+-------------+
| Sales      |           2 |
| Legal      |           2 |
| IT         |           1 |
+------------+-------------+
3 rows in set (0.00 sec)
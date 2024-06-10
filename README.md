## 1. Environment

- WSL(Ubuntu 20.04.6 LTS)
- Docker version 20.10.2 |build 2291f61
- mysql/mysql-server:8.0

## 2. Reference

[MySQL Tutorial - W3Schools](https://www.w3schools.com/mysql/default.asp)

### 3. Docker

### 3-1. Setup MySQL and Login

```bash
$ echo 'export MYSQL_PASSWORD="password"' >> ~/.bash_profile
$ docker-compose up -d
```

### 3-2. Copy `setup.sql` to `/tmp` directory in Docker container

```bash
$ docker cp setup.sql {CONTAINER ID}:/tmp/
```

### 3-3. Create DB, Tables and Insert Records

```bash
$ docker-compose exec db mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 163
Server version: 8.0.24 MySQL Community Server - GPL

Copyright (c) 2000, 2021, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> source /tmp/setup.sql
```

---

Check if the database, tables and records are created successfully.

```bash
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| tutorial           |
+--------------------+
5 rows in set (0.00 sec)

mysql> USE tutorial;
Database changed
mysql> SHOW TABLES;
+--------------------+
| Tables_in_tutorial |
+--------------------+
| categories         |
| customers          |
| employees          |
| order_details      |
| orders             |
| products           |
| shippers           |
| suppliers          |
+--------------------+
8 rows in set (0.00 sec)

mysql> SELECT * FROM {TABLE_NAME};
```

## 4. Tables

### 4-1. categories

|id |name |description |
|:-|:-|:-|
|PRIMARY KEY |varchar(255) |varchar(255) |

### 4-2. customers

|id |name |contact |address |City |zipcode |country |
|:-|:-|:-|:-|:-|:-|:-|
|PRIMARY KEY |varchar(255) |varchar(255) |varchar(255) |varchar(255) |varchar(255) |varchar(255) |

### 4-3. employees

|id |last_name |first_name |birthdate |photo |notes |
|:-|:-|:-|:-|:-|:-|
|PRIMARY KEY |varchar(255) |varchar(255) |date |varchar(255) |varchar(255) |

### 4-4. shippers

|id |name |phone |
|:-|:-|:-|
|PRIMARY KEY |varchar(255) |varchar(255) |

### 4-5. suppliers

|id |name |contact |address |city |zipcode |country |phone |
|:-|:-|:-|:-|:-|:-|:-|:-|
|PRIMARY KEY |varchar(255) |varchar(255) |varchar(255) |varchar(255) |varchar(255) |varchar(255) |varchar(255) |

### 4-6. products

|id |name |supplier_id |category_id |unit |price |
|:-|:-|:-|:-|:-|:-|
|PRIMARY KEY |varchar(255) |FOREIGN KEY |FOREIGN KEY |varchar(255) |float(5) |

### 4-7. orders

|id |customer_id |employee_id |order_date |shipper_id |
|:-|:-|:-|:-|:-|
|PRIMARY KEY |FOREIGN KEY |FOREIGN KEY |date |FOREIGN KEY |

### 4-8. order_details

|id |order_id |product_id |quantity |
|:-|:-|:-|:-|
|PRIMARY KEY |FOREIGN KEY |FOREIGN KEY |int |

# MariaDB Sheet
## Introduction

MariaDB is a powerful open-source relational database management system and a fork of MySQL. It is widely used in web development and other applications to store, retrieve, and manage data efficiently. This guide will cover the fundamental steps for getting started with MariaDB.

## Installation

To use MariaDB, you first need to install it on your system. You can follow these steps to install it on various operating systems:

### Windows

1. Download the MariaDB installer from the official website.
2. Run the installer and follow the on-screen instructions to complete the installation.

### macOS

1. Install MariaDB using Homebrew package manager by running the following command in Terminal:

```
brew install mariadb
```



## Install MariaDB on Ubuntu 20.04 LTS
```bash
sudo apt update
sudo apt install mariadb-server
sudo mysql_secure_installation
```

## Install MariaDB on  Red Hat/CentOS-based systems, use:
```
sudo yum install mariadb-server
```

## Connecting to MariaDB
Once MariaDB is installed, you can connect to it using the following steps:

1. Open a terminal or command prompt.
2. Use the `mysql` command to connect to the database server:

```shell
mysql -u username -p
```

Replace `username` with your database username. You'll be prompted to enter your password. 
## Access Database from outside
Open `/etc/mysql/mariadb.conf.d/50-server.cnf` and change the `bind-address` to:
```
...

bind-address = 0.0.0.0

...
```

## Connecting via code to the Database
To connect to the database from code, you can use various programming languages. For example, to connect via [PHP](language/Php)

## Create Administrative User
1. Create a new user `newuser` for the host `localhost` with a new `password`:
```mysql
CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
```

2. Grant all permissions to the new user
```mysql
GRANT ALL PRIVILEGES ON * . * TO 'newuser'@'localhost';
``` 

3. Update permissions
```mysql
FLUSH PRIVILEGES;
```


## Creating a Database

To create a new database, follow these steps:

1. After connecting to MariaDB, use the following command:

```MySql
CREATE DATABASE your_database_name;
```

Replace `your_database_name` with the desired name for your database.

## Creating Tables

Tables are used to organize and store data in MariaDB. To create a table, follow these steps:

1. Select the database in which you want to create the table:

```MySql
USE your_database_name;
```

2. Create the table using the `CREATE TABLE` command:

```MySql
CREATE TABLE your_table_name (     column1 datatype1 constraints,     column2 datatype2 constraints,     ... );
```

Replace `your_table_name`, `column1`, `datatype1`, etc., with your desired table name and column definitions.

## Inserting Data

To add data to a table, use the `INSERT INTO` statement:

```MySql 
INSERT INTO your_table_name (column1, column2, ...) VALUES (value1, value2, ...);
```


Replace `your_table_name`, `column1`, `column2`, etc., with the appropriate values.

## Querying Data

To retrieve data from a table, use the `SELECT` statement:

```MySql 
SELECT column1, column2, ... FROM your_table_name WHERE condition;
```


Replace `column1`, `column2`, etc., with the desired columns and `condition` with any necessary filtering criteria.

## Updating Data

To modify existing data in a table, use the `UPDATE` statement:

```MySql
UPDATE your_table_name SET column1 = new_value1, column2 = new_value2, ... WHERE condition;
```

Replace `column1`, `column2`, etc., with the columns you want to update and provide new values.

## Deleting Data

To remove data from a table, use the `DELETE FROM` statement:

```MySql
DELETE FROM your_table_name WHERE condition;
```

Replace `your_table_name` and `condition` with the appropriate values.

## Conclusion

This guide covers the basic usage of MariaDB, including installation, connecting to the database, creating databases and tables, inserting, querying, updating, and deleting data. It provides a solid foundation to start working with MariaDB for various projects.

Please note that this is just a basic overview, and MariaDB has many more features and capabilities to explore as you become more comfortable with it. For more detailed information and advanced usage, refer to the official [MariaDB documentation](https://mariadb.org/documentation/). Happy data managing!
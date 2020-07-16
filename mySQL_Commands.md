---
title: MySQL Command Reference
description: Commands for interacting wit a mySQL database using the client program isql
published: true
date: 2020-07-04T14:52:41.360Z
tags: 
editor: undefined
---

# mySQL Command Reference and Examples
Commands for interacting wit a mySQL database using the client program isql

## Command Reference

### Selecting and retrieving data

The following statement uses the SELECT statement to retrieve a single column named <column_name> from the database table named <table>.
```
SELCECT <column_name> FROM <table_name>
```
To retrieve multiple columns from table <table_name>:
```
  SELCECT <column_name_1>, <column_name_2>, <column_name_3> FROM <table_name>
  ```
To retrieve all columns, the wildcard "*" can be used:
  ```
  SELECT * from <table_mame>
  ```

## Examples

All of the commands given below are illustrated using, as an example, the Symetrica fleet server.

- To connect to the database using the client program isql
```
sudo isql symetrica
```
To list all of the tables available use the **show** command:
```
show tables;
```
The structure of the table is displayed using the "desc" command, so for the "Occupancies" table:
```
desc Occupancies;
```
Display the first 10 rows:
```
select * from Occupancies LIMIT 10
```
selecting columns by name
```
select col_a, col_b from table_name 
```

Grab the latest 200 rows
select CTime, Path from ( select * from Occupancies order by id desc limit 200 ) sub order by id asc


Looks like the names of the hosts are in the Hosts table. To show them:
select id, Name from Hosts order by id asc
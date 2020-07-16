---
title: Installing PostgreSQL
description: How to install and configure PostgreSQL database server on Ubuntu 18.04.4 LTS
published: true
date: 2020-07-01T10:10:02.240Z
tags: 
editor: undefined
---

# Introduction
Your content here


# Instructions


## Add the package repository


Create the file repository configuration:
```
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
```
Import the repository signing key:
```
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
```
Update the package lists:
```
sudo apt-get update
```

## Install

Install the latest version of PostgreSQL. If you want a specific version, use 'postgresql-12' or similar instead of 'postgresql':
```
sudo apt-get install postgresql
```
Check that the database has been initialised:
```
sudo -u postgres psql -c "show data_directory;"
```

The output of this command should display something silimalr to this:

> /var/lib/postgresql/12/main
{.is-success}


## Add rules to the firewall
Allow connections from the local subnet (or whatever address range you choose) on port 5432. For UFW, execute the following:
```
sudo ufw allow from 172.16.0.0/24 to any port 5432
```

## Set the database to listen to the external network
By default postgres is configured to listen for TCP/IP connection on the 127.0.0.1 (localhost) only. To change this, edit the following file:
**/etc/postgresql/12/main/postgresql.conf**
and make the following change:
```
listen_addresses = '*'
```
The "*" tells postgres to listed on all addresses on all interfaces.

## Configure host-based authentication

PostgreSQL can restrict accesss by database user, to certain databases within the database cluster and from certain addresses as well as specifying the authentifiaction method (passwrod etc.). To allow any user access to any database from the local subnet 172.16.0.1/24 using encrypted password, and add the following line to **/etc/postgresql/12/main/pg_hba.conf**
```
host    all             all             172.16.0.1/24           md5
```
For further details, see the documentation for [host-based authentication](https://www.postgresql.org/docs/12/auth-pg-hba-conf.html).


## Set a password for the admin account. 
The admin account will default to the linux user that initialised the database; in this instance it is the user "postgres". In a terminal, type:
```
sudo -u postgres psql postgres
```
this connects as a role with same name as the local user, i.e. "postgres", to the database called "postgres" (1st argument to psql). Set a password for the "postgres" database role using the command:
```
\password postgres
```
and give your password when prompted. The password text will be hidden from the console for security purposes.

Type Control+D or \q to exit the posgreSQL prompt. 

## Check connection on remote client

### Install postgres client


### Check connetion


```
psql -h <host> -p <port> -U <username> <database>
```
```
psql -h 172.16.0.22 -p 5432 -U postgres postgres
```
  
You will be propted for a password.

# Useful Locations
Below is a list of locations of useful files such as logs and configuration

> **Logs are located here:** /var/log/postgresql/postgresql-12-main.log
{.is-info}

> **The configuration file is here:** /etc/postgresql/12/main/postgresql.conf
{.is-info}

> T**he host-based authentication configuration file is here:** /etc/postgresql/12/main/pg_hba.conf
{.is-info}

# Useful Links


- [PostgresSQL Docs *Documentation for server installation and configuration for version 12 of PostgreSQL*](https://www.postgresql.org/docs/12/admin.html)
- [Installation on Ubuntu *Documentation for instaling postgreSQL client and server on Ubuntu*](https://help.ubuntu.com/community/PostgreSQL)
- [Remote connection *Useful information on configuring and establishing a remote connection to the database*](https://stackoverflow.com/questions/32439167/psql-could-not-connect-to-server-connection-refused-error-when-connecting-to)
{.links-list}
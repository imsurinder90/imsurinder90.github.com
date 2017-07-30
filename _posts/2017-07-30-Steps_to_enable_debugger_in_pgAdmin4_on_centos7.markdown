---
layout: post
title: Steps to enable debugger in pgAdmin4 on Centos 7
category: pgAdmin4
comments: true
---

Debugger is used to debug pl/pgsql functions in PostgreSQL, To use debugger with pgAdmin4 to debug functions, it has to be enabled.
It comes with PostgreSQL and present in location `/opt/PostgreSQL/9.5/share/postgresql/extension/pldbgapi--1.0.sql`.
So, first install PostgreSQL 9.5.


### Follow the steps to enable pl/pgsql debugger in pgAdmin4:###


- go to directory `/opt/PostgreSQL/9.5/`.

- find pldbgapi `pldbgapi--1.0.sql` extension by typing:

      [surinder@localhost 9.5]$ find . -name *pld*.sql
      # following files will be listed:
      ./share/postgresql/extension/pldbgapi--1.0.sql
      ./share/postgresql/extension/pldbgapi--unpackaged--1.0.sql

- go to `bin` directory and then connect to postgres server:

      [surinder@localhost bin]$ ./psql -h localhost -p 5432 -U postgres pem
      # It will prompt for password that you entered while installing.
      Password for user postgres:
      psql.bin (9.5.7)
      SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
      Type "help" for help.
      pem=#

- Now run `pgdbgapi` api extension file on psql prompt, like:

      pem=# \i /opt/PostgreSQL/9.5/share/postgresql/extension/pldbgapi--1.0.sql
      # Above file will execute and you will see output like:
      Installing pldebugger as unpackaged objects. If you are using PostgreSQL
      version 9.1 or above, use "CREATE EXTENSION pldbgapi" instead.
      CREATE TYPE
      CREATE TYPE
      CREATE TYPE
      CREATE TYPE
      CREATE FUNCTION
      CREATE FUNCTION
      CREATE FUNCTION
      CREATE FUNCTION
      CREATE FUNCTION
      CREATE FUNCTION
      CREATE FUNCTION
      CREATE FUNCTION
      CREATE FUNCTION
      CREATE FUNCTION
      CREATE FUNCTION
      CREATE FUNCTION
      CREATE FUNCTION
      CREATE FUNCTION
      CREATE FUNCTION
      CREATE FUNCTION
      CREATE FUNCTION
      CREATE FUNCTION
      CREATE FUNCTION
      CREATE FUNCTION
      CREATE TYPE
      DO
      pem=#


- Then register `pldbgapi` extension by creating on psql prompt:

      pem=# create extension pldbgapi;
      # you will see output like:
      ERROR:  type "breakpoint" already exists


-  Exit `psql` prompt:
      `pem=# \q`


- Restart PostgreSQL service by typing:

      [surinder@localhost bin]$ sudo service postgresql-9.5 restart

Now open pgAdmin4, browse to functions and right click of any function and then click on `debugging > debug` option to debug function.

That's it. Enjoy debugging `pl/pgsql` functions.

Thanks!


---

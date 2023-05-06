---
title: PostgreSQL and PL/pgSQL
---

### Shell Commands for PostgreSQL
* `p1` - start PostgreSQL server
* `p0` - stop PostgreSQL server
* `createdb <db name>`- creates a database
* `psql <db name>` - opens a database
* `psql <db name> -f <.sql file location>` - opens sql file for a database
* `psql -l` - displays all databases
* `dropdb <db name>` - deletes a database
* `pg_dump <db name> > <file name>` - exports shell commands to dump database contents
* `psql <db name> -f <dump file>` - restores database contents from dump file

### PostgreSQL Commands
* `\d [relation name]` - list relation(s)
* `\dv [relation name]` - list view(s)
* `\x` - expanded view mode
* `\e` - editor for previous command ???
* `\q` - quit

### PL/pgSQL
* Use `$1`, `$2`, etc. to access arguments
* Functions with SQL language:
    ```sql
    CREATE OR REPLACE
    funcName(arg1type, arg2type, ....)
    RETURNS rettype 
    AS $$
    SQL statements
    $$ LANGUAGE sql;
    ```
* E.g.
    ```sql
    create or replace function
    hotelsIn(text) returns setof Bars
    as $$
    select * from Bars where addr = $1;
    $$ language sql;

    -- usage examples
    select * from hotelsIn('The Rocks');
        name        |   addr    | license
    Australia Hotel | The Rocks |  123456
    Lord Nelson     | The Rocks |  123888

    select * from hotelsIn('Randwick');
        name    |   addr   | license
    Royal Hotel | Randwick |  938500
    ```
* Functions with PL/pgSQL language:
    ```sql
    CREATE OR REPLACE
    funcName(param1, param2, ....)
    RETURNS rettype AS $$
    DECLARE
    variable declarations
    BEGIN
    code for function
    END;
    $$ LANGUAGE plpgsql;
    ```
* E.g.
    ```sql
    create function
        withdraw(acctNum text, amount integer) returns text
    as $$
    declare bal integer;
    begin
        select balance into bal
        from   Accounts
        where  acctNo = acctNum;
        if bal < amount then
            return 'Insufficient Funds';
        else
            update Accounts
            set    balance = balance - amount
            where  acctNo = acctNum;
            select balance into bal
            from   Accounts
            where  acctNo = acctNum;
            return 'New Balance: ' || bal;
    end if; end;
    $$ language plpgsql;
    ```
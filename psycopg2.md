---
title: Psycopg2
---

* Psycopgy2 is a Python module that allows:
    * a method to connect to PostgreSQL databases
    * a collection of DB-related exceptions
    * a collection of type and object constructors

### Setup
```py
import psycopg2
conn = psycopg2.connect("dbname=<mydb>")
```

### Operations on `connections`
* `cur = conn.cursor()`
    * set up a handle for performing queires/updates on a database
    * can create multiple cursors for the same connection
    * each cursor handles one DB operation at a time
    * cursors can see each other's changes (i.e. not isolated)
* `conn.close()`
* `conn.commit()`
    * commit changes to a database

### Operations on `cursors`
* `cur.execute(<SQL statement>, <values>)`
* E.g.  
    ```py
    # run a fixed query
    cur.execute("select * from R where x = 1")

    # run a query with values inserted
    cur.execute("select * from R where x = %s", (1,)) # tuple
    cur.execute("select * from R where x = %s", [1])

    # run a query stored in a variable
    query = "select * from Students where name ilike %s"
    pattern = "%mith%"
    cur.execute(query, [pattern]) # square bracket is a list
    ```
* `cur.callproc(<procedure>, <values>)`
* E.g.  
    ```py
    # using a standard function call from SQL
    cur.execute("select * from brewer(5)")
    t = cur.fetchone()
    print(t[0])

    # using special callproc() method
    # parameters supplied as a list of values/vars cur.callproc("brewer",[5])
    t = cur.fetchone()
    print(t[0])
    ```
* `cur.mogrify(<SQL statement>, <values>`
    * returns SQL statement as a string with values inserted
    * useful for testing what SQL statement you are stating
* E.g.
    ```py
    query = "select * from R where x = %s" print(cur.mogrify(query, [1]))
    # Produces: b'select * from R where x = 1'

    query = "select * from R where x = %s and y = %s" print(cur.mogrify(query, [1,5]))
    # Produces: b'select * from R where x = 1 and y = 5'

    query = "select * from Students where name ilike %s"
    pattern = "%mith%"
    print(cur.mogrify(query, [pattern]))
    # Produces: b"select * from Students where name ilike '%mith%'"

    query = "select * from Students where family = %s"
    fname = "O'Reilly"
    print(cur.mogrify(query, [fname]))
    # Produces: b"select * from Students where family = 'O''Reilly'"
    ```
* `list = cur.fetchall()`
    * gets all answers for a query and stores in a list of tuples
* `tup = cur.fetchone()`
    * gets next result for a queyr and stores in a type
* `tup = cur.fetchmany(<no of tuples>)`
    * list of tuples of length `n`
* `cur.close()`



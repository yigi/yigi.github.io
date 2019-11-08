### pip install psycopg2

### Connect DB

```python
import psycopg2
try:
    connection = psycopg2.connect(user = "xxx",
                                  password = "xxx",
                                  host = "127.0.0.1",
                                  port = "5432",
                                  database = "xxx")

    cursor = connection.cursor()
    # Print PostgreSQL Connection properties
    print ( connection.get_dsn_parameters(),"\n")

    # Print PostgreSQL version
    cursor.execute("SELECT version();")
    record = cursor.fetchone()
    print("You are connected to - ", record,"\n")

except (Exception, psycopg2.Error) as error :
    print ("Error while connecting to PostgreSQL", error)
finally:
    #closing database connection.
        if(connection):
            cursor.close()
            connection.close()
            print("PostgreSQL connection is closed")
```

### Create Table

```python
import psycopg2
from psycopg2 import Error

try:
    connection = psycopg2.connect(user = "xxx",
                                  password = "xxx",
                                  host = "127.0.0.1",
                                  port = "5432",
                                  database = "xxx")

    cursor = connection.cursor()
    
    create_table_query = '''CREATE TABLE mobile
          (ID INT PRIMARY KEY     NOT NULL,
          MODEL           TEXT    NOT NULL,
          PRICE         REAL); '''
    
    cursor.execute(create_table_query)
    connection.commit()
    print("Table created successfully in PostgreSQL ")

except (Exception, psycopg2.DatabaseError) as error :
    print ("Error while creating PostgreSQL table", error)
finally:
    #closing database connection.
        if(connection):
            cursor.close()
            connection.close()
            print("PostgreSQL connection is closed")
``` 

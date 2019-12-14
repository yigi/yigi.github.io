## Structured Query language

### Data Definition Language (DDL) commands:

CREATE to create a new table or database.

ALTER for alteration.

Truncate to delete data from the table.

DROP to drop a table.

RENAME to rename a table.

### Data Manipulation Language (DML) commands:

INSERT to insert a new row.

UPDATE to update an existing row.

DELETE to delete a row.

MERGE for merging two rows or two tables.

### Data Control Language (DCL) commands:

COMMIT to permanently save.

ROLLBACK to undo the change.

SAVEPOINT to save temporarily.

_______________________________________________________________________

<img align="center" width="800" height="800" src="http://cdn.differencebetween.net/wp-content/uploads/2011/09/difference-between-inner-join-vs-join.png">

_______________________________________________________________________

Atomicity is the condition where either all the actions of the transaction are performed or none. This means, when there is an incomplete transaction, the database management system itself will undo the effects done by the incomplete transaction.

_______________________________________________________________________

The primary key is that column of the table whose every row data is uniquely identified. Every row in the table must have a primary key and no two rows can have the same primary key. Primary key value can never be null nor can it be modified or updated.

The foreign key is a field in the table that is primary key in another table.

_______________________________________________________________________

After the execution of ‘DELETE’ operation, COMMIT and ROLLBACK statements can be performed to retrieve the lost data.

After the execution of ‘TRUNCATE’ operation, COMMIT, and ROLLBACK statements cannot be performed to retrieve the lost data.

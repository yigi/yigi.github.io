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

_______________________________________________________________________

A query is a single statement in SQL's data manipulation language: typically one of SELECT, INSERT, UPDATE or DELETE (the latter three may modify data, while SELECT only reads data).

A transaction is a group of statements which taken together, are usually defined to have "ACID" semantics (my own off the cuff definitions are below, but these are defined in any web or paper reference to relational database):

```sql
START TRANSACTION;
UPDATE accounts SET balance = balance + 100 WHERE account_id = 98;
UPDATE accounts SET balance = balance - 100 WHERE account_id = 42;
COMMIT;
```
_______________________________________________________________________

Veritabanı mimarisinde bu tür iş süreci(transaction) gerektiğinde uyulması gereken prensibe ACID (Atomicity, Consistency, Isolation, Durability) denir.

– Bölünemezlik(Atomicity)

Transaction işleminin ana özelliği olarak açıkladığımız bölünemezlik prensibini yansıtır. Bir transaction bloğu yarım kalamaz. Yarım kalan transaction bloğu veri tutarsızlığına neden olur. Ya tüm işlemler gerçekleştirilir, ya da transaction başlangıcına geri döner. Yani transaction’ın gerçekleştirdiği tüm değişiklikler geri alınarak gerçekleşmeden önceki haline döner.

– Tutarlılık(Consistency)

Bölünemezlik kuralının alt yapısını oluşturduğu bir kuraldır. Transaction veri tutarlılığı sağlamalıdır. Yani bir transaction içerisinde güncelleme işlemi gerçekleştiyse ve ya kalan tüm işlemler de gerçekleşmeli ya da güncelle işlemi de geri alınmalıdır. Bu veri tutarlılığı açısından çok önemlidir.

– İzolasyon(Isolation)

Her transaction veritabanı için bir istek paketidir. Bir istek paketi (transaction) tarafından gerçekleştirilen değişiklikler tamamlanmadan bir başka transaction tarafından görülememelidir. Her transaction ayrı olarak işlenmelidir. Transaction’ın tüm işlemleri gerçekleştikten sonra bir başka transaction tarafından görülebilmelidir.

– Dayanıklılık (Durability)

Transaction’lar veri üzerinde karmaşık işlemler gerçekleştirebilir. Bu işlemlerin bütününü güvence altına almak için transaction hatalara karşı dayanıklı olmalıdır. SQL Server’da meydana gelebilecek sistem sorunu, elektrik kesilmesi, işletim sisteminden ya da farklı yazılımlardan kaynaklanabilecek hatalara karşı hazırlıklı ve dayanıklı olmalıdır.

_______________________________________________________________________

Bu ifadeler ile transaction başlatılabilir (BEGIN), işlemler geri alınabilir (ROLLBACK), transaction bitirilebilir (COMMIT) ya da kayıt noktaları (SAVE) oluşturulabili

# Learn SQL Syntack
this is my note for learning mysql

## Type table in mysql

1. MyISAM
    - MyISAM static
    ```
    This type is used when all the columns are in the table defined by a fixed size.
    ```
    - MyISAM DYNAMIC
    ```
    This type is used when there are columns with type which is dynamic, like the VARCHAR column type.
    ```
    - MyISAM Compressed
    ```
    The uncompressed table can not be subjected to operations such as INSERT, UPDATE and DELETE.
    ```
2. InnoDB
    ```
    table types that support the process transaction.
    ```
3. HEAP
    ```
    Table for trying, because this table save in memory when server shutdown or connection is disconnected this table will lose.
    ```

## Type field in mysql

1. Type numeric
    - TINYINT
        - 1 byte (8 bit)
        - range -128 s/d 127
    - SMALLINT
        - 2 byte (16 bit)
        - range -32.768 s/d 32.767
    - MEDIUMINT
        - 3 byte (24 bit)
        - range -8.388.608 s/d 8.388.607
    - INT
        - 4 byte (32 bit)
        - range -2.147.483.648 s/d 2.147.483.647
    - BIGINT
        - 8 byte (64 bit)
        - range ± 9,22 x 10 18
    - FLOAT
        - 4 byte (32 bit)
        - -3.402823466E+38 s/d -1.175494351E-38, 0, dan
1.175494351E-38 s/d 3.402823466E+38
    - DOUBLE / REAL / DECIMAL / NUMERIC
        - 8 byte (64 bit)
        - -1.79...E+308 s/d -2.22...E-308, 0, dan
2.22...E-308 s/d 1.79...E+308

2. Type Date and Time 
    - DATE
        - 3 byte
        - 1000-01-01 s/d 9999-12-31 (YYYY-MM-DD)
    - TIME
        - 3 byte
        - -838:59:59 s/d +838:59:59 (HH:MM:SS)
    - DATETIME
        - 8 byte
        - '1000-01-01 00:00:00' s/d '9999-12-31 23:59:59'
    - YEAR
        - 1 byte
        - 1900 s/d 2155

3. Type String
    - CHAR (static)
        - 0 s/d 255
    - VARCHAR (dinamis) / TINYTEXT (text) / TEXT
        - 0 s/d 65.535 (version 5.0.3)
    - MEDIUMTEXT
        - 0 s/d 2^24 - 1
    - LONGTEXT
        - 0 s/d 2^32 - 1

4. Type BLOB
    - BIT
        - 64 digit biner
    - TINYBLOB
        - 255 byte
    - BLOB
        - 2^16 - 1 byte
    - MEDIUMBLOB
        - 2^24 - 1 byte
    - LONGBLOB
        - 2^32 - 1 byte

5. Etc
    - Enum (choice)
        - 65535 string
    - Set
        - 255 string anggotas

## Type Syntax Mysql

- DDL (Data Definition Language)
    - CREATE
    - ALTER
    - RENAME
    - DROP

- DML (Data Manipulation Language)
    - SELECT
    - INSERT
    - UPDATE
    - DELETE

- DCL (Data Control Language)
    - GRANT
    - REVOKE

# Data Definition Language

### Create Database
```mysql
CREATE DATABASE [IF NOT EXISTS] name_database;
```

### Showing Database
```mysql
SHOW DATABASES;
```

### Open Database
```mysql
USE DATABASES;
```

### Delete Database
```mysql
DROP DATABASE [IF EXISTS] name_database;
```

### Create Table
```mysql
CREATE TABLE nama_tabel (
name_field1 type_field(length),
name_field2 type_field(length),
...
name_fieldn type_field(length),
PRIMARY KEY (name_field)
);
```

### Show Tables
```mysql
SHOW TABLES;
```

### Showing Structure Table
```mysql
DESC name_table;
```

### Change Table field
```mysql
ALTER TABLE name_table alter_options;
```

### Alter_options
- ADD
- CHANGE
- MODIFY
- DROP
- RENAME TO

### Add field
```mysql
ALTER TABLE pelanggan ADD tgllahir date NOT NULL;
```

### Change field
```mysql
ALTER TABLE pelanggan CHANGE tgllahir tgl_lahir date NOT NULL;
```

### Modify field
```mysql
ALTER TABLE pelanggan MODIFY tgl_lahir YEAR NOT NULL;

ALTER TABLE cobatable MODIFY id INT UNSIGNED NOT NULL AUTO_INCREMENT;
```

### Drop field
```mysql
ALTER TABLE pelanggan DROP tgl_lahir;
```

### Rename Table
```mysql
RENAME TABLE pelanggan TO plg;
ALTER TABLE plg RENAME TO pelanggan;
```

### Delete Table
```mysql
DROP TABLE name_table;
```

### Show Type table
```
SHOW TABLE STATUS WHERE Name = 'name_table';
```

### Change Engine Table
```
ALTER TABLE nameTable ENGINE = typeTable;
```
### Show Open Table
```
SHOW OPEN TABLES FROM d WHERE condition;
```

# Data Manipulation Language

### Insert Value
```mysql
INSERT INTO name_table VALUES (‘value1’,’value2’,...);
or
INSERT INTO name_table(field1,field2,...)
VALUES (value1,value2,...);
or
INSERT INTO name_table
SET field1=’value1’, field2=’value2’,...;
```

### Showing Value Table
```mysql
SELECT [field | *] FROM nama_tabel [WHERE kondisi];
or
SELECT id_pelanggan, nm_pelanggan, email
FROM pelanggan WHERE email LIKE '%yahoo%';
or
SELECT id_pelanggan, nm_pelanggan, alamat, email
FROM pelanggan WHERE alamat = 'Jakarta Selatan' &&
email LIKE '%gmail.com';
or
SELECT id_pelanggan, nm_pelanggan
FROM pelanggan ORDER BY nm_pelanggan [asc | desc];
or
SELECT id_pelanggan, nm_pelanggan
FROM pelanggan ORDER BY nm_pelanggan LIMIT 0,3;
```

### INNER Join
```mysql
SELECT tabel1.*, tabel2.* FROM tabel1, tabel2
WHERE tabel1.PK=tabel2.FK;

SELECT tabel1.*, tabel2.*
FROM tabel1 INNER JOIN tabel2
ON tabel1.PK=tabel2.FK;
```

### OUTER Join
```mysql
SELECT tabel1.*, tabel2.*
FROM tabel1 LEFT JOIN tabel2
ON tabel1.PK=tabel2.FK;

SELECT tabel1.*, tabel2.*
FROM tabel1 RIGHT JOIN tabel2
ON tabel1.PK=tabel2.FK;
```

### Example 3 table
```mysql
SELECT pesan.id_pesan, produk.id_produk, produk.nm_produk,
detil_pesan.harga, detil_pesan.jumlah
FROM pesan, detil_pesan, produk
WHERE pesan.id_pesan=detil_pesan.id_pesan AND
detil_pesan.id_produk=produk.id_produk
AND pesan.id_pesan='1';
```

### GROUP BY
```mysql
SELECT pesan.id_pesan, pesan.tgl_pesan,
SUM(detil_pesan.jumlah) as jumlah
FROM pesan, detil_pesan
WHERE pesan.id_pesan=detil_pesan.id_pesan
GROUP BY id_pesan;
```

### Having
```mysql
SELECT pesan.id_pesan, COUNT(detil_pesan.id_produk) as
jumlah
FROM pesan, detil_pesan
WHERE pesan.id_pesan=detil_pesan.id_pesan
GROUP BY pesan.id_pesan
HAVING jumlah > 2;
```

### subSelect
```mysql
SELECT id_pelanggan, nm_pelanggan FROM pelanggan
WHERE id_pelanggan IN (SELECT id_pelanggan FROM
pesan);
```

### Update Value Table
```mysql
UPDATE name_table SET field1=’valuenew’
[WHERE kondisi];
```

### Delete Value
```mysql
DELETE FROM name_table [WHERE kondisi];
```

# DCL (Data Control Language)

```mysql
GRANT priv_type
ON {tbl_name | * | *.* | db_name.*}
TO user_name [IDENTIFIED BY 'password']
[WITH GRANT OPTION]

REVOKE priv_type
ON {tbl_name | * | *.* | db_name.*}
FROM user_name
```

### prive type
|ALL PRIVILEGES|FILE|RELOAD|
|---|---|---|
|ALTER|INDEX|SELECT|
|CREATE|INSERT|SHUTDOWN|
|DELETE|PROCESS|UPDATE|
|DROP|REFERENCES|USAGE|

### Show
```mysql
SHOW GRANTS;

SHOW GRANTS FOR 'username';
```

### Drop
```mysql
DROP USER 'jeffrey'@'localhost'
```

# Triggers
```mysql
CREATE TRIGGER name
[BEFORE|AFTER] [INSERT|UPDATE|DELETE]
ON tablename
FOR EACH ROW statement
```

### Example
```mysql
DELIMITER $$
CREATE TRIGGER penjualan.before_insert BEFORE INSERT ON
penjualan.pelanggan
FOR EACH ROW BEGIN
INSERT INTO `log` (description, `datetime`, user_id)
VALUES (CONCAT('Insert data ke tabel pelanggan id_plg
= ', NEW.id_pelanggan), now(), user());
END;
$$
DELIMITER ;
```

### Show
```mysql
show triggers;
```

### Drop
```mysql
DROP TRIGGER tablename.triggername;
```

# View
```mysql
CREATE
[OR REPLACE]
[ALGORITHM = {UNDEFINED | MERGE | TEMPTABLE}]
[DEFINER = { user | CURRENT_USER }]
[SQL SECURITY { DEFINER | INVOKER }]
VIEW view_name [(column_list)]
AS select_statement
[WITH [CASCADED | LOCAL] CHECK OPTION]
```

### example
```mysql
CREATE VIEW lap_jumlah_brg_transaksi
AS
(SELECT pesan.id_pesan, pesan.tgl_pesan,
pelanggan.id_pelanggan, pelanggan.nm_pelanggan,
detil_pesan.jumlah
FROM pesan, detil_pesan, pelanggan
WHERE pesan.id_pesan=detil_pesan.id_pesan AND
pelanggan.id_pelanggan=pesan.id_pelanggan
GROUP BY pesan.id_pesan)
```

### Call
```mysql
SELECT * FROM lap_jumlah_brg_transaksi;
```

### Change
```mysql
ALTER
[ALGORITHM = {UNDEFINED | MERGE | TEMPTABLE}]
[DEFINER = { user | CURRENT_USER }]
```

### Delete
```mysql
DROP VIEW view_name;
```

### Show Create View
```mysql
show create view nameview;
```


# Function Mysql String
- CONCAT (str1, str2, ...)
```mysql
SELECT nm_pelanggan, CONCAT(alamat,' ',telepon)
FROM pelanggan;
```

- CONCAT_WS (separator, str1, str2, ...)
```mysql
SELECT CONCAT_WS (',','Adi','Ida','Edi');
```

- SUBSTRING (string FROM FOR)
```mysql
SELECT SUBSTRING ('Linxcodev',1,4);
```

- LENGTH (string)
```mysql
SELECT LENGTH ('Linxcodev');
```

- LEFT (string, panjang)
```mysql
SELECT LEFT ('Linx Codev', 4);
```

- RIGHT (string, panjang)
```mysql
SELECT LEFT ('Linx Codev', 4);
```

- LTRIM (string)  
```mysql
SELECT LENGTH (' Linxcodev');
```

- RTRIM (string)  
```mysql
SELECT LENGTH ('Linxcodev ');
```

- TRIM (string)
```mysql
SELECT LENGTH (' Linxcodev ');
```

- REPLACE (string, from_str, to_str)
```mysql
SELECT REPLACE ('www.mysql.com', 'w', 'j' );
```

- REPEAT (string, jumlah)
```mysql
SELECT REPEAT ('Mont', 3);
```

- REVERSE (string)
```mysql
SELECT REVERSE ('mysql.com');
```

- LOWER (string)
```mysql
SELECT LOWER ('MySQL');
```

- UPPER (string)
```mysql
SELECT UPPER ('mysql');
```

# Function Mysql Date and Time
- NOW ()
```mysql
SELECT NOW();
```

- MONTH (date)
```mysql
SELECT MONTH (‘1982-06-05’);
```

- WEEK (date)
```mysql
SELECT WEEK (‘1982-06-05’);
```

- YEAR (date)
```mysql
SELECT YEAR (now());
```

- HOUR (time)
```mysql
SELECT HOUR (now());
```

- MINUTE (time)
```mysql
SELECT MINUTE (now());
```

- SECOND (time)
```mysql
SELECT SECOND (now());
```

- TIME_FORMAT(time, format)
```mysql
SELECT DATE_FORMAT (now(), '%d-%M-%Y %H:%i:%s');
```

# Function Numeric
- OPERATION ARITMATIKA
```mysql
SELECT 10+20;
```

- ABS(x)
```mysql
SELECT ABS(-20);
```

- MOD(m, n)
```mysql
SELECT MOD(10,3);
```

- ROUND (x, d)
```mysql
SELECT ROUND(10.3576, 2);
SELECT FLOOR(10.3576);
SELECT CEILING(10.3576);
```

- POW (x, n)
```mysql
SELECT POW(2, 10);
```

- RAND();
```mysql
SELECT RAND();
```

- TRUNCATE(x, d)
```mysql
SELECT TRUNCATE(10.28372, 1);
```

# Etc

- GREATEST(nil1, nil2, ...)
```mysql
SELECT GREATEST(2,5,2,6,3,7,4,2,5,1);
```

- COUNT(*)
```mysql
SELECT COUNT(*) FROM pelanggan;
```

- MAX(range)
```mysql
SELECT MAX(field) FROM nilai_ujian;
```

- MIN(range)
```mysql
SELECT MAX(field) FROM nilai_ujian; 
```

- SUM(range)
```mysql
SELECT SUM(field) FROM nilai_ujian;
```

- AVG(range)
```mysql
SELECT AVG(field) FROM nilai_ujian;
```

- DATABASE()
```mysql
SELECT DATABASE();
```

- USER()
```mysql
SELECT USER();
```

- PASSWORD(str)
```mysql
SELECT PASSWORD('qwerty');
```

- ENCODE(str, pass)
```mysql
SELECT ENCODE('qwerty', 'password');
```

- DECODE(encripted_str, pass)
```mysql
SELECT DECODE('câ┬♠e|', 'password');
```

- MD5(str);
```mysql
SELECT MD5('qwerty');
```

- VERSION()
```mysql
SELECT VERSION();
```

# Function and Procedure
``` mysql
CREATE
[DEFINER = { user | CURRENT_USER }]
PROCEDURE sp_name ([proc_parameter[,...]])
[characteristic ...] routine_body

CREATE
[DEFINER = { user | CURRENT_USER }]
FUNCTION sp_name ([func_parameter[,...]])
RETURNS type
[characteristic ...] routine_body
```

### Show List
```mysql
SHOW [function | procedure] STATUS WHERE Db = 'nmDB';
```

### Create procedure
```mysql
DELIMITER $$
CREATE PROCEDURE hello()
BEGIN
SELECT "Hello World!";
END$$
DELIMITER ;
```

### Call procedure
```mysql
CALL hello();
```

### Example
```mysql
DELIMITER $$
CREATE PROCEDURE jumlahPelanggan2(OUT hasil AS INT)
BEGIN
SELECT COUNT(*) INTO hasil FROM pelanggan;
END$$
DELIMITER ;
```
```mysql
mysql> CALL jumlahPelanggan2(@jumlah);
Query OK, 0 rows affected (0.00 sec)
mysql> SELECT @jumlah AS `Jumlah Pelanggan`;
+------------------+
| Jumlah Pelanggan |
+------------------+
| 5                |
+------------------+
1 row in set (0.02 sec)
```

### Show Proc
```mysql
SHOW CREATE PROCEDURE proc_name
```

### Create Function
```mysql
DELIMITER $$
CREATE FUNCTION jumlahStockBarang(produk VARCHAR(5))
RETURNS INT
BEGIN
DECLARE jumlah INT;
SELECT COUNT(*) INTO jumlah FROM produk
WHERE id_produk=produk;
RETURN jumlah;
END$$
DELIMITER ;
```
```mysql
SELECT jumlahStockBarang('B0001');

+----------------------------+
| jumlahStockBarang('B0001') |
+----------------------------+
|1                           |
+----------------------------+
```

### Change
```mysql
ALTER {PROCEDURE | FUNCTION} sp_name
[characteristic ...]
```

### Drop
```mysql
DROP {PROCEDURE | FUNCTION} [IF EXISTS] sp_name
```

# Export Data Mysql
```mysql
mysqldump -u [uname] -p db_name > db_backup.sql

mysqldump -u [uname] -p --all-databases > all_db_backup.sql

mysqldump -u [uname] -p db_name table1 table2 > table_backup.sql
```

# Import Data Mysql
```mysql
mysql -u username -p -h localhost DATA-BASE-NAME < data.sql
```

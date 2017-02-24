# mysql常用命令

```bash
# 连接mysql
mysql -h localhost -u root -p
```

### DATABASE
```sql
-- DATABASE == SCHEMA
CREATE DATABASE db_test;
SHOW DATABASES;
DROP DATABASE db_test;
USE db_test;
```

### TABLE
```sql
USE db_test;
SHOW TABLES;
DESC tb_emp1; --DESCRIBE tb_emp1
SHOW CREATE TABLE tb_emp1\G;
```

#### CREATE TABLE
```sql
CREATE TABLE tb_emp1
(
  id INT(11) PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(25) NOT NULL UNIQUE,
  deptId INT(11) DEFAULT 111,
  salary FLOAT,
  UNIQUE INDEX UniqIdx(name)
);

-- PRIMARY KEY
CREATE TABLE tb_emp2
(
  id INT(11),
  name VARCHAR(25),
  deptId INT(11),
  salary Float,
  PRIMARY KEY(id,name)
);

-- FOREIGN KEY
CREATE TABLE IF NOT EXISTS tb_emp3
(
  id INT(11) PRIMARY KEY,
  name VARCHAR(25),
  deptId INT(11),
  salary Float,
  CONSTRAINT fk_emp_dept FOREIGN KEY(deptId) REFERENCES tb_dept(id)
);
```

#### ALTER TABLE
```sql
ALTER TABLE tb_emp1 RENAME tb_emp_1;
ALTER TABLE tb_emp_1 MODIFY name VARCHAR(30);
ALTER TABLE tb_emp_1 CHANGE name username VARCHAR(60);
ALTER TABLE tb_emp_1 ADD managerId INT(10);
ALTER TABLE tb_emp_1 ADD column2 INT(11) FIRST;
ALTER TABLE tb_emp_1 ADD column3 INT(11) AFTER name;
ALTER TABLE tb_emp_1 DROP column3;
ALTER TABLE tb_emp_1 MODIFY column2 VARCHAR(12) AFTER name;
ALTER TABLE tb_emp3 DROP FOREIGN KEY fk_emp_dept;
```

#### DROP TABLE
```sql
DROP TABLE IF EXISTS tb_emp_1;
```

#### shuju类型
```
TINYINT, SMALLINT, MEDIUMINT, INT, BIGINT, FLOAT, DOUBLE, DECIMAL
YEAR, TIME, DATE, DATETIME, TIMESTAMP
CHAR, VARCHAR, BINARY, VARBINARY, BLOB, TEXT, ENUM, SET
```

#### INSERT RECORDS
```sql
INSERT INTO tb_user(username, description)
VALUES("haohao", "I'm haohao...");

INSERT INTO tb_user(username, description)
VALUES("haohao", "I'm haohao..."), ("mingming", "I'm ming..");
```

### UPDATE RECORDS
```sql
UPDATE tb_user
SET username="guohaoaa"
WHERE id=6;

UPDATE person
SET info="student"
WHERE id BETWEEN 19 AND 22;
```

### DELETE RECORDS
```sql
DELETE FROM tb_user WHERE id=6;
```

### INDEX
```sql
-- putong index
INDEX(year_publication)
-- 唯一index
UNIQUE INDEX UniqIdx(id)
-- danlie index
INDEX SingleIdx(name(20))
-- zhuhe index
INDEX MultiIdx(id, name, age(100))
-- quanwen index
FULLTEXT INDEX FullTxtIdx(info)

ALTER TABLE book ADD INDEX BkNameIdx (bookname(30))
```

### USER
```sql
CREATE USER 'myuser'@'localhost' IDENTIFIED BY 'mypass';
DROP USER 'myuser'@'localhost'
mysqladmin -u root -p password "root2"

mysqldump -u root -p db_test > C:\db_test.sql
mysqldump -u root -p db_test tb_user > C:\db_test_user.sql

mysql -u root -p db_test < C:\db_test.sql
```

### SELECT RECORDS
```sql
SELECT username, description
FROM tb_user;

SELECT id, username, description
FROM tb_user
WHERE id > 3;

SELECT id, username, description
FROM tb_user
WHERE id IN(3,4);

SELECT id, username, description
FROM tb_user
WHERE id BETWEEN 2 AND 6;

SELECT id, username, description
FROM tb_user
WHERE description LIKE "%hao%";

SELECT id, username, description
FROM tb_user
WHERE description LIKE "__m%";

SELECT id, username, description
FROM tb_user
WHERE description IS NULL;

SELECT id, username, description
FROM tb_user
WHERE id >3 AND description IS NOT NULL;

SELECT id, username, description
FROM tb_user
WHERE id =1 OR description IS NULL;

SELECT DISTINCT username
FROM tb_user;

SELECT id,username,description
FROM tb_user
ORDER BY username DESC; -- ASC

SELECT age, COUNT(*) AS total
FROM tb_user
GROUP BY age WITH ROLLUP;

SELECT age, COUNT(*) AS total
FROM tb_user
GROUP BY age
HAVING age >20
ORDER BY age DESC
LIMIT 2, 1; -- skip 2 limit 1

SUM(), AVG(), MAX(), MIN(), COUNT()

SELECT username, description
FROM tb_user AS u1, tb_info AS u2
WHERE u1.username=u2.username AND u2.id > 2;

SELECT customers.c_id, orders.o_num
FROM customers
LEFT OUTER JOIN orders
ON customers.c_id=orders.c_id;

SELECT customers.c_id, orders.o_num
FROM customers
RIGHT OUTER JOIN orders
ON customers.c_id=orders.c_id;

SELECT customers.c_id, orders.o_num
FROM customers
INNER JOIN orders
ON customers.c_id=orders.c_id AND customers.c_id=1001;

SELECT num
FROM tb_user
WHERE num > ANY(SELECT num2 FROM tbl2);

SELECT num
FROM tb_user
WHERE num > ALL(SELECT num2 FROM tbl2);

SELECT num
FROM tb_user
WHERE EXISTS
(SELECT s_name FROM suppliers WHERE s_id=107);

SELECT num
FROM tb_user
WHERE o_num IN
(SELECT s_name FROM suppliers WHERE s_id=107);

SELECT num
FROM tb_user
WHERE o_num <>
(SELECT s_name FROM suppliers WHERE s_id=107);

SELECT s_id, f_name, f_price
FROM fruits
WHERE f_price < 9
UNION ALL
SELECT s_id, f_name, f_price
FROM fruits
WHERE s_id IN(101,103);

SELECT CONCAT(TRIM(s_name),'(',TRIM(s_city),')')
AS suppliers_title
FROM suppliers
ORDER BY s_name

SELECT id, username, description
FROM tb_user
WHERE description REGEXP 'hao$';

```

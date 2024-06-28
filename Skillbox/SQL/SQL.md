# Задача 1

SELECT orderNumber, productCode, quantityOrdered * priceEach AS totalPrice
FROM orderdetails
ORDER BY totalPrice DESC
LIMIT 10

# Задача 2

SELECT orderNumber, SUM(quantityOrdered * priceEach) AS totalPrice
FROM orderdetails
GROUP BY orderNumber
HAVING totalPrice >  59000
ORDER BY totalPrice DESC

# Задача 3

SELECT orderdetails.orderNumber, orderDate, status, SUM(quantityOrdered * priceEach) AS totalPrice
FROM orderdetails
INNER JOIN orders
ON orderdetails.orderNumber = orders.orderNumber
GROUP BY orderNumber
HAVING totalPrice >  59000
ORDER BY totalPrice DESC

# Задача 4

SELECT  
 contactFirstName,
 contactLastName,
 country,
 orderdetails.orderNumber,
 orderDate,
 status,
 SUM(quantityOrdered * priceEach) AS totalPrice
FROM orderdetails
INNER JOIN orders
ON orderdetails.orderNumber = orders.orderNumber
INNER JOIN customers
ON orders.customerNumber = customers.customerNumber
GROUP BY orderNumber
HAVING totalPrice >  59000
ORDER BY totalPrice DESC

# Задача 5

SELECT productName, SUM(quantityOrdered * priceEach) AS total
FROM orderdetails
INNER JOIN products
ON orderdetails.productCode = products.productCode
GROUP BY productName
ORDER BY total DESC
LIMIT 10


# Задача 6

SELECT firstName, lastName, contactFirstName, contactLastName
FROM employees
LEFT JOIN customers
ON employees.employeeNumber = customers.salesRepEmployeeNumber
UNION
SELECT firstName, lastName, contactFirstName, contactLastName
FROM employees
RIGHT JOIN customers
ON employees.employeeNumber = customers.salesRepEmployeeNumber

Задача 7

SELECT t1.firstName, t1.lastName, t1.jobTitle, t2.firstName AS contactFirstName, t2.lastName AS contactLastName
FROM employees AS t1
LEFT JOIN employees AS t2
ON t1.employeeNumber = t2.reportsTo

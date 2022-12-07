/* joins: select all the computers from the products table:
SELECT * from bestbuy.products WHERE CategoryID = 1;
using the products table and the categories table, return the product name and the category name */
SELECT p.Name, c.Name
FROM products AS p
INNER JOIN categories AS c
ON p.CategoryID = c.CategoryID
WHERE c.Name = 'Computers';
/* joins: find all product names, product prices, and products ratings that have a rating of 5 */
SELECT p.Name, p.Price, r.Rating
FROM products AS p
JOIN reviews AS r
ON p.ProductID = r.ProductID
WHERE r.Rating = 5;
/* joins: find the employee with the most total quantity sold.  use the sum() function and group by */
SELECT e.EmployeeID, e.FirstName, e.LastName, Sum(Quantity) as Quantity
FROM employees AS e
INNER JOIN sales AS s ON e.EmployeeID = s.EmployeeID
GROUP BY e.EmployeeID
ORDER BY Quantity DESC;
/* joins: find the name of the department, and the name of the category for Appliances and Games */
SELECT d.Name AS Department, c.Name AS Category
FROM categories AS c
INNER JOIN departments as d
ON d.DepartmentID = c.DepartmentID
WHERE c.Name = "Appliances" OR c.Name = "Games";
/* joins: find the product name, total # sold, and total price sold,

 for Eagles: Hotel California --You may need to use SUM() */
SELECT products.Name AS Product, SUM(sales.Quantity) AS `Total Units Sold`,
SUM(sales.Quantity * sales.PricePerUnit) AS Gross_Revenue
FROM sales
INNER JOIN products
ON sales.ProductID = products.ProductID
WHERE products.Name LIKE "%Hotel%California%";
/* joins: find Product name, reviewer name, rating, and comment on the Visio TV. (only return for the lowest rating!) */
SELECT p.Name, r.reviewer, r.rating, r.comment
FROM products as p
JOIN reviews as r
ON p.ProductID = r.ProductID
WHERE r.rating = 1 AND p.name LIKE "Visio%TV";
-- ------------------------------------------ Extra - May be difficult

/* Your goal is to write a query that serves as an employee sales report.

This query should return the employeeID, the employee's first and last name, the name of each product, how many of that product they sold */
SELECT employees.EmployeeID, employees.FirstName, employees.LastName, 
products.Name, SUM(sales.Quantity) AS Total_Units_Sold, SUM(Quantity * PricePerUnit) AS Gross_Revenue
FROM employees
INNER JOIN sales
ON employees.EmployeeID = sales.EmployeeID
INNER JOIN products
ON sales.ProductID = products.ProductID
GROUP BY sales.EmployeeID, sales.ProductID
ORDER BY sales.EmployeeID, Gross_Revenue DESC;
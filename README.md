# SQL

1. Write a query that displays state and provides an average training cost for all employees from Utah.  Don’t include employees with the last name ‘Matsko’.  Limit the output to two decimal places
SELECT CAST(AVG(TrainingCost) As decimal (8,2)) As 'Avg training cost', e.state
FROM employee as e JOIN Employee_Training as et
	ON e.EmployeeID = et.EmployeeID
		JOIN Training_Course as tc
			ON et.TrainingID = tc.TrainingID 
WHERE e.State = 'UT' AND e.lastname <> 'Matsko'
GROUP BY e.state;

2.Create a view called vSTATE that contains the full name of the employee along with the full spelling of the state using a CASE EXPRESSION. 
CREATE VIEW vSTATE as 
SELECT CONCAT (FirstName, Lastname) as 'Name',
	CASE State
	 WHEN 'UT' then 'Utah' 
	 WHEN 'CA' Then 'California'
	 WHEN 'TX' then 'Texas'
	 WHEN 'MT' then 'Montana'
	 End as 'State'
FROM Employee;

3. In the current product database, if the quality is 1, the actual quality is Very Good.  If the quality is 2, the actual quality is About Uncirculated.  Finally, if the quality is 3, the actual quality is Mint State.  Write an SQL view called vQuality that creates a new virtual column that includes actual quality descriptions.  Show the ProductID, ProductName, and New Column.
CREATE VIEW vQuality as 
SELECT ProductID, ProductName,
	CASE QualityID
	 WHEN 1 then 'Very Good' 
	 WHEN 2 Then 'About Uncirculated'
	 WHEN 3 then 'Mint State'
	 End as 'Actual Quality Description'
FROM Product;

4. Write an SQL query to show the day of the week each customer purchased a product.  Include an alias when needed.  Order by Last Name from A –Z.
SELECT Lastname, DATENAME(dw, saledate) As 'day of the week of Purchase' 
 FROM Sale as s join Customer as c 
  ON s.CustomerID = c.customerID
  ORDER BY lastName asc;
  
  
  
  
  
  

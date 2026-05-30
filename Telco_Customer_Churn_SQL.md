# SQL QUERIES 


## Total Customers and Churned Cusomers

SELECT
COUNT(*) AS Total_Customers,
SUM(CASE WHEN Churn_Label = "Yes", THEN 1 ELSE 0 END) AS Churned_Customers
FROM Telco_Customer_Churn;



## Churn by contract type 

SELECT
Contract,
COUNT(*) AS Customers
FROM Telco_Customer_Churn
WHERE Churn_Label = "Yes"
GROUP BY Contract;


## Average Monthly Charges by Churn

SELECT 
AVG(Monthly_Charges) as Averrage_Monthly_Charges
FROM Telco_Customer_Churn
GROUP BY Churn_Label;


## Churn by Tenure Group

SELECT 
CASE 
 WHEN Tenure_Months < 12 THEN "New Customer"
ELSE 
"Existing Customer"
END AS Customer_Type,

COUNT(*) AS Customers
FROM Telco_Customer_Churn
GROUP BY
CASE 
 WHEN Tenure_Months < 12 THEN "New Customer"
ELSE
"Existing Customer"
END AS Customer_Type;


## Payment Method Analysis

SELECT
COUNT(*) AS Churned_Customers,
Payment_Method
FROM
Telco_Customer_Churn
WHERE Churn_Label = "Yes"
GROUP BY Payment_Method
ORDER BY Churned_Customers;

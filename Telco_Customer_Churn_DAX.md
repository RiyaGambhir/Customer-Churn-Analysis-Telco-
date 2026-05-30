#DAX MEASURES - 


## Total Customers

Total Customers = 
COUNTROWS('Telco_Customer_Analysis') 



## Total Churn Customers

Total Churn Customers =
CALCULATE(COUNTROWS('Telco_Customer_Analysis),
('Telco_Customer_Analysis'[Churn Label] = "Yes")



## Churn Rate

Churn Rate =
DIVIDE([Total Churn Customers], COUNTROWS('Telco_Customer_Analysis'), 0)



## Total Monthly Revenue

Total Monthly Revenue =
SUM('Telco_Customer_Analysis'[Monthly Charges])



## Average Revenue per user

Average Revenue per  user =
AVERAGE('Telco_Customer_Analysis'[Monthly Charges])



## Average Revenue per user churned

Average revenue per user churned =
CALCULATE[Average Revenue per user],
'Telco_Customer_Analysis'[Churn Label] = "Yes"



## Revenue at risk

Revenue at risk =
CALCULATE(SUM('Telco_Customer_Analysis'[Monthly Charges]), 
'Telco_Customer_Analysis'[Churn Label] = "Yes")


## Revenue at risk %

Revenue at risk % =
DIVIDE([Revenue at risk], [Total Customers],0)

_______________________________________________________

# CALCULATED COLUMNS - 


## High risk flag

High risk flag =
IF('Telco_Customer_Analysis'[Contract] = "Month-to-month"
   & 'Telco_Customer_Analysis'[Tenure Months] <=12,
   "High Risk",
   "Standard"
 )



## Pricing Tier

Pricing Tier = 
SWITCH(
TRUE(),
'Telco_Customer_Analysis'[Monthly Charges] < $35, "Low(<$35),
'Telco_Customer_Analysis'[Monthly Charges] < $70, "Medium($35-70),
"High(>$0)
)


## Pricing Tier Sort

Pricing Tier Sort =
SWITCH(
TRUE(),
'Telco_Customer_Analysis'[Monthly Charges] < $35, 1,
'Telco_Customer_Analysis'[Monthly Charges] < $70, 2,
3
)


## Tenure Cohort

Tenure Cohort =
SWITCH(
TRUE(),
'Telco_Customer_Analysis'[Tenure Months] < 12, "0-12 months",
'Telco_Customer_Analysis'[Tenure Months] <= 24, "13-24 months",
'Telco_Customer_Analysis'[Tenure Months] <= 48, "25-48 months",
"49+ months"
)


## Tenure Cohort Sort 

Tenure Cohort Sort =
SWWITCH(
TRUE(),
'Telco_Customer_Analysis'[Tenure Months] <= 12, 1,
'Telco_Customer_Analysis'[Tenure Months] <=24, 2,
'Telco_Customer_Analysis'[Tenure Months] <=48, 3,
4
)





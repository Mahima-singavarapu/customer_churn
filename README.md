A synthetic dataset of a fake company called databel is analysed for analysing the customer churn.

Different measures have been created to perform the analysis:

Unique customers count:
Number of Unique Customers = DISTINCTCOUNT('Databel - Data'[Customer ID])

Total number of customers:
Number of Customers = COUNTROWS('Databel - Data')

Churned customers:
Number of Churned Customers = CALCULATE( COUNTROWS('Databel - Data'), 'Databel - Data'[churnbio] = 1)

GB consumption:
Grouped Consumption = 
SWITCH(
    TRUE(),
    'Databel - Data'[Avg Monthly GB Download] < 5, "Less than 5 GB",
    'Databel - Data'[Avg Monthly GB Download] >= 5 &&
    'Databel - Data'[Avg Monthly GB Download] < 10, "Between 5 and 10 GB",
    'Databel - Data'[Avg Monthly GB Download] >= 10, "10 or more GB"
)

Data by age:
Demographics = IF(
    'Databel - Data'[Age] <= 30, 
    "Under30",
    IF(
        'Databel - Data'[Age] >= 65,
        "Senior",
        "Other"
    )
)

Data by contract:
Contract Category = SWITCH(
    TRUE(),
    'Databel - Data'[Contract Type] = "One Year", "Yearly",
    'Databel - Data'[Contract Type] = "Two Year", "Yearly",
    'Databel - Data'[Contract Type] = "month-to-month", "Monthly",
    "Unknown"
)

churnbio = IF('Databel - Data'[Churn Label] = "Yes", 1, 0)

Churn rate = DIVIDE([Number of Churned Customers], [Number of Customers])

Avg Extra International Charges = SUM('Databel - Data'[Extra International Charges])/ [Number of Customers]

Avg Extra Data Charges = SUM('Databel - Data'[Extra Data Charges])/ [Number of Customers]

Avg Customer Service Calls = AVERAGE('Databel - Data'[Customer Service Calls])


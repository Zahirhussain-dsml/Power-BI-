METHODOLOGY:
1) Importing Data 
Import the "Loan Details" and "Borrower Details" sheets from the "bank loan.xlsx" file into Power BI.
2) Transformation Using Power Query
Data Cleaning:
Handling Missing Values and Duplicates: 
1.	Replace missing values (null) in the 'emp_ length' column of the "Borrower Details" table with '0 year'. 
2.	Remove rows with missing values in the 'last_ pymnt_ d' and 'delinq_2yrs' columns. 
3.	Remove duplicate rows in the 'id' column of the "Loan Details" table. 
Dealing with Inconsistencies: 
4.	Ensure words in the 'purpose' column are separated by spaces instead of underscores (e.g., "credit card" instead of "credit_card"). 
5.	Format the 'purpose' and 'home_ownership' columns to proper case.
Data Transformation:
Column Transformation:
6.	Change the data type of the 'total_pymnt' column to 'Fixed decimal number'. 
7.	Round off the numbers in the 'funded_amnt' column to 2 decimal places.
Column Renaming: 
8.	Rename the column 'issue_d' to 'issue_date'. 
9.	Rename the column 'last_pymnt_d' to 'last_pymnt_date'.
Creating New Columns: 
10.	Create a new custom column named 'total_amount_paid' to calculate the total amount paid by each borrower by subtracting 'out_prncp' from 'total_pymnt'.
11.	Add a new conditional column named 'delinquency_status' to identify if the borrower has any delinquencies. If the number of delinquencies in 'delinq_2yrs' is greater than 0, the status should be "Delinquent", otherwise "Not Delinquent".
Column Dropping: 
12.	Remove the 'sub_grade' column as that does not significantly contribute to the analysis.

3)	Data Modeling: 
13.	Identify the common column between both the tables and establish relationships between the two tables. Ensure the cross-filter direction is set to "Both". This step is crucial for enabling cross-table analysis and ensuring data integrity within the dataset.

4)	Creating Measures and Calculated Columns using DAX 

14.	Create a new calculated column named 'remaining_installments' using DAX in the "BorrowerDetails" table to calculate the number of remaining installments by dividing the remaining principal amount ('out_prncp') by the monthly installment amount ('installment') and round up the result using the CEILING() function to account for any partial payments.
15.	Create a measure named 'Non-Verified Borrowers Count' using DAX to count the number of loans that have been 'Not Verified'.
16.	Create a measure named 'Fully Paid Loan Percentage' to calculate the percentage of fully paid loans. Divide the number of loans with a "Fully Paid" loan status by the total number of loans and then format this measure as Percentage.




Report 1: Loan Performance Analysis 
The Loan Performance Analysis report aims to provide insights into the performance of loans based on various factors such as loan amount, loan status, term, interest rate, and purpose.
1)	Total Funded Amount: Create a card visual to display the total funded amount.

2)	Fully Paid Loan Percentage: Create a gauge chart to display the 'Fully Paid Loan Percentage' measure.

3)	Average Interest Rate by Term: Create a multi-row card to show the average interest rate for each term.

4)	Loan Status Distribution: Create a pie chart to visualize the sum of total payments by loan status.

5)	Loan Amount by Purpose: Create a treemap to show the average loan amount by purpose.

6)	Installment Over Time: Create a line chart to visualize the sum of installments by Year and Quarter of the issue date.

7)	Maximum Total Amount Paid by Loan Status: Create a column chart to display the maximum total amount paid by loan status.

8)	Minimum Annual Income by Grade: Create a funnel chart to show the minimum annual income by grade. 

9)	Issue Date Slicer: Add a slicer for the Month of the issue date to enable dynamic data exploration.










Report 2: Borrower Profile Analysis 
The Borrower Profile Analysis report aims to provide insights into the characteristics of borrowers such as home ownership, annual income, employment length, verification status, debt-to-income ratio, and delinquency history.
1)	KPI Visual: Create a KPI visual with the sum of total payment as the value, the year of last payment date as the trend axis, and the sum of loan amount as the target. Round off to 2 decimal points and format as $ currency.

2)	Average of Annual Income: Display the average of annual income using a card visual.

3)	Non-Verified Borrowers Count: Display the count of non-verified borrowers using a card visual.

4)	Average Debt-to-Income by Delinquency Status: Create a multi-row card to show the average debt-to-income ratio by delinquency status.

5)	Sum of Loan Amount by Home Ownership: Create a table to show the total loan amount by home ownership.

6)	Average Remaining Principal by Verification Status: Create a donut chart to display the average remaining outstanding principal by verification status.

7)	Sum of Delinquencies by Home Ownership: Create a bar chart to show the total number of delinquencies in the past 2 years by home ownership and filter the visual to display only Mortgage, Rent, and Own.

8)	Max Remaining Installments by Employment Length: Create a treemap to show the maximum remaining installments by employment length.

9)	Total Amount Paid and Funded Amount Over Time: Create a line chart to display the sum of total amount paid and the sum of funded amount by the year of last payment date. 

10)	Purpose Slicer: Add a slicer for loan purpose to enable dynamic data exploration.

# Personal Finance Dashboard


## Introduction
This report delves into the insights gleaned from your personal finance dashboard. This dashboard serves as a valuable tool for gaining a comprehensive picture of your financial health. By analyzing the data presented, we can identify areas for improvement, optimize your financial strategies, and ultimately achieve your financial goals.

## Problem Statement /  Objective

1: Analyze income and expenses to determine if spending is exceeding income. If so, identify areas for potential cost-saving measures to create a budget surplus.
2: Evaluate the gap between current income and targeted income and explore strategies to increase income or adjust spending to meet financial goals.

3: Analyze current savings and available balance to assess progress towards savings goals. Identify areas to optimize the budget and allocate more funds towards savings.

4: If you have debt, analyze your debt repayment progress to understand the effectiveness of your current strategy. Explore options to accelerate debt repayment if needed.

5: Analyze data across income, expenses, savings, and debt to gain a comprehensive understanding of your overall financial health.

6: Gain insights into your spending habits to identify areas for potential optimization and cost reduction.

7: Develop a budget that allocates your income towards essential expenses, savings goals, and debt repayment.

8: Track your financial progress over time to monitor the effectiveness of your financial strategies and make adjustments as needed.

9: Identify opportunities to increase your income or explore additional income streams to achieve your financial goals faster.

## Data Sourcing
i have downloaded xls file then i extracted into a powerbi for cleaning, analysis and visualization
it contains - 3 sheets/tables

- main data>> 300 rows and 7 columns
- income goals>> 12 rows and 2 columns
- distribution>> 6 rows and 4 columns

## Data Transformation/Cleaning
  
- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : It was observed that in none of the columns errors & empty values were present.
- Step 4 : Promote headers and change the data type
- Step 5: Close and apply 
## Data Modelling
snap of data model structure
![Modelling data](https://github.com/AdityaaPujari/Personal-Finance-Dashboard/assets/131788257/41c601b4-d9ef-43eb-af49-15265dd12a77)

## Dax Created
- Total Income = CALCULATE([Total Amount],FILTER('Main Data','Main Data'[Main Type]="income"))
- Total Expences = CALCULATE([Total Amount],FILTER('Main Data','Main Data'[Main Type]="Expenses"))
- Total Amount = SUM('Main Data'[Amount])
- Side Income = CALCULATE([Total Income],FILTER('Main Data','Main Data'[Category]="Side Income"))
- Records = COUNTROWS('Main Data')
- Personal = CALCULATE([Total Amount],FILTER('Main Data','Main Data'[Category]="Personal"))
- Main Income = CALCULATE([Total Income],FILTER('Main Data','Main Data'[Category]="Main Income"))
- Housing = CALCULATE([Total Amount],FILTER('Main Data','Main Data'[Category]="Housing"))
- Gauge Caption = 
  VAR Variance_Goal=[Total Income]-[Total Income Target]
  VAR Month_Selected=SELECTEDVALUE('Main Data'[Month])
  RETURN
  IF(Variance_Goal>1,"Total Income is greater than Targeted income"&"
  "&FORMAT(Variance_Goal,"$#,##"),"You could no met your target in "&"
  "&Month_Selected&" ."&FORMAT(Variance_Goal,"$#,##")&"Lower than target")
- Available Balance = [Total Amount]-[Total Expences]
- Alert = 
  VAR No_late_pay=CALCULATE([Records],FILTER('Main Data','Main Data'[Status]="unpaid"))
  VAR late_pay_Amount=CALCULATE([Total Amount],FILTER('Main Data','Main Data'[Status]="unpaid"))

  // late_pay_Amount
  var selected_month=SELECTEDVALUE('Main Data'[Month])
  var Conjunction_in="in"
  var select_in=IF(selected_month=BLANK(),"",Conjunction_in)
  RETURN
  IF(No_late_pay>1,"You have" & No_late_pay&"debt due to be paid, worth"&FORMAT(late_pay_Amount,"$#,##")&" "& select_in&""& selected_month,"No unpaid debt in "&selected_month
- Unpaid Debt = CALCULATE([Total Amount],'Main Data'[Status]="unpaid")

## Analysis and Visualization
### Income Dashboard
![income](https://github.com/AdityaaPujari/Personal-Finance-Dashboard/assets/131788257/03a08084-9861-4701-be44-9e68e9ab98d6)

### Key Performance Indicators (KPIs):
- Income: Analyze your total income streams, including salary, investments, or any other sources of income.
- Expenses: Categorize and track your expenses to understand where your money is going.
- Savings: Evaluate your current savings rate and progress towards your financial goals.
- Net Worth: Track your net worth, which is the total value of your assets minus your liabilities.

### Income Breakdown
- Main Income
- Side income

### Income Trends
- NOV showing highest income ($1,68,282) and july showing lowest income($236)

 ### Expenses Dashboard 
![Expenses](https://github.com/AdityaaPujari/Personal-Finance-Dashboard/assets/131788257/7c3f1072-9fc8-420d-9b5d-82409a247f7f)

## Actionable Recommendations:
#### Based on the analysis of your personal finance dashboard, here are some potential recommendations:

- Create a Budget: If you don't have a budget yet, consider creating one to allocate your income towards your expenses, savings goals, and debt repayment.
- Optimize Spending: Identify areas where you can cut back on unnecessary expenses and reallocate those funds towards your savings goals or debt repayment.
- Increase Income: Explore opportunities to increase your income through career advancement, freelance work, or side hustles.
- Debt Repayment Plan: If you have debt, develop a debt repayment plan to prioritize high-interest debt and accelerate the repayment process.
- Automate Savings: Automate your savings transfers to ensure consistent saving towards your financial goals.
- Review Regularly: Regularly review your personal finance dashboard to monitor progress and adjust your strategies as needed.

## Conclusion:
By leveraging the insights from personal finance dashboard and implementing the recommended actions, you can gain greater control over your finances, achieve your savings goals, and build a secure financial future. Remember, this is an ongoing process, and consistent monitoring and adjustments will be crucial for your financial success.





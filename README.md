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

### Data Sourcing
i have downloaded xls file then i extracted into a powerbi for cleaning, analysis and visualization
it contains - 3 sheets/tables

- main data>> 300 rows and 7 columns
- income goals>> 12 rows and 2 columns
- distribution>> 6 rows and 4 columns

### Data Transformation/Cleaning
  
- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : It was observed that in none of the columns errors & empty values were present.
- Step 4 : Promote headers and change the data type
- Step 5: Close and apply 
### Data Modelling
snap of data model structure
![Modelling data](https://github.com/AdityaaPujari/Personal-Finance-Dashboard/assets/131788257/41c601b4-d9ef-43eb-af49-15265dd12a77)

### Dax Created
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

### Analysis and Visualization


### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : It was observed that in none of the columns errors & empty values were present.
- Step 5 : For calculating average delay time, null values were not taken into account as only less than 1% values are null in this column(i.e column named "Arrival Delay") 
- Step 6 : In the report view, under the view tab, theme was selected.
- Step 7 : Since the data contains various ratings, thus in order to represent ratings, a new visual was added using the three ellipses in the visualizations pane in report view. 
- Step 8 : Visual filters (Slicers) were added for four fields named "Class", "Customer Type", "Gate Location" & "Type of travel".
- Step 9 : Two card visuals were added to the canvas, one representing average departure delay in minutes & other representing average arrival delay in minutes.
           Using visual level filter from the filters pane, basic filtering was used & null values were unselected for consideration into average calculation.
           
           Although, by default, while calculating average, blank values are ignored.
- Step 10 : A bar chart was also added to the report design area representing the number of satisfied & neutral/unsatisfied customers. While creating this visual, field named "Gender" was also added to the Legends bucket, thus number of customers are also seggregated according the gender. 
- Step 11 : Ratings Visual was used to represent different ratings mentioned below,

  (a) Baggage Handling

  (b) Check-in Services
  
  (c) Cleanliness
  
  (d) Ease of online booking
  
  (e) Food & Drink
  
  (f) In-flight Entertainment

  (g) In-flight Service
  
  (h) In-flight wifi service
  
  (i) Leg Room service
  
  (j) On-board service
  
  (k) Online boarding
  
  (l) Seat comfort
  
  (m) Departure & arrival time convenience
  
In our dataset, Some parameters were assigned value 0, representing those parameters are not applicable for some customers.

All these values have been ignored while calculating average rating for each of the parameters mentioned above.

- Step 12 : In the report view, under the insert tab, two text boxes were added to the canvas, in one of them name of the airlines was mentioned & in the other one company's tagline was written.
- Step 13 : In the report view, under the insert tab, using shapes option from elements group a rectangle was inserted & similarly using image option company's logo was added to the report design area. 
- Step 14 : Calculated column was created in which, customers were grouped into various age groups.

for creating new column following DAX expression was written;
       
        Age Group = 
        
        if(airline_passenger_satisfaction[Age]<=25, "0-25 (25 included)",
        
        if(airline_passenger_satisfaction[Age]<=50, "25-50 (50 included)",
        
        if(airline_passenger_satisfaction[Age]<=75, "50-75 (75 included)",
        
        "75-100 (100 included)")))
        
Snap of new calculated column ,

![Snap_1](https://user-images.githubusercontent.com/102996550/174089602-ab834a6b-62ce-4b62-8922-a1d241ec240e.jpg)

        
- Step 15 : New measure was created to find total count of customers.

Following DAX expression was written for the same,
        
        Count of Customers = COUNT(airline_passenger_satisfaction[ID])
        
A card visual was used to represent count of customers.

![Snap_Count](https://user-images.githubusercontent.com/102996550/174090154-424dc1a4-3ff7-41f8-9617-17a2fb205825.jpg)

        
 - Step 16 : New measure was created to find  % of customers,
 
 Following DAX expression was written to find % of customers,
 
         % Customers = (DIVIDE(airline_passenger_satisfaction[Count of Customers], 129880)*100)
 
 A card visual was used to represent this perecntage.
 
 Snap of % of customers who preferred business class
 
 ![Snap_Percentage](https://user-images.githubusercontent.com/102996550/174090653-da02feb4-4775-4a95-affb-a211ca985d07.jpg)

 
 - Step 17 : New measure was created to calculate total distance travelled by flights & a card visual was used to represent total distance.
 
 Following DAX expression was written to find total distance,
 
         Total Distance Travelled = SUM(airline_passenger_satisfaction[Flight Distance])
    
 A card visual was used to represent this total distance.
 
 
 ![Snap_3](https://user-images.githubusercontent.com/102996550/174091618-bf770d6c-34c6-44d4-9f5e-49583a6d5f68.jpg)
 
 - Step 18 : The report was then published to Power BI Service.
 
 
![Publish_Message](https://user-images.githubusercontent.com/102996550/174094520-3a845196-97e6-4d44-8760-34a64abc3e77.jpg)

# Snapshot of Dashboard (Power BI Service)

![dashboard_snapo](https://user-images.githubusercontent.com/102996550/174096257-11f1aae5-203d-44fc-bfca-25d37faf3237.jpg)

 
 # Report Snapshot (Power BI DESKTOP)

 
![Dashboard_upload](https://user-images.githubusercontent.com/102996550/174074051-4f08287a-0568-4fdf-8ac9-6762e0d8fa94.jpg)

# Insights

A single page report was created on Power BI Desktop & it was then published to Power BI Service.

Following inferences can be drawn from the dashboard;

### [1] Total Number of Customers = 129880

   Number of satisfied Customers (Male) = 28159 (21.68 %)

   Number of satisfied Customers (Female) = 28269 (21.76 %)

   Number of neutral/unsatisfied customers (Male) = 35822 (27.58 %)

   Number of neutral/unsatisfied customers (Female) = 37630 (28.97 %)


           thus, higher number of customers are neutral/unsatisfied.
           
### [2] Average Ratings

    a) Baggage Handling - 3.63/5
    b) Check-in Service - 3.31/5
    c) Cleanliness - 3.29/5
    d) Ease of online booking - 2.88/5
    e) Food & Drink - 3.21/5
    f) In-flight Entertainment - 3.36/5
    g) In-flight service - 3.64/5
    h) In-flight Wifi service - 2.81/5
    i) Leg room service - 3.37/5
    j) On-board service - 3.38/5
    k) Online boarding - 3.33/5
    l) Seat comfort - 3.44/5
    m) Departure & arrival convenience - 3.22/5
  
  while calculating average rating, null values have been ignored as they were not relevant for some customers. 
  
  These ratings will change if different visual filters will be applied.  
  
  ### [3] Average Delay 
  
      a) Average delay in arrival(minutes) - 15.09
      b) Average delay in departure(minutes) - 14.71
Average delay will change if different visual filters will be applied.

 ### [4] Some other insights
 
 ### Class
 
 1.1) 47.87 % customers travelled by Business class.
 
 1.2) 44.89 % customers travelled by Economy class.
 
 1.3) 7.25 % customers travelled by Economy plus class.
 
         thus, maximum customers travelled by Business class.
 
 ### Age Group
 
 2.1)  21.69 % customers belong to '0-25' age group.
 
 2.2)  52.44 % customers belong to '25-50' age group.
 
 2.3)  25.57 % customers belong to '50-75' age group.
 
 2.4)  0.31 % customers belong to '75-100' age group.
 
         thus, maximum customers belong to '25-50' age group.
         
### Customer Type

3.1) 18.31 % customers have customer type 'First time'.

3.2) 81.69 % customers have customer type 'returning'.
       
       thus, more customers have customer type 'returning'.

### Type of travel

4.1) 69.06 % customers have travel type 'Business'.

4.2) 30.94 % customers have travel type 'Personal'.

        thus, more customers have travel type 'Business'.

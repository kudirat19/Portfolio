# Customer Churn Analysis

## Table of Contents
- [Project Overview](#project-overview)
- [Data sources](#data-sources)
- [Tools](#tools)
- [Data cleaning](#data-cleaning)
- [Data analysis](#data-analysis)
- [Results](#results)
- [Recommendation](#recommendation)
- [limitations](#limitations)
- [Credits](#credits)

### Project Overview
This dashboard helps the company understand their customers better. It helps the company know if their customers are satisfied with their services. Through different ratings, they get to know their improvement area, & thus they can improve their services by identifying these area. It also lets them know the churn rate, causes of customer churn, thus since by using this dashboard they have identified this problem, they can further work on factors responsible for these.

Since, 83% number of churn customers  are more than 17% satisfied customers, thus in all they must work on improving their services.

Also since the churn customers are mostly male with 73% and Female with 27%, thus they must try to reduce it.


### Data Sources

The data used was primary data from the company.

### Tools

-Excel : Data Cleaning

-PowerBI : Creating Report and dashboard

### Data cleaning

(1)  Load data into Power BI Desktop, dataset is a csv file.

(2)  Open power query editor & in view tab under Data preview section, check "Table view" option.

(3)  Also since by default, profile will be opened only for 324 rows.

(4)  It was observed that in none of the columns errors & empty values were present except column named "Email","Channel_Desc" and "Channel_ID".

(5)  For calculating total number of customers, null values were not taken into account as only less than 1% values are null in the column i.e column named "Email", "Channel_Desc" and "Channel_ID"

(6)  In the report view, under the view tab, theme was selected.

    Note: The theme used and the font sizes were according to the company's guidelines for the project

(7)  Since the data contains various ratings, thus in order to represent ratings, a new visual was added using the three ellipses in the visualizations pane in report view which open to different pages of visualizations named "Home page", "All Customers", "Churned Customer's Details".

(8)  Visual filters (Slicers) were added for two fields named "Customer ID", and "Account ID".

(9)  Eleven card visuals were added to the canvas, representing total number of customers, total number of churn customer, % of Male customer, % of female customer, etc. Using visual level filter from the filters pane, basic filtering was used & null values were unselected for consideration into average calculation.

Note: blank values were ignored when calculating avarege.
    
(10)  Five bar chart was also added to the report design area representing the number of customers versus tenure and channel_id. Also, number of churned customers versus tenure, payments, and channel_id.

(11)  One table was added to the report design area representing the number of customers versus the location.

(12)   Ratings Visual was used to represent different ratings mentioned below,

  * Total number of males customer
  * Total number of female customer
  * Total number of churned male customer
  * Total number of churned female customer
  * Total number  of Credit card
  * Total number of cash
  * Total number of Bank Transfer


### Data Analysis

In our dataset, Some parameters were assigned value 0, representing those parameters are not applicable for some customers.

All these values have been ignored while calculating average rating for each of the parameters mentioned above.

(a)  In the report view, under the insert tab, a text box was added to the canvas, a short description of customer churn was written.

Snap

(b)  Calculated column was created in which, payment method were grouped into various groups.

  For creating new column following DAX expression was written;

    Payments = 
    
    SWITCH(
        TRUE(),
        'Branch_research'[payment method] = "prepaid card", "Bank transfer",
        'Branch_research'[payment method] = "credit card", "Credit card",
        'Branch_research'[payment method] = "express credit", "Cash",
    
    )

    
Snap of new calculated column 

![pay_meth](https://github.com/user-attachments/assets/1fe83ccc-31fa-469f-b157-ec76fb6572fc)

(c)  Another column was created for Sol_ID.

For creating new column following DAX expression was written;

    Tenure category = 
    
    IF(
    'Branch_research'[sol_ID] <= 215, 
    "short", 
    "long"
    )

    
Snap of new calculated column 

![tenu](https://github.com/user-attachments/assets/9dfa4a6f-afbf-48c5-915b-b964ccdd5ad7)

(d)  Another column was created for Channel_ID.

For creating new column following DAX expression was written;

    Channel ID = 
    
    SWITCH(
    TRUE(),
    'Branch_research'[channel_ID] = "Alat", "Alat",
    'Branch_research'[channel_ID] = "cdapp", "cdapp",
    'Branch_research'[channel_ID] = "smel", "smel",
    ISBLANK('Branch_research'[channel_ID]), "agent",
    )



(e) Another coulumn was created for Account Balance

For creating new column following DAX expression was written;

    Churn = 
    
    IF(
    'Branch_research'[account balance] <= 40, 
    "yes", 
    "no"
    )

Snap of new calculated column 

![acctb_churn](https://github.com/user-attachments/assets/6ce5f7a1-dbd5-47a8-b9b4-4833b26582d6)



(13)  New measure was created to find total count of customers.

Following DAX expression was written for the same,

     
     Total no of customers = DISTINCTCOUNT('Export'[Customer ID])
    
A card visual was used to represent total no of customers.


![Total no  Cus](https://github.com/user-attachments/assets/8b96474f-a5fb-4ef6-947c-b2f1eda595f7)


(14)  New measure was created to find % of Bank.

Following DAX expression was written to find % of Bank,

     % of Bank = DIVIDE([Total no of Bank meth], [Total no of customers], 0)
A card visual was used to represent this perecntage.

(15)  New measure was created to find % of Cash.

Following DAX expression was written to find % of Cash,

    % of Cash = DIVIDE([Total no of Cash meth], [Total no of customers], 0)

(16)  New measure was created to find % of churn females.

Following DAX expression was written to find % of churn females,

    % of churn Females = DIVIDE([Total no of churn Females], [Total churned cus],0)  

(17)  New measure was created to find % of churn males.

Following DAX expression was written to find % of churn males,

    % of churn Males = DIVIDE([Total no of churn Males], [Total churned cus],0)

(18)  New measure was created to find % of credit.

Following DAX expression was written to find % of credit,

    % of Credit = DIVIDE([Total no of Credit meth], [Total no of customers], 0)

(19)  New measure was created to find % of female customers.

Following DAX expression was written to find % of female customers,

    % of female cus = DIVIDE([Total no of Females], [Total no of customers], 0)
    
(20)  New measure was created to find % of male customers.

Following DAX expression was written to find % of male customers,

    % of male cus = DIVIDE([Total no of Males], [Total no of customers], 0)

(21)  New measure was created to find Total no of churned customers.

Following DAX expression was written to find total no of churned customers,

    Total churned cus = CALCULATE([Total no of customers], 'Export'[Churn] = "Yes")

Snap

![Total no  churn](https://github.com/user-attachments/assets/61d5fb9a-674a-4954-9f8d-48ff76b7011b)

(22)  New measure was created to find total no of Bank method. 

Following DAX expression was written to find total no of Bank method,

    Total no of Bank meth = CALCULATE([Total no of customers], 'Export'[Payment] = "Bank Transfer")

(23)  New measure was created to find total no of cash method.

Following DAX expression was written to find total no of cash method,

    Total no of Cash meth = CALCULATE([Total no of customers], 'Export'[Payment] = "Cash")

(24)  New measure was created to find total no of churn female.

Following DAX expression was written to find total no of churn female,

    Total no of churn Females = CALCULATE([Total churned cus], 'Export'[GENDER] = "F")
    
(25)  New measure was created to find total no of churn male.

Following DAX expression was written to find total no of churn male,

    Total no of churn Males = CALCULATE([Total churned cus], 'Export'[GENDER] = "M")

(26)  New measure was created to find total no of credit method.

Following DAX expression was written to find total no of credit method,

    Total no of Credit meth = CALCULATE([Total no of customers], 'Export'[Payment] = "Credit Card")

(27)  New measure was created to find total no of females.

Following DAX expression was written to find total no of females,

    Total no of Females = CALCULATE([Total no of customers], 'Export'[GENDER] = "F")

(28)  New measure was created to find total no of males.

Following DAX expression was written to find total no of males,

    Total no of Males = CALCULATE([Total no of customers], 'Export'[GENDER] = "M")

## Snap of each page

Home page


![Home page](https://github.com/user-attachments/assets/57d54d3f-3aed-4a51-be55-44f66581d428)

Customers page

![All customers](https://github.com/user-attachments/assets/1738ef79-5e79-4bb3-bed9-a6cd1b473cfc)

Churned page


![Churned cus](https://github.com/user-attachments/assets/1b2b0305-a392-41de-9be8-128c655f5a3b)

### Results

*Insights*

Three pages report was created on Power BI Desktop.

Following inferences can be drawn from the dashboard;

* Total number of customers = 299

* Number of male customers = 216 (72%)

* Number of female customers = 83 (28%)

* Total number of churned customer = 248 (82.9%)

* Total number of customers using credit card = 139 (46%)

* Total number of customers using cash = 75 (25%)

* Total number of customers using bank transfer = 85 (28%)

* Total number of churned male = 181 (73%)

* Total number of churned female = 67 (27%)

  (a) 83% of the customers under review have churned, while the remaining 17% have not churned.
  
  (b) 73% of the churned customers are under the male category.
  
  (c) Majority of the customers used the credit card method.
  
  (d)  Majority of the customers are introduced to the company by the agent.
  
  (e)  8% of the customers open their account at the Marina branch.

These ratings will change if different visual filters will be applied.


### Recommendation
* Improving customer experience
  
* Educating customers
  
* Rewarding loyalty
  
* Regular feature updates
  
* Listening to more than just top-level customers


### limitations
* Data quality issues
  
* Choosing the right analysis Techniques
  
* Limited Experience
  
* Time constraints
  
* Interpreting results
  
* Communication of findings



## Credits
- **[Olamide Jolaoso](https://linkedin.com/in/olamidejolaoso)** - Supervisor
 
- **[Oluchi Igwe](https://linkedin.com/in/igwe-oluchi-abda™-031334146)** - Line Manager
  
- **[Ehi Asher](https://linkedin.com/in/ehi-kenneth-asher-7807a325)** - Line manager

 Provided valuable feedback, mentorship, and project oversight during my internship,

# RossmannStore - Forescasting Sales

![](img/rossmann_store.png)

---

# 1.0 CONTEXT

Rossmann operates over 3,000 drug stores in 7 European countries. Currently, Rossmann store managers are tasked with predicting their daily sales for up to six weeks in advance. Store sales are influenced by many factors, including promotions, competition, school and state holidays, seasonality, and locality. With thousands of individual managers predicting sales based on their unique circumstances, the accuracy of results can be quite varied. we've found at a kaggle competition, where you can download the dataset here: https://www.kaggle.com/c/rossmann-store-sales/data.


# 2.0. BUSINESS PROBLEM

- What is the context?

    - At a meeting with the leads of each department, the Rossmann's CEO made a proposal to renovate all of their store.

- What is the couse?

    - The Rossmann's CEO want to predict how much each store will sell on next 6 weeks. He need to know if the budget will be enough to make a renovate each store.

- Who will lead the project?

    - We need someone who really know what is the business problem, because he will lead the solution. Therefore, he's our stakeholder.

- How will be our solution?
    - What is the format?
      - granularity(hour,day,product) ---> 6 weeks
      - Problem type(Classification, regression, clustering etc) ---> Regression
      - How we will deliver? (dashboard, csv, telegram bot) ---> Telegram bot
      
 # 3.0. TELEGRAM BOT
 
 
 # 4.0. DATA DESCRIPTION
 
 ## 4.1. Data Types
 
 This step is important for us to understand what is the type of our features. Therefore, we need to treat each variable according to its specific type ... for example, we cannot treat a date as a number or as a text, we cannot treat a number as a text. It is necessary for us to understand the context of our business for the changes to be made.

As we can see below, our columns "date" is like a "object"...we will change it to "datetime" type.
 
![](img/data_type1.png)
![](img/data_types2.png)

## 4.2. Fillout NA

This step is extremely important because our machine learning algorithms are not able of handling null values. To solve this problem there is no right answer, it will depend on your business context, we have to be aware of it and test what will be best suited to that situation. There are three ways to fix this.

Exclude lines with null values.
Replace with the average or median, for example.
Change according to the business context.
This choice is very important because, if we choose to exclude the rows from our data set, depending on the amount of null values, we will eliminate a considerable amount of data so that our model could train.

![](img/na1.png)

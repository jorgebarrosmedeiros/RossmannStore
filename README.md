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

As I said above, there is no 100% correct or 100% wrong answer about how you should treat the missing values in your dataset. Every choice has a waiver. You have to be aware of this and test what will best suit that situation.

Therefore, this section will focus on filling in these null values. For that to happen, I chose to use the business context to solve our problem. Below, we will explain each change.

- competition_distance
    - This variable tells us how far the nearest competitor is from our store. I chose to replace it with 200000, as this will be big enough to tell us that there is no competitor close to our store.

- competition_open_since_month
    - This column tells us how long in months the competing store opened. We will replace it with the month that was filled in the date column.

- competition_open_since_year
    - This column tells us how long in years the competing store has opened. We will replace it with the year that was filled in the date column.

- promo2_since_week
    -   describes the calendar week when the store started participating in Promo2. We will extract the week from the date column and replace the values that are null.

- promo2_since_year
    - describes the year when the store started participating in Promo2. We will extract the year from the date column and replace the values that are null.

- promo_interval
    - describes the consecutive intervals Promo2 is started, naming the months the promotion is started anew. E.g. "Feb,May,Aug,Nov" means each round starts in February, May, August, November of any given year for that store. We replaced the null values with 0 and checked if the store participated in promo2 or not represented by 0 and 1.
    
After fillout na:

![](img/na2.png)

## 4.3. Statistical Descriptive

![](img/stat_desc.png)

Let's look at our "sales" column

- Min = 0, means that on that day the store was closed.
- Max = 41551
- Mean = It tells us that on average, 5773 sales are made per day.
- Median = Median very close to the average
- Std = Tell us that our sales may vary by +/- 3849, that is, there are days that total sales are (5773 + 3849) and there are days that total sales are (5773 - 3849)
- Skew = Informs us how shifted our graph is in relation to the origin.
- Kurtosis = Tells us how "pointy" our distribution is, or how close to a normal distribution it is.

# 5.0. MindMapHypothesis

![](img/mindmap.png)

From the mind map above, we created some features to validate the hypotheses.

# 6.0. Exploratory Data Analysis

## 6.1. Univariate Analysis

![](img/eda1.png)

As we can see, it is close to a normal distribution, however, it has a positive skewness, so it is shifted to the left. 

## 6.2. Numerical Variables

![](img/eda2.png)

- competition_distance -> we can see that we have bigger concentrations in smaller intervals. So, there's a lot close competitors.

- competition_open_since_month -> has an increase until the fourth month and reaches the maximum. From that there is a fall. Therefore, this feature has a certain variation.

- day_of_week -> There is no variation, so, the day of the week will not influence sales. There is no variation.

- is_promo -> we have a lot more sales when there are no promotions. This can be an insight, we will check soon.

- promo2_since_year -> there is a very high peak in 2013, we need to check what happened that year.

## 6.2. Categorical Variables

![](img/eda3.png)

- state_holiday -> We have a much larger amount of sales on public holidays, but at Christmas, which has a smaller amount of sales than easter_holiday, it has a higher peak.

- store_type -> The store_type "a" that sells more, does not have such a peak compared to the others.

- assortment -> We see that stores with the "extra" type assortment sell less, but have a higher distribution. So, there are stores that sell more with the "extra" assortment and stores that sell less.

## 6.3. Hypothesis

### H8. Stores should sell more over the years.

![](img/eda4.png)

False Stores sell less over the years.

### H9. Stores should sell more in the second half of the year.

![](img/eda5.png)

False Stores sell less in the second half of the year.

### H6. Stores with more consecutive promotions should sell more.

![](img/eda6.png)

False Stores with more consecutive promotions sell less.

### H11. Stores should sell less on weekends.

![](img/eda7.png)

True Stores sell less on weekends.

### Summary Hypothesis

We also outlined other hypotheses, but the previous presented ones were the most insightful.

![](img/eda8.png)

## 6.4. Multivariate Analysis

![](img/eda9.png)

We will look at the columns that have the lightest and darkest data, note the following columns:

The variables that have some dependence on the response variable are: 'day_of_week', 'open' and 'promo'. We also have the variable 'Customers', but it would be necessary to build a project to predict this variable and after that, we could use it, so we can remove it.

![](img/eda10.png)

According to the heat map, we found that there is a high correlation between the variables assortment and store type. The result of 0.54 is an average correlation. This means that the bigger the store, the bigger the product range. The other variables have weak correlations with each other.

## 7.0. Machine Learning Modelling

### 7.1. Single Performance

![](img/ml1.png)

We obtained the following results, however, in order for our model to be reliable, we applied the cross-validation technique.

### 7.2. Real Performance - Cross-Validation

![](img/ml2.png)

As we see above, our best performing algorithm was the XGBoost Classifier
For computational reasons, we did not perform cross-validation at RandomForest.

### 7.3. Hyperparameter Fine Tunning - XGBoostClassifier

In our best algorithm, we apply the technique to find the best parameters. Below, we can see its performance with the chosen parameters.

![](img/ml3.png)

## 8.0. Business Performance

![](img/ml5.png)

As observed in the results, we need to report to the business team, that there are stores that are more difficult to make the predictions.

![](img/ml6.png)

There are stores that are more difficult to make the predictions. Thus, some strategies that may solve this challenge in the next project iteration could be:

- Taking a closer look on the variables (add or remove).
- Try other methods and other techniques in order to improve the predictions.

## 9.0. Machine Learning Performance

![](img/ml7.png)

- By observing the first and second line plots, we can see that the predictions or our model is pretty close to the real value for sales. On the other hand, the error rate has some variance.

- Observing the histogram, the error distribution almost follow a normal distribution.

- Observing the scatterplot, there are some stores with higher error. However, the other points seems like a horizontal tube, which means that there are a few variation rate in the error.

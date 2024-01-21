Exploratory Data Analysis for Used Car sales features and its impact on price


# What is bank marketing problem?

Bank has run several marketing about their latest loan program and collected outcome of each compaign. Bank also has associated campaign outcome with client information they have collected during the execution those campaigns. The ask is to perform various classification model , collect the base performance , perform feature engineering to reduce dimenansionality and then perform hyperparameter tuning. 

Data Description:

The dataset the collected over 17 campigns with ~42K outcomes.

# bank client data:
1 - age (numeric)
2 - job : type of job (categorical: 'admin.','blue-collar','entrepreneur','housemaid','management','retired','self-employed','services','student','technician','unemployed','unknown')
3 - marital : marital status (categorical: 'divorced','married','single','unknown'; note: 'divorced' means divorced or widowed)
4 - education (categorical: 'basic.4y','basic.6y','basic.9y','high.school','illiterate','professional.course','university.degree','unknown')
5 - default: has credit in default? (categorical: 'no','yes','unknown')
6 - housing: has housing loan? (categorical: 'no','yes','unknown')
7 - loan: has personal loan? (categorical: 'no','yes','unknown')
# related with the last contact of the current campaign:
8 - contact: contact communication type (categorical: 'cellular','telephone')
9 - month: last contact month of year (categorical: 'jan', 'feb', 'mar', ..., 'nov', 'dec')
10 - day_of_week: last contact day of the week (categorical: 'mon','tue','wed','thu','fri')
11 - duration: last contact duration, in seconds (numeric). Important note: this attribute highly affects the output target (e.g., if duration=0 then y='no'). Yet, the duration is not known before a call is performed. Also, after the end of the call y is obviously known. Thus, this input should only be included for benchmark purposes and should be discarded if the intention is to have a realistic predictive model.
# other attributes:
12 - campaign: number of contacts performed during this campaign and for this client (numeric, includes last contact)
13 - pdays: number of days that passed by after the client was last contacted from a previous campaign (numeric; 999 means client was not previously contacted)
14 - previous: number of contacts performed before this campaign and for this client (numeric)
15 - poutcome: outcome of the previous marketing campaign (categorical: 'failure','nonexistent','success')
# social and economic context attributes
16 - emp.var.rate: employment variation rate - quarterly indicator (numeric)
17 - cons.price.idx: consumer price index - monthly indicator (numeric)
18 - cons.conf.idx: consumer confidence index - monthly indicator (numeric)
19 - euribor3m: euribor 3 month rate - daily indicator (numeric)
20 - nr.employed: number of employees - quarterly indicator (numeric)

Output variable (desired target):
21 - y - has the client subscribed a term deposit? (binary: 'yes','no')



# Data breakdown

Dataset doesn't contain any null value columns. I have performed encoder to convert categorial columns to numberical values before begining model comparison. 

# 
Results of duplicates

No duplicate found in this dataset.

# Base line model performance and comparison

DummyClassifier accuracy is 0.8873458288821987 which will serve as baseline performance that Logistic, Decision Tree, SVM and KNN classification should be beat. 

Now, we aim to compare the performance of the Logistic Regression model to our KNN algorithm, Decision Tree, and SVM models.  Using the default settings for each of the models, fit and score each.  Also, be sure to compare the fit time of each of the models.  Present your findings in a `DataFrame` similar to that below:


|	Model |	Train Accuracy	| Test Accracy	| Train Time |
| ------- | --------------- | --------------| -----------|
|   LR 	| 88.71	| 88.73	| 0.379202 |
|	KNN	| 88.54	| 88.69	| 0.015654 |
|	SVM	| 88.71	| 88.73	| 2.305266 |
|	DT	| 88.36	| 88.29	| 0.028404 |

## Feature engineering

  |---------| ------------ |
   | duration   |       0.064381   |       
      |       nr.employed   |              0.062872   |       
   | emp.var.rate    |            0.044628   |       
   | euribor3m    |               0.041646   |       
   | poutcome   |                 0.032109   |       
   | pdays       |                0.027936   |       
   | cons.conf.idx    |           0.026440   |       
   | cons.price.idx    |          0.019259   |       
   | previous     |               0.018524   |       
   | contact    |                 0.011845   |       
   | month     |                  0.009613   |       
   | job     |                    0.006593   |       
   | default    |                 0.005946   |       
   | age      |                   0.005715   |       
   | education    |               0.002711   |       
   | marital         |            0.002625   |       
   | day_of_week     |            0.000000   |       
   | loan      |                  0.000000   |       
   | housing     |                0.000000   |       
   | campaign     |               0.000000   |       
Name: MI Scores, dtype: float64

Looking at above MI scores, duration, nr.employed,emp.var.rate,euribo3m,poutcome,pdays,consumer confidance, previous campaign outcome, contact has more influence on outcome of the campign.  Age, education,days_of_week etc has least positive influence on campaign outcome. 

#  Model performance after hyperparameter tuning

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Model</th>
      <th>Train Accuracy</th>
      <th>Test Accracy</th>
      <th>Train Time</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>LR</td>
      <td>90.81</td>
      <td>91.02</td>
      <td>2.058776</td>
    </tr>
    <tr>
      <th>1</th>
      <td>KNN</td>
      <td>90.63</td>
      <td>88.68</td>
      <td>0.018194</td>
    </tr>
    <tr>
      <th>2</th>
      <td>SVM_WO_POLY</td>
      <td>88.78</td>
      <td>88.76</td>
      <td>33.226872</td>
    </tr>
    <tr>
      <th>3</th>
      <td>SVM_WTH_POLY</td>
      <td>90.74</td>
      <td>91.00</td>
      <td>580.443674</td>
    </tr>
     <tr>
      <th>4</th>
      <td>DT</td>
      <td>88.74</td>
      <td>88.45</td>
      <td>0.434</td>
    </tr>
  </tbody>
</table>
</div>

# Summary

-  SVM is giving best accuracy of 91% with polynomial kernel.  The biggest challenge is the execution time it takes to find best model.
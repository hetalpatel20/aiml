Exploratory Data Analysis for Used Car sales features and its impact on price


# What is Used Car Pricing Problem?

Customer looking for used car will always try to get maximize features within affordability. Based on consumer's personal equestion, he/she has list of must have features and optional features in used cars at the sametime considering affordability equation as well. I find buying a used car is hardest decision to make compare to buying a new car.  

For this problem, Used car dealer want to understand what all features drives the price of a used car.  Dealer also wants to understand features that are most valuble to buyer of a used car. The dataset given to us has no consumer demographic information. Hence, we can analyze the features and price correlationship and see how we can connect that analysis to consumer.  First we need to explore the data and see what all information is available to us.

 Data Description

There is only 1 CSV file provided containing vehicle data. 
Looking at this dataset, dataset contains more categorical attributes compare to continuoys or numerical attributes. These attributes can be grouped based on
1) Geographic 
   - Region
   - State
2) Ownership
      - Title Status
3) Manufacture and Model
      - Manufaturer
      - Model
4) Core features of the car
      - Price
      - year
      - titel status
      - vin (grouping purpose)
      - condition
      - cylinders
      - fuel
      - odometer
      - transmission
      - drive
      - size
      - type
      - paint_color

In real-life above all factors can affect the overall price of used car. I think Geographic, ownership/vin and Manufacture/Model information will all too much categorical and can increase the complexity of model by adding unnessary dimensionality.
For this study, i want to focus on core features of the car which directly incluences the price of the car. Next step is to prepare the dataset around using "core feartures of the used car".  lets see how the fidelity of data maintains. If it drops the records drastically, we need to comeup with different approch.

# Data breakdown

   - total no fo records -426880    with unique vehicles of = 118246

   - we can not apply dropna at this stage because it will reduce the size of recordset drastically.

Next step :  Lets merge rows or drop duplicate rows based on VIN. We will use core attributes of used car to indentify duplicate rows.

# Results of duplicates

Identifying duplicates will be two step process. 
- Step 1 - First we apply "all core attributes of used cars" as duplicate rule. That way will have dataframe having all attributes carrying values.
- Step 2 - Secondly, apply duplicates rule based on VIN on the Step1 output.

So, this dataset carries 118427 clean vehicle records.

Next step... check for NAN...

# Total clean vehicles record 22560 out of 118246.  It feels like we are loosing good amount of information when we applied dropna.

### No Cars by cylinders
-  4,6 and 8 cylinders cars are most popular used car

### Aging of used cars conisdering car is still operative today vs price

-   Oldest Used Car  118.0
-   Newest Used Car  1.0
-   Highest Used Car  167500
-   Lowest Used Car  0

### Why the price of used car is zero?  Does it has title issue?

Most of the used car having zero price has clean title. Looks like data issue . Lets remove records with price equal to zero.

    title_status    Count
-   clean           1234
-   rebuilt         2
-   salvage         1
###  Correlation matrix based on attributes grouping

 1)  Correlation Matrix - Core Used car attributes ( Age, Mileage, cyclinders)
 2)  Correlation Matrix -  Type of Cars
 3)  Correlation Matrix - Cosemetic Attributes

 ### PCA Analyis 
      
      As we can see PC1 has 98% coef. Highlighted attributes has positive coef contrinbuting to PC1. in modeling, we will use highlighted attributes for modeling.
 
                  PC1       PC2
# price        0.262236 -0.079975
# year         0.020170 -0.468296
# cylinders    0.365946  0.147005
# odometer     0.029375  0.125105
age         -0.020170  0.468296
excellent   -0.030442 -0.127727
fair        -0.021766  0.130715
# good         0.042846  0.145774
like new    -0.002573 -0.063509
# new          0.001949 -0.024808
salvage     -0.012361  0.019204
# diesel       0.244599  0.022936
electric    -0.010560 -0.012997
gas         -0.195766 -0.001921
hybrid      -0.049948 -0.042433
# other        0.012329  0.016067
# automatic    0.107417 -0.324352
manual      -0.107417  0.324352
# 4wd          0.276448 -0.135274
fwd         -0.362485 -0.095401
# rwd          0.093511  0.284277
compact     -0.202234  0.049590
# full-size    0.353663  0.014957
mid-size    -0.209763 -0.062420
sub-compact -0.079902  0.034478
# SUV          0.045098 -0.145161
# bus          0.023055  0.030797
convertible -0.045767  0.181005
coupe       -0.066811  0.186919
hatchback   -0.127249  0.000756
mini-van    -0.036163 -0.017455
# offroad      0.008043  0.037215
# pickup       0.164670  0.031013
sedan       -0.263369 -0.068047
# truck        0.279332  0.034647
# van          0.041766  0.016371
wagon       -0.043140  0.004649
# black        0.004317 -0.052909
blue        -0.044243  0.012393
brown       -0.006148  0.010353
# custom       0.025962  0.035292
green       -0.009465  0.082260
grey        -0.048050 -0.061812
orange      -0.013272  0.056837
purple      -0.011262  0.024794
red         -0.028743  0.060670
silver      -0.065845 -0.029986
# white        0.141165 -0.008473
yellow      -0.006965  0.083910

### KMean
Total we have 118K cars records, which effectively forms 8 clusters.
# Exploratory Data Analysis for Golf Swing data collected by simulators & perfomed by golfer


# Wish i can find out golf ball trajectory based on swing measurements?

Any golfer with any skill level starting from beginner to pro, they are always curious about how to controll swring parameters to shape ball trajectory. Golfer always struggles swing after swing to control the factors affecting shape of ball trajectory. As a outdoor sports, golfer wants to create different shape of trajectory to cope up with wind, rain, hold position, avoiding hazzards. For this probelm golfer want to understand what all swing measurements drive ball trajectory. This dataset has no golfer demographic and skill level information. 
First we need to explore the data and see what all information is available to us.

Overall, we want to find out two parameters
1)  Golf strike distance
    This is regression problem which can help us predict distance based on swing parameters
2)  Ball trajectory
    This is classification problem which can help us classify the swing trajectory based on parameters.

#  Common Utility Functions

This section contains common utility functions to plot graphs and generate base classification models.

# Data Description

Using golf simulator i have collected 850 swings which includes 24 swing measurements.  This dataset contains both categorical and non-categorical attributes. Here are the list of swing measurements.
								
1) Carry Distance - The carry of a golf shot is how far the ball travels before it hits the ground for the first time.
2) Total Distance - Total distance = carry distance + distance ball rolls after hiting the ground
3) Side Distance - Side is the distance from the target line based on where the ball lands.
4) Smash Factor - Smash Factor relates to the amount of energy transferred from the club head to the golf ball. The higher the smash factor the better the energy transfer.
5) Club Speed - Speed of club in mph
6) Side Spin -  Ball side spin - left or right spin measured in degree at which ball spins
7) Back Spin -  back spin rate of ball
8) Ball Speed - Ball speed is a measure of how fast your ball leaves the club head after impact.
9) Lie angle - Lie angle is the angle created between the center of the shaft and ground when you put your iron down in the address position.
10) Attack Angle - The up or down movement of the club head at the time of maximum compression. Attack angle is measured relative to the horizon.
11) Launch Angle - Launch Angle is the angle the ball takes off at relative to the horizon. Launch angle is highly correlated to dynamic loft.
12) Side Angle - Side Angle Determines if You Will Hit a Power Fade or a Slice.
13) Decent Angle - A ball rolling along the ground has a landing angle of zero, whereas a golf ball dropping from the heavens has a descent angle of 90 degrees
14) Apex - maximum height ball attains
15) Flight Time - time in the air
16) Swing Type - fade, draw, straight etc
17) Sping Axis - Spin axis represents the amount of curvature of a golf shot. A negative spin axis represents a ball curving to the left, a positive spin axis represents a right
18) Face Angle - Face Angle is the direction the club face is pointed (right or left) at impact 
19) Club Path
20) Club Lie - club angle when resting on the ground
21) Impact POS - NA
22) Dynamic Loft - NA
23) Face to path - face open or close relative to pathof the swing.

In real-life above all factors can affect the overall price of used car. I think Geographic, ownership/vin and Manufacture/Model information will all too much categorical and can increase the complexity of model by adding unnessary dimensionality.
For this study, i want to focus on core features of the car which directly incluences the price of the car. Next step is to prepare the dataset around using "core feartures of the used car".  lets see how the fidelity of data maintains. If it drops the records drastically, we need to comeup with different approch.

# Data Cleanup

1.  Drop unnessary columns
2.  Parse the column values to separate direction and distance
3.  Remove record having less than 70 yrds total distance that can be resulted becaus of miss hit
4.  Convert columns datatype
5.   Convert categorical columns using simple strategy which is assign 1 for L(Left) and 2 for R(Right).


# Data breakdown

  -  End of all data cleanups , we have total 820 swings data

# Results of duplicates

Since, this entire dataset captured by actual swing perfomed by actual golfer. There is chance of having duplicates in this dataset.

# Data Exploration

### No of swing by ball trajectory
    -  This golfer has majority of swing types in straight, draw, fade and hook and slice. occessionally, golfer has pull hook and push hook swing type. 
![no_of_Swing_type.png](attachment:no_of_Swing_type.png)

### Carry distance vs smash factor
-  This graph shows as smash factor increases which results in overall carry distance. So, for golfer having right smash factor is very important. Smash factor of 1.3 and above is very important to achieve good carry distance.


![Carry vs smash.png](<attachment:Carry vs smash.png>)

###  Carry Distance vs Ball speed

As you can see Carry distance and ball speed are positively correlated. 

![image.png](attachment:image.png)

###  Carry distance vs launch angle

As launch angle decreases carry distance increases. 

![image.png](attachment:image.png)

# Overall Correlation Matrix using complete dataset
- Step 1.  Encode target column "Type"

    -    Straight      0
    -    Fade          1
     -    Draw          2
     -    Slice         3
     -    Hook          4
     -    Pull Hook     5
     -    Push Slice    6
     -    Pull Slice    7
     -    Push Fade     8
     -    Pull Draw     9
     -    Push Hook     10
     -    Push          11
     -    Pull Fade     12
     -    Pull          13

-  Step 2:  Lets categorized attributes to develop more insight into correlation matrix

| Index | Column            |  Non-Null Count  |Dtype       |   Factors incluencing targets                                           |
|-------|  ------           |   -------------- | -----      |    -------------------------------                    |
| 0     |Carry              |  725 non-null    |float64     |    Target Attribute                                      |
| 1   |Total               |725 non-null    |float64| NA | 
|2  | Side Dist           |725 non-null   | float64| Target Attribute to find out distance away from target line|
| 3  | Smash Factor       | 725 non-null  |  float64| Carry |
| 4  | Club Speed         | 725 non-null  |  float64| Carry |
| 5  | Ball Speed         | 725 non-null  |  float64| Carry |
| 6  | Back Spin           |725 non-null   | float64| Carry |
| 7  | Side Spin Angle     |725 non-null   | int64  | Type|
| 8  | Side Spin           |725 non-null   | float64| Type |
| 9  | Launch Angle        |725 non-null   | float64| Carry|
| 10 | Side Angle          |725 non-null   | object | Type|
| 11 | Decent Angle        |725 non-null   | float64| Type|
| 12  |Type                |725 non-null   | int64  | Target to predict shape of the ball flight |
| 13 | Spin Axis           |725 non-null   | float64| Carry |
| 14 | Face Angle         | 725 non-null   | int64  | Type|
| 15 | Face Path Angle    |725 non-null   | float64| Type|
| 16  |Club Path           |725 non-null   | float64| Type|
| 17  |Club Path Angle    | 725 non-null   | int64  | Type|
| 18 | Face to Path Angle  |725 non-null   | int64  | Type|
| 19  |Face to Path       | 725 non-null   | float64| Type|
| 20  |Side Dist Angle    | 725 non-null   | int64  | Type|
| 21 | Side Angle Dir     | 725 non-null   | int64  | Type|

As we can see from the correlation matrix that smash factor, club speed and ball speed has positive impact of overall carry distance. Golfer trying to maximize distance should focus on these three factors. Factors such as back spin, side spin and spin axis has negative effect of carry distance. Interestingly launch angle has negative impact on carry distance whereas decent angle has positive impact on carry distance. 

# Reduce dimensionality of this dataset using PCA method

Total no of attributes in this dataset is too high, which makes correlation matrix hard to interpret. We will breakdown features into two sets, first one is related to carry distance and second is related to swing type(trajectory). We will use these attributes to perform dimensionality reduction. 

## Problem 1: Golf strike distance PCA analysis

|            |       PC1 |      PC2 |
|------------|-----------|----------|
Carry        |-0.436347 |-0.315888|
Smash Factor |-0.360746 |-0.016522|
Club Speed   |-0.383214| -0.301832|
Ball Speed   |-0.460498 |-0.240967|
Back Spin    | 0.323242 |-0.432859|
Side Spin    |-0.003745 | 0.244154|
Spin Axis    | 0.038862 |-0.086620|
Launch Angle  |0.419366 |-0.226664|
Decent Angle  |0.196658 |-0.667021|

![image.png](attachment:image.png)

# Kmean clustering of Carry dataset using Elbow method

![image-2.png](attachment:image-2.png)

Optimal cluster value is 6. Which means 875 golf swings can be clustered in 8 clusters.



## Ploblem 2 : PCA of shape of trajectary data attributes

![image-2.png](attachment:image-2.png)

|                  |       PC1     |  PC2|
|------------------|---------------|-----|
Back Spin       |    0.011439| -0.284711|
Side Spin Angle  |   0.413378| -0.087277|
Side Spin       |    0.199156 | 0.286111|
Side Angle      |    0.040970 | 0.512493|
Type            |    0.171317|-0.072542|
Face Angle       |   0.346412| -0.090865|
Spin Axis         |  0.392884 |-0.032781|
Face Path Angle  |   0.050470 | 0.528567|
Club Path       |    0.073904 | 0.143316|
Club Path Angle  |  -0.119292 |-0.172804|
Face to Path Angle | 0.376864 | 0.051810|
Face to Path    |    0.058795|  0.442987|
Side Dist Angle |    0.466244| -0.113300|
Side Angle Dir |     0.314374| -0.103335|

![image.png](attachment:image.png)

### Kmean clustering of Swing Type dataset using Elbow method

![image.png](attachment:image.png)

Optimal cluster value is 8. Which means 875 golf swings can be clustered in 8 clusters.

## Baseline Model Performance

Baseline model performance is 32.13%

This dataset contains both regression and classification problem. Predicting carry distance based on smash factors, club and ball speed is regression problem. Predicting shape of ball trajectory is classification problem

To futher the model design, i have selected classification problem of predicting shape of ball trajectory. 

For that i have selected four model and each model followed steps of:
1)  baseline model performance
2)  Model performane after hyperparameter tuning
3)  confusion matrix of tuned model.
4)  Model comparison

# Model Comparison

| Model | Base model Performance | Performance of Tuned Model |
|-------|------------------------|----------------------------|
| LGR   |  82.75%                | 71% |
| KNN   |  64.97%               |  67.94% |
| SVM   |  96%                  |  95.14% |
| DS    |  98%                   | 97.58% |


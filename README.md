### Will a Customer Accept the Coupon?

**Context**

Imagine driving through town and a coupon is delivered to your cell phone for a restaraunt near where you are driving. Would you accept that coupon and take a short detour to the restaraunt? Would you accept the coupon but use it on a sunbsequent trip? Would you ignore the coupon entirely? What if the coupon was for a bar instead of a restaraunt? What about a coffee house? Would you accept a bar coupon with a minor passenger in the car? What about if it was just you and your partner in the car? Would weather impact the rate of acceptance? What about the time of day?

Obviously, proximity to the business is a factor on whether the coupon is delivered to the driver or not, but what are the factors that determine whether a driver accepts the coupon once it is delivered to them? How would you determine whether a driver is likely to accept a coupon?

**Overview**

The goal of this project is to use what you know about visualizations and probability distributions to distinguish between customers who accepted a driving coupon versus those that did not.

**Data**

This data comes to us from the UCI Machine Learning repository and was collected via a survey on Amazon Mechanical Turk. The survey describes different driving scenarios including the destination, current time, weather, passenger, etc., and then ask the person whether he will accept the coupon if he is the driver. Answers that the user will drive there ‘right away’ or ‘later before the coupon expires’ are labeled as ‘Y = 1’ and answers ‘no, I do not want the coupon’ are labeled as ‘Y = 0’.  There are five different types of coupons -- less expensive restaurants (under \\$20), coffee houses, carry out & take away, bar, and more expensive restaurants (\\$20 - \\$50). 


INVESTIGATE THE DATASET AND MISSING DATA

I have devided data into three categories.
1. Consumer demographics
2. consumer current preferences and behaviours
3. Coupon acceptance rate

Step 0:  Investigate data
To easy way investigate data, i have used excel file filter funtion that can gives us different dat anomalies and different values. I have used value_count function of python as well to understand different data attirbutes.

Step 1.  Missing and problamatic data
Based on observation,  I don't see any data massaging needed for consumer demographic data. Data attributes associated with consumer current preferences has two type of issues datatype conversion and handling range values. To, solve range values i have used average of the range to simplify our query operations and graphing. 

Step 2. Used coding to for range value
-    NAN - represented as -1
-   <1 =  1
-   Never = 0
-   1~3 = 1.5
-   4-8 = 6
-   >8 =  8

DECIDE WHAT TO DO ABOUT YOUR MISSING DATA, DROP, REPLACE ETC

i have decided to perform conver range data values into averages and convert datatypes of specfic columns to represent data more effectively.

INVESTIGATION USE CASES

4. What proportion of the total observations chose to accept the coupon? 
Findings:  
            56.84% of observations accepted coupons of some kind at the sametime 43.5% of observations not accepted coupons

5. Use a bar plot to visualize the `coupon` column.
Findings: 
        5474 consumers not used the coupon. 7210 consumers used coupon.

6. Use a histogram to visualize the temperature column.
Findings:
            Most of the observation recorded when temprature was 80 degree. Findings:
            Data indicates that most of the coupons accepted when temprature was 80 degree. at the sametime most of the coupons were not accepted when temprature was 80 degree.  So, i don't see effect of temprature on concumers decision of accepting coupons.


INVESTIGATING BAR COUPONS

Now, we will lead you through an exploration of just the bar related coupons.  

1.  What proportion of bar coupons were accepted?

    Finding:   
    - Bar Coupon Usage  Count
    - 0         Not Used   1190
    - 1             Used    827

    Closed to 60% of bar coupons were not accepted whereas 40% of bar coupons accepted.


2. Compare the acceptance rate between those who went to a bar 3 or fewer times a month to those who went more.
    Findings:
            Consumers going to bar fewer than 3 and bar visits more than 3 has coupon acceptance rate of 81% and 19.6% respectively. 

        Bar	Y	Count	Total	Acceptance Rate
    1	-1	1	8	827	0.967352
    3	0	1	156	827	18.863362
    5	0.5	1	253	827	30.592503
    7	1.5	1	257	827	31.076179
    9	6	1	117	827	14.147521
    11	8	1	36	827	4.353083

4. Compare the acceptance rate between drivers who go to a bar more than once a month and are over the age of 25 to the all others.  Is there a difference?

    Findings:  

    Drivers with age over 25 and 1-3 times bar visits has hest base coupon acceptance rate of 32.69%. Approximately same acceptance rate noticed for drivers with age over 25 and 0-1 visits.

        Bar	Y	Count	Total	Acceptance Rate
    1	-1	1	8	580	1.379310
    3	0	1	97	580	16.724138
    5	0.5	1	183	580	31.551724
    7	1.5	1	187	580	32.241379
    9	6	1	84	580	14.482759
    11	8	1	21	580	3.620690

5. Use the same process to compare the acceptance rate between drivers who go to bars more than once a month and had passengers that were not a kid and had occupations other than farming, fishing, or forestry. . 

    Findings:

    the total acceptance rate between drivers who go to bars more than once a month and had passengers that were not a kid and had occupations other than farming, fishing, or forestry is closed to 80%

        Bar	Y	Count	Total	Acceptance Rate
    1	-1	1	8	823	0.972053
    3	0	1	156	823	18.955043
    5	0.5	1	249	823	30.255164
    7	1.5	1	257	823	31.227217
    9	6	1	117	823	14.216282
    11	8	1	36	823	4.374241

6. Compare the acceptance rates between those drivers who:

    Findings:  Consumers going to bars more than once a month, had passengers that were not a kid, and were not widowed vs. going bars more than once a month and are under the age of 30 showing similar acceptance rate patterns in which visiting bar 1-3 times a month has highest acceptance rate of 31%. Interestingly, cosumers who go to cheap resturants more than 4 time with salary less than 50 has lowest coupon acceptance rate compare to above two conditions.

    - go to bars more than once a month, had passengers that were not a kid, and were not widowed *OR*
        Bar	Y	Count	Total	Acceptance Rate
    1	-1	1	8	820	0.975610
    3	0	1	149	820	18.170732
    5	0.5	1	253	820	30.853659
    7	1.5	1	257	820	31.341463
    9	6	1	117	820	14.268293
    11	8	1	36	820	4.390244

    - go to bars more than once a month and are under the age of 30 *OR*
        Bar	Y	Count	Total	Acceptance Rate
    1	-1	1	3	440	0.681818
    3	0	1	81	440	18.409091
    5	0.5	1	107	440	24.318182
    7	1.5	1	139	440	31.590909
    9	6	1	80	440	18.181818
    11	8	1	30	440	6.818182

    - go to cheap restaurants more than 4 times a month and income is less than 50K. 
        RestaurantLessThan20	Y	Count	Total	Acceptance Rate
    1	6.0	1	924	173966	0.531138
    3	8.0	1	445	173966	0.255797


INEPENDENT INVESTIGATION

Investigation 1:

    How age and gender influences the coupon acceptance rate?

    My findings indicates that coupon acceptance decreases as age increases and than after it increases again for age greater than 50 years old.  Age less than 26 male has higher coupon acceptance than female with same age group. Overall, I see gender and age plays role in consumers willingness to use coupons.

    Run jupyter notebook to see visualization.

Investigation 2:

    What is the most accepted coupon type during specific time of the day?

    Data shows that time of the day is very important facotr determining which type of coupon will be more pouplar during that time period. For example, coffee coupons has increased accepance between 7AM and 10AM. Carryout and bar coupons has downward trends in the morning and upward trend during 2PM to 6PM, both showed same acceptance trend. Restaurants <20 coupon shows upward trend during 10AM and 2PM whereas Resturants 20-50 shows upward trend during 2PM-6PM.

    Run jupyter notebook to see visualization.

Investigation 3:

    What is the most rejected coupon type during specific time of the day?

    Findings:
    Carryout, Bar and Restuarant 20-50 has highest coupon rejection at 10PM.  Coffee coupons has highest rejection at 6PM. This analysis will tell us which coupon to spread during specific time of the day. 

    Run jupyter notebook to see visualization.

Investigation 4

    Most effective coupon type based on destination

    Findings:

    At work and home, Carry out and take away coupons has the most acceptance rate. Whereas Resturants <20 coupons are very popular at urgent places. Other iteresting observation is that all coupons types are very popular at urgent place when we compare volume with home and work destination. Coffee coupons are the second most poupar coupon used at urgent places.

    
    Coffee coupons has highest rejection in all three destination home, work and urgent places. Bar coupons has highrest rejection at urgent places. 

    Run jupyter notebook to see visualization.


5. Coupon acceptance and rejection of a married female by age

    Findings:    
            Based on below analysis, It appears married female with age of 30,40 and >50 has dominant coupon usage especially Restaurant20-50, coffee and restaurant<20 coupons. At the sametine, married female with age of 30 and >50 has rejected carryout coupon the most. Overall, Restaurnat 20-50 is the most effective coupon strategy for married female with age of 30, 40 and >50 and Carry out is the most rejected coupon.  

    lets find out effectiveness of "Restaurant20" coupons among married females who visited resturant 20 and restaurant20-50 visits.

    Findings:  

        Restaurant20 coupon which is consider as coupon targeted for value consumers.To analyze how much Resturant20 coupons are accepted by married female who visits either cheap or expensive restaurants. Based on below analyis "Restaurant20" coupons has highest acceptance rate in married feamle visiting cheap restaurant 1-3 and 4-8 times a month.  At the sametime "Restaurant20" coupon also has highest acceptance rate in married feamle who visits expensive restaurants 0 to 1 times a month.
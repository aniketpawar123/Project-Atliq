# Atliq



## Problem Statement

Atliq, a prominent player in the hospitality industry, operates luxury and business hotels across major Indian cities like Bangalore, Hyderabad, Mumbai, and Delhi. To enhance operational insights and decision-making, Atliq aims to leverage Microsoft Power BI. The project entails developing intuitive dashboards and reports to provide actionable insights into occupancy rates, revenue generation, guest satisfaction, and regional performance trends. The goal is to empower stakeholders with data-driven narratives that optimize resource allocation, refine marketing strategies, and improve overall efficiency and profitability across Atliq's diverse hotel portfolio in India.



### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : Errors and empty values were seen in the columns, which will be eliminated. 
- Step 5 : In the report view, under the view tab, theme was selected. 
- Step 6 : Visual filters (Slicers) were added for date month wise and also for week.
- Step 7 : Six card visuals were added to the canvas,to show key measures.![cards](https://github.com/aniketpawar123/Project-Atliq/assets/123149177/ffee10b4-847f-4a4a-8c37-7f00d0a9eb86)
           
           
- Step 9 : Realisation perecntage and ADR of booking platform is shown by line and stacked column chart. 
- Step 10 : Property key matric table is created to show performance of each hotel using key matric.
- Step 11 : Week wise trend shown by trend line using RevPar(Revenue per Available room),ADR(Average Daily Rate),Occupancy %.
![trend](https://github.com/aniketpawar123/Project-Atliq/assets/123149177/95330dc3-ba8b-471e-b944-972d48e60e60)
- Step 12 : In the report view, under the insert tab, using shapes option from elements group a rectangle was inserted & similarly using image option company's logo was added to the report design area. 
Following is the image of sales report:

![Report](https://github.com/aniketpawar123/Project-Atliq/assets/123149177/1aaeb884-dd8d-4655-bea5-e0dfb29bbc12)



        
- Step 13 : Second page is of performance of hotel city wise.
Following image of performance report:

![performance](https://github.com/aniketpawar123/Project-Atliq/assets/123149177/6b1e934e-89db-478e-8e6b-9871f99ed906)

## Measure Table Calculation:

1.Revenue : To get the total revenue_realized

    Revenue = SUM(fact_bookings[revenue_realized])

2.Total Bookings : To get the total number of bookings happened

    Total Bookings = COUNT(fact_bookings[booking_id])

3.Total Capacity : To get the total capacity of rooms present in hotels

    Total Capacity = SUM(fact_aggregated_bookings[capacity])

4.Total Succesful Bookings : To get the total succesful bookings happened for all hotels

    Total Succesful Bookings = SUM(fact_aggregated_bookings[successful_bookings])

5.Occupancy % : Occupancy means total successful bookings happened to the total rooms available(capacity)
    
    Occupancy % = DIVIDE([Total Succesful Bookings],[Total Capacity],0)

6.Average Rating : Get the average ratings given by the customers

    Average Rating = AVERAGE(fact_bookings[ratings_given])

7.No of days : To get the total number of days present in the data.
In our case, we have data from May to July. So 92 days.

    No of days = DATEDIFF(MIN(dim_date[date]),MAX(dim_date[date]),DAY) +1

8.Total cancelled bookings : To get the"Cancelled" bookings out of all Total bookings happened

    Total cancelled bookings = CALCULATE([Total Bookings],fact_bookings[booking_status]="Cancelled")

9.Cancellation % : calculating the cancellaton percentage

    Cancellation % = DIVIDE([Total cancelled bookings],[Total Bookings])

10.ADR : (Average Daily rate)

It is the ratio of revenue to the total rooms booked/sold. 
It is the measure of the average paid for rooms sold in a given time period

    ADR = DIVIDE( [Revenue], [Total Bookings],0)

11.Realisation % : 
It is nothing but the succesful "checked out" percentage over all bookings happened.

    Realisation % = 1- ([Cancellation %]+[No Show rate %])

12.RevPAR : (Revenue Per Available Room)

RevPAR represents the revenue generated per available room, whether or not they are occupied. RevPAR helps hotels measure their revenue generating performance to accurately price rooms. RevPAR can help hotels measure themselves against other properties or brands.

    RevPAR = DIVIDE([Revenue],[Total Capacity])

13.DBRN : (Daily Booked Room Nights)

This metrics tells on average how many rooms are booked for a day considering a time period

    DBRN = DIVIDE([Total Bookings], [No of days])

14.DSRN  : (Daily Sellable Room Nights)

This metrics tells on average how many rooms are ready to sell for a day considering a time period

    DSRN = DIVIDE([Total Capacity], [No of days])

15.Revenue WoW change % : To get the revenue change percentage week over week.

Here, 
revcw  for current week
revpw for previous week

    Revenue WoW change % = 
    Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date [wn]),MAX(dim_date[wn]))
    var revcw = CALCULATE([Revenue],dim_date[wn]= selv)
    var revpw =  CALCULATE([Revenue],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

    return
    DIVIDE(revcw,revpw,0)-1

16.Occupancy WoW change % : To get the occupancy change percentage week over week.

Here, 
revcw  for current week
revpw for previous week

    Occupancy WoW change % = 
    Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
    var revcw = CALCULATE([Occupancy %],dim_date[wn]= selv)
    var revpw =  CALCULATE([Occupancy %],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

    return
    DIVIDE(revcw,revpw,0)-1

17.ADR WoW change % : To get the ADR(Average Daily rate) change percentage week over week.

Here, 
revcw  for current week
revpw for previous week

    ADR WoW change % = 
    Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
    var revcw = CALCULATE([ADR],dim_date[wn]= selv)
    var revpw =  CALCULATE([ADR],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

    return
    DIVIDE(revcw,revpw,0)-1

18.Revpar WoW change % : To get the RevPar(Revenue Per Available Room) change percentage week over week.

Here, 
revcw  for current week
revpw for previous week

    Revpar WoW change % = 
    Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
    var revcw = CALCULATE([RevPAR],dim_date[wn]= selv)
    var revpw =  CALCULATE([RevPAR],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

    return
    DIVIDE(revcw,revpw,0)-1

19.Realisation WoW change % : To get the Realisation change percentage week over week.

Here, 
revcw  for current week
revpw for previous week

    Realisation WoW change % = 
    Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
    var revcw = CALCULATE([Realisation %],dim_date[wn]= selv)
    var revpw =  CALCULATE([Realisation %],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

    return
    DIVIDE(revcw,revpw,0)-1

20.DSRN WoW change % : To get the DSRN(Daily Sellable Room Nights) change percentage week over week.

Here, 
revcw  for current week
revpw for previous week

    DSRN WoW change % = 
    Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
    var revcw = CALCULATE([DSRN],dim_date[wn]= selv)
    var revpw =  CALCULATE([DSRN],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

    return
    DIVIDE(revcw,revpw,0)-1



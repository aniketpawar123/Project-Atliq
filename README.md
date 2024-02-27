# Atliq
## Problem Statement

Atliq, a prominent player in the hospitality industry, operates luxury and business hotels across major Indian cities like Bangalore, Hyderabad, Mumbai, and Delhi. To enhance operational insights and decision-making, Atliq aims to leverage Microsoft Power BI. The project entails developing intuitive dashboards and reports to provide actionable insights into occupancy rates, revenue generation, guest satisfaction, and regional performance trends. The goal is to empower stakeholders with data-driven narratives that optimize resource allocation, refine marketing strategies, and improve overall efficiency and profitability across Atliq's diverse hotel portfolio in India.

## Steps followed
Step 1 : Load data into Power BI Desktop, dataset is a csv file.

Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.

Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".

Step 4 : Errors and empty values were seen in the columns, which will be eliminated.

Step 5 : In the report view, under the view tab, theme was selected.

Step 6 : Visual filters (Slicers) were added for date month wise and also for week.

Step 7 : Six card visuals were added to the canvas,to show key measures.cards

Step 9 : Realisation perecntage and ADR of booking platform is shown by line and stacked column chart.

Step 10 : Property key matric table is created to show performance of each hotel using key matric.

Step 11 : Week wise trend shown by trend line using RevPar(Revenue per Available room),ADR(Average Daily Rate),Occupancy %. trend

Step 12 : In the report view, under the insert tab, using shapes option from elements group a rectangle was inserted & similarly using image option company's logo was added to the report design area. 
### Following is the image of sales report:
![Sales Page](https://github.com/aniketpawar123/Project-Atliq/assets/123149177/d565b26e-8884-4837-aebd-c0e9a53c1397)



Step 13 : Second page is of performance of hotel city wise. 
### Following image of performance report:


![Perfo](https://github.com/aniketpawar123/Project-Atliq/assets/123149177/62390f43-f24c-4887-b4fb-07783a0b311d)

### Key Measure Calculation:

1.  ADR : (Average Daily rate)

    It is the ratio of revenue to the total rooms booked/sold. It is the measure of the average paid for rooms sold in a given time period

    ADR = DIVIDE( [Revenue], [Total Bookings],0)

2.  RevPAR : (Revenue Per Available Room)

    RevPAR represents the revenue generated per available room, whether or not they are occupied. RevPAR helps hotels measure their revenue generating performance to accurately price rooms. RevPAR can help hotels measure themselves against other properties or brands.

    RevPAR = DIVIDE([Revenue],[Total Capacity])

3.  DBRN : (Daily Booked Room Nights)

    This metrics tells on average how many rooms are booked for a day considering a time period

    DBRN = DIVIDE([Total Bookings], [No of days])
    
4.  DSRN : (Daily Sellable Room Nights)

    This metrics tells on average how many rooms are ready to sell for a day considering a time period

    DSRN = DIVIDE([Total Capacity], [No of days])
    
5.  Occupancy % :
    Occupancy means total successful bookings happened to the 
total rooms available(capacity)

    Occupancy % = DIVIDE([Total Succesful Bookings],[Total Capacity],0)



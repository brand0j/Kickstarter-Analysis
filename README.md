# Kickstarter Analysis

## Overview of Project
We were tasked with analyzing Kickstarter data where we focused on analyzing overall outcomes in regard to their launch date along with their initial kickstarter goal. 

### Purpose
Our purpose was to analyze and draw conclusions about the data so we can make suggestions to Louise regarding her own Kickstarter goal for a play.

## Analysis and Challenges

### Analysis of Outcomes Based on Launch Date
I began the analysis by extracting the year from the Date Created column to a new column within the datasheet. Through the use of a pivot table and selecting the fields we were interested in, I was able to see all the necessary data to begin drawing insights regarding Louise's goals for her kickstarter campaign. Arranging this table in descending order and plotting the corresponding graph helped visualize and confirm when kickstarter campaigns for theater are the most succesful with respect to time (arranged by month).

![Theater_Outcomes_vs_Launch](https://github.com/brand0j/Kickstarter-Analysis/blob/main/Resources/Theater_Outcomes_vs_Launch.png)

### Analysis of Outcomes Based on Goals
The next step in my analysis was to help Louise pinpoint the ideal amount for her kickstarter goal to ensure the highest probability of it being succesful. The goal is to gain insight on the following with respect to their goal amount:

- *# Succesful*
- *# Failed*
- *# Canceled*
- *# Total Outcomes*
- *% Succesful*
- *% Failed*
- *% Canceled*

Splitting up the goal amount into intervals of values *(a,b]*, where:

- a = {0,1000,5000,10000,15000,20000,25000,30000,35000,40000,45000,50000}
- b = {1000,5000,10000,15000,20000,25000,30000,35000,40000,45000,50000,inf}

we can get a count of outcomes for that interval along with the specification that we are only interested in the subcategory *"plays"*. This is implemented in the following way using the [COUNTIFS() function](https://support.microsoft.com/en-us/office/countifs-function-dda3dc6e-f74e-4aee-88bc-aa8c2a866842?ui=en-us&rs=en-us&ad=us) :

```
=COUNTIFS(Kickstarter!F:F,"successful",Kickstarter!D:D,">999",Kickstarter!D:D,"<5000",Kickstarter!R:R,"plays")
=COUNTIFS(Kickstarter!F:F,"failed",Kickstarter!D:D,">999",Kickstarter!D:D,"<5000",Kickstarter!R:R,"plays")
=COUNTIFS(Kickstarter!F:F,"canceled",Kickstarter!D:D,">999",Kickstarter!D:D,"<5000",Kickstarter!R:R,"plays")
```

I applied this formula going down each respective column while adjusting the interval as necessary. The result was a table with the desired count with respect to the conditions previously mentioned. Now that we have this information it's time to analyze these outcomes as a percentage against the total number of kickstarters. Take the sum of each row to get the amount of total projects within that range. For an interval *(a,b]*: ```Total_Projects = (Succesful + Failed + Canceled) in =SUM(B2:D2)```. Now that we have a sum of the total number of projects given an interval *(a,b]* we can get the percentage of each outcome by simply taking the number of outcomes and dividing it by the total 
```% = (Outcomes / Total )``` and setting the number format to %
    
All of the data is now sorted in a way we can begin to visualize. The final step was to graph what was discovered in the hopes we can understand it better. Setting the X-axis to our intervals and the Y-axis as the %, it becomes much more clear how the goal amount affects the amount of succesful kickstarter campaigns which was what we were interested in from the start.

![Outcomes_Based_on_Goal](https://github.com/brand0j/Kickstarter-Analysis/blob/main/Resources/Outcomes_vs_Goals.png)

### Challenges and Difficulties Encountered

When looking at outcomes based on Launch Date everything was fairly straightforward, but the biggest issue would be assigning the rows, columns, values & filters correctly and removing what wasn't necessary. Another thing that might have caused issues would be arranging the data in descending order.

After I began analyzing outcomes based on goals I couldn't figure out a clever way to specify the upper & lower bounds inside COUNTIFS(). I ultimately settled on writing the correct form of the function at the top of each column, applying it to the entire column, and then going in and changing the upper & lower bounds to what I needed them to be. This was tedious since the syntax inside of COUNTIFS() is easy to mess up. An additional note is that for each range of values, the lower bound needs to be 1 less than the specified amount while the upper bound needs to be 1 more than the specified amount. 

Taking the sum of each row for Total Projects was straightforward as was calculating the percentage since I changed the number format appropriately. Plotting the graph was easy enough, but making the X-axis legible means you need to increase the size of the image itself. Otherwise it's almost impossible to tell what the values are supposed to be making it harder to read for someone else. You should immediately notice that success & failure have a perfect negative correlation (the relationship between them is exactly opposite all of the time). This is due to there being no count of canceled outcomes. If there were canceled outcomes the two would be negatively correlated, but not perfectly.

## Results

- What are two conclusions you can draw about the Outcomes based on Launch Date?

The first thing you can see by looking at Theatre Outcomes by Launch Date is that from April to May there is a significant increase in the amount of succesful kisckstarter campaigns compared to the amount that fail during this time. Another thing you should notice is that in December the amount of kickstarters that succeed & fail is almost exactly equal and we could expect to have the lowest % of success during this time. 

- What can you conclude about the Outcomes based on Goals?

When we are looking at percentages in Outcomes Based on Goal, you can see that the highest chance of success would be in the interval *(0,1000]*, closely followed by *(1000,5000]*. When it comes to which one is more of an accurate statistic I would say it's *(1000,5000]* since there is almost 3x the amount of total projects within this interval. Another thing to note is that success & failure are perfectly negatively correlated due to there being no data of canceled projects. 

- What are some limitations of this dataset?

This leads perfectly into the limitations of this set of data. Just looking at the graph you might think that kickstarters with goals between $35,000 and $45,000 are relatively succesful as well, but when you look at the table you will realize that this is due to a lack of data in general. There are only 9 total projects within this range which wouldn't be a large enough sample to accurately describe the success rate. 

- What are some other possible tables and/or graphs that we could create?

In terms of being able to use additional data I believe looking at Outcomes Based on Goals and applying it to the entire "Theatre" parent cateogory might be effective. Something that came to mind when looking at success/failure based on goals was being able to visualize this in a boxplot with success & failure on the same plot. This would be able to convey at a quick glance where the majority of our succesful campaigns were in regards to their target goal, similarly with where the majority of campaigns failed. This would provide a useful conclusion of exactly where we would want to set our Kickstarter campaign goal to ensure the highest probability of success. 

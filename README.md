# Kickstarting with Excel

## Overview of Project
We were tasked with analyzing Kickstarter data where we focused on analyzing overall outcomes in regard to their launch date along with their initial kickstarter goal. 

### Purpose
Our purpose was to analyze and draw conclusions about the data so we can make suggestions to Louise regarding her own Kickstarter goal for a play.

## Analysis and Challenges

### Analysis of Outcomes Based on Launch Date
I began the analysis by extracting the year from the Date Created column to a new column within the datasheet. Through the use of a pivot table, I was able to see all the necessary data to begin drawing insights regarding Louise's goals for her kickstarter campaign. Arranging this table in descending order and plotting the corresponding graph helped visualize and confirm when kickstarter campaigns for theater are the most succesful with respect to time (arranged by month). The tricky part in this step was making sure to remove what wasn't necessary after assigning the rows to Date Created and arranging the table in descending order. Using a pivot chart the data was much easier to understand once it was visualize in the following graph.

![Theater_Outcomes_vs_Launch](file:///C:/Users/nodna/Desktop/Rutgers_Data_Science_Bootcamp/MODULE_1_CHALLENGE/Resources/Theater_Outcomes_vs_Launch.png)

### Analysis of Outcomes Based on Goals
The next step in my analysis was to help Louise pinpoint the ideal amount for her kickstarter goal to ensure the highest probability of it being succesful. The goal is to gain insight on the following with respect to their goal amount:

    * # Succesful
    * # Failed
    * # Canceled
    * % Succesful
    * % Failed
    * % Canceled

Splitting up the goal amount into intervals of values (a,b], where:

    * a = {0,1000,5000,10000,15000,20000,25000,30000,35000,40000,45000,50000}
    * b = {1000,5000,10000,15000,20000,25000,30000,35000,40000,45000,50000,inf}
        - first interval: (0,1000]
        - second interval: (1000,5000]
        - etc.

By splitting up our goal amount into these intervals we can get a count of outcomes for that interval along with the specification that we are only interested in analyzing these counts regarding the subcategory "plays". This is implemented in the following way:

```
=COUNTIFS(Kickstarter!F:F,"successful",Kickstarter!D:D,">999",Kickstarter!D:D,"<5000",Kickstarter!R:R,"plays")
=COUNTIFS(Kickstarter!F:F,"failed",Kickstarter!D:D,">999",Kickstarter!D:D,"<5000",Kickstarter!R:R,"plays")
=COUNTIFS(Kickstarter!F:F,"canceled",Kickstarter!D:D,">999",Kickstarter!D:D,"<5000",Kickstarter!R:R,"plays")
```

I applied this formula going down each respective column while adjusting the interval as necessary. The result was a table with the desired count with respect to the conditions previously mentioned. Now that we have this information it's time to analyze these outcomes as a percentage against the total number of kickstarters. Take the sum of each row to get the amount of total projects within that range. For an interval (a,b]: #_Total_Projects = (#_Succesful + #_Failed + #_Canceled) in (a,b]

```
=SUM(B2:D2)
```

Now that we have a sum of the total number of projects given an interval (a,b] we can get the percentage of each outcome by simply doing the following:

    * %_Outcome = #_Outcome/#_Total_Projects 
    
All of the data is now sorted in a way we can begin to visualize. The final step was to graph what was discovered in the hopes we can understand it better. Setting the X-axis to our intervals and the Y-axis as the %, it becomes much more clear how the goal amount affects the amount of succesful kickstarter campaigns which was what we were interested in from the start.

![Outcomes_Based_on_Goal](file:///C:/Users/nodna/Desktop/Rutgers_Data_Science_Bootcamp/MODULE_1_CHALLENGE/Resources/Outcomes_vs_Goals.png)

### Challenges and Difficulties Encountered

When I began analyzing outcomes based on goals I couldn't figure out a clever way to specify the upper & lower bounds inside COUNTIFS. I ultimately settled on writing the correct form of the function at the top of each column, applying it to the entire column, and then going in and changing the upper & lower bounds to what I needed them to be. This step was repeated across the row where you switched "succesful" to "failure", applied to the entire column, and then adjusting the upper & lower bounds for each cell going down the column. One thing to note here is that for each range of values, the lower bound needs to be 1 less than the specified amount while the upper bound needs to be 1 more than the specified amount. Taking the sum of each row for Total Projects was straightforward as was calculating the percentage. Plotting the graph you should immediately notice that success & failure have a perfect negative correlation (the relationship between them is exactly opposite all of the time). This is due to there being no count of canceled outcomes. If there were canceled outcomes the two would be negatively correlated, but not perfectly.

## Results

- What are two conclusions you can draw about the Outcomes based on Launch Date?

- What can you conclude about the Outcomes based on Goals?

- What are some limitations of this dataset?

- What are some other possible tables and/or graphs that we could create?

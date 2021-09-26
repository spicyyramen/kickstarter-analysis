# Kickstarting with Excel

## Overview of Project
To analyze Kickstarter data and uncover trends.

### Purpose
The purpose of this project is to help Louise determine whether her funding goal is reasonable and when she should launch her play project using the data from other Kickstarter projects as our reference data.

## Analysis and Challenges
### Analysis of Outcomes Based on Launch Date
First, a new column titled **years** was added to the original `kickstarter_challenge.xlsx` file. In this column, the `Year()` function was used to extract the year from the 'Date Created Conversion' column. 
![Example of newly created *years* column](/resources/year-example.png)

Next, a pivot table was created from the Kickstarter data and the new sheet was labeled "Theater Outcomes by Launch". The PivotTable Fields were made as follows: Filters were created for **parent category** and **years**, Columns for **outcomes**, Rows for **date created conversion**, and Values for **count of outcomes**. 

![PivotTable Fields- completed](/resources/PivotTable.png)

The PivotTable was then filtered to show only **theater** campaigns, and the 'live' outcome was filtered out. The remaining outcomes (successful, failed, and canceled) were sorted in descending order. An example of the finished PivotTable is shown below.

![Final PivotTable](/resources/PivotTable-complete.png)

A line chart was then created from the PivotTable which displayed the Launch Month on the x-axis and the percentage of each outcome along the y-axis. An example of this line chart can be found below in the [**Results**](https://github.com/spicyyramen/kickstarter-analysis#results) section.

### Analysis of Outcomes Based on Goals
The purpose of this analysis was to evaluate the relationship between play campaign outcomes and their funding goal amounts. A new sheet was created with a table that looks like the image below.

![Example Table](/resources/play-table.png)

The `COUNTIFS()` function was then used to populate the number of projects with each outcome at the specified funding goal amounts. Here is an example of the formula in use:
>`=COUNTIFS(Kickstarter!$F:$F,"successful",Kickstarter!$D:$D,"<1000",Kickstarter!$O:$O,"plays")`

In this formula, the 'F' column from the 'Kickstarter' sheet is being searched for the value "successful", the 'D' column is being searched for values "<$1000", and the 'O' column is being searched for the value "plays". The formula will then count each occurence where all of these criteria are met, and output the value into my '**number successful**' column in the '**Less than 1000**' row. The formula was reused to populate all the values in columns B-D.

To populate values for the '**total projects**' column in E, the `SUM()` function was used. An example of the formula in use on cell E2 is shown below:
>`=SUM(B2:D2)`

In this formula, the number successful, failed, and canceled for each funding goal range are summed to give a total number of projects with that funding goal range.

To calculate the percentage for each outcome/funding range, the number of a given outcome was divided by the total # of projects within the same funding range and multiplied by 100. An example of the formula in use from cell F2 is shown below:
>`=IFERROR(B2/$E$2*100,0)`

***Note, the `IFERROR` was not necessary for this to work. Inclusion will be explained later in the challenges section***

Lastly, a line chart was created with the 'Funding Goal Ranges' listed on the x-axis and the 'Percentage of Outcome' on the y-axis. An image of this graph can be seen in the [**Results**](https://github.com/spicyyramen/kickstarter-analysis#results) section below.

### Challenges and Difficulties Encountered
The primary issues I encountered were simple syntax errors. For instance, with the Outcomes v Goals formulas. When calculating the percentage outcomes, I ended up with divide-by-zero errors. Initially I thought it was because some of the values may have actually been zero. To correct this, I added the `IFERROR()` function before division formula, and set the value to be '0'. After further investigation I realized that the values weren't supposed to be zero, and that I had made a small mistake with syntax, so I fixed that issue and just left the `IFERROR()` formulas as they were (since it doesn't make a difference). 


## Results

### Theater Outcomes Vs Launch Date
**- What are two conclusions you can draw about the Outcomes based on Launch Date?**
	
Two conclusions that can be drawn from the graph below are:

1. All outcomes seem to follow the same trends based on month of the year
2. Summer (May-July) appears to be the best time to launch a theater project, and winter (Nov-Jan) seems to be the worst time to launch a theater project.

![Theater Outcomes vs Launch](/resources/theater_outcomes_vs_launch.png)

### Outcomes vs Goals
**- What can you conclude about the Outcomes based on Goals?**
  
   At the lower funding goal ranges, a large percentage of projects are succesful. As you begin moving into mid-range funding goals, rates of project success and failure both begin to approach ~50%, indicating that at this funding range there's about a 50% chance of success or failure. As you begin approaching the higher end funding ranges the data becomes more unpredictable, and rates of success and failure fluctuate quite a bit between high-end ranges. This might be due to lower n values (fewer projects) in the high-end ranges, which could skew the results. This indicates that lower funding goals often result in successful campaigns, mid-level funding goals result in successful campaigns approximately 50% of the time, and the success of high funding goal projects is inconsistent and unpredictable.

![Project Outcomes vs Goal Amounts](/resources/outcomes_vs_goals.png)

**- What are some limitations of this dataset?**
   
One limitation of this dataset is we do not know some of the other factors that contributed to whether a campaign met its funding goals or not. For instance, we do not know how different types of advertising may have helped some campaigns reach their goals more effectively than others. 

**- What are some other possible tables and/or graphs that we could create?**
We could look more into how the number of backers and average donation amounts relate to the outcomes of projects. This could then be compared to the length of the project campaign to see if there's any meaningful trends.










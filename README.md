# Kickstarting with Excel
## Overview Of Project:
### Purpose
Our client, Louise, has enlisted our help to understand how different fundraising campaigns have performed in relation to their launch dates and the funding goals which they set out. This analysis will help Louise to compare how her own campaign to raise funds for her play ‘Fever’ performed. She will also be able to tell if she launched at a different time of year or set a different goal for her fundraising, if this would have impacted the success of her overall campaign based on the data we are analyzing. 

## Analysis and Challenges:
### Kickstarting
As a starting point for analysis, I reviewed the set of data which had been provided to determine how usable the data was in its current form.  The data needed some minor cleansing to extract information into separate columns to provide a better way to analyze the specific Subcategory of “plays” which Louise was particularly interested in. Firstly, I took the category/subcategory field and used the ‘text to columns’ function to split this data into two separate columns: “Parent Category” and “Subcategory”. Also, the data which was being held in the ‘launched_at’ column was not human readable, so this was converted using a formula to translate Unix Time into a familiar date format in a new column ‘Date Created Conversion’. Using my newly created column, I also extracted the Year from the date into another newly created column ‘Years’. 

### Analysis of Outcomes based on Launch Date
Using the cleansed data, now I can begin analyzing as per Louise’s asks. I created a pivot table based on the data in the ‘Kickstarter’ sheet. I included 2 filters fields: Parent Category and Years to allow me to focus on ‘Theater’ specifically. Then I used the Date Created Conversion to generate rows and the Outcomes field to generate columns. Louise was also not interested ‘Live’ campaigns, so these have been filtered out from columns and sorted descending so Successful appears first. Finally, I converted this into the following line chart so the results were easily digestible for the client. 

<img src="https://github.com/JerryMcG/KickstarterAnalysis/blob/main/Resources/Theater_Outcomes_vs_Launch.png">

### Analysis of Outcomes Based on Goals
Each of the Column Headers and Goal ranges were manually entered and then I began building COUNTIFS() formulas to calculate the results. 
**Example: =COUNTIFS(Kickstarter!$F:$F,"successful",Kickstarter!$D:$D,"<1000",Kickstarter!$R:$R,"plays")**
To break down the above formula; the first section contains the range of where the data and everything following is a criteria for inclusion in the final result. This particular formula looks for only successful outcomes, with a goal of under $1000 and a subcategory of plays. This formula was then copied and updated for Failed and Canceled Campaigns within the same ranges. Next, I summed up Successful, Failed and Canceled Projects for each range using the SUM() function in col E. Finally, I created percentages of each by taking the original number, diving by total projects and then formatting the cell to display % values. Now that the data is generated, I created a line chart to display this information again in an easily digestible format for Louise. 

<img src="https://github.com/JerryMcG/KickstarterAnalysis/blob/main/Resources/Outcomes_vs_Goals.png">

### Challenges and Difficulties Encountered
1. When creating my Pivot for Theatre Outcomes by Launch Date, when I pulled Data Created Conversion into the Pivot table, Excel automatically added Years and Quarters to further categorize this Date field. However I was not interested in this level of granularity, so I removed both leaving me only with Date Created Conversion Month being displayed in the rows.
2. Some of the formulas I was not entirely familiar with, so I had to read and understand them before applying them to my data. When using the COUNTIFS() formula, I manually checked some of the results of my data to ensure the formula was working as expected. I did this manual check by applying the same filters on the raw data to ensure the numbers were equal. As a secondary check – I added sum totals for each of the Successful/Failed/Canceled to quickly check the manually filtered data was matching the same count. 
3. When copying the COUNTIFS() formula to another cell, I originally had forgotten to use the static definition of a cell using $. This meant that the result was incorrect and I had to refactor the formulas to ensure the columns required stayed the same.
4. When calculating ‘Number of Cancelled’ fields for the Goal ranges – I was concerned that my formula was not working since all results were 0. Using another manual check for Canceled only, I was able to confirm that no ‘Plays’ were canceled and hence my result was correct. 

## Results:
- What are two conclusions you can draw about the Theatre Outcomes by Launch Date?
May, June and July are the most successful months to launch a Theatre funding Campaign. There are less funding campaigns launched in Nov and Dev, with Dec showing us an almost equal likelihood of success/failure on a newly launched campaign.

- What can you conclude about the Outcomes based on Goals?
If a new Play campaign has a goal between 45000 – 49999, it is 100% likely to fail, based on the data we have analyzed.  

- What are some limitations in this dataset? 
Within this dataset, there is no detail on what the goal amount intends to finance. We just know that this is to fund a Play that Louise hopes to launch, however we cannot compare if she needs more actors/stagehands to perform or if she has chosen a more expensive theatre to showcase the play in. This dataset does not contain any data to determine what happens after the campaign is completed. It would have been great to see revenues achieved 6-12months after campaign closure to give a full story of how a successful campaign can turn into a financially successful venture. 

- What are some other possible tables and/or graphs we could create?
An additional area we could have analyzed was impact of the number of donations a campaign received could have on outcome (Outcomes based on Number of Backers). Similarly, we could have use length of campaign as a factor in success of a campaign (Outcomes Based on Campaign Length). This could all have been further refined using country selection based on where Louise plans to launch her campaign for both number of donations/campaign length. (Outcomes Based on Campaign Length in US, Outcomes based on Number of Backers in US).

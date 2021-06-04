# **Channel Spend Optimization**

## 1. Problem Motivation
Using a combination of data driven analytics and market knowledge, the leadership team has identified a strong opportunity to increase its market share within a specific market segment. The team also believes that the appropriate market lever to drive market share would be to increase **brand awareness**. 

The leadership team believes in the idea of their customer behavior to purchase to resemble the McKinsey’s Consumer Decision Journey. Within this framework, they have identified huge potential for driving sales by increasing the number of target customers who consider their product. That is, increasing the number of customers who have their product in the **initial consideration set**.

[add pic here]

The marketing team is poised to accomplish this directive, but they need the help from a marketing data scientist for a problem they are having. They’d like to make sure that they are using their marketing dollars in the most efficient way possible across their marketing channels. More specifically, they’d like to maximizing the number of customers in the Initial Consideration Set using their marketing budget.  

## 2. Problem Structuring
The marketing data scientist works with the marketing team to structure the problem as follows:

-	**Identify Primary Metrics**: Identify a suitable metric that acts as robust and sensitive indicator of quantifying the idea of the number of the customers in the ‘Initial Consideration Set’. Several metrics were considered but the team settled on maximizing the number of clicks for this analysis. One of the reasons for this selection was that the number of clicks has been found to be strongly correlated with sales conversions from historic data. 
-	**Source Data and Plan Analysis Type**: Data is sourced from sql database. Analysis will use both predictive and optimization modeling.
-	**Validate Assumptions**: Is the historic data even relevant for the planned future marketing efforts? Are there any secondary or competing metrics to keep in mind when optimizing for a single CTR metric? Is paid last-touch attribution model suitable? What is an acceptable performance for the predictive model? 
-	Hypothesis: CTR can be adequately modeled as a function of the marketing channel and the marketing spend.


## 3. Analysis Methodology
After the assumptions are discussed and screened through with the team, the analytics proceeds to the analysis step. The steps in the analysis phase is as summarized below:

1. **Regression Model**: Develop a predictive model of CTR (unknown target variable) as a function of marketing expenditure (known input variable) to get the cost curves for each channel. Other variables like ad creative, seasonality considerations, etc. can be taken into account as well, but the team does not have adequate data for other variables at this time.
2. **Optimization Algorithm**: Use a greedy optimization algorithm to maximize the marginal number of clicks for every dollar value spent. The algorithm starts with zero spend for all channels, then repeatedly allocates a dollar to the channel that has the highest clicks-to-spend slope (from the cost curves in Step 1) at the channel’s current spend. Process is repeated until the budget is reached, and we have our optimal spend targets.


## 4. Results

The table below provides the performance of the model

| Channel | R2 Score  |
| ---   | :-: | 
| Bing| 0.93 | 
| Facebook | 0.98 |  
| Google | 0.94 |  

For a marketing budget of $500, the following table provides an optimal spend across the channels

| Channel | Optimal Ad Spend  |
| ---   | :-: | 
| Bing| $81 | 
| Facebook | $161 |  
| Google | $258 |  
| Total Budget | $500 | 

### 5. Significance and Next Steps

Findings from this effort allowed the marketing team to be more scientific about deciding how much to spend on each channel. Going forward, the marketing team will need additional help in setting up optimal campaign-level spend targets for automated bidding. A similar approach to the above can be used for helping the marketing team with this decision as well. 

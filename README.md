# **Channel Spend Optimization**

## 1. Problem Motivation
The leadership team has identified a strong opportunity to increase its market share within a specific market segment. The team also believes that the appropriate market lever to drive market share would be to increase **brand awareness**. 

The leadership team believes in the idea of their customer behavior to purchase to resemble the McKinsey’s Consumer Decision Journey. Within this framework, they have identified huge potential for driving sales by increasing the number of target customers who consider their product. That is, increasing the number of customers who have their product in the **initial consideration set**.

![Problem Motivation](https://github.com/sahilsaxena21/channel_spend_optimization/blob/main/CDJ.png)

The marketing team is poised to act on this directive, but they need the help from a marketing data scientist for a problem they are having. They’d like to make sure that they are using their marketing dollars in the most efficient way possible across their marketing channels. More specifically, they’d like to maximizing the number of customers in the Initial Consideration Set using their limited marketing budget. 

Currently, the team allocates the budget evenly across all 3 channels.

## 2. Problem Structuring
The marketing data scientist works with the marketing team to structure the problem as follows:

-	**Identify Primary Metrics**: Identify a suitable metric that acts as robust and sensitive indicator for quantifying number of the customers in the ‘Initial Consideration Set’. Several metrics were considered but the team settled on **maximizing the CTR** for this analysis.
-	**Source Data and Plan Analysis Type**: Data is sourced from sql database. Analysis will use both predictive and optimization modeling.
-	**Validate Assumptions**: Is the historic data even relevant for the planned future marketing efforts? Are there any metrics that can be cannabailized when optimizing for CTR? The existing dataset uses paid last-touch attribution, is this suitable? What is an acceptable performance for the predictive model? 
-	**Hypothesis**: CTR can be adequately modeled as a function of the marketing spend.


## 3. Analysis Methodology
After the assumptions are discussed and screened by the team, the project proceeds to the analysis phase. The analytical approach is as summarized below:

1. **Regression Model**: Develop a predictive model for CTR (unknown target variable) as a function of marketing expenditure (known input variable) to get the cost curves for each channel. 
2. **Optimization Algorithm**: Use a greedy optimization algorithm to maximize the marginal CTR for every dollar value spent. The algorithm starts with zero spend for all channels, then repeatedly allocates a dollar to the channel that has the highest CTR-to-spend slope (from the cost curves in Step 1) at the channel’s current spend. Process is repeated until the budget is reached, and we have our optimal spend targets.

## 4. Results

The cross validation performance of the model is as follows:

| Channel | R2 Score  | Standard Deviation | 
| ---   | :-: | :-: | 
| Bing| 0.95 | 0.03 | 
| Facebook | 0.95 | 0.06 | 
| Google | 0.81 | 0.09 | 

For a marketing budget of $5000, the optimal spend across the channels is as follows:

| Channel | Optimal Ad Spend  |
| ---   | :-: | 
| Bing| $400 | 
| Facebook | $2,200 |  
| Google | $2,400 |  
| Total Budget | $5000 | 

### 5. Significance and Next Steps

Findings from this effort allowed the marketing team to be more scientific about deciding how much to spend on each channel. Going forward, the marketing team will need additional help in setting up optimal campaign-level spend targets for automated bidding. A similar approach to the above can be used for helping the marketing team with this decision as well. Moreover, other variables like ad creative, seasonality considerations, etc. can be taken into account as well to further improve the model R2 score.

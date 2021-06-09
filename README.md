# **Channel Spend Optimization**

## 1. Problem Motivation
A hypothetical leadership team has identified a strong opportunity to increase its market share within a specific market segment. The team also believes that the appropriate market lever to drive market share would be to increase **brand awareness**. 

The leadership team believes that their target segment's journey-to-purchase is aligned with the McKinsey’s Consumer Decision Journey. Within this framework, they have identified huge potential for driving sales by increasing the number of target customers who consider their product i.e. increasing the number of customers in the **initial consideration set**.

![Problem Motivation](https://github.com/sahilsaxena21/channel_spend_optimization/blob/main/CDJ.png)

The marketing team is poised to act on this directive, but they need the help from a marketing data scientist for a problem they are having. They’d like to make sure that they are using their marketing budget ($5,000) in the most efficient way possible across their marketing channels. 

Currently, the team allocates the budget evenly across all 3 channels.

## 2. Problem Structuring
The marketing data scientist works with the marketing team to structure the problem as follows:

-	**Identify Metric**: Identify a suitable metric that acts as robust and sensitive indicator for quantifying the number of the customers in the ‘Initial Consideration Set’. Several metrics were considered, but the team settled on **maximizing the CTR** for this analysis. 
-	**Source Data and Plan Analysis Type**: Data is sourced from sql database. Analysis will use both predictive and optimization modeling.
-	**Validate Assumptions**: Is the historic data relevant for the planned future marketing efforts? Are there any metrics that can be cannabailized when optimizing for CTR (e.g. brand reputation from possible click-baiting)? Moreover, the existing dataset uses paid last-touch attribution, is this suitable?
-	**Analysis Hypothesis**: CTR can be modeled as a function of the marketing spend.

## 3. Data
The following summarizes relevant findings to contexualize the problem:
- Existing dataset of CTR vs. campaign ad spend is available.
- Expected value of the number of impressions per ad campaign has been found to be around a 1,000.
- Each click is worth a $1,000 to the business. This was calculated using the equation **E(c) = P(conversion|c) * LTV** where **E(c)** is the expected revenue generated from a click, **P(conversion | c)** represents the probability of conversion given a user has clicked, and **LTV** represents the lifetime value of the customer.

## 4. Analysis Methodology
After the assumptions are screened by the team for acceptability, the project proceeds to the analysis phase. The analytical approach is as summarized below:

1. **Regression Model**: Develop a regression model for CTR (unknown target variable) as a function of marketing expenditure (known input variable) to get the cost curves for each channel. Regression model should be within +/- 10% to be deemed a good fit. 
2. **Optimization Algorithm**: Use a greedy optimization algorithm to maximize the marginal CTR for every dollar value spent. The algorithm starts with zero spend for all channels, then iteratively allocates a dollar to the channel that has the highest cost curve slope at the channel's current spend. The algorithm continues to allocate spending across the channels, until the budget is reached, and we have our optimal spend targets.

## 5. Key Results

The cross validation performance of the cost curve regression model for each channel is as follows. All models meet our acceptability criterion of +/- 10%. Moreover, performance of all models were found to be robust, as per the standard deviation results of a 5-fold cross validation.  

| Channel | Standard Error of Regression | Standard Deviation of Adjusted R2 | 
| ---   | :-: | :-: | 
| Bing| 6% | 0.03 | 
| Facebook | 5% | 0.002 | 
| Google | 1% | 0.09 | 

Utilizing the cost curves, optimal spend across the channels for a marketing budget of $5,000 is as follows:

| Channel | Optimal Ad Spend  |
| ---   | :-: | 
| Bing| $400 | 
| Facebook | $2,200 |  
| Google | $2,400 |  

By spending marketing dollars more efficiently, we achieve a lift of **43 clicks**. The expected dollar value benefit from this lift is an additional revenue of **$43,000** from each campaign.

## 6. Next Steps

Going forward, the marketing team will need additional help in setting up optimal campaign-level spend targets for automated bidding. A similar approach to the above can be used for helping the marketing team with this decision as well. Moreover, other variables like ad creative, seasonality considerations, etc. can also be taken into account to further improve the standard error of regression of the regressed cost curves.

# Predicting Analyst Consensus in the Stock Market

### The Business Problem

We've been tasked by (ficticious) hedge fund Frye Street Capital to gauge the impact of fundamental financial data on a stock's value. 

### The Dataset

For our data, used the YahooQuery API to assist in scraping fundamental financial data for all the companies in the S+P500 and the NASDAQ. Then, we scraped TipRanks for analysts consensus data for each of the stocks, as we cannot get accuracy scores if we decide to predict the future. We then dropped all rows with missing values (mainly pre-revenue Biotech companies), and dropped any rows with outliers. The resulting dataframe had around 2000 companies in it.

### Classification Algorithms and Results

Initially, our plan was to create classification algorithms based on each companies fundamentals to predict whether or not the consensus price target of analyst was beating the S+P500 on an average year. Our baseline model was a Random Forest, and our tuned model gave us a F1 score of 0.81. Although this seems good, this is actually below our baseline score due to the class imbalance in the data.

Next, I made a Convolutional Neural Network with 1 1D convolutional layer and 2 dense layers. This barely performed better than our baseline model (F1 = 0.82), and still was beat out by our baseline score. With these 2 models proving to be epic failures, I decided to shift to projecting they expected growth rate based on analyst consensus, rather than mapping those rates to something discrete.

### Regression Algorithms and Results

For my first model, I ran a basic linear regression. Right away this blew away our naive baseline, with a RMSE of 0.16, corresponding to an average of 16% between our model and the actual datapoints, as shown by the graph below.

<p align="center">
  <img src = images/LinearRegressionActualvsPredicted.png width="750" height="500">
</p>

Next, I made a Feedforward Neural Network with 2 dense layers. This lowered our RMSE to 0.13, which is quite strong. That is shown on the following graph.

<p align="center">
  <img src = images/NeuralNetworkActualvsPredicted.png width="750" height="500">
</p>

Finally, I decided to aggregate the test predictions based on each of the companies sectors, in order to see which types of companies are most impacted by their fundamental financial data. As shown on the graph below, Real Estate and Financial Services are most impacted, with Healthcare, Communication Services, and Technology are the least impacted.

<p align="center">
  <img src = images/ResidualMagnitudeViz.png width="750" height="500">
</p>

### Next Steps

Deploy Model to help valuation of REIT, Materials, and Financial Stocks

Test on actual market performance, rather than analyst predictions.
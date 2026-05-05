# Solar energy generation analysis using k-means clustering

The aim of this project was to use k-means clustering to discover which atmospheric conditions contribute most towards solar panel power generation.

This analysis could prove useful for anyone considering home solar panels. Livings in an area with frequent partial cloud could mean that the panels generate around 50% as much as those with regularly sunny skies. This result can be used to calculate average panel output and thus time to break even on the installation cost. 

These results could also influence solar farm placement. Choosing a generally warm, dry, sunny location should increase ROI. 


## Data source and cleaning

The data used in this analysis is [available here](https://www.kaggle.com/datasets/pythonafroz/solar-powe-generation-data).

Here's an example of that the data looks like:\
![First five rows of data](/images/01-top-five-rows.png)

And here are some summary statistics. Sunshine, radiation and production have very high standard deviations, meaning that they have a large spread which could lead to misrepresentative clustering.\
![Summary statistics](/images/02-summary-stats.png)

Some notes on the data:
* All rows were unique and there were no null values.
* The data types for each row were int or float, so no categorical field encoding was necessary.
* The dataset holds hourly values for each day. There is no point in analyising records without any energy generation, so these rows were dropped. This left >3k rows.


## Methodology

The purpose of this project was to train a machine model to identify sets of conditions that determined solar panel generation. K-means clustering has been chosen for this analysis. It is an unsupervised ML technique, meaning that the correct results are not known beforehand and the ML is run in hopes of discovering new knowledge.

K-means was chosen to categorise the conditions into meaningful groups (the resultant clusters). This will hopefully allow for the identification of sets of conditions that lead to different power generation levels. Machine learning is especially useful in this situation, as it’s difficult to compare all seven variables at once using less mathematical methods.


### EDA

Boxplots\
![Boxplots](/images/03-boxplots.png)

Pairwise grid of all fields\
![Pairwise grid of all fields](/images/04-pairwise-grid-original-data.png)

Correlation matrix\
![Correlation matrix](/images/05-correlation-matrix.png)

Average power production by hour of day\
![Mean power generation](/image/07-mean-kwh.png)


### Training prep

Explain the elbow method\
![Elbow curve](/images/08-elbow.png)

## Results

Coefficients\
![Coefficients](/images/09-coefficients.png)

Pairwise grid\
![Pairwise grid](/images/10-pairwise-results.png)


## Conclusion and next steps



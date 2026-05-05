# Solar energy generation analysis using k-means clustering

The aim of this project was to use k-means clustering to discover which atmospheric conditions contribute most towards solar panel power generation.

This analysis could prove useful for anyone considering home solar panels. Livings in an area with frequent partial cloud could mean that the panels generate around 50% as much as those with regularly sunny skies. This result can be used to calculate average panel output and thus time to break even on the installation cost. 

These results could also influence solar farm placement. Choosing a generally warm, dry, sunny location should increase ROI. 

## Data source

The data used in this analysis is [available here](https://www.kaggle.com/datasets/pythonafroz/solar-powe-generation-data).

Some notes on the data:
* All rows were unique and there were no null values.
* The data types for each row were int or float, so no categorical field encoding was necessary.
* The dataset holds hourly values for each day. As there is no point in analyising records without any energy generation, these rows were dropped.

Here's an example of that the data looks like:
![First five rows of data](#)

And here are some summary statistics. Sunshine, radiation and production have very high standard deviations, meaning that they have a large spread which could lead to misrepresentative clustering.
![Summary statistics](#)

## Methodology

The purpose of this project was to train a machine model to identify sets of conditions that determined solar panel generation. K-means clustering has been chosen for this analysis. It is an unsupervised ML technique, meaning that the correct results are not known beforehand and the ML is run in hopes of discovering new knowledge.

K-means was chosen to categorise the conditions into meaningful groups (the resultant clusters). This will hopefully allow for the identification of sets of conditions that lead to different power generation levels. Machine learning is especially useful in this situation, as it’s difficult to compare all seven variables at once using less mathematical methods.

### Data cleaning

dfsadf

### Basic EDA

sdfgdf

### Further EDA

askjdhask

### Training prep

Explain the elbow method

## Results

Show coefficients and pairwise grid

## Conclusion and next steps



# Solar energy generation analysis using k-means clustering

The aim of this project was to use k-means clustering to discover which atmospheric conditions contribute most towards solar panel power generation.

This analysis could prove useful for anyone considering home solar panels. Livings in an area with frequent partial cloud could mean that the panels generate around 50% as much as those with regularly sunny skies. This result can be used to calculate average panel output and thus time to break even on the installation cost. 

These results could also influence solar farm placement. Choosing a generally warm, dry, sunny location should increase ROI. 
<br/><br/>


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
* Data was missing for May and some radiation values were below 0 (obviously impossible). These rows were dropped with the 0 radiation rows.
<br/><br/>


## Methodology

The purpose of this project was to train a machine model to identify sets of conditions that determined solar panel generation. K-means clustering has been chosen for this analysis. It is an unsupervised ML technique, meaning that the correct results are not known beforehand and the ML is run in hopes of discovering new knowledge.

K-means was chosen to categorise the conditions into meaningful groups (the resultant clusters). This will hopefully allow for the identification of sets of conditions that lead to different power generation levels. Machine learning is especially useful in this situation, as it’s difficult to compare all seven variables at once using less mathematical methods.
<br/><br/>


### EDA

Figure 5 displays boxplots for each field after zero production records were removed. Most of these contain outliers, which could throw off clustering.

Plot of power production over daily, weekly and monthly timescales:\
![Time series](/images/06-time-series.png)

Boxplots:\
![Boxplots](/images/03-boxplots.png)

Pairwise grids plot fields against one another to help identify patterns. Figure 6 scatterplots show broad spread for all pairs. The density plots are also useful, revealing one or more concentrations.

Pairwise grid of all fields. Scatter plots in the top triangle, bar charts on the diagonal and density plots in the lower triangle:\
![Pairwise grid of all fields](/images/04-pairwise-grid-original-data.png)

A correlations plot can also reveal relationships between fields. Figure 7 shows strong positive correlation between sunshine/radiation, radiation/production, temperature/radiation and temperature/production, with the greatest between sunshine/production. There are also strong negative corelations between humidity/sunshine, humidity/radiation and humidity/production.

Correlation matrix:\
![Correlation matrix](/images/05-correlation-matrix.png)

As production and radiation have the highest correlation, its worth plotting their average hourly values to see how they correspond. Figures 9 and 10 indicates they follow one another quite closely.

Average power production by hour of day\
![Mean power generation](/images/07-mean-kwh.png)
![Mean power generation](/images/11-mean-radiation.png)
<br/><br/>


### Training prep

The elbow method indicates the optimal number of clusters (k) by plotting the within-cluster sum of squares (WCSS, or inertia) against k. This is equivalent to running the model several times with different values of k. Low inertia indicates a tight cluster and vice versa. The goal is to find the point of diminishing return, the so-called elbow [citation]. Figure 11 indicates k=3 as optimal.

Note that a cluster value of 1 is never useful, as a single cluster represents the whole dataset. A high k is also unhelpful as it becomes harder to assign meaningful differences to each cluster.

Other methods for determining k are available. These include the silhouette method (calculating intra-cluster cohesion/separation), gap statistic (compares WCSS to random points), Calinski-Harabasz index (rewards higher cohesion) and hierarchical clustering (use a dendrogram to visualise data).

Elbow method plot:\
![Elbow curve](/images/08-elbow.png)
<br/><br/>


## Results

The model was run after choosing k. Because the k-means algorithm is sensitive to large numbers, each field was scaled to prevent any from introducing bias. Figure 13 shows the 7-dimensional coordinates of the three clusters. 

There is little separation within the following fields, meaning that they do not contribute highly to the centroid position: windspeed, pressure, temperature, humidity. Sunshine is more spread out, meaning it has a moderate effect on centroids. Radiation and production are highly spread, meaning that they are the main determinants of centroid position. This latter reinforces the relationship indicated in the correlation matrix.

Centroid locations:\
![Coefficients](/images/09-coefficients.png)

Pairwise grid with cluster differentiated by colour. Production shows clear banding of low/mid/upper generation across all other variables. The low generation band seems to be dominant across all other pairs, indicating that the system spending most of the daylight hours generating little power. There seems to be some overlap between the mid and upper generation bands, indicating the other fields have a weak influence on generation.

Pairwise grid of each field showing scatter by cluster assignment in the lower triangle, plus area charts on the diagonal:\
![Pairwise grid](/images/10-pairwise-results.png)
<br/><br/>


## Considerations

The dataset units are not known. This doesn’t necessarily affect the model (its simply examining distances between points) but this does make interpretation a little more difficult. However, we can make educated guesses about the units (such as temperature being in °C).

It is also unknown where the readings were taken, type of solar panels were used, if they were homogeneous brands, which direction they were facing and what angle they were placed at. All of which are likely to affect the power generated and thus the model outputs.

The data also had some basic errors (some radiation values below 0, data missing for May), so the accuracy of the data is suspect. 

At the time of writing, the data is somewhat old, being from 2017. Solar efficiency is likely to have improved since this time. Indeed, climate change could have altered local conditions slightly which could lead to different model results.
<br/><br/>


## Conclusion

Results show that radiation is the main determinant of production. Sunshine would intuitively be main factor. However, radiation measures the actual energy transferred to the panels, whereas the sunshine value merely measures sunshine time. Clouds only partly block solar energy, and thick or high clouds can still allow substantial radiation through [citation]. 

The model did differentiate three clusters based on production. Sunshine, humidity and temperature all influence production, but the main factor is radiation. These variables are of course linked and follow intuition; that production is generally best on sunny, dry, warm days and vice versa. Also, party clouded skies generally produce significantly more power than overcast days.

However, it’s hard to draw conclusions about the fields other than radiation/production due to the frequent overlap between clusters 1 and 2. 




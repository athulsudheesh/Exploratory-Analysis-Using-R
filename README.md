# Exploratory-Analysis-Using-R
This repository has the codes and figures from the analysis of World Health Dataset using various multivariate techniques such as PCA, CA, MCA, PLS, BADA, DICA and MFA.

*Multivariate Statistics* is the area of statisitcs that deals with the analysis of data sets with more than one variable. The main objective is to study how the variables are related to each other, and how they work in combination to discriminate between the groups on whcih the observations are made.

## Types of Analysis 

There are many different models, each with it's own type of analysis. In this project we will be dealing mostly with the following ones [@MultiVariateAnalysis]:

1. **Principal Component Analysis (PCA)** decompose the data table with correlated measurements into a new set of orthogonal variables. 
2. **Correspondence Analysis (CA)** is a generalization of PCA to contigency table.
3. **Multiple Correspondence Analysis (MCA)** is a generalization of CA when several nominal variables are analyzed. 
4. **Partial Least Squares (PLS)** methods relate the information present in two data tables that collect measurements on the same set of observations.
5. **Discriminant Analysis (DA)**  is used when a set of independent variables are used to predict the group to which a given unit belongs.
6. **Multiple Factor Analysis (MFA)** combines several data tables into one single analysis
7. **Multi-dimensional Scaling (MDS)** is used to represent the units as points on a map such that their Euclidean distances on the map approximate the original similarities.
8. **Cluster Analysis (CA) ** assign objects into groups so that objects from the same cluster are more similar to each other than objects from different groups.

## Resampling 

Resampling is a variety of methods for doing one of the following:

1. Estimating the precision of sample statisitcs by using subsets of available data (**jackknifing**) or drawing randomly with replacement from a set of data points (**bootstraping**)
2. Exchanging labels on data points when performing significance tests(**permutation tests**)
3. Validating models using random subsets (**cross validation**)

### Jackknife 

Jackknife was initially developed as a cross validation technique and was later extended to include variance estimation. In jackknife we start with estimating the parameter of interest from the whole sample. Then each variable is dropped from the sample and the parameter of interest is estimated from this smaller sample. This new estimates are called *partial estimates*. A *pseudo-value* is computed by finding the difference between *partial estimates* and whole sample estimates. These pseudo-values are used instead of the original values to make the estimate of the parameter of interest and their standard deviation is used to estimate the parameter standard error for computing confidence intervals.

### Bootstrap

Bootstrap is a statistical method for inferences - standard error and bias estimates, confidence intervals, and hypothesis tests - without assumptions such as nomral distributions or equal variances.

### Permutation Tests

A permutation test gives a simple way to compute the sampling distribution for any test statistic, under the strong null hypothesis that a set of genetic variants has absolutely no effect on the outcome. To estimate the sampling distribution of the test statistic we need many samples generated under the strong null hypothesis. If the null hypothesis is true, changing the exposure would have no effect on the outcome. By randomly shuffling the exposures we can make up as many data sets as we like. If the null hypothesis is true the shuffled data sets should look like the real data, otherwise they should look different from the real data. The ranking of the real test statistic among the shuffled test statistics gives a p-value.

## Datasets 

### `World Health` Data {-}

This dataset was downloaded from https://www.gapminder.org/data/ and was curated from WHO, UNICEF Child Info and MRI-HPA Center for Environment & Health. The data was preprocessed to isolate countries that were not missing data across a number of variables. It measures 175 countries (observations) on 16 quantitative variables(refer Table 1.1). The data was collected in 2002.

![alt text](https://github.com/athulsudheesh/Exploratory-Analysis-Using-R/blob/master/Figures/Data.png)

Correlation Plotting is one of the best first step processes in data analysis, for getting a sense of how different variables might be interacting with each other. Figure \@ref(fig:WorldCorPlot) shows the correlation plot of `World Health` data.

```{r WorldCorPlot, fig.align="center", fig.cap="Correlation Plot of World Health Dataset", out.width="60%", echo=FALSE, fig.pos="H"}
# ggcorr is a heatmap plot function based on ggplot2
ggcorr(WorldHealth)
```

![alt text](https://github.com/athulsudheesh/Exploratory-Analysis-Using-R/blob/master/Figures/plot1Heat.png)

For most part of this textbook we will be only using a subsection of this dataset namely `WorldHealth_Risk` with the variables `T.Chole_F`, `T.Chole_M`, `BP_F`, `BP_M`, `BMI_F` and `BMI_M`. 
    
### `Orange Juice Rating` Data {-} 

This is the dataset from an experiment where a set of 10 orange juice were rated on 22 descriptors. The number at the intersection of a row and a column indicates the number of participants who rated the column(variable) relevant for the row(observations). Here the dataset is a contigency table (frequency count) and hence a correlation plot doesn't make much sense. So we do a heatmap of the given table(Ref. Figure \@ref(fig:OrangeJuiceMosaic)). 

```{r OrangeJuiceMosaic, fig.width=10, fig.height=5, fig.align="center", out.width="60%", echo=FALSE, fig.pos="H", message=FALSE, fig.cap="Heatmap of Orange Juice Rating"}
# RColorBrewer helps us to choose color pallettes 
# Rowv, Colv = NA prevents the heatmap from applying clustering 
require(RColorBrewer)
heatmap(as.matrix(Orange_rating), 
        Rowv = NA, 
        Colv = NA, 
        col= colorRampPalette(brewer.pal(5, "Blues"))(256))
```

### `Musical Sorting` Data {-} 

These are data from a sorting experiemnt conducted at The University of Texas at Dallas in Dr. Dowling's lab on 36 clips of classical music, each composed by 1 of 3 composers - Bach, Beethoven and Mozart. The experiment had 37 subjects to do the sorting. 

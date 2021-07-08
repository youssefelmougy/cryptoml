---
layout: default
---

![ProjectProposal](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/projmidpoint.jpg)

## Introduction/Background

Cryptocurrencies, or virtual currencies, are digital means of exchange that use cryptography for security. The word 'crypto' comes from the ancient greek word, 'kryptós', which means hidden or private. A digital currency that is created and used by private individuals or groups has multiple benefits. Currently, cryptocurrencies can be divided into three categories: **Bitcoin**, **altcoins** (anything other than Bitcoin that has value), and **shitcoins** (coins with ultimately no value). 

The term shitcoin refers to a cryptocurrency with little to no value or a digital currency that has no immediate, discernible purpose. Shitcoins are characterized by short-term price increases followed by nosedives caused by investors who want to capitalize on short-term gains. As such, these currencies are considered to be bad investments.


## Problem definition

Shitcoins have their pros and cons, as the purpose is for small investors who like to take risk and flip their money in efforts to make a 100-1000% increase in profit returns. The cons come in where the creators of these shitcoins often rug out the coin, meaning they initially own a very large portion of the coin, wait for a series of investments, then sell immediately causing those new investors to lose most of their money and make no profit. Other ways rugs can be detected are through fraudulent contracts, but we will focus on the large account holders.

Previous models, such as [1], have used linear models, random forests (RFs), and SVMs to forecast prices of the Bitcoin and altcoins but have given little attention to shitcoins.

Our goal is to use predictive analysis techniques to help indicate whether a shitcoin is a potential rug or not, which can be determined by looking at all the recent transaction histories, holders, and contracts of the shitcoin [2][3]. We will look at shitcoins that have already been rugged and ones that are still going strong to help with future coins. This will be valuable to evaluate the risk of investments into these shitcoins.


## Dataset Collection

The data collection process is the most important and crucial part of this project, which is also why it was also the most difficult portion. Our problem relies on a significant amount of data and features to determine whether or not a cryptocurrency is a rug pull or a scam. We ended up using various web scraping tools and tedious data scraping without tools to acquire all the needed data. The data collected includes Bitcoin, altcoins, and coins that have been rug-pulled. Certain cryptocurrencies have limited information simply due to lack of professional development, which itself is a feature we have included (lack of credibility). The other features used include the coin symbol, price, volume,  market cap, coingecko rank, volume to market cap ratio, dominance, number of holders, if it has social media, if it has a whitepaper, if 5 holders own 50% of the supply, if it has an unlocked liquidity pool, and whether it's a scam/rug-pull.

Since data came from differing sources, we ended up having entries with more or less data than needed. After the collection of the data, we had to clean everything and unify the formatting to give us a clean and flushed out dataset. This is discussed in the following section.


## Dataset Processing

Before any feature sensitivity analysis, we first did some data clean up. The following is a snapshot of our full dataset which contains 9143 cryptocurrencies and 14 features:

![tabledata](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/tabledata.png)

The features that were dropped were the coin names and coin symbols. These features were unique to each coin and is irrelevant to our success metrics. Furthermore, all boolean fields were converted to integer values, such that FALSE='0' & TRUE='1'. The following is a snapshot of the cleaned dataset:

![tabledatanormalized](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/tabledatanormalized.png)

As a result of obtaining and scraping data points from several sources, there were some irregularities in the data. To display these anomalies, we displayed the description of the data and obtained the mean, standard deviation, minimum, and maximum of each feature in our dataset. The table below shows the statistics for each of the features. As can be seen, there are several anomalies in the dataset which can be identified. For example, the minimum price is seen to be 0, although this is not mostly accurate. Moreover, the coingecko rank can be seen to be -1 which means the coin is unranked, which can perhaps be displayed differently.

![describeddata](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/describeddata.png)


## Dataset Visualization

It is important to know the distributions of the features in the dataset in order to choose the most appropriate machine learning models to train. After dataset cleaning and processing, the dataset contained 12 unique features that will be used in our models. Feature distribution analysis, class correlation, and feature correlation were done on the dataset to further understand the data points.

The distribution of each feature is a very important aspect in understanding the correlation in the dataset. Below are distribution graphs for each of our 12 features:

![data_initial](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/data_initial.png) 
![whitepaperDist](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/whitepaperDist.png)
![socialDist](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/socialDist.png)
![fiveDist](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/fiveDist.png)
![liquidityDist](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/liquidityDist.png)
![ruggedDist](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/ruggedDist.png)

From the visualizations of feature distribution, we can see that the features are not linearly distributed, hence further distribution and correlation analysis can be greatly important. One of the most useful correlation indicators is the Correlation Matrix, where we can visualize the feature correlation present in the dataset. The following displays the correlation matrix for the dataset:

![confusionmatrix](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/confusionmatrix.png)

The correlation matrix provided very important details as to how the features intertwine together in the dataset. Since our project goal is to identify whether a coin is rugged or not, it is as well important to evaluate the correlation of each feature against the rugged classification feature. The following set of graphs show the class correlation between each of the 11 features with the rugged classification feature:

![pricevol](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/pricevol.png) 
![caprank](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/caprank.png)
![ratiodominance](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/ratiodominance.png)
![holderswhitepaper](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/holderswhitepaper.png)
![mediapercent](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/mediapercent.png)
<p float="left" align="middle">
  <img src="https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/liquid.jpeg" width="400" />
</p>

By looking at the correlation of the 11 features with the rugged feature as well as the correlation matrix, we get a clearer picture of the distributions, correlations, and usefulness of the features in our model to predict if a cryptocurrency is rugged or not. The coingecko_rank, whitepaper, and social_media features are highly positively correlated with rugged. This makes sense since less professional and social presence of a cryptocurrency, the higher the risk of the coin being rugged. On the other hand, the num_holders feature is highly negatively correlated with rugged. This as well makes sense because the higher the number of holders then the lower the risk of the coin being rugged. The other features in our dataset have a slight positive/negative correlation with the rugged feature.

The following is the complete correlation matrix of the dataset, with the feature distribution graphs on the diagonal, after scaling and normalizing the dataset:

![bigmatrix](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/bigmatrix.png)

## Methods and Results

Due to the nature of the two options output (TRUE, FALSE) produced by the algorithm, this problem is a binary classification problem. As part of our unsupervised learning approach, we used PCA (Principal Component Analysis). PCA is used for reducing the amount of dimensions within a dataset, increasing interpretability but at the same time minimizing information loss. We aim to optimize the number of features used in the prediction by using PCA. We use the classic 80/20 training/testing split. The following is the count of data points classified rugged or not, as well as the split of training and testing data:

<p float="left" align="middle">
  <img src="https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/ruggedcount.png" width="400" />
  <img src="https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/trainingsplit.png" width="400" />
</p>

The ML performance metrics that were used to evaluate our model were Accuracy, Balanced-Accuracy, Macro-Precision, Precision, Macro-Recall, Recall, Macro-F1, F1, Macro-ROC, and ROC. After using PCA to train the model for 20 full iterations (each taking ~5sec), the following is the results of the model (arranged in ascending order according to F1-Score):

![resultstable](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/resultstable.png)

Discuss results

The results in more detail:

<p float="left" align="middle">
  <img src="https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/accuracy.png" width="310" />
  <img src="https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/precision.png" width="310" />
  <img src="https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/recall.png" width="310" />
</p>
<p float="left" align="middle">
  <img src="https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/macrof1.png" width="310" />
  <img src="https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/roc.png" width="310" />
</p>






## Discussion

One of the biggest issues we encountered was collecting good consistent data, and combining the data we had without any overlap. The best websites had the least amount of tokens available to us whereas the websites with a surplus of tokens usually lacked information on that token relevant to the needed respective features of the token. We hope to improve our data set and make it more organized for a smoother testing/training process during our final report and analysis.

## References

[1] Sebastião, H., Godinho, P. Forecasting and trading cryptocurrencies with machine learning under changing market conditions. Financ Innov 7, 3 (2021). [Retrieve](https://doi.org/10.1186/s40854-020-00217-x).

[2] Bitcoin, B. (2021). Shitcoin Due Diligence. [Retrieve](http://www.blacksinbitcoin.com/2021/04/shitcoin-due-diligence.html).

[3] Riley, Z. (2021). What are "Shitcoins"? How to find & Avoid in Cryptocurrency Market. [Retrieve](https://the-tech-trend.com/cryptocurrency/what-are-shitcoins-how-to-find-avoid-in-cryptocurrency-market/).

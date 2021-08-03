---
layout: default
---

![ProjectProposal](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/projfinal.jpg)

## Introduction/Background

Cryptocurrencies, or virtual currencies, are digital means of exchange that use cryptography for security. The word 'crypto' comes from the ancient greek word, 'kryptós', which means hidden or private. A digital currency that is created and used by private individuals or groups has multiple benefits. Currently, cryptocurrencies can be divided into three categories: **Bitcoin**, **altcoins** (anything other than Bitcoin that has value), and **shitcoins** (coins with ultimately no value). 

The term shitcoin refers to a cryptocurrency with little to no value or a digital currency that has no immediate, discernible purpose. Shitcoins are characterized by short-term price increases followed by nosedives caused by investors who want to capitalize on short-term gains. As such, these currencies are considered to be bad investments. Shitcoins are also referred to as Memecoins.


## Problem definition

Shitcoins have their pros and cons, as the purpose is for small investors who like to take risk and flip their money in efforts to make a 100-1000% increase in profit returns. The cons come in where the creators of these shitcoins often rug out the coin, meaning they initially own a very large portion of the coin, wait for a series of investments, then sell immediately causing those new investors to lose most of their money and make no profit. Other ways rugs can be detected are through fraudulent contracts, but we will focus on the large account holders.

Previous models, such as [1], have used linear models, random forests (RFs), and SVMs to forecast prices of the Bitcoin and altcoins but have given little attention to shitcoins.

Our goal is to use predictive analysis techniques to help indicate whether a coin is a potential memecoin or not, which can be determined by looking at all the recent transaction histories, holders, and contracts of the coin [2][3]. We will look at coins that have already been classified as memecoins and ones that are still going strong to help with future coins. This will be valuable to evaluate the risk of investments into these shitcoins.


## Dataset Collection

The data collection process is the most important and crucial part of this project, which is also why it was also the most difficult portion. Our problem relies on a significant amount of data and features to determine whether or not a cryptocurrency is a meme coin or a scam. We ended up using various web scraping tools and tedious data scraping without tools to acquire all the needed data. The data collected includes Bitcoin, altcoins, and memecoins. Certain cryptocurrencies have limited information simply due to lack of professional development, which itself is a feature we have included (lack of credibility). The other features used include the coin symbol, price, volume,  market cap, coingecko rank, volume to market cap ratio, dominance, social media coingecko likes, fully diluted valuation, and whether it's a memecoin.

Since data came from differing sources, we ended up having entries with more or less data than needed. After the collection of the data, we had to clean everything and unify the formatting to give us a clean and flushed out dataset. This is discussed in the following section.


## Dataset Processing

Before any feature sensitivity analysis, we first did some data clean up. The following is a snapshot of our full dataset which contains 2395 cryptocurrencies and 11 features:

![tabledatanew](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/tabledatanew.png)

The features that were dropped were the coin names and coin symbols. These features were unique to each coin and is irrelevant to our success metrics. Furthermore, the meme_coin field was converted to integer values, such that NOT-MEME-COIN='-1' & MEME-COIN='1'. The following is a snapshot of the cleaned dataset:

![tabledatanormalizednew](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/tabledatanormalizednew.png)

As a result of obtaining and scraping data points from several sources, there were some irregularities in the data. To display these anomalies, we displayed the description of the data and obtained the mean, standard deviation, minimum, and maximum of each feature in our dataset. The table below shows the statistics for each of the features. As can be seen, there are several anomalies in the dataset which can be identified. For example, the minimum price is seen to be 0, although this is not mostly accurate.

![describeddatanew](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/describeddatanew.png)


## Dataset Visualization

It is important to know the distributions of the features in the dataset in order to choose the most appropriate machine learning models to train. After dataset cleaning and processing, the dataset contained 9 unique features that will be used in our models. Feature distribution analysis, class correlation, and feature correlation were done on the dataset to further understand the data points.

The distribution of each feature is a very important aspect in understanding the correlation in the dataset. Below are distribution graphs for each of our 9 features:

![data_initialnew](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/data_initialnew.png) 
![ruggedDistnew](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/ruggedDistnew.png)

From the visualizations of feature distribution, we can see that the features are not linearly distributed, hence further distribution and correlation analysis can be greatly important. One of the most useful correlation indicators is the Correlation Matrix, where we can visualize the feature correlation present in the dataset. The following displays the correlation matrix for the dataset:

![confusionmatrixnew](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/confusionmatrixnew.png)

The correlation matrix provided very important details as to how the features intertwine together in the dataset. Since our project goal is to identify whether a coin is a memecoin or not, it is as well important to evaluate the correlation of each feature against the meme_coin classification feature. The following set of graphs show the class correlation between each of the 9 features with the meme_coin classification feature:

![pricevolnew](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/pricevolnew.png) 
![capranknew](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/capranknew.png)
![ratiodominancenew](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/ratiodominancenew.png)
![mediapercentnew](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/mediapercentnew.png)


By looking at the correlation of the 9 features with the rugged feature as well as the correlation matrix, we get a clearer picture of the distributions, correlations, and usefulness of the features in our model to predict if a cryptocurrency is memecoin or not. The coingecko_rank and coingecko_likes features are highly positively correlated with memecoin. This makes sense since less professional and social presence of a cryptocurrency, the higher the risk of the coin being a memecoin. On the other hand, the fully_diluted_valuation feature is highly negatively correlated with rugged. This as well makes sense because the higher the diluted valuation then the lower the risk of the coin being a memecoin. The other features in our dataset have a slight positive/negative correlation with the memecoin feature.

The following is the complete correlation matrix of the dataset, with the feature distribution graphs on the diagonal, after scaling and normalizing the dataset:

![bigmatrixnew](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/bigmatrixnew.png)

## Methods and Results

### Principle Component Analysis (PCA)

Due to the nature of the two options output (TRUE, FALSE) produced by the algorithm, this problem is a binary classification problem. As part of our unsupervised learning approach, we used PCA (Principal Component Analysis). PCA is used for reducing the amount of dimensions within a dataset, increasing interpretability but at the same time minimizing information loss. We aim to optimize the number of features used in the prediction by using PCA. We use the classic 80/20 training/testing split. The following is the count of data points classified memecoin or not, as well as the split of training and testing data:

<p float="left" align="middle">
  <img src="https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/ruggedcountnew.png" width="400" />
  <img src="https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/trainingsplitnew.png" width="400" />
</p>

The ML performance metrics that were used to evaluate our model were Accuracy, Balanced-Accuracy, Macro-Precision, Precision, Macro-Recall, Recall, Macro-F1, F1, Macro-ROC, and ROC. After using PCA to train the model for 20 full iterations (each taking ~5sec), the following is the results of the model (arranged in ascending order according to F1-Score):

![resultstable](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/resultstable.png)

These results show high accuracy, through several ML performance metrics, for the PCA model. The model achieved a high of 0.855803 for accuracy, 0.814644 for balanced accuracy, 0.769254 for macro precision, 0.814644 for macro recall, 0.787675 for macro F1, 0.893438 for macro ROC, 0.602815 for precision, 0.747491 for recall, 0.667403 for F1, and 0.893438 for ROC. To have a deeper look at the results of the iterations, below is the ROC graph and Confusion Matrix for iteration 20 (final iteration):

<p float="left" align="middle">
  <img src="https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/iteration20graph.png" width="500" />
</p>
<p float="left" align="middle">
  <img src="https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/iteration20matrixx.png" width="1000" />
</p>

The performance evaluation of PCA using the ML metrics chosen were displayed in the previous table of results. The below graphs display more detail of the performance evaluation of the testing and training sets using each metric:

<p float="left" align="middle">
  <img src="https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/accuracy.png" width="1200" />
</p>
<p float="left" align="middle">
  <img src="https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/precision.png" width="1200" />
</p>
<p float="left" align="middle">
  <img src="https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/recall.png" width="1200" />
</p>
<p float="left" align="middle">
  <img src="https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/macrof1.png" width="1200" />
</p>
<p float="left" align="middle">
  <img src="https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/roc.png" width="1200" />
</p>

### Support Vector Machines (SVM)

## Discussion

One of the biggest issues we encountered was collecting good consistent data, and combining the data we had without any overlap. The best websites had the least amount of tokens available to us whereas the websites with a surplus of tokens usually lacked information on that token relevant to the needed respective features of the token. We hope to improve our data set and make it more organized for a smoother testing/training process during our final report and analysis.

The feature analysis and correlation analysis done show that the coingecko_rank, whitepaper, and social_media features are highly positively correlated with whether the coin is rugged or not, whereas the num_holders feature is highly negatively correlated with whether the coin is rugged or not. Using PCA and an 80/20 split, we found that our model reaches a testing accuracy of 88% with an area under the curve of the ROC graph of 0.917190. We aim to train more unsupervised and supervised machine learning models for the final report and analysis.

## Conclusion

Conclusion text.

## Final Video

<iframe width="800" height="400" src="" title="CryptoML" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## References

[1] Sebastião, H., Godinho, P. Forecasting and trading cryptocurrencies with machine learning under changing market conditions. Financ Innov 7, 3 (2021). [Retrieve](https://doi.org/10.1186/s40854-020-00217-x).

[2] Bitcoin, B. (2021). Shitcoin Due Diligence. [Retrieve](http://www.blacksinbitcoin.com/2021/04/shitcoin-due-diligence.html).

[3] Riley, Z. (2021). What are "Shitcoins"? How to find & Avoid in Cryptocurrency Market. [Retrieve](https://the-tech-trend.com/cryptocurrency/what-are-shitcoins-how-to-find-avoid-in-cryptocurrency-market/).

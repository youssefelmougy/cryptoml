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

![data_initial](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/data_initial.png) | ![whitepaperDist](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/whitepaperDist.png)
![socialDist](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/socialDist.png)
![fiveDist](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/fiveDist.png)
![liquidityDist](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/liquidityDist.png)
![ruggedDist](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/ruggedDist.png)




For data preprocessing, we used PCA (Principal component analysis), which is an unsupervised learning technique used for ​​reducing the amount of dimensions within a dataset, increasing interpretability but at the same time minimizing information loss.


## Methods

Required data, such as who is holding the coin and how much of the coin they hold, will be taken in, and an output of whether the shitcoin is a rug or not will be evaluated. This data can be easily obtained from [Blockchain.com](https://www.blockchain.com/explorer/) and [Etherscan.io](https://etherscan.io).

Due to the nature of the two options output produced by the algorithm, this problem is a binary classification problem. To go about tackling the problem we may use one neural network along with a binary cross entropy loss function, which is standard for binary classification problems. Moreover, relevant and popular algorithms including Logistic Regression, k-Nearest Neighbors, Decision Trees, SVM, and Naive Bayes will be used in the evalutations.

As the semester progresses, these techniques are subject to change as we will be learning a variety of other predictive analysis techniques that could possibly do better than our initial potential solutions.

## Results and Discussion

One of the biggest issues we encountered was collecting good consistent data, and combining the data we had without any overlap. The best websites had the least amount of tokens available to us whereas the websites with a surplus of tokens usually lacked information on that token relevant to the needed respective features of the token. We hope to improve our data set and make it more organized for a smoother testing/training process during our final report and analysis.

## References

[1] Sebastião, H., Godinho, P. Forecasting and trading cryptocurrencies with machine learning under changing market conditions. Financ Innov 7, 3 (2021). [Retrieve](https://doi.org/10.1186/s40854-020-00217-x).

[2] Bitcoin, B. (2021). Shitcoin Due Diligence. [Retrieve](http://www.blacksinbitcoin.com/2021/04/shitcoin-due-diligence.html).

[3] Riley, Z. (2021). What are "Shitcoins"? How to find & Avoid in Cryptocurrency Market. [Retrieve](https://the-tech-trend.com/cryptocurrency/what-are-shitcoins-how-to-find-avoid-in-cryptocurrency-market/).

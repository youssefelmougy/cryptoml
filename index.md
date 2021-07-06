---
layout: default
---

![ProjectProposal](https://raw.githubusercontent.com/youssefelmougy/cryptoml/master/projmidpoint.jpg)

## Introduction/Background

Cryptocurrencies, or virtual currencies, are digital means of exchange that use cryptography for security. The word 'crypto' comes from the ancient greek word, 'kryptós', which means hidden or private. A digital currency that is created and used by private individuals or groups has multiple benefits. Currently, cryptocurrencies can be divided into three categories: **Bitcoin**, **altcoins** (anything other than Bitcoin that has value), and **shitcoins** (coins with ultimately no value). 

The term shitcoin refers to a cryptocurrency with little to no value or a digital currency that has no immediate, discernible purpose. Shitcoins are characterized by short-term price increases followed by nosedives caused by investors who want to capitalize on short-term gains. As such, these currencies are considered to be bad investments.


## Problem definition

Shitcoins have their pros and cons, as the purpose is for small investors who like to take risk and flip their money in efforts to make a 100-1000% increase in profit returns. The cons come in where the creators of these shitcoins often rug out the coin, meaning they initially own a very large portion of the coin, wait for a series of investments, then sell immediately causing those new investors to lose most of their money and make no profit. Other ways rugs can be detected are through fraudulent contracts, but we will focus on the large account holders. 

Previous models, such as [1], have used linear models, random forests (RFs), and SVMs to forcast prices of the Bitcoin and altcoins but have given little attention to shitcoins.

Our goal is to use predictive analysis techniques to help indicate whether a shitcoin is a potential rug or not, which can be determined by looking at all the recent transaction histories, holders, and contracts of the shitcoin [2][3]. We will look at shitcoins that have already been rugged and ones that are still going strong to help with future coins. This will be valuable to evaluate the risk of investments into these shitcoins.

## Methods

Required data, such as who is holding the coin and how much of the coin they hold, will be taken in, and an output of whether the shitcoin is a rug or not will be evaluated. This data can be easily obtained from [Blockchain.com](https://www.blockchain.com/explorer/) and [Etherscan.io](https://etherscan.io).

Due to the nature of the two options output produced by the algorithm, this problem is a binary classification problem. To go about tackling the problem we may use one neural network along with a binary cross entropy loss function, which is standard for binary classification problems. Moreover, relevant and popular algorithms including Logistic Regression, k-Nearest Neighbors, Decision Trees, SVM, and Naive Bayes will be used in the evalutations.

As the semester progresses, these techniques are subject to change as we will be learning a variety of other predictive analysis techniques that could possibly do better than our initial potential solutions.

## Potential results and Discussion

With the use of accurate predictive analysis techniques, we hope that our model can provide traders and cryptocurrency holders an accurate prediction of the next possible shitcoin to aid in providing the best investment opportunities.

## References

[1] Sebastião, H., Godinho, P. Forecasting and trading cryptocurrencies with machine learning under changing market conditions. Financ Innov 7, 3 (2021). [Retrieve](https://doi.org/10.1186/s40854-020-00217-x).

[2] Bitcoin, B. (2021). Shitcoin Due Diligence. [Retrieve](http://www.blacksinbitcoin.com/2021/04/shitcoin-due-diligence.html).

[3] Riley, Z. (2021). What are "Shitcoins"? How to find & Avoid in Cryptocurrency Market. [Retrieve](https://the-tech-trend.com/cryptocurrency/what-are-shitcoins-how-to-find-avoid-in-cryptocurrency-market/).

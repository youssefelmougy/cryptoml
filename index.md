---
layout: default
---

## Introduction/Background

Cryptocurrencies, or virtual currencies, are digital means of exchange that use cryptography for security. The word 'crypto' comes from the ancient greek word, 'kryptós', which means hidden or private. A digital currency that is created and used by private individuals or groups has multiple benefits. Currently, crypto currencies can be divided into three categories: **Bitcoins**, **altcoins** (anything other than bitcoin that has value), and **shitcoins** (coins with ultimately no value). 

The term shitcoin refers to a cryptocurrency with little to no value or a digital currency that has no immediate, discernible purpose. Shitcoins are characterized by short-term price increases followed by nosedives caused by investors who want to capitalize on short-term gains. As such, these currencies are considered to be bad investments.


## Problem definition

Shitcoins have their pros and cons, as the purpose is for small investors who like to take risk and flip their money in efforts to make a 100-1000% increase in profit returns. The cons come in where the creators of these shitcoins often rug out the coin, meaning they initially own a very large portion of the coin, wait for a series of investments, then sell immediately causing those new investors to lose most of their money and make no profit. Other ways rugs can be detected are through fraudulent contracts, but we will focus on the large account holders. 

Our goal is to use predictive analysis techniques to help indicate whether a shitcoin is a potential rug or not, which can be determined by looking at all the recent transaction histories, holders, and contracts of the shitcoin. We will look at shitcoins that have either already been rugged, or are still going strong to help with future coins. 

## Methods

We hope to create a program that will take in the required data (who is holding, and how much they hold), and give us an output as to whether the shitcoin is a rug or not. This means that the problem is a binary classification problem since the output is only one of two options. To go about tackling the problem we may use one neural network along with a binary cross entropy loss function, which is standard for binary classification problems. As the semester progresses, these techniques are subject to change as we will be learning a variety of other predictive analysis techniques that could possibly do better than our initial potential solution.

## Potential results and Discussion

## References

Sebastião, H., Godinho, P. Forecasting and trading cryptocurrencies with machine learning under changing market conditions. Financ Innov 7, 3 (2021). <href=https://doi.org/10.1186/s40854-020-00217-x>

Bitcoin, B. (2021). Shitcoin Due Diligence. Retrieved from <href=http://www.blacksinbitcoin.com/2021/04/shitcoin-due-diligence.html>

Riley, Z. (2021). What are "Shitcoins"? How to find & Avoid in Cryptocurrency Market. Retrieved from <href=https://the-tech-trend.com/cryptocurrency/what-are-shitcoins-how-to-find-avoid-in-cryptocurrency-market/>

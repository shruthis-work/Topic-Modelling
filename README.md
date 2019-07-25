### Web Scraping and Topic Modelling  
Author: Shruthi


Problem Statement: Model a binary classifier to execute classification

Modus Operandi Overview:
Posts are collected from two sub-reddits: Sports and Politics. This is done by sending a request to reddit's api. Since, the api only allows 25 posts per request a for loop is run to collect over 1000 posts. Once 1000 posts are collected for each of the sub-reddits, all the text in every post is going to be count vectorized which will then be the input into the classifiers. A Naive-Bayes classifier is used to train the model and a logistic regression classifier is used to compare the performance.

Process Highlights:

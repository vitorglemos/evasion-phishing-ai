# Machine Learning Security Evasion Competition 2022

## Introduction

The Machine Learning Security Evasion Competition (MLSEC) 2022 took place from August 12th to September 23th 2022 and was organized by Adversa AI, CUJO AI, and Robust Intelligence. I will explain here what I use as a method to bypass the machine learning models produced for this competition.

## About Anti-Phishing Evasion challenge

The goal was to manipulate the HTML code in the teen phishing websites to try to evade a total of 8 machine learning models. For this challenge, it is considered success in the evasion when this probability web page is lower than 0.1. Besides, the web pages need to be rendered in the same way, the screenshot hash must be the same on both pages. 

## Solution

The solution is simple, but several tests are needed during this process. Here, I choose several samples web pages for a brief tests in the machine learning models. It always important check as the ML classifiers change the probability when we manipule the HTML elements.
- **First**, I inserted several benign code snippets inside the pages to check how the models behaved. Some ML classifiers had their probabilities reduced, while others didn't change anything.
- **Second**, It is possible to create dynamic pages, that is, to modify them through a script during  loading the web page on browser. That worked for me, but not all pages behaved the same.
- **Third**, I created javascript code so that some snippets were uncommented during the loading on internet browser, while the malicious code was inserted instead. This ensured that the top 4 models were bypassed.

The models that were bypassed had their detection probability always between 0.002 and 0.008. Unfortunately, some this ML classifiers even had very high odds, like somewhere around 0.68 and 0.92. I created generic tags so that javascript could identify where the modifications would occur, in this case, the parts that should be replaced were inside a tag called `<here></here>`. I believe that other tags can have better results but I didn't have time to test them. In addition, it is worth remembering that the phishing code was commented, a javascript inside the head was responsible for modifying it. This modification would happen when loading the page, through the statement `<body onload="myFunction()">`. Some `<meta>` tags were also inserted in the page's `<head>`, in some cases this helped. Unfortunately, some pages had their screenshot hash changed during page load. This ended up invalidating some results.

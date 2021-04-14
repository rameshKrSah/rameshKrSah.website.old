---
title: "A gudie for Exploratory Data Analysis (EDA)."
date: 2021-04-14
comments: True
mathjax: True
tags: [machine learning, data analysis]
categories:
  - machine learning
  - data analysis
---


Data is like food for machine learning, and any machine learning project should always begin with exploratory data analysis(EDA). EDA allows us (the practitioner) to understand the data and make informed decisions about different downstream components of the machine learning pipeline. Below I have listed down some guidelines for completing a good EDA. 

1. Always know the source of your data. Where the data came from, what does it mean, and what it should be telling you, and so on. Ask as many questions as possible.
2. Calculate descriptive statistics such as mean, median, mode, standard deviation, min, max, quartiles, skewness, and others that you need.  Understand these numbers. 
3. Analyze relationships between variables. Use correlation matrix, scatter plots between two variables, histogram of a single variable, box-plot of a single variable, and other types as needed.
4. Clean the data if needed by identifying and removing redundant variables, outliers, and invalid entries.
5. Perform statistical tests.
6. Finally, always take extensive notes of your process and make your EDA reproducible.

Finally, some tools that I use for EDA:
1. [pandas-profiling](https://github.com/pandas-profiling/pandas-profiling)
2. [dataprep](https://github.com/sfu-db/dataprep)

Enjoy your EDA :sunglasses:
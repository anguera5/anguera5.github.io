---
title: Bayesian Inference for sludge biodegradation experiments
description: Bayesian analysis on truncated biodegradation data with high variance
categories: [Bayesian Statistics]
tags: [Bayesian, Statistics, Environmental Chemistry, Exploratory Data Analysis, Rate Constants]
image:
  path: /assets/img/sludge_biodegradation/sludge_post.jpeg
---

Modelling of biodegration halflifes is an endpoint of increasing interest in current research lines. Such models are generally underperforming due to the sensitivity of the endpoint prediction to experimental conditions, the high variability of the experimental conditions (microbial community composition, their activness, pH, temperature, bioreactor type, etc.) and due to this, the lack of reproducibility of experiments. Due to this one can find cases where the halflifes of a same compound can be below the LOQ, above the LOQ and between them (as we will see later in this post).

In this post, I will follow the guidelines provided by [Hafner (et. al.)](https://pubs.acs.org/doi/10.1021/acs.estlett.3c00526) to find good estimates for halflife distributions that are truncated. Those can later be used in modelling pipelines to estimate the output and provide the uncertainty on the prediction.

The dataset that will be used in this post is [EAWAG-SLUDGE](https://envipath.org/package/7932e576-03c7-4106-819d-fe80dc605b8a) extracted on 16th of December 2024 using [enviPath-python](https://github.com/enviPath/enviPath-python) and [PEPPER](https://github.com/FennerLabs/pepper), both of them projects on which I contributed to develop.

To reduce the amount of requests performed to [enviPath](https://envipath.org), I provide the dataset (here on referred as `data_sludge.tsv`) as a static .tsv file [here](https://docs.google.com/spreadsheets/d/1tzNPpsOJlhmBjJcWgQ5vcqnM8JEzKr8Bt-zh9Ro4pmo/edit?gid=1454238983#gid=1454238983). The main relevant columns of the dataset are:
* asda
* asdasd


```python
data = pd.read_csv("data_sludge.tsv", sep="\t")
sorting_column = "halflife_log"
data = data.sort_values(sorting_column, ascending=True).reset_index(drop=True)
data.head()
```



![Box plot for biodegradation of compounds on sludge experiments](/assets/img/sludge_biodegradation/image.png "Box plot for biodegradation of compounds on sludge experiments")

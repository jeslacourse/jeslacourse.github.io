---
title: "Feature Choice in Classification of Kernels"
header:
  teaser: assets/images/2020-05-17/figure-markdown_github/unnamed-chunk-3-2.png
permalink: /feature-choice/
categories: 
  - Rstats
  - Statistics
  - Visualizations
  - Classification
tags: 
  - dataviz
  - rstats
  - ggplot
  - classification
excerpt: "Feature selection is just as important as hyperparameter choice, yet many classifiers cherry-pick features without much empirical basis. While hyperparameters are easier to tweak, we must account for the impact of boosting these hyperparameters and the risk and impact of overfit."
---

# Feature Choice in Classification of Wheat Kernels

<center><b> Abstract</b></center>

<center><p> Frequently, k-nearest neighbors classification is applied with features chosen arbitrarily, while `k` is adjusted to improve the accuracy of the model. For this experiment, `k` is fixed. Using correlations with the strict acknowledgement that all features are continuous, a feature set with high correlation within itself is selection. Visual analysis using density and scatter plots show that these features also share distinct distributions and thusly make great candidates for k-nearest neighbors clustering. The four features return a well classified set, while tweaking the set by removing features with less distinctive groupings returns very high accuracy with an increased risk of overfit. Both features sets perform better than using all features with the same fixed hyperparameter. 
    </p></center>


## Introduction 

With a small database, it's easy enough to fit all features to a model, or select all quantitative data, then frequently modify the hyperparameters to boost up the accuracy. But what information are we losing in the process? 

Feature selection is just as important as hyperparameter choice, yet many classifiers cherry-pick features without much thought for their empirical basis. The focus of this experiment will look at the impact of feature selection on wheat kernel classification. Given the distinctive groupings, that occur within many features, k-nearest neighbors will be used for classification. While the hyperparameter, `k` will be easier to tweak, we must account for the impact of boosting hyperparameters on the risk of overfit. 

## Data Information and Attributes

The dataset is comprised of 210 sample kernels with three varieties of wheat, Kama, Rosa, and
Canadian.

Each wheat kernel is assigned seven attributes: grain area, perimeter, compactness, length and width
of kernel, asymmetry coefficient and length of kernel groove.

Each measurement is given in with millimeter-based units.

### Sourcing Data

Wheat seed data provided by UCI’s Center for Machine Learning and Intelligent Systems.

<center><a href="https://archive.ics.uci.edu/ml/datasets/seeds#" class="uri">https://archive.ics.uci.edu/ml/datasets/seeds#</a></center>

### Data Information and Attributes

There are 210 sample kernels of three varieties of wheat, Kama, Rosa, and Canadian.

Each wheat kernel is assigned seven attributes: grain area, perimeter, compactness, length and width of kernel, asymmetry coefficient and length of kernel groove.

Each measurement is given in millimeters.

## Data Structure and Cleaning

*Table 1: Raw Data Input*

<table>
<thead>
<tr>
<th style="text-align:right;">
V1
</th>
<th style="text-align:right;">
V2
</th>
<th style="text-align:right;">
V3
</th>
<th style="text-align:right;">
V4
</th>
<th style="text-align:right;">
V5
</th>
<th style="text-align:right;">
V6
</th>
<th style="text-align:right;">
V7
</th>
<th style="text-align:right;">
V8
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:right;">
15.26
</td>
<td style="text-align:right;">
14.84
</td>
<td style="text-align:right;">
0.8710
</td>
<td style="text-align:right;">
5.763
</td>
<td style="text-align:right;">
3.312
</td>
<td style="text-align:right;">
2.221
</td>
<td style="text-align:right;">
5.220
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:right;">
14.88
</td>
<td style="text-align:right;">
14.57
</td>
<td style="text-align:right;">
0.8811
</td>
<td style="text-align:right;">
5.554
</td>
<td style="text-align:right;">
3.333
</td>
<td style="text-align:right;">
1.018
</td>
<td style="text-align:right;">
4.956
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:right;">
14.29
</td>
<td style="text-align:right;">
14.09
</td>
<td style="text-align:right;">
0.9050
</td>
<td style="text-align:right;">
5.291
</td>
<td style="text-align:right;">
3.337
</td>
<td style="text-align:right;">
2.699
</td>
<td style="text-align:right;">
4.825
</td>
<td style="text-align:right;">
1
</td>
</tr>
</tbody>
</table>



Our source data is a text file with headless, tab-separated data (Table 1). 

To improve readability and analysis, each feature is assigned a descriptive name. The response variable, ‘wheat‘, is factored into a categorical variable with levels "Kama", "Rosa", and "Canadian" replacing numeric variables 1,2, and 3, respectively (Table 2).



*Table 2: Legible Dataframe*
<table>
<thead>
<tr>
<th style="text-align:right;">
area
</th>
<th style="text-align:right;">
perimeter
</th>
<th style="text-align:right;">
compactness
</th>
<th style="text-align:right;">
length
</th>
<th style="text-align:right;">
width
</th>
<th style="text-align:right;">
asymmetry
</th>
<th style="text-align:right;">
groove
</th>
<th style="text-align:left;">
wheat
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:right;">
15.26
</td>
<td style="text-align:right;">
14.84
</td>
<td style="text-align:right;">
0.8710
</td>
<td style="text-align:right;">
5.763
</td>
<td style="text-align:right;">
3.312
</td>
<td style="text-align:right;">
2.221
</td>
<td style="text-align:right;">
5.220
</td>
<td style="text-align:left;">
Kama
</td>
</tr>
<tr>
<td style="text-align:right;">
14.88
</td>
<td style="text-align:right;">
14.57
</td>
<td style="text-align:right;">
0.8811
</td>
<td style="text-align:right;">
5.554
</td>
<td style="text-align:right;">
3.333
</td>
<td style="text-align:right;">
1.018
</td>
<td style="text-align:right;">
4.956
</td>
<td style="text-align:left;">
Kama
</td>
</tr>
<tr>
<td style="text-align:right;">
14.29
</td>
<td style="text-align:right;">
14.09
</td>
<td style="text-align:right;">
0.9050
</td>
<td style="text-align:right;">
5.291
</td>
<td style="text-align:right;">
3.337
</td>
<td style="text-align:right;">
2.699
</td>
<td style="text-align:right;">
4.825
</td>
<td style="text-align:left;">
Kama
</td>
</tr>
</table>




### Missing Values 

![](Seeds_Report_files/figure-markdown_github/unnamed-chunk-3-1.png)

*Figure 1. Outlier and Quantile Analysis by Feature *



Upon initial inspection (Fig 1), the data appears to be complete and contains no missing values. Two
or three Kama kernel appears to fall outside the normal distribution in several categorical factors, but
they are not far enough away from the rest of the level to warrant removal. With no major outliers
and no missing values, data cleaning was a relatively simple process involving only the adjustment of
variate names and factor levels.

## Visualizations and Analysis

The wheats create distinctive groups when classified by area and perimeter. Length and width also
provide significant groupings, while compactness, asymmetry, and groove have substantial overlap
between the wheat variants (Fig 2). When classifying by wheat groove, in particular, the wheats fall
into two distinctive groups, with Canadian and Kama wheats sharing nearly identical distributions.
The groove on Rosa wheat is significantly longer and has almost no overlap with the opposing groups.



![](assets/images/2020-05-17/figure-markdown_github/unnamed-chunk-3-2.png)

*Figure 2: Histograms with Density Overlays by Feature*



### Correlation and Associativity

With no categorical data, we can create a table of comparative values between all of our variates (Fig 3). Area is highly correlated with the perimeter (r = 0.994), length (r=0.950), and width (r=0.971) of a given kernel. These values are highly correlated with each other as well. Another notable factor, the kernel groove, is also highly correlated with the four noted factors. 

![](assets/images/2020-05-17/figure-markdown_github/unnamed-chunk-4-1.png)

*Figure 3: Correlation and Associativity *


## Classification

Given the distinctions in distribution, as well as the high correlation between the given factors,
k-nearest neighbors with factors area, perimeter, length, and width as the classifying features. All
features are given in millimeters and will not be standardized.

For all experiments, `k=5`.

### K-Nearest Neighbors with Selected Features

*Table 3: Confusion Matrix: Classification with Area, Perimeter, Height and Width*

<table>
<thead>
<tr>
<th style="text-align:left;">
    Pred/Acc 
</th>
<th style="text-align:right;">
Kama
</th>
<th style="text-align:right;">
Rosa
</th>
<th style="text-align:right;">
Canadian
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Kama
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:left;">
Rosa
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
14
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:left;">
Canadian
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
13
</td>
</tr>
</tbody>
</table>



The initial classification did well, 90.47% (Table 3). Two issues stand out: (a) Kama kernels are misclassified relatively frequently, and (b) other kernels are misclassified as Kama kernels relatively frequently. These results are relatively intuitive, as the peak of the distribution for Kama kernels falls between Rosa and Canadian kernels for the factors area, perimeter, length, and width.

The Kama distribution tails for length and width, as noted before overlap significantly. There is very little to no misclassification between Rosa and Canadian wheat kernels as the factor distributions and means are consistently more distant from each other when compared to the difference in means with Kama kernels for either wheat.

### K-Nearest Neighbors with Minimal Features

*Table 4: Confusion Matrix: Classification with Area and Perimeter*

<table>
<thead>
<tr>
<th style="text-align:left;">
Pred/Acc    
</th>
<th style="text-align:right;">
Kama
</th>
<th style="text-align:right;">
Rosa
</th>
<th style="text-align:right;">
Canadian
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Kama
</td>
<td style="text-align:right;">
13
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:left;">
Rosa
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
14
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:left;">
Canadian
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
13
</td>
</tr>
</tbody>
</table>



Removing height and width as factors increased the accuracy of our knn prediction to 95.24%, but that number on it’s own raises some suspicion (Table 4). The highly accurate result is likely more accidental, but it does show us that these features with more overlap in the tails do have a significant impact on the number of misclassified values.

### K-Nearest Neighbors with All Features

*Table 5: Confusion Matrix: Classification with All Features*

<table>
<thead>
<tr>
<th style="text-align:left;">
Pred/Acc
</th>
<th style="text-align:right;">
Kama
</th>
<th style="text-align:right;">
Rosa
</th>
<th style="text-align:right;">
Canadian
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Kama
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:left;">
Rosa
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
14
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:left;">
Canadian
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
13
</td>
</tr>
</tbody>
</table>


As a control, we can train with all seven features. Given the significant overlap in compactness, asymmetry, and groove, the accuracy is expected to be lower than when strictly training with area and perimeter. The results are as expected, 90.47% (Table 5).

### Conclusion
The experiment shows the value of data exploration when choosing features. The experiment also
shows that increasing the number of features doesn’t necessarily improve the accuracy of testing.
Taking care to minimize inadvertent p-hacking should always be at the forefront of a researcher’s
mind when building experiments.

With that said, the analysis is based off of a single fixed training and test sample. Improvements can
be made to the experiment by replicating the analysis with cross validation, bootstrapping, or k-folds to ensure repeatability.

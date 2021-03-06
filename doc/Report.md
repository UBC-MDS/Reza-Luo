DSCI 522 Project: Wine Quality Predictors
================

### Team Members

-   Reza Bagheri (github ID: reza-bagheri)
-   Luo Yang (github ID: lyiris22)

### Introduction

In this project, a wine quality dataset set will be used to study the effect of different parameters on the red and white wine quality. The main question is that what are the top three predictors for the red and white wine quality? This is a predictive question which can be important for the wine industry. The wine quality is determined by human tasters which need a certain amount of experience to do this task. If we can predict the wine quality using some chemical predictors that can be easily measured in the lab, we can automate and accelerate the process of wine certification. It can also help the wine industry to determine which factors can improve the wine quality. It is also intersting to know if red and white wines share the same top predictors or not? So this study uses a machine learning method to predict the wine quality (a target variable) based on the wine features. A tree classifier has been used for this purpose, and the top three predictors were determined using this classifier.

### Dataset

The wine quality data was obtained from UCI Machine Learning Repository [\[1\]](#1), however, the original data was prepared by P. Cortez [\[2\]](#2). The wine data is divided into to datasets for the red and white variants of the Portuguese "Vinho Verde" wine. The most common physicochemical (features) and sensory (target) variables are available in these two datasets, and they have 12 with 1599 red and 4898 white examples totally [\[3\]](#3). The features include fixed acidity, volatile acidity, citric acid, residual sugar, chlorides, free sulfur dioxide, total sulfur dioxide, density, pH, sulfates and alcohol. The target variable is the wine quality which is defined as a numerical score between 0 (the worst wine) and 10 (the best wine). However, in these datasets there is no observation with a quality of lower than 3 and higher than 9. Table 1 shows the summary of feature statistics for each dataset.

<br>
<p style="text-align:center">
<b>Table 1. The summary of feature statistics for each dataset</b>
</p>
<center>
<table>
<tr>
    <th rowspan="2">Feature</th>
    <th colspan="3">Red wine</th> 
    <th colspan="3">White wine</th>

</tr>
<tr>
    <td>Min</td>
    <td>Mean</td>
    <td>Max</td>
    <td>Min</td>
    <td>Mean</td>
    <td>Max</td>

</tr>
<tr>
    <td>Fixed acidity</td>
    <td>4.60</td>
     <td>8.32</td>

<td>
15.90
</td>
    <td>3.80</td>
    <td>6.85</td>
    <td>14.20</td>

</tr>
<tr>
    <td>Volatile acidity</td>
    <td>0.12</td>
    <td>0.53</td>
    <td>1.58</td>
    <td>0.08</td>
    <td>0.28</td>
    <td>1.10</td>

</tr>
<tr>
    <td>Citric acid</td>
    <td>0.00</td>
    <td>0.27</td>
    <td>1.00</td>
    <td>0.00</td>
    <td>0.33</td>
    <td>1.66</td>

</tr>
<tr>
    <td>Residual sugar</td>
    <td>0.90</td>
    <td>2.54</td>
    <td>15.50</td>
    <td>0.60</td>
    <td>6.39</td>
    <td>65.80</td>

</tr>
<tr>
    <td>Chlorides</td>
    <td>0.01</td>
    <td>0.09</td>
    <td>0.61</td>
    <td>0.01</td>
    <td>0.05</td>
     <td>0.35</td>

</tr>
<tr>
    <td>Free sulfur dioxid</td>
    <td>1.00</td>
    <td>15.87</td>
    <td>72.00</td>
    <td>2.00</td>
     <td>35.31</td>
    <td>289.00</td>

</tr>
<tr>
    <td>Total sulfur dioxid</td>
    <td>6.00</td>
    <td>46.47</td>
    <td>289.00</td>
    <td>9.0</td>
     <td>138.4</td>
    <td>440.0</td>

</tr>
<tr>
    <td>Density</td>
    <td>0.990</td>
     <td>0.997</td>
    <td>1.004</td>
    <td>0.987</td>
     <td>0.994</td>
    <td>1.039</td>

</tr>
<tr>
    <td>pH</td>
    <td>2.74</td>
    <td>3.31</td>
    <td>4.01</td>
    <td>2.72</td>
    <td>3.19</td>
    <td>3.82</td>

</tr>
<tr>
    <td>Sulphates</td>
    <td>0.33</td>
     <td>0.66</td>
     <td>2.00</td>
    <td>0.22</td>
    <td>0.49</td>
    <td>1.08</td>

</tr>
<tr>
    <td>Alcohol</td>
    <td>8.40</td>
    <td>10.42</td>
    <td>289.00</td>
    <td>8.00</td>
    <td>10.51</td>
    <td>14.20</td>

</tr>
<tr>
    <td>Quality</td>
    <td>3.00</td>
    <td>5.64</td>
    <td>8.00</td>
    <td>3.00</td>
    <td>5.88</td>
    <td>9.00</td>

</tr>
</table>
</center>
</br>

### Data cleaning

The datasets have been checked to make sure that no missing element is present. The classes in the datasets for both red and white wine are not balanced. That is because there are much more normal wines than good or bad ones. Figure 1 shows the bar plot of the number of observations for different wine qualities in the red wine dataset. Figure 2 shows a similar bar plot for the white wine dataset (the number of observations for each quality have been given on top of the bars). <br>

<br>
<center>
<img src="../results/hist_raw_red.png" width="350px"/>
</center>
<p style="text-align:center">
Figure 1. The bar plot of the number of observations for different wine qualities in the red wine dataset
</p>
<br>
<center>
<img src="../results/hist_raw_white.png" width="350px"/>
</center>
<p style="text-align:center">
Figure 2. The bar plot of the number of observations for different wine qualities in the white wine dataset
</p>
<br>

These figures clearly show that both datasets are imbalanced. In addition, the wine quality is a numerical variable and it is more meaningful to be converted into a categorical variable before starting the decision tree analysis.

To overcome these problems, some of the values if the quality variables have combined together and the resulting values have been turned into categorical values. To goal was to combine the qualities with a very low number of observations. Two different patterns have been tried for this purpose. Figures 3 and 4 show how this transformation has been done for the first pattern. <br>

<center>
<img src="../results/old_hist_clean_red.png" width="350px"/>
</center>
<p style="text-align:center">
Figure 3. The bar plot of the number of observations for different wine qualities in the cleaned red wine dataset (pattern 1)
</p>
<br>
<center>
<img src="../results/old_hist_clean_white.png" width="350px"/>
</center>
<p style="text-align:center">
Figure 4. The bar plot of the number of observations for different wine qualities in the cleaned white wine dataset (pattern 1)
</p>
<br> In this pattern, the observations of poor wine qualities of 3 and 4 have been combined into a category of "low" quality to increase the number of observations. Similarly, any good quality equal to or higher than 7 has been converted into a category of "high" quality. The middle quality values of 5 and 6 have been converted into categories of "med-low" and "med-high" respectively. Figures 5 and 6 show how this transformation has been done in the second pattern. <br> <br>
<center>
<img src="../results/hist_clean_red.png" width="350px"/>
</center>
<p style="text-align:center">
Figure 5. The bar plot of the number of observations for different wine qualities in the cleaned red wine dataset (pattern 2)
</p>
<br>
<center>
<img src="../results/hist_clean_white.png" width="350px"/>
</center>
<p style="text-align:center">
Figure 6. The bar plot of the number of observations for different wine qualities in the cleaned white wine dataset (pattern 2)
</p>
<br> <br> In this pattern, the observations of poor wine with qualities equal or less than 4 have been combined into a category of "low" quality, and any good quality equal or higher than 7 has been converted into a category of "high" quality. The middle quality values of 5 and 6 have been combined into a "med" category. As the figures show these transformations can relieve the imbalance of the observations, but cannot completely remove it.

### Exploratory data analysis

The effect of each wine feature on the quality has been studied using exploratory data visualization of the cleaned datasets. Figure 7 shows the violin and jitter plots of each feature versus the red wine quality in one of the cleaned data (pattern 2) as an example. <br> <br> <br>
<center>
<img src="../results/violin_red.png" width="750px"/>
</center>
<p style="text-align:center">
<b>Figure 7. The violin and jitter plot of each feature versus red wine quality with error bars (pattern 2)</b>
</p>
<br>

The graphs for the other datasets have been given in Appendix 1. The results suggest that alcohol is probably the most important predictor for both red and white wines in pattern 1. In pattern 2, alcohol looks like an important feature, however, for low and med values the error bars are overlapped for both red and white wines. On the other hand, sulphates looks a little better than alcohol for the red wine.

### Data analysis: Decision tree classifier

In this study, the three top features that affect the wine quality for both the red and white wines should be determined, and a decision tree classifier will be used for this purpose. A decision tree is a classifier that uses a tree-like model for the decisions and their possible outcomes. What makes it useful for this study is that it chooses the attributes one at a time, according to some criteria, and it tries to find the best attribute each time, so it allows to rank the predictive features and choose the best ones [\[4\]](#4). Since this study only looks for the top three predictors, the tree depth will be set to 3, and this hyperparameter will not be subjected to optimization. However, a 10-fold cross validation with a 90:10 ratio (train: validation) was used to calculate the accuracy of the classifier on the validation sets. Both pattern 1 and 2 for the red and white wine have analyzed using the decision tree classifier. In addition, the scikit learn class\_weight attribute has been used to balance the observations. It can automatically adjust some weights inversely proportional to class frequencies in the input data [\[5\]](#5). The analysis has been done with and without balancing the datasets.

Figures 8 and 9 show the decision tree for both red and white wines in pattern 2 with balancing. The decision tree for the other dataset are given in Appendix 2. <br><br><br>
<center>
<img src="../results/tree_red_3_bal.png" width="750px"/>
</center>
<p style="text-align:center">
<b>Figure 8. The decision tree for the red wine (pattern 2) with balancing</b>
</p>
<br>
<center>
<img src="../results/tree_white_3_bal.png" width="750px"/>
</center>
<p style="text-align:center">
<b>Figure 9. The decision tree for the white wine (pattern 2) with balancing</b>
</p>
<br> <br>

### Results and discussion

Table 2 summarizes all the results of the previous figures. It shows the top three predictors for each tree. To determine the top three predictors, the 'tree.feature\_importances\_' of DecisionTreeClassifier in scikit learn has been used. It returns the Gini importance of that feature. In addition, it shows the average accuracy of a 10-fold cross validation with 90:10 ratio for train: validation sets.

<br>
<p style="text-align:center">
<b>Table 2. A summary of the decision tree analysis</b>
</p>
<center>
<table style="width:39%;">
<colgroup>
<col width="5%" />
<col width="5%" />
<col width="5%" />
<col width="5%" />
<col width="5%" />
<col width="5%" />
<col width="5%" />
</colgroup>
<thead>
<tr class="header">
<th>Cleaning pattern</th>
<th>Wine type</th>
<th>Balancing used in analysis</th>
<th>Accuracy</th>
<th>First top predictor</th>
<th>Second top predictor</th>
<th>Third top predictor</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>1</td>
<td>Red</td>
<td>No</td>
<td>54%</td>
<td>Alcohol</td>
<td>Sulphates</td>
<td>Total sulfur dioxide</td>
</tr>
<tr class="even">
<td>1</td>
<td>Red</td>
<td>Yes</td>
<td>47%</td>
<td>Alcohol</td>
<td>Sulphates</td>
<td>Volatile acidity</td>
</tr>
<tr class="odd">
<td>1</td>
<td>White</td>
<td>No</td>
<td>53%</td>
<td>Alcohol</td>
<td>Volatile acidity</td>
<td>Free sulfur dioxide</td>
</tr>
<tr class="even">
<td>1</td>
<td>White</td>
<td>Yes</td>
<td>46%</td>
<td>Alcohol</td>
<td>Free sulfur dioxide</td>
<td>Volatile acidity</td>
</tr>
<tr class="odd">
<td>2</td>
<td>Red</td>
<td>No</td>
<td>84%</td>
<td>Alcohol</td>
<td>Volatile acidity</td>
<td>Sulphates</td>
</tr>
<tr class="even">
<td>2</td>
<td>Red</td>
<td>Yes</td>
<td>53%</td>
<td>Sulphates</td>
<td>Alcohol</td>
<td>Volatile acidity</td>
</tr>
<tr class="odd">
<td>2</td>
<td>White</td>
<td>No</td>
<td>75%</td>
<td>Alcohol</td>
<td>Volatile acidity</td>
<td>pH</td>
</tr>
<tr class="even">
<td>2</td>
<td>White</td>
<td>Yes</td>
<td>57%</td>
<td>Alcohol</td>
<td>Free sulfur dioxide</td>
<td>Volatile acidity</td>
</tr>
</tbody>
</table>

</center>
</br>

The first thing that can be concluded from this table is that pattern 2 gives higher accuracies than pattern 1. This can be attributed to the way that the features combined. The quality of a wine is assessed and scored by a human taster. In pattern 2 we have low, med and high quality wines. However, in pattern 1 we have two large classes of average wines with the scores of 5 and 6. Distinguishing between a very good wine, a very bad wine, and an average wine is much easier than distinguishing between two average wines, and it is likely that these human tasters do not have strict rules to distinguish between these two scores (5 and 6) and simply pick a number for that. So it can be very difficult for the learning algorithm to classify these two classes and it will affect the accuracy. So it is evident that pattern 2 is a much better way to clean the dataset and it is not a good idea to use a learning algorithm to classify the middle classes based on the scores of a human expert.

It is important to note that only for one case (Pattern 1, red wine with balancing), there was a mismatch between the tree structure and the reported important features. In this case, the alcohol has the highest Gini impact reported by scikit learn, however in the tree structure (Figure A.5 in the Appendix 2), sulphates sits at the root of the tree. The reason is that in the tree structure alcohol is used three times to split the nodes, so its total impact is higher than sulphates. In addition, it seems that when balancing is done, both patterns 1 and 2 give the same order of predictors for the red and wine wines.

It seems that balancing the data set in scikit-learn decreases the accuracy. This can be attributed to the fact that without proper weighting of the less abundant target categories, the algorithm can get a higher score with labeling most of the examples with more abundant target categories and ignoring the less abundant ones at a lower cost. Finally, we pick the three top predictors from the decision analysis of pattern 2 with balancing. For red wines, they are sulphates, alcohol, and volatile acidity respectively. For white wines, they are alcohol, free sulfur dioxide, and volatile acidity. These results are consistent with the exploratory data analysis results mentioned before. So Alcohol and volatile acidity are the common important features for both red and white wines.

### Conclusions

In this study a decision tree classifier was used to determine the top three predictors for the red and wine quality in a public dataset. The data cleaning was showed to be an important step which affects the later results. Having a balanced dataset is also important. This study was carried out on a dataset which was not balanced and we used a cleaning pattern and Scikit learn balancing feature to improve it. The results were consistent with an initial exploratory data analysis. Sulphates and alcohol were the most important predictors for red and white wine respectively, and alcohol and volatile acidity were found to be the common important features for both red and white wines.

### Future work

This study has used the decision tree classifier to find the top three predictors. We know that ensemble methods like random forest can improve the results, so it can be used in this study to improve the accuracy. In addition some other learning algorithms like support vector machines or neural networks can be tried too, and these methods can be compared together to see whether changing the algorithm changes the top predictors and which one gives the highest accuracies?

### References

<a name="1"></a> \[1\] <a href="https://archive.ics.uci.edu/ml/datasets/Wine+Quality">Wine Quality Data Set</a>, UCI Machine Learning Repository.</br> <a name="2"></a>\[2\] P. Cortez, University of Minho, Guimares, Portugal (<http://www3.dsi.uminho.pt/pcortez>).</br> <a name="3"></a> \[3\] P. Cortez at al., "Modeling wine preferences by data mining from physicochemical properties", *Decision Support Systems* 47 (**2009**) 547-533.</br> <a name="4"></a> \[4\] M. Kubat, An Introduction to Machine Learning, Springer International Publishing, **2015**.<br/> <a name="5"></a> \[5\] <a href="https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html">Scikit-learn documentation.</a><br/>

### Appendix 1: Exploratory data analysis

The effect of each wine feature on the quality has been studied using exploratory data visualization of the cleaned datasets. Figure A.1 shows the violin and jitter plots of each feature versus red wine quality in the cleaned dataset with pattern 1. The error bars have been shown too. Figure A.2 shows a similar plot for the white wine in this cleaned dataset (pattern 1). Figure A.3 shows the same plots for the white wine in the cleaned dataset with pattern 2. </br> <br> <br>
<center>
<img src="../results/old_violin_red.png" width="750px"/>
</center>
<p style="text-align:center">
<b>Figure A.1. The violin and jitter plot of each feature versus red wine quality with error bars (pattern 1)</b>
</p>
<br>
<center>
<img src="../results/old_violin_white.png" width="750px"/>
</center>
<p style="text-align:center">
<b>Figure A.2. The violin and jitter plot of each feature versus white wine quality with error bars (pattern 1)</b>
</p>
<br>
<center>
<img src="../results/violin_white.png" width="750px"/>
</center>
<p style="text-align:center">
<b>Figure A.3. The violin and jitter plot of each feature versus white wine quality with error bars (pattern 2)</b>
</p>
<br>

These figures suggest that alcohol is probably the most important predictor for both red and white wines since the difference between the alcohol value of different qualities is larger than its standard error for both red and white wines.

### Appendix 2: Decision trees

The decision trees for all the remaining dataset are given here. Figures A.4 and A.5 show the decision tree for both red and white wines in pattern 1 without balancing. <br><br><br>
<center>
<img src="../results/tree_red_4.png" width="750px"/>
</center>
<p style="text-align:center">
<b>Figure A.4. The decision tree for the red wine (pattern 1) without balancing</b>
</p>
<br>
<center>
<img src="../results/tree_white_4.png" width="750px"/>
</center>
<p style="text-align:center">
<b>Figure A.5. The decision tree for the white wine (pattern 1) without balancing</b>
</p>
<br> Figures A.6 and A.7 show the decision tree for both red and white wines in pattern 1 with balancing.<br></br> <br>
<center>
<img src="../results/tree_red_4_bal.png" width="750px"/>
</center>
<p style="text-align:center">
<b>Figure A.6. The decision tree for the red wine (pattern 1) with balancing</b>
</p>
<br>
<center>
<img src="../results/tree_white_4_bal.png" width="750px"/>
</center>
<p style="text-align:center">
<b>Figure A.7. The decision tree for the white wine (pattern 1) with balancing</b>
</p>
<br> Figures A.8 and A.9 show the decision tree for both red and white wines in pattern 2 without balancing.<br></br> <br>
<center>
<img src="../results/tree_red_3.png" width="750px"/>
</center>
<p style="text-align:center">
<b>Figure A.8 The decision tree for the red wine (pattern 2) without balancing</b>
</p>
<br>
<center>
<img src="../results/tree_white_3.png" width="750px"/>
</center>
<p style="text-align:center">
<b>Figure A.9 The decision tree for the white wine (pattern 2) without balancing</b>
</p>
<br>

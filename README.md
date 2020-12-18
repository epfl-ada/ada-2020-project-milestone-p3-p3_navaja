# Title: Benchmarking predictive frameworks of civil war onset

## 1. Abstract

In the wake of the Second World War, the world has seen a steady increase in intrastate conflicts [1], often with dire consequences for the affected countries. Recent advancements in data science have catalyzed the development of predictive models for various problems, including political conflicts such as civil wars [2] [3] [4]. In 2016, Muchlinski et al. [5] significantly improved previous models of civil war onset. In this project, we first aimed at benchmarking these results against other common machine learning algorithms, namely neural networks and gradient boosted trees. As the geographical area was an important feature in the abovementioned study ("Western Europe and US Dummy" in Fig. 4 [5]), we examined whether predictions differ when training separate models for different geographical areas. Finally, we explored whether civil war events can be forecast as time series instead of simple regression points, e.g., using time-delayed features.

## 2. Research questions
1. How does the Random Forests model from Muchlinski _et al._ [[5]](#5) compare with neural networks and gradient boosted trees in terms of predictive accuracy and feature importance?
2. Can spatial separation of civil war data (i.e., by continent or subregion) help improve predictive accuracy of civil war events?
3. While most analyses have considered civil war onset prediction as regression problems, can these events be forecast as time series? In other words, can we predict civil war onset at a year Y in a given country C given data from previous years {Y-1, Y-2, ...}?

## 3. Proposed dataset
 * "SambnisImp.csv" from the Muchlinski _et al._ [[5]](#5) paper was the only dataset used in this project. This dataset corresponds to the Civil War Data (CWD) from 1945 to 2000 [[4]](#4). It includes 88 features for 7140 “country-years”. The response is a binary variable indicating whether a civil war was ongoing for a given country-year. 
 
## 4. Methods
 ### 4.1. Comparing machine learning algorithms for civil war onset classification
 #### 4.1.1. Data collection
We used the same features than Muchlinski _et al._ [[5]](#5), minus the features related to geographical area separation (e.g.,  "Western Europe and US Dummy") (82 features in total). Indeed, we investigated the effect of data aggregation by continent/subregion in a subsequent analysis (cf. **4.2**). To ensure a meaningful comparison, the same training and testing sets were used to assess each tested algorithm.

 #### 4.1.2 Models
The Random Forests model from the paper were compared with two common machine learning algorithms: multi-layer perceptrons (MLPs) and XGBoost, a type of gradient boosted decision tree (GBDT) [[6]](#6). Machine learning library scikit-learn [[7]](#7) was used to implement these algorithms.

 #### 4.1.3. Training
Parameter hyperoptimization was performed using grid search combined with 10-fold cross-validation. To compensate the heavy imbalance in civil war events, downsampling was implemented to balance the classes in the training set.

 #### 4.1.4. Metrics
In the same vein as Muchlinski _et al._ [[5]](#5), ROC-AUC and F1 scores were used to evaluate model performance. PR-AUC was also added as an evaluation metric. While ROC-AUC is commonly used for binary classification, F1 and PR-AUC are more robust to data imbalance.

 ### 4.2. Effect of spatial data separation
Following the importance of the "Western Europe and US Dummy" variable in Muchlinski _et al._ [[5]](#5), we aggregated the data by specific geographical areas, and explored whether predictive accuracy differed when fitting XGBoost separately on each group. The same training paradigm and metrics as in **4.1** were used. Subsequently, we analyzed permutation importance to see whether different variables could better explain civil war events in different geographical areas.

 ### 4.3. Predicting civil war onset as time series forecasting
In this section, we researched whether civil war onset could be forecast given past data using simple time forecasting models. In particular, we fitted XGBoost (and LSTMs, see Appendix in Notebook) on time-delayed features, that is taking features from previous years to predict civil war events at a given year.
 
## 5. Proposed timeline
 ### 5.1. Week 1: Implementation of steps 4.1, 4.2
Downloading the data, implementing the ML models, wrangling/cleaning the dataset, preparing visualizations, analyzing feature importance for each model in methods 4.1 and 4.2.
 ### 5.2. Week 2: Finish 4.1-4.2, Implementation of steps 4.3
Finish methods 4.1 and 4.2 if not done.
Wrangling/cleaning the dataset, implementing and testing recurrent/autoregressive models, and preparing visualizations for task 4.3
 ### 5.3 Week 3: Wrapping up
Finishing the analysis, writing the data story, cleaning code and figures, preparing the video.

## 6. Organization plan within the team 
* Neil will share his code used in Milestone 2 for downloading the data and implementing the Random Forests model of Muchlinski _et al._ [[5]](#5).
* In Week 1, Julie will handle data wrangling for tasks 4.1 et 4.2. Neil will implement the cross-validated grid search function(s) and adapt the machine learning algorithms of interest to the problem. After that, Victor will work on feature importance analysis. In the meantime, Julie will focus on research for time series forecasting.
* In Week 2, the group will implement one or more solutions for time series forecasting, discuss on the obtained results and finish the steps in Week 1 if not done.
* In Week 3, Neil will clean the code, while Victor prepares the data story and Julie focuses on preparing the video summary.

## 7. Data story

The data story is available <a href="https://neclow.github.io/ada-2020-project-milestone-p3-p3_navaja/">here</a>

## References
<a id="1">[1]</a> Pettersson, T., & Öberg, M. (2020). Organized violence, 1989–2019. _Journal of peace research_, 57(4), 597-613.

<a id="2">[2]</a> Fearon, J. D., & Laitin, D. D. (2003). Ethnicity, insurgency, and civil war. _American political science review_, 75-90.

<a id="3">[3]</a> Collier, P., & Hoeffler, A. (2004). Greed and grievance in civil war. _Oxford economic papers_, 56(4), 563-595.

<a id="4">[4]</a> Hegre, H., & Sambanis, N. (2006). Sensitivity analysis of empirical results on civil war onset. _Journal of conflict resolution_, 50(4), 508-535.

<a id="5">[5]</a> Muchlinski, D., Siroky, D., He, J., & Kocher, M. (2016). Comparing random forest with logistic regression for predicting class-imbalanced civil war onset data. _Political Analysis_, 87-103.

<a id="6">[6]</a> Chen, T., & Guestrin, C. (2016, August). Xgboost: A scalable tree boosting system. In _Proceedings of the 22nd acm sigkdd international conference on knowledge discovery and data mining_ (pp. 785-794).

<a id="7">[7]</a> Pedregosa, F., Varoquaux, G., Gramfort, A., Michel, V., Thirion, B., Grisel, O., ... & Vanderplas, J. (2011). Scikit-learn: Machine learning in Python. _Journal of machine learning research_, 12, 2825-2830.

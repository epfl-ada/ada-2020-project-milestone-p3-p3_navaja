# Title: Benchmarking predictive frameworks of civil war onset

## 1. Abstract

In the wake of the Second World War, the world has seen a steady increase in intrastate conflicts [[1]](#1), often with dire consequences for the affected countries. Recent advancements in data science have catalyzed the development of predictive models for various problems, including political conflicts such as civil wars [[2]](#2) [[3]](#3) [[4]](#4). In 2016, Muchlinski _et al._ [[5]](#5) significantly improved previous models of civil war onset. In this project, we first aim at benchmarking these results against other common machine learning algorithms, namely neural networks and gradient boosted trees. As the geographical area was an important feature in the abovementioned study ("Western Europe and US Dummy" in Fig. 4 [[5]](#5)), we will examine whether prediction differs when training separate models for each continent (or subregions). Finally, we will explore whether civil war events can be forecast as time series instead of simple regression points, e.g., using autoregressive models.

## 2. Research questions
1. How does the Random Forests model from Muchlinski _et al._ [[5]](#5) compare with neural networks and gradient boosted trees in terms of predictive accuracy?
2. Can spatial separation of civil war data (i.e., by continent or subregion) help improve predictive accuracy of civil war events?
3. While most analyses have considered civil war onset prediction as regression problems, can these events be forecast as time series? In other words, can we predict civil war onset at a year Y in a given country C given data from previous years {Y-1, Y-2, ...}?

## 3. Proposed dataset
 * "SambnisImp.csv" from the Muchlinski _et al._ [[5]](#5) paper will be the only dataset used in this project. This dataset corresponds to the Civil War Data (CWD) from 1945 to 2000 [[4]](#4). The response is a binary variable indicating whether a civil war was ongoing for a given country-year. 
 
## 4. Methods
 ### 4.1. Comparing machine learning algorithms for civil war onset classification.
 #### 4.1.1. Data collection
We will use the same features than Muchlinski _et al._ [[5]](#5), minus the the features related to geographical area separation (e.g.,  "Western Europe and US Dummy"). Indeed, we will investigate whether the effect of data aggregation by continent or subregion in a subsequent analysis (cf. **4.2**). To ensure a meaningful comparison, the same training and testing sets will be used to assess each tested algorithm.

 #### 4.1.2 Models
The Random Forests model from the paper will be compared with two common machine learning algorithms: multi-layer perceptrons (a "simple" type of neural networks), and gradient boosted decision trees (GBDTs). Whereas multi-layer perceptrons will be implemented using machine learning library PyTorch [[6]](#6) as both more intuitive and flexible than the neural network functions of scikit-learn [[7]](#7), XGBoost will be used as a fast and robust implementation of GDBTs [[8]](#8). 

 #### 4.1.3. Training
Parameter hyperoptimization will be performed using grid search combined with 10-fold cross-validation. To compensate the heavy imbalance in civil war events, downsampling will be implemented to balance the classes in the training set. Random Forests and XGBoost will be trained using their standard loss functions, while binary cross-entropy will serve as a loss function for neural networks.

 #### 4.1.4. Metrics
In the same vein as Muchlinski _et al._ [[5]](#5), both ROC-AUC and F1 scores will be used to evaluate model performance. These metrics are commonly used for binary classification of imbalanced data.

 ### 4.2. Effect of spatial data separation
Following the importance of the "Western Europe and US Dummy" variable in Muchlinski _et al._ [[5]](#5), we will aggregate the data by geographical area (either continent or subregion, to be determined), and see whether predictive accuracy differs when fitting the models separately on each group. The same training paradigm and metrics as in **4.1** will be used. We will then analyze feature importance to see whether different variables can explain better civil war events in different geographical areas.

 ### 4.3. Predicting civil war onset as time series forecasting
In this section, we will consider that each country is assigned to a time series of civil war/peace events, and see whether civil war events could be forecasted given past data using simple time forecasting models (e.g., autogressors (AR) or ARIMA). 
 
## 5. Proposed timeline
 ### 5.1. Week 1: Implementation of steps 4.1, 4.2
Downloading the data, implementing the ML models, wrangling/cleaning the dataset, preparing visualizations, analyzing feature importance for each model in methods 4.1 and 4.2.
 ### 5.2. Week 2: Finish 4.1-4.2, Implementation of steps 4.3
Finish methods 4.1 and 4.2 if not done.
Wrangling/cleaning the dataset, implementing and testing recurrent/autoregressive models, and preparing visualizations for task 4.3
 ### 5.3 Week 3: Wrapping up
Finishing the analysis, writing the data story, cleaning code and figures, preparing video.

## 6. Organization witing the team 
* Neil will share his code used in Milestone 2 for downloading the data and implementing the Random Forests model of Muchlinski _et al._ [[5]](#5).
* In Week 1, Julie will handle data wrangling for tasks 4.1 et 4.2. Neil will implement the cross-validated grid search function(s) and adapt the machine learning algorithms of interest to the problem. After that, Victor will work on feature importance analysis. In the meantime, Julie will focus on research for time series forecasting.
* In Week 2, the group will implement one or more solutions for time series forecasting, discuss on the obtained results and finish the steps in Week 1 if not done.
* In Week 3, Neil will clean the code, while Victor prepares the data story and Julie focuses on preparing the video summary.

## References
<a id="1">[1]</a> Pettersson, Therése, and Magnus Öberg. "Organized violence, 1989–2019." _Journal of peace research_ 57, no. 4 (2020): 597-613.

<a id="2">[2]</a> Fearon, James D., and David D. Laitin. "Ethnicity, insurgency, and civil war." _American political science review_ (2003): 75-90.

<a id="3">[3]</a> Collier, Paul, and Anke Hoeffler. "Greed and grievance in civil war." _Oxford economic papers_ 56, no. 4 (2004): 563-595.

<a id="4">[4]</a> Hegre, Håvard, and Nicholas Sambanis. "Sensitivity analysis of empirical results on civil war onset." _Journal of conflict resolution_ 50, no. 4 (2006): 508-535.

<a id="5">[5]</a> Muchlinski, David, David Siroky, Jingrui He, and Matthew Kocher. "Comparing random forest with logistic regression for predicting class-imbalanced civil war onset data." _Political Analysis_ (2016): 87-103.

<a id="6">[6]</a> Paszke, Adam, Sam Gross, Francisco Massa, Adam Lerer, James Bradbury, Gregory Chanan, Trevor Killeen et al. "Pytorch: An imperative style, high-performance deep learning library." In Advances in neural information processing systems, pp. 8026-8037. 2019.

<a id="7">[7]</a> Pedregosa, Fabian, Gaël Varoquaux, Alexandre Gramfort, Vincent Michel, Bertrand Thirion, Olivier Grisel, Mathieu Blondel et al. "Scikit-learn: Machine learning in Python." the Journal of machine Learning research 12 (2011): 2825-2830.

<a id="8">[8]</a> Chen, Tianqi, and Carlos Guestrin. "Xgboost: A scalable tree boosting system." In Proceedings of the 22nd acm sigkdd international conference on knowledge discovery and data mining, pp. 785-794. 2016.

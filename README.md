# Title

## Abstract

In the wake of the Second World War, the world has seen a steady increase in intrastate conflicts [[1]](#1), often with dire consequences for the affected countries. Recent advancements in data science have catalyzed the development of predictive models for various problems, including political conflicts such as civil wars [[2]](#2) [[3]](#3) [[4]](#4). In 2016, Muchlinski _et al._ [[5]](#5) significantly improved previous models of civil war onset. In this project, we first aim at benchmarking these results against other common machine learning algorithms, namely neural networks and gradient boosted trees. As the geographical area was an important feature in the abovementioned study ("Western Europe and US Dummy" in Fig. 4 [[5]](#5)), we will examine whether prediction differs when training separate models for each continent (or subregions). Finally, we will explore whether civil war events can be forecast as time series instead of simple regression points, e.g., using autoregressive models.

## Research questions
1. How does the Random Forests model from Muchlinski _et al._ [[5]](#5) compare with neural networks and gradient boosted trees in terms of predictive accuracy?
2. Can spatial separation of civil war data (i.e., by continent or subregion) help improve predictive accuracy of civil war events?
3. While most analyses have considered civil war onset prediction as regression problems, can these events be forecast as time series? In other words, can we predict civil war onset at a year Y in a given country C given data from previous years {Y-1, Y-2, ...}?

## Proposed dataset
 * "SambnisImp.csv" from the Muchlinski _et al._ [[5]](#5) paper will be the only dataset used in this project. This dataset corresponds to the Civil War Data (CWD) from 1945 to 2000 [[4]](#4). The response is a binary variable indicating whether a civil war was ongoing for a given country-year. 
 
## Methods
 1. Comparing machine learning algorithms for civil war onset classification.
We will examine the predictive accuracy of multi-layer perceptrons (MLPs) (a "simple" type of neural networks) and gradient boosted decision trees (GBDTs) against the results obtained Muchlinski _et al._ [[5]](#5) using Random Forests. To ensure a meaningful comparison, we will use same training and testing sets for each algorithm. Among the variables used by Muchlinski _et al._ [[5]](#5), the features related to geographical area separation will be discarded 

## References
<a id="1">[1]</a> Pettersson, Therése, and Magnus Öberg. "Organized violence, 1989–2019." _Journal of peace research_ 57, no. 4 (2020): 597-613.
<a id="2">[2]</a> Fearon, James D., and David D. Laitin. "Ethnicity, insurgency, and civil war." _American political science review_ (2003): 75-90.
<a id="3">[3]</a> Collier, Paul, and Anke Hoeffler. "Greed and grievance in civil war." _Oxford economic papers_ 56, no. 4 (2004): 563-595.
<a id="4">[4]</a> Hegre, Håvard, and Nicholas Sambanis. "Sensitivity analysis of empirical results on civil war onset." _Journal of conflict resolution_ 50, no. 4 (2006): 508-535.
<a id="5">[5]</a> Muchlinski, David, David Siroky, Jingrui He, and Matthew Kocher. "Comparing random forest with logistic regression for predicting class-imbalanced civil war onset data." _Political Analysis_ (2016): 87-103.





Improve the methods and/or the analyses done in the paper:
* Neural networks
* XGBoost, LightGBM (Extreme gradient boosting methods)
* Clustering (t-SNE)?

Propose and analyze a different dataset with which you could answer similar questions as the replicated paper:
* Something with American election?
* Predict other wars...

Propose answering additional research questions with the dataset used in the paper:
* Could take countries that had civil wars --> try to predict if it will happen the next year given data on previous years (RNNs)? 

Do better on oob data 9/20 for random forest
Pb use model with interpretable parametres otherwise useless

Part 2: 

Dependance of the predictive parameters on the area (continent/aire culturelles)
Voir plus refined separé les données par continent
Interpreter les differences de parametres

Part 1: 

Train best ever predictor:
* Neural networks
* XGBoost, LightGBM (Extreme gradient boosting methods)
* Clustering (t-SNE)?

* Could take countries that had civil wars --> try to predict if it will happen the next year given data on previous years (RNNs)? 
      * Use the probability of CW in the previous year as a feature.
      
Part 3:

Exploration of time dependency ?

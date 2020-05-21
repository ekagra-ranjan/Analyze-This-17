<h1 align="center">
Analyze-This-17
</h1>

<h2 align="center">
(American Express Flagship Data Science Competition)
</h2>

<p align="center">
  <a href="https://github.com/ekagra-ranjan/Analyze-This-17/raw/master/Method_Presentation_Top_Floors_IITGuwahati.pptx"><img src="http://img.shields.io/badge/Slides-ppt-orange.svg"></a>
  <a href="https://github.com/ekagra-ranjan/Analyze-This-17/raw/master/Method_Presentation_Top_Floors_IITGuwahati.pptx"><img src="http://img.shields.io/badge/Result-Outstanding Performer-blue.svg"></a>
  <a href="https://github.com/ekagra-ranjan/Analyze-This-17/raw/master/Method_Presentation_Top_Floors_IITGuwahati.pptx"><img src="http://img.shields.io/badge/Team Name-Top Floors-purple.svg"></a>
</p>

<p align="center">
Declared <b> 'Outstanding Performer' </b> by American Express.
</p>

<br>
<br>

## Estimation Technique Used
We used a Gradient Boosting Machine – implementing the **xgboost** Python library.
 
A Gradient Boosting Machine iteratively trains decision trees, and ensembles them (essentially combining their predictions), all while minimizing the error function (in our case, the ‘softmax’ function) at each step. 
The xgboost library provides an out-of-the-box implementation of a GBM.It is a form of extreme Gradient Boosting. 

We used **transformation (log or cuberoot)** to make the distribution Gaussian as well as normalized 21 feature columns, whiich we got  after removing, and combining some of the input data – explained in the following slides.

## Strategy to decide final list
The output of the xgboost classifier is an array of 4 probabilities – corresponding to how likely the model predicts “None”, “Supp”, “Elite”, “Credit” respectively, for each entry.

We removed the “None” probability from the entire array of predictions (called y_final, corresponding to the input data stored in X_final) and sorted y_final according to the maximum of the remaining three probabilities, in each entry.

This ensured that the entries for which the xgboost classifier was most sure about were at the top of the calling list.
We predicted the maximum of the remaining three classes as the output for each entry.


## Details of each Variable used in the logic/mode/strategy
* We removed outliers from dataset based on very high values of Electronics, Travel, Household, Car, Retail, Total Expenditures. We also removed samples which had unusually small income.
* We combined the quarterly Electronics, Travel, Household, Car, Retail, Total Expenditures into yearly features, by summing them. 
* We imputed the values of Income.
* We dropped the columns Industry Code because there were too many missing values, throwing our classifier off. Card Product Type had all entries as ‘Charge’, meaning it had no significance altogether, and was dropped as well. Customer Spending Capacity was having ~24000 values missing out of ~40000, so we didn’t bother to impute this variable using its mean , median or mode beacuse it had too much variability and it would lead to bad estimation by comution 24k values based only on 16k values. So we dropped this column too.
* Indicators of extension/acceptance for supplementary, elite and credit cards were combined into  three features, one for each card type as, (number of times customer accepted)/(number of times an offer was extended), beacuse this would us an intuition that whats the probability that the customer will accept a specific card if we      offer them.We also took the reciprocal of the values obtained by this ratio, if the ratio was greater than 1(because accepted cannot be more than extended) because we thought that this could be because of some practical reasons like typing mistake.

* Variables leaving out mvar3, mvar10, mvar41-51 were transformed using log while mvar3 was transformed using cuberoot function.Each column was subtracted by its mean and divided by its standard deviation. These were done to get a normailsed Gaussian distribution os the features for better optimisation and better classification.

* The xgboost classifier worked best with the following parameters:
    * Objective: softprob (similar to the softmax function)
    * Learning Rate: 0.1
    * Number of Estimators: 1000
    * Min Child Weight =5
    * Maximum Depth (for each tree): 5, sub_sample=0.8 ,col_pos_weight=0.8


<br>
<br>

## Github repos of similar Data Science Competitions:

* [Analyze-This-18](https://github.com/ekagra-ranjan/Analyze-This-18)
* [GS-Quantify-17](https://github.com/ekagra-ranjan/GS-Quantify-17/)
* [Inter-IIT-Techmeet-17](https://github.com/ekagra-ranjan/Optimal-Bidding/)
* [awesome-undergrad-hackathons](https://github.com/ekagra-ranjan/awesome-undergrad-hackathons)

<p align="center">
	Please star the repo if you found the materials in the repo useful :)
</p>

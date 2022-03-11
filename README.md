# NBA MVP 2021 prediction

## Data collection

The data is extracted from the nba_api (https://github.com/swar/nba_api). This API client allows access to all the NBA’s data included in the official stats.nba.com website.
To achieve the goal of our analysis, different information from different datasets has been used. The four datasets that have been selected to perform the study are:

* commonallplayers which contains the list of all NBA players and the period
when they have played;
* playercareerstats which records all the data (such as points scored, number of matches, minutes played, field goal made and free throw made) of all players for each season;
* playerawards which lists the awards that each player has won in each season;
* teamyearbyyearstats which contains, for each regular season, both the Eastern and the Western conference standings.

## Proposed solution

To predict our response variable, three binary classifiers have been implemented using the sklearn library: a logistic regression using LogisticRegression(), a Support Vector Machine using SVC() and a Random Forest using RandomForestClassifier(). To find the best parameters for each classifier, leave-one-out cross-validations have been used as auto-tuning through the function RandomizedSearchCV(). To evaluate the performance of the cross-validated models scoring=’balanced accuracy’ has been selected. The parameters that have been
auto-tuned for the three models are:
 
* Logistic regression: the inverse of regularisation strength and the algorithm used to solve the optimization problem of the regression. As regularisation term we have chosen the L2 term since the feature selection was already part of the data preparation;
* Support vector machine: the inverse of regularisation strength and the type of kernel function;
* Random forest: the criterion to measure the quality of a split, the maximum depth of the trees and the number of trees in the forest. As number of independent variables selected in the learning phase by each tree, we decided to use the square root of the total number of features since we are facing a classification problem.

Once we have found the parameters for each classifier, the three models
have been trained. In the learning phase we have set, in all the three mod-
els, class weight=”balanced” that automatically adjust weights inversely propor-
tional to class frequencies in the training set, due to the fact that the database
is still unbalanced.

## Evaluation of the performances

The test set has been used to evaluate the performances of the three classifiers and thus to understand which one is the most appropriate to predict the MVP. Once the predictions on the test set were performed, the balanced accuracy of the three different models have been calculated. This measurement of quality has been selected since it is suitable and appropriate for unbalanced datasets. Indeed, contrary to the conventional accuracy that counts the correct classifications out of the total number of predictions, the balanced accuracy is the average between sensitivity and specificity [4]. The balanced accuracy for the three models are:

* Logistic regression: 0.999, with sensitivity = 1 and specificity = 0.997;
* Support vector machine: 0.9, with sensitivity = 0.8 and specificity = 0.998;
* Random forest: 0.799, with sensitivity = 0.6 and specificity = 0.999.

The logistic regression is thus the most appropriate model for our study, since it has the highest balanced accuracy. By looking at the confusion matrices of the three classifiers, we reach the same conclusion. Indeed, the logistic regression has very few false positives (players that have been classified as winners but that in reality they haven’t won) and it is the only classifier that has zero false negatives (players that have been classified as non winners but that in reality they have won the MVP).

# Prediction of season 2021-2021

To complete our study, we have used the trained logistic regression to predict the MVP of season 2020-2021. The first graph shows the ten players who have the highest probability of winning the award. Nicola Jokic is the favourite with 99.5% probability of winning (he is the actual MVP of season 2020-2021).

![alt text](https://github.com/thomasverardo/NBA_MVP_2022_prediction/blob/main/Code/plot/log_reg_test30.png)

The second graph shows the different impact that the features had in the prediction of the response variable. The features with the highest influence are: ’Final confederation rank’, ’Field goal percentage’, ’Assists’ and ’Personal fouls’.

![alt text](https://github.com/thomasverardo/NBA_MVP_2022_prediction/blob/main/Code/plot/log_reg_importance.png)



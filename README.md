# LaSerenaDataScienceSchool
Repository for my final project at the la serena data science school in Chile.

[Launch notebook :notebook:](https://nbviewer.jupyter.org/github/josiahcoad/LaSerenaDataScienceSchool/blob/master/ExoplanetAnalysis.ipynb)
## Topics Covered
 - Classification: Random forest, Adaboost, etc.
 - tSNE
 - GridSearch
 - PCA (kPCA)
 - Feature Importance

## Outline
0. Define the goal and our product:
        a. classify unclassified planets from the kepler database with defendable metrics
        b. give future astro-surveys suggestions on the most important features to collect to detect planets
1. Import the data and get a summary
2. Start with ~150 features, ~10,000 samples and class: FALSE_POSITIVE, CANDIDATE or POSITIVE. Note: FALSE_POSITIVE means that the object was a canidate and was found to not be a planet. So this label is essentially the same as NEGATIVE and will be called that to remove confusion.
3. Our domain experts hand select possibly relevant features, reducing our features to  about ~100.
4. Start by imputing the missing data with medians. *\[future work would be to choose a better imputation\]*
5. Throw all features in a random forest tree with default parameters, test with cross validation, get decent metric scores and rank features by importance.
6. Get the VIF scores for the features and remove features one-by-one that have a very high VIF/correlation score (like hand-done PCA)
7. Rerun random forest with only one feature, the most important and test with cross validation. Do this over and over for the top 40 features. Plot the metrics and look for an elbow where we stop getting better results by including more features. For us, that was around 20 features.
8. Look closely at these top 20 features, make sure that the unlabeled data follows a similar distribution to our labeled data (ideally bimodal) [Note: at this point, we found our greatest feature only existed as a good indicator for our labeled data. Go back to 6 without this feature.]
9. Compare the performance on several classifiers with default parameters on our 20 features. Find that adaboost does the best, but random forest also does very well.
10. [Maybe] Perform GridSearch to find the best hyper parameters for our classifier with the completeness as our optimization metric.
11. Tune the probability prediction of our model.
12. Run t-SNE to make sure that our unlabeled data is evenly distributed in the same space as our labeled data (not its own cluster).
13. Make predictions 

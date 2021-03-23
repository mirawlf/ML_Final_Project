# ML_Final_Project

https://www.youtube.com/watch?v=rzGb40PUVX8 - step by step instruction of installation and configuration Blender for Brain Painter with further pictures obtaining.

**baseline.ipynb** - the script performs the algorithms from baseline section of our project - KNN, Logistic regression, Random Forest, XGBoost.

1. as an input it takes `st_features_without_nans_and_y_with_nans.csv`. Drops the NaN values. Then remaps the Y to 0 and 1 depending on the classification mode (AD vs NL, AD vs MCI, AD+MCI vs NL).

2. then it performs KNN, Logistic Regression, RF using `cross_val_score` and gets the cross\_val score (metric is `roc_auc`).

3. then it performs KNN, Logistic Regression, RF using `fit` and gets the train and test scores.

4. then it perofrms XGBoost using `roc_auc` metric (test data is 30 percent).

5. the notebook outputs `feature_importance.png` and scores tables.

**make\_latent\_space.ipynb** - the script performs the translation from the original space of the features to the latent space.

1. as an input it takes `distributions/pdf.pickle' file that stores the features' original distributions.

2. then it draws the graphs of the distributions into `plots/` folder.

3. then it creates the distributions in the latent space.

4. then it creates the graphs of the latent space distributions into `latent/` folder.

5. finally, it creates the `latent_unified_with_nan_y_with_nan_age.csv` that stores the dataset in the latent space.

**Conditional\_Model.ipynb** - makes prediction based on fixed features in the latent space.

1. takes `latent_unified_with_nan_y_with_nan_age.csv` as an argument

2. fixes some features and outputs the distribution in the reduced space of features.

3. then we can get a prediction for any feature in the reduced space

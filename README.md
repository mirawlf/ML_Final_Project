# Patient-specific Conditional Joint Models of Shape, Image Features and Clinical Indicators <br/>(Machine Learning 2021 Course)

<p align="center">
<img src="https://github.com/samymone/ML_Final_Project/blob/main/plots/disco.gif" width="400" height="300" center="True">
</p>

In this work we investigate how clinical indicators may affect the anatomical shape of the brain of Alzheimer's patients. We provide a set of machine learning models as a baseline. Then we try to incorporate a novel Joint Model approach to fit into our data. The Joint Models are related to Bayesian methods as they use conditional distributions to predict features. As a result we get a significant error decrease when using conditioning. The outputs are visualized with the help of Brain Painter software. As a side note, one of the authors found a bug in the software and made a video tutorial on how to fix it, which will be used by the Brain Painter developers in the next official release.

## Experiment reproduction

Due to privacy protection policy original data can't be disclosed freely. Please, apply to the official ADNI [website](http://adni.loni.usc.edu/) for access.

In this repository only trained models can be found, without any personal data extractable.

To reproduce distribution conditioning, the **Conditional_model.ipnb** the Jupyter notebook was prepared. It applies age conditioning to learned distribution in order to obtain conditioned values in latent space for **ST56SA** feature, which corresponds to the surface area of the Left Superior Frontal segment of a brain.

**Conditional\_Model.ipynb** - makes predictions based on fixed features in the latent space.

1. takes `latent_unified_with_nan_y_with_nan_age.csv` as an argument;

2. fixes some features and outputs the distribution in the reduced space of features;

3. then we can get a prediction for any feature in the reduced space.

## Other scripts

**baseline.ipynb** - the script performs the algorithms from the baseline section of our project - KNN, Logistic regression, Random Forest, XGBoost.

1. as an input it takes `st_features_without_nans_and_y_with_nans.csv`. Drops the NaN values. Then remaps the target value Y to 0 and 1 depending on the classification mode (AD vs NL, AD vs MCI, AD+MCI vs NL - different phases of Alzheimer disease);

2. then it performs KNN, Logistic Regression, RF using `cross_val_score` and gets the cross\_val score (metric is `roc_auc`);

3. then it performs KNN, Logistic Regression, RF using `fit` and gets the train and test scores;

4. then it performs XGBoost using `roc_auc` metric (test data is 30 percent);

5. the notebook outputs `feature_importance.png` and scores tables.

**make\_latent\_space.ipynb** - the script performs the translation from the original space of the features to the so-called latent space.

1. as an input it takes `distributions/pdf.pickle' file that stores the features' original distributions;

2. then it draws the graphs of the distributions into `plots/` folder;

3. then it creates the distributions in the latent space;

4. then it creates the graphs of the latent space distributions into `latent/` folder;

5. finally, it creates the `latent_unified_with_nan_y_with_nan_age.csv` that stores the dataset in the latent space.

**ADNI_SVD_PCA_intrinsic_dim.ipynb** - the script performs data cleaning and normalizing, dimensional analysis.

1. as an input in takes concatenated data `full_data_with_nans.csv` with possible nan values;

2. nan values for scan specific features are replaced by corresponding mean values, the data is normalized and stored for further processing steps;

3. scatter plot distributions are build to investigate correlations between ST features;

4. SVD and PCA decompositions performed to estimate the number of significant singular values;

5. Intrinsic dimensionality through KNN applied to for possible dimension reduction;

6. Covariance and Information matrices of features are calculated to visualize the dependency structure of features.

**ADNI_PCA_Encoders.ipynb** - script trains auto-encoder for possible dimensionality reduction;

## Brain Painter software
  
To visualize distributions on brain segments the Brain Painter [software](https://github.com/razvanmarinescu/brain-coloring/) was used.
Here you can find a [step-by-step instruction](https://www.youtube.com/watch?v=rzGb40PUVX8) of installation and configuration Blender for Brain Painter with further pictures obtained.

## Fitter

Fitter [library](https://pypi.org/project/fitter/) for automatic distribution fitting. Compatible with `scipy.stats` library. Used to automatically fit marginal feature distributions.

## References

1. Anderson, T. and Olkin, I. Maximum-liklihood estimationof the parameters of a multivariate normal distribution.Linear Algebra and its Applications, 70:147–171, 1985.

2. Egger, B., Kaufman, D., Schönborn, S., Roth, V., and Vetter,T. Copula eigenfaces - semiparametric principal component analysis for facial appearance modeling.  InInter-national Conference on Medical Image Computing andComputer-Assisted Intervention, pp. 48–56, 2016.

3. Egger,  B.,  Schirmer,  M.  D.,  Dubost,  F.,  Nardin,  M.  J.,Rost, N. S., and Golland, P. Patient-specific conditionaljoint models of shape, image features and clinical indi-cators.  InInternational Conference on Medical ImageComputing and Computer-Assisted Intervention, pp. 93–101. Springer, 2019.

4. Gloria, C., Giovanna, C. M., Matteo, C. R., Daniele, M.,Federica, D., Antonio, R., Paolo, V., Nicoletta, A., adnPalesi Fulvia adn Sinforiani Elena, B. S., Alfredo, C.,Giuseppe, M., Egidio, D., Giovanni, M., and M., G. W.-K. C. A. A machine learning approach for the differentialdiagnosis of alzheimer and vascular demential fed by mriselected features.Frontiers in Neuroinformatics, 14:25,2020.

5. Petersen, R., Aisen, P., Beckett, L., Donohue, M., Gamst,A., Harvey, D., Jack Jr., C., Jagust, W., Shaw, L., Toga, A.,Trojanowski, J., and Wiener, M. Alzheimer’s disease neu-roimaging initiative clinical characterization.Neurology,74:201–209, 2010.


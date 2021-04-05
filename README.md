# Case Study Overview
Predicting Central Neuropathic Pain (CNP) in people with Spinal Cord Injury (SCI) from Electroencephalogram (EEG) data.
* CNP is pain in response to non-painful stimuli, episodic (electric shock), “pins and needles”, numbness.
* There is currently no treatment, only prevention.
* Preventative medications have strong side-effects.
* Predicting whether a patient is likely to develop pain is useful for selective treatment.

# Code and Resources Used
* Python Version: 3.9
* Packages: pandas, numpy, sklearn, matplotlib, seaborn
* Data: Provided by The University of Glasgow as part of coursework.

# About the Data
The data is preprocessed brain EEG data from SCI patients recorded while resting with eyes closed (EC) and eyes opened (EO)
* 48 electrodes recording electrical activity of the brain at 250 Hz.
* 2 classes: subject will / will not develop neuropathic pain within 6 months.
* 18 subjects: 10 developed pain and 8 didn’t develop pain.
* The data has already undergone some preprocessing.
* The data is provided in a single table ('data.csv') consisting of
  1. 180 rows (18 subjects x 10 repetitions), each containing
  2. 432 columns (9 features x 48 electrodes)
  3. rows are in subject major order, i.e. rows 0-9 are all samples from subject 0, rows 10-19 all samples from subject 1, etc.
  4. columns are in feature_type major order, i.e. columns 0-47 are alpha band power, eyes closed, electrodes 0-48
  5. feature identifiers for all columns are stored in 'feature_names.csv'
  6. 'labels.csv' defines the corresponding class (0 or 1) to each row in data.csv

# Objective
Report on the feature engineering pipeline, the classifier used to evaluate performance, and the performance as mean and standard deviation of accuracy, sensitivity and specificity across folds.

# Data Cleaning & preprocessing
The provided has no missing values and it's already been preprocessed to some extent. I used Standard scaler to standardize the data to compare the Leave One group out cross validation scores wihout Standardizing.

# Feature Engineering/Selection
The provided data had 432 features and too many features affects the performance of the model. I have implemented three types of feature selection and evaluated their performance.
* Filter Method
  1. Pearson Correlation.
  2. Chi Square test.
  3. Anova test.
  4. Mutual Gain.
* Wrapper Methods
  1. Forward Feature Selection.
  2. Backward Elimination.
  3. Exhaustive feature selection.
* Embedded Methods
  1. L1 Regularization with Logistic Regression.
  2. Feature importance with Random Forest Classifier.

# Model Building
As we are aksed to use leave one subject out cross validation, I went with Leave One Group Out Cross validation method. So there were *18* Subjects, so totally *18 fold* cross validation. I defined a function which could split the data into train and test split and also create a *Classification Report* and *Confusion matrix* to calculate the mean accuracy, recall and specificity.

Being experimented with KNN, LogisticRegression and Random forest classifier, I went with *Logistic Regression*, as the accuracy was better with the raw data before dimensionality reduction.

I also created a pipeline, which I used to evaluate the performance before Standardizing and after Standardizing.

# Model Performance

Model used: Logistic Regression

### Without Standardizing
Method | Total number of features | Accuracy | Sensitivity | Specificity
------ | ------------------------ | -------- | ----------- | -----------
Pearson Correlation | 189 | 85 | 83.75 | 86
Chi Squared | 120 | 83 | 83.75 | 83
Anova test | 325 | 84 | 83.75 | 84
Mutual Gain | 180 | 87 | 87.5 | 86
Forward Feature Selection | 180 | 86 | 76.25 | 93
Backward Feature Elimination | 180 | 91 | 91.25 | 91
L1 Regularisation | 43 | 91 | 88.75 | 92
Random Forest Selector | 170 | 85 | 80 | 89
 
### After Standardizing
Method | Total number of features | Accuracy 
------ | ------------------------ | -------- 
Pearson Correlation | 189 | 87.2
Mutual Gain | 180 | 92
Forward Feature Selection | 180 | 95 
Backward Feature Elimination | 180 | 91.1
L1 Regularisation | 43 | 90
Random Forest Selector | 170 | 92.7

# References

* Wrapper methods 
https://stackabuse.com/applying-wrapper-methods-in-python-for-feature-selection/
* Cross-validation
https://scikit-learn.org/stable/modules/cross_validation.html
* Embedded Methods for Feature selection
https://heartbeat.fritz.ai/hands-on-with-feature-selection-techniques-embedded-methods-84747e814dab
* Exhaustive Feature selector
http://rasbt.github.io/mlxtend/user_guide/feature_selection/ExhaustiveFeatureSelector/







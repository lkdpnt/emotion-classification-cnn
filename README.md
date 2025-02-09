Fundamentals of Machine Learning Report.

1. Approach
For this assignment, I performed a binary classification
task to determine whether images depict happy or sad
scenes using a set of 4096 features per image. The dataset
consists of features extracted from Convolutional Neural
Networks (CNN) and GIST descriptors, with two training
datasets provided: one complete dataset with no missing
values and another dataset with some missing values. The
approach involved a combination of data imputation,
feature scaling, dimensionality reduction through Principal
Component Analysis (PCA) [1], and model selection
followed by hyperparameter tuning to optimise predictive
performance.

The initial stage of the project focused on data
preprocessing to handle missing values and normalise the
features. Given the high dimensionality of the data,
dimensionality reduction was necessary to enhance
efficiency and reduce the risk of overfitting. After
preprocessing, multiple classifiers were evaluated,
including Logistic Regression, Random Forest, Gradient
Boosting, and Support Vector Machine (SVM) [2]. The
SVM with a radial basis function (rbf) kernel was selected
as the final model due to its superior performance in
handling high-dimensional data and achieving the best F1
score during validation. GridSearchCV was used for
hyperparameter tuning to ensure optimal performance for
each classifier.

2. Methods
2. 1 Imputation
The second training dataset contained missing values,
which were imputed using the mean of each feature. This
step was essential to ensure that the training process was
not compromised by incomplete data. SimpleImputer from
scikit-learn was employed for this task, which replaced
missing values with the mean of the respective features.
This imputation method is straightforward yet effective in
maintaining the integrity of the dataset without introducing
significant bias [3].

2.2 Feature Scaling
Given the varying scales of the features, it was crucial to
normalise the data to ensure that all features contributed
equally to the model training. StandardScaler from
scikit-learn was used to scale the data to have a mean of
zero and a standard deviation of one. This step was
particularly important for models like SVM and Logistic
Regression, which are sensitive to the scale of input
features. By scaling the features, the convergence of
gradient-based optimisers was improved, leading to better
model performance.

2.3 Dimensionality Reduction
Principal Component Analysis (PCA) was applied to
reduce the feature space while retaining 95% of the
variance in the data. This reduction resulted in 335
principal components, significantly lowering the
computational load and mitigating the risk of overfitting
[1]. PCA helped in identifying the most informative
features, thereby simplifying the model training process
without losing essential information. The explained
variance plot (Figure 1) was used to determine the number
of components to retain, ensuring that the selected
components captured the majority of the data’s variability.
[Figure 1: Cumulative explained variance plot indicating the
number of principal components needed to retain 95% of the
total variance. This plot was used to determine the optimal
number of components for dimensionality reduction through
PCA.]

2.4 Training and Testing
The dataset was split into training and validation sets to
ensure that both sets represented the overall distribution of
the data. This split was crucial for evaluating the models’
performance and adjusting the hyperparameters
accordingly. A stratified split was used to maintain the
class distribution in both sets. The training set was used to
train the models, while the validation set was used to
assess their performance and prevent overfitting.

2.5 Cross-Validation and Hyperparameter Tuning
GridSearchCV was employed to perform exhaustive grid
searches over specified parameter values for each model.
This approach was applied to SVM, Random Forest,
Logistic Regression, and Gradient Boosting classifiers.

GridSearchCV was set up with 5-fold cross-validation to
ensure robust evaluation of model performance. The SVM
emerged as the top performer, with optimal
hyperparameters identified as C=1 and rbf kernel [2]. The
use of cross-validation helped in selecting the best model
and hyperparameters by providing a reliable estimate of
model performance on unseen data.

2.6 Feature Selection
While explicit feature selection was not performed beyond
PCA, the reduction to 335 principal components
effectively acted as a selection mechanism. PCA
highlighted the most significant features from both CNN
and GIST descriptors, ensuring that the models trained on
the most informative subset of the data (Figure 2). This
step helped in reducing the dimensionality of the data,
thereby simplifying the model training process and
improving generalisation.

3. Results and Discussion
[Figure 2: Heatmap showing the correlation coefficients between
different features in the training dataset. This visualisation helps
identify relationships and potential multicollinearity issues
among the features.]

3.1 Best Model
The SVM model, configured with C=1 and rbf kernel,
provided the best F1 score during cross-validation (Figure
3). This model was subsequently used to make predictions
on the test dataset. The SVM’s ability to handle non-linear
relationships in high-dimensional space made it
particularly effective for this classification task. The
model achieved a balanced performance across various
metrics, including precision, recall, and F1 score.

3.2 Evaluation Metrics
The evaluation metrics used included F1 score, precision,
recall, and accuracy. The F1 score was prioritised due to
the imbalanced nature of the dataset, providing a balance
between precision and recall. The SVM model achieved an
F1 score of approximately 0.726 during cross-validation,
indicating a solid performance in distinguishing between
happy and sad images.
[Figure 3: Bar chart comparing the performance metrics (F1
Score, Precision, Recall) of different models tested, including
SVM, Logistic Regression, Random Forest, and Gradient
Boosting. The SVM model demonstrated superior performance.]

3.3 Observations
The SVM’s ability to capture non-linear relationships in
high-dimensional space contributed significantly to its
effectiveness. PCA played a crucial role in managing the
challenges associated with high-dimensional data,
improving model efficiency, and focusing on the most
informative features. The combination of PCA and SVM
provided a powerful approach to handling the complex
feature set in the dataset.

3.4 Limitations and Future Work
Despite the strong performance of the SVM model, there
are potential areas for improvement. Future work could
explore deep learning models, which might better capture
the complexity of the data and provide higher accuracy.
Further research could also investigate advanced
imputation techniques and feature selection methods to
enhance model performance.


4. References
1. Jolliffe, I.T. (2002) Principal Component Analysis. 2nd ed. New York: Springer-Verlag.
2. Cortes, C. and Vapnik, V. (1995) 'Support-vector networks', Machine Learning, 20(3), pp. 273-297.
3. Little, R.J.A. and Rubin, D.B. (2002) Statistical Analysis with Missing Data. 2nd ed. New York: John
Wiley & Sons.

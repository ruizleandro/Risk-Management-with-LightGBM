# Risk Management with LightGBM
Using LightGBM to predict bank customers' credit risk, based on their financial history.

## Project's Objective
* There are two types of credit: good credit and bad credit.
* The main task is to predict if a customer will be going to pay his credit according to the available data.
> Note: the dataset used for this task is really small (the `customer_data` set has 1125 rows, and the `payment_data` has 8250 rows), so that will definitely impact in the accuracy of the final model.

## Introduction to LightGBM

### Important Parameters
1. *max_depth*: Set this parameter to prevent trees from growing too deep. Shallow trees have less likelihood to overfit. Setting this parameter is particularly important if the dataset is small.
2. *num_leaves*: Controls the complexity of the tree model. The value should be less than 2^(max_depth) to prevent overfitting. Setting `num_leaves` to a large value can increase accuracy at the risk of a higher chance of overfitting. 
3. *min_data_in_leaf*: Setting this parameter to a large value can prevent trees from growing too deep. This is another parameter you can set to help control overfitting. Setting the value too large can cause underfitting.
4. *max_bin*: LightGBM groups the values of continuous features into discrete bukcets using histograms. Set `max_bin` to specify the number of bins that the values will be grouped in. A small value can help control overfitting and improve training speed, while a larger value improves accuracy.
5. *feature_fraction*: This parameter enables feature subsampling. This parameter specifies the fractions of features that will be randomly selected in each iteration. For instance, setting `feature_fraction` to 0.75 will randomly select 75 % of the features in each iteration. Setting this parameter can increase training speed and help prevent overfitting.
6. *bagging_fraction*: Specifies the fraction of data that will be selected in each iteration. For instance, setting `bagging_fraction` to 0.75 will randomly select 75 % of the data in each iteration. Setting this parameter can increase training speed and help prevent overfitting.
7. *num_iteration*: Sets the number of boosting iterations. The default is 100. For multiclass classification, LightGBM builds `num_class` * `num_iteration` trees. Setting this parameter influences training speed.
8. *objective*: Like XGBoost, LightGBM supports multiple objectives. The default objective is set to regression. Set this parameter to specify the type of tasj that your model is trying to perform. For regression tasks, the options are `regression_l2`, `regression_l1`, `poisson`, `quantile`, `mape`, `gamma`, `huber`, `fair`, or `tweedie`. For classification tasks, the options are `binary`, `multiclass`, or `multiclassova`. It is important to set the objective correctly to aovid unpredictable results or poor accuracy.

## Model Evaluation

The final results were:
1. The accuracy of prediction is: 0.7988165680473372
2. The roc_auc_score of prediction is: 0.5
3. The null accuracy is: 0.7988165680473372

As the accuracy of prediction and the null accuracy are the same, this means that the model predicted all the samples with the most common target label. This can be explained knowing that the dataset used to train the model was very small. But at least now I know how to use LightGBM and how to tune his parameters.

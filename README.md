
## Tuning GBMs (hyperparameter tuning)

The goal of this repo is to study the impact of having one dataset/sample/"the dataset" only 
when training and tuning machine learning models in practice (or in competitions) 
on the prediction accuracy on new data 
that usually comes from a (slightly) different distribution (due to non-stationarity).

To to keep things simple/to begin with we focus on binary classification, use only one source dataset 
with mix of numeric and categorical features, don't perform feature engineering,
tune only GBMs with lightgbm and random search (might also ensemble the best models), and 
use only AUC as a measure of accuracy.

From the source data we pick 1 year of data for training/tuning and the following 1 year for testing (hold-out).
We take samples of give sizes from these. (**TODO:** For now we have only 1 year and 1 sample of each train/test.
The main goal of the repo is actually to study what happens when we resample this.)

We choose a grid of hyperparameter values and 100 random combinations from the grid.
For each hyperparameter combination we repeat the following resampling procedure 20 times:
Split the training set 80-10-10 into data used for (1) training (2) validation for early stopping
and (3) evaluation for model selection. 
We train the GBM models with early stopping and record the AUCs on the last split (3). We record 
the average and the standard deviation.
Finally, we compute the AUC on the test (hold-out set) of the ensemble of the 20 models obtained
with resampling (simple average of their predictions).

We study the test AUC of the top performing hyperparameter combinations (selected based only on 
the information from the resampling procedure without access to the test set).



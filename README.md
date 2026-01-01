# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### NAME: [Your Name Here]

## Initial Training
**What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?**
The initial predictions contained negative values (e.g., -2.5). Since Kaggle does not accept negative numbers for the target "count" (you cannot rent a negative number of bikes), I had to modify the code to replace all negative predictions with 0 before saving the submission CSV.

**What was the top ranked model that performed?**
The `WeightedEnsemble_L3` model generally performed the best across the iterations, leveraging the strengths of multiple individual models.

## Exploratory Data Analysis and Feature Creation
**What did the exploratory analysis find and how did you add additional features?**
The initial histogram analysis showed that the `datetime` column was not providing distinct patterns in its raw format. By visualizing the data, it became clear that time of day is critical. I parsed the `datetime` column to extract the `hour` as a new feature. I also converted `season` and `weather` to categorical variables so AutoGluon would treat them as distinct categories rather than continuous numbers.

**How much did the model improvement using your new additional features?**
The improvement was substantial. The score improved from approximately **1.42** down to **0.51**. This confirms that separating the "hour" information allowed the model to capture morning and evening rush hour trends.

## Hyperparameter Tuning
**What were the top 3 hyperparameters we tuned?**
1. **num_trials**: Set to 5 to give the model multiple attempts to find better settings.
2. **searcher**: Set to 'random' to explore the hyperparameter space.
3. **scheduler**: Set to 'local' to manage the training resources.

**What was the score improvement using hyperparameter tuning?**
The HPO score was **0.54807**, which was very close to the feature engineering score. While it didn't drastically beat the "add_features" model in this specific run due to time constraints, it maintained a high level of accuracy compared to the initial raw data model.

## Model Performance Table
| model | score |
|---|---|
| initial | 1.42355 |
| add_features | 0.51154 |
| hpo | 0.54807 |

## Plot of Model Score
![model_train_score.png](model_train_score.png)

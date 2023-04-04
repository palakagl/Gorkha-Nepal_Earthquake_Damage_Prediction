# Nepal Earthquake Damage Prediction by Driven Data - Scored Rank in Top 5%

## Nepal is one of the most disaster-prone countries in the world:

Due to its location and variable climatic conditions, Nepal is one of the most disaster-prone countries in the world. Every year, these events cause heavy loss of life and damage to properties. Climate change and an increasing population further exacerbate the impacts of natural disasters

Every year, more than 1 000 people in Nepal are killed by landslides and floods during the monsoon season. The potential threat of earthquakes, glacial lake outbursts, avalanches, and cold and heat waves always looms large.

## Using Machine Learning, we could predict which building to repair to minimize the damage brought by the future earthquakes

1. Prioritization of Building Retrofit & Repair

   • Based on geographical location, shape, size and height, age, structure and material used
   
   • Goal: "if a building located in x region with the shape of y, that is z years old with foundation type of x, and roof type of y, using material type of z tbuild, it must be prioritized
   
2. Formulation of better Urban Planning & Construction Standards

3. A pilot for disastrous preparedness that can be used for other disasters

4. A pilot for other countries prone to earthquakes and other disasters

## Model:

• I started my modeling process by using Azure Auto ML which helped me get started quickly with data loading, EDA, model creation, showing feature importance, and ranking many different models. However, I faced a challenge when trying to get results for test data for competition submission. It required extra steps to either export the model for my own use or to generate a result csv from the best model created.

• To begin with, I used the Random Forest algorithm, which gave me a model in the least possible time. I used it without any hyperparameter tuning, but its accuracy was slightly below 0.70. I manually changed hyperparameters such as estimators and maxdepth, and was able to improve the accuracy up to 0.7123.

• Then, I tried Catboost, a really cool algorithm that can run with categorical columns, which allowed me to remove all the pre-processing steps to convert columns to numerical. With a little bit of hyperparameter tuning, I got my second-best score of 0.7461. Another feather in the cap was discovering a library called ‘Shap’ that generated informative bar charts with the importance of each feature column for each of the target classes in the dataset.

• My best run so far has been with XGBoost, after hypertuning and pre-processing, where I achieved a score of 0.7477.
  
  Model parameters : XGBoost Best With RandomSearchCV  n_estimators=500, max_depth=10, learning_rate= 0.1, colsample_bytree=0.5 (n_estimators=np.arange(100,1000,100) learning_rate=[0.03,0.01,0.1] max_depth=np.arange(10,100,15))​

  XGboost Optuna  : {'n_estimators': 912, 'max_depth': 6, 'reg_alpha': 0, 'reg_lambda': 0, 'min_child_weight': 5, 'gamma': 0, 'learning_rate': 0.06583720693236587, 'colsample_bytree': 0.39, 'subsample': 0.473997903445895, 'num_boost_round': 921.5868838155058}. Best is trial 3 with value: 0.7457300706003445.

  CatBoost  params = { 'leaf_estimation_method': 'Gradient', 'learning_rate': 0.01, 'max_depth': 8, 'bootstrap_type': 'Bernoulli', 'objective': 'MultiClass', 'eval_metric': 'MultiClass', 'subsample': 0.8, 'random_state': 42, 'verbose': 0, "eval_metric" : 'TotalF1', "early_stopping_rounds" : 100 }

## Learnings:

Potential improvement opportunities found are:

1. More computing power / more memory

   • Limited computing power resulted in fewer trials for hyperparameter tuning
   
   • Category encoding for geo levels caused an error due to low RAM
   
   • Optuna Stepwise could be used to select the best subset of features if more computing power was available
   
   • SaS Viya provides cloud analytics with significant computing power

2. More knowledge and experience on alternative tools 

   • VotingEnsemble on Azure could not be used due to limitations on Google Colab 
  
   • Exploring alternative tools like SaS Viya could be beneficial

3. More relevant data

   • Data on the number of poles on building structures could play a crucial role in predicting earthquake resistance
  
   • Historical earthquake data, including duration, magnitude, and frequency in different regions, could help in better predictive modeling

4. Interpreting the confusion matrix

   • Confusion matrix interpretation can be confusing, and there is a need to improve skills in interpreting results correctly
  
   • Practicing on applying the findings from ML to the problem we are trying to solve can help improve our skills

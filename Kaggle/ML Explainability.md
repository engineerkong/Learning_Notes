# Machine Learning Explainability

- Use Cases for Model Insights

Debugging, Informing Feature Engineering, Directing Future Data Collection, Informing Human Decision-Making, Building Trust

1. What features in the data did the model think are most important?

2. For any single prediction from a model, how did each feature in the data affect that particular prediction?

3. How does each feature affect the model's predictions in a big-picture sense (what is its typical effect when considered over a large number of possible predictions)?

- Permutation Importance 排列重要性

1. Get a trained model.

2. Shuffle the values in a single column, make predictions using the resulting dataset. Use these predictions and the true target values to calculate how much the loss function suffered from shuffling. That performance deterioration measures the importance of the variable you just shuffled.

3. Return the data to the original order (undoing the shuffle from step 2). Now repeat step 2 with the next column in the dataset, until you have calculated the importance of each column.

```
perm = PermutationImportance(my_model, random_state=1).fit(val_X, val_y)
eli5.show_weights(perm, feature_names = val_X.columns.tolist())
```

- Partial Plots

partial dependence plots (PDP) show how a feature affects predictions.

```
tree_graph = tree.export_graphviz(tree_model, out_file=None, feature_names=feature_names)
graphviz.Source(tree_graph)
# Create and plot the data
disp1 = PartialDependenceDisplay.from_estimator(tree_model, val_X, ['Goal Scored'])
plt.show()
# Similar to previous PDP plot except we use tuple of features instead of single feature
f_names = [('Goal Scored', 'Distance Covered (Kms)')]
disp4 = PartialDependenceDisplay.from_estimator(tree_model, val_X, f_names, ax=ax)
plt.show()
```

- SHAP values

SHAP values interpret the impact of having a certain value for a given feature in comparison to the prediction we'd make if that feature took some baseline value.

sum(SHAP values for all features) = pred_for_team - pred_for_baseline_values

```
row_to_show = 5
data_for_prediction = val_X.iloc[row_to_show]  # use 1 row of data here. Could use multiple rows if desired
data_for_prediction_array = data_for_prediction.values.reshape(1, -1)
my_model.predict_proba(data_for_prediction_array)

# Create object that can calculate shap values
explainer = shap.TreeExplainer(my_model) # also shap.DeepExplainer, shap.KernelExplainer
# Calculate Shap values
shap_values = explainer.shap_values(data_for_prediction)
shap.initjs()
shap.force_plot(explainer.expected_value[1], shap_values[1], data_for_prediction)
```

Advanced Uses of SHAP Values

1. Summary Plots

![Ew9X3su](https://github.com/engineerkong/Learning_Notes/assets/89781823/a2dc7960-228d-455e-b3d3-624fc892ae26)

`shap.summary_plot(shap_values[1], val_X)`

2. Dependence Contribution Plots

![uQ2JmBm](https://github.com/engineerkong/Learning_Notes/assets/89781823/c2de167a-dcaa-4eda-9516-b19cc827e206)

`shap.dependence_plot('Ball Possession %', shap_values[1], X, interaction_index="Goal Scored")`

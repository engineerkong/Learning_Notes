# Intro to AI Ethics

- In the **human-centered design** lesson, you’ll learn how to design an AI system to ensure that it serves the needs of the people that it is intended for.
6 Steps:
  
1. Understand people's needs to define the problem
2. Ask if AI adds value to any potential solution
3. Consider the potential harms that the AI system could cause
4. Prototype, starting with non-AI solutions
5. Provide ways for people to challenge the system
6. Build in safety measures

- In the **bias** lesson, you’ll determine how AI systems can learn to discriminate against certain groups.

Bias refers to negative, unwanted consequences of ML applications, especially if the consequences disproportionately affect certain groups.

6 Types of bias:

1. Historical bias occurs when the state of the world in which the data was generated is flawed.
2. Representation bias occurs when building datasets for training a model, if those datasets poorly represent the people that the model will serve.
3. Measurement bias occurs when the accuracy of the data varies across groups.
4. Aggregation bias occurs when groups are inappropriately combined, resulting in a model that does not perform well for any group or only performs well for the majority group.
5. Evaluation bias occurs when evaluating a model, if the benchmark data does not represent the population that the model will serve.
6. Deployment bias occurs when the problem the model is intended to solve is different from the way it is actually used.

- In the **fairness** lesson, you’ll learn to quantify the extent of the bias in AI systems.

4 fairness criteria: 

1. Demographic parity / statistical parity: Demographic parity says the model is fair if the composition of people who are selected by the model matches the group membership percentages of the applicants.
2. Equal opportunity: Equal opportunity fairness ensures that the proportion of people who should be selected by the model ("positives") that are correctly selected by the model is the same for each group.
3. Equal opportunity: That is, the percentage of correct classifications should be the same for each group.
4. Group unaware:removes all group membership information from the dataset.

confusion matrix - Sensitivity / True positive rate

- In the **model cards** lesson, you’ll learn how to use a popular framework for improving public accountability for AI models.

A model card is a short document that provides key information about a machine learning model. Model cards increase transparency by communicating information about trained models to broad audiences.

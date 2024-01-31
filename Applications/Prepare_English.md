## Master's Thesis
- Keywords: robot tasks, reinforcement learning algorithms and hyperparameters, sim2real transfer, landscape visualization.
- Details:
1. Define three robot tasks: reach, push, pick and place. Select two algorithms: SAC and PPO. Select two hyperparameters: learning rate and discount factor. 
2. Search and tailor the simulation environment to match the real robot environment.
3. Conduct trial training with one combination of algorithms and hyperparameters in the simulation to identify the suitable reward function and determine the total time consumption.
4. Train multiple combinations for each robot task in the simulation over a cloud server.
5. Implement the trained models in the real robot environment and compare the performance between simulation and reality.
6. Evaluate the results and create a landscape visualization to show the impact of algorithms and hyperparameters on Sim2Real Transfer.
- Facts:
1. Using the SAC algorithm for the reach task. A middle learning rate and lower discount factor are used to minimize Sim2Real transfer. This means it performs best in reality when it already performs well in simulation.
2. However, the results from my research do not utilize models trained comprehensively in simulation and do not have a wide variety of combinations due to time constraints.
## Student Project
- Keywords: data processing, deep learning models, computer vision, image and lidar point cloud.
- Details:
1. Annotate and split images with labels for cars and pedestrians.
2. Search and tailor deep learning models for traffic participants.
3. Train the deep learning models with a training dataset from open-source image sets.
4. Convert 2D to 3D using intrinsic and extrinsic matrices based on coordinate relations.
5. Compare 3D results with the 3D point cloud and identify corresponding points on the lidar.
6. Remove anomaly points, such as outliers and floor points.
7. Compute the 3D position and orientation.
- Consequences:
1. This method can improve the accuracy of 3D information prediction and is better than direct prediction from deep learning models.
2. However, the results show that only some participants are detected due to differences between training and testing data. Besides, this algorithm needs further improvement due to suboptimal 3D position and orientation results.
## Azure AI Engineer Associate
- Keywords:
- Knowledge:
1. AI: ML Studio, Decision support, Computer Vision, NLP, Knowledge mining, Document Intelligence, OpenAI.
2. Data: Data storage, database, Data analytics with PowerBI/Spark, ETL/ELT processes.
3. Cloud: Azure Cloud Architecture, Computing services, Networking services, Storage services, Management Services, Security services, Kubernetes/Docker.
## Proposal: Use Case: Predictive Analytics in Healthcare
### Objective:
To develop a machine learning model that predicts patient health risks (such as the likelihood of developing a certain condition) based on a wide range of healthcare data.

### Implementation:
- Data Collection and Management (FAIR Principles):

1. Findable: Aggregate data from various sources like electronic health records (EHRs), genomic databases, wearable device data, and patient surveys. Ensure each data set is tagged with comprehensive metadata, including patient demographics, diagnosis codes, treatment information, and outcomes.
2. Accessible: Store the data in a secure, centralized data lake (e.g., Azure Data Lake) ensuring compliance with healthcare regulations like HIPAA. Implement role-based access to ensure data is accessible to authorized personnel and ML algorithms.
3. Interoperable: Standardize data formats using healthcare data standards (like HL7 FHIR) to ensure compatibility between different types of data and systems.
4. Reusable: Annotate data with detailed information about data collection methods, consent forms (if applicable), and anonymization techniques to ensure the data can be reused for other research purposes while maintaining patient privacy.

- Machine Learning Development:

1. Data Preprocessing: Clean and preprocess the data to handle missing values, normalize data ranges, and encode categorical variables.
2. Feature Selection: Use statistical methods to select relevant features that could significantly impact health risk predictions.
3. Model Training and Validation: Train various ML models (e.g., logistic regression, random forests, neural networks) on a portion of the data. Use cross-validation to evaluate model performance.
4. Model Interpretation: Apply techniques like SHAP (SHapley Additive exPlanations) to interpret the model's predictions, understanding which features are most influential in predicting patient risks.

- Deployment and Monitoring:

Deploy the best-performing model into a clinical setting. Integrate it with existing hospital systems to provide real-time risk assessments for patients.
Continuously monitor the model's performance and accuracy, making adjustments as needed based on feedback from healthcare providers and changes in the underlying data.

### Outcome:
The implementation of this use case can lead to:

- Early identification of patients at risk for certain conditions, allowing for timely intervention.
- Personalized treatment plans based on individual risk profiles.
- Enhanced understanding of the factors contributing to various health conditions.
- Improved overall patient care and outcomes.

### Ethical Considerations:
It's crucial to address privacy, consent, and bias in the data. Anonymizing patient data to protect privacy and ensuring that the data used for training the ML models is representative of the diverse patient population are key considerations.

This use case demonstrates how FAIR data principles can enhance the quality and utility of data in a machine learning context, particularly in a sensitive and impactful field like healthcare.

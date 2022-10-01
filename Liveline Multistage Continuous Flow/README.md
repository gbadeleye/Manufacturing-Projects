### LIVELINE MULTI-STAGE CONTINUOUS-FLOW MANUFACTURING PROCESS MODELLING (FROM KAGGLE)


**AUTHOR:** Gbenga Adeleye ([LinkedIn](www.linkedin.com/in/gbenga-adeleye-p-eng-29189716))

**DATE:** 7 September 2022
<br>
<br>
#### INTRODUCTION
This is a project, which attempts to apply Machine Learning (ML) techniques to a dataset made available by [Liveline Technologies](https://www.liveline.tech/) on the [Kaggle site](https://www.kaggle.com/datasets/supergus/multistage-continuousflow-manufacturing-process?rvi=1). As indicated in the Kaggle page, the dataset has been taken from an actual manufacturing line near Detroit, Michigan, USA. The line is a high-speed, continuous manufacturing process with parallel and series stages.
<br>
<br>

**MANUFACTURING PROCESS DESCRIPTION**

The dataset comes from a multi-stage continuous flow manufacturing process. The production line is a high-speed, continuous manufacturing process with parallel and series stages. The line consists of 2 stages. In the first stage, there are 3 machines - Machines 1, 2, and 3, which operate in parallel, and feed their outputs into a step that combines the flows. Output from the combiner is measured in 15 locations surrounding the outer surface of the material exiting the combiner. The combiner output then flows into a second stage, where 2 machines - Machines 4 and 5 - process in series. After Machine 5, measurements are made again in the same 15 locations surrounding the outer surface of the material exiting Machine 5.
<br>
<br>

**DATA FILE DESCRIPTION**

The dataset (*continuous_factory_process.csv*) is a time series that comes from a production line test run spanning approx. 4 hours. Samples are in 1-sec intervals. In the first stage, Machines 1, 2, and 3 operate in parallel, and feed their outputs into a step that combines the flows. Output from the combiner is measured in 15 locations. Next, the output flows into a second stage, where Machines 4 and 5 process in series. Measurements are made again in the same 15 locations.

The 30 measurements are noisy, and each measurement also has a target or Setpoint (SP) variable. There are 116 columns in the dataset (1 timestamp column + 115 variables columns). More details about the dataset can be found in the included .txt file (notes_on_dataset.txt).

The dataset source Kaggle page does not provide an illustrative process flow diagram for the production line. However, a diagram has been sketched by the author of this project, based on the process description above, to aid comprehension of the manufacturing process. See below:

![Liveline Multistage Continuous Flow Process](https://user-images.githubusercontent.com/106351334/193079176-658619a2-d48c-46ab-889d-820584ec97c4.png)
<br>
<br>

**OBJECTIVE**

The objective of this project is to apply ML techniques to the Liveline dataset to train model(s) to predict the 15 measurements of the Stage 1 Combiner output. The Stage 2 measurements models will not be part of this project's scope.

**Business Value:** This objective serves as an enabler for several production applications, such as developing process control applications, which could help optimize output of the value-driving process variables of the production line, or help operate the production line within health, environmental, and equipment safety limits. The models can also be used for anomaly detection, which could aid early fault diagnosis in event of operational issues in the production line.

The objective is implemented in the Jupyter notebook, which consists of the following sections:

*   Requisite Library Installation & Dataset Load/Preview
*   Dataframe Review & Pre-processing
*   Dataframe EDA
*   Targets & Features Selection
*   Model Structure
*   Baseline Model Identification & Evaluation
*   Model Parameters Tuning
*   Conclusion & Suggested Opportunities
<br>
<br>

**DATASET PLOTS**

![Liveline Multistage Continuous Flow Process Variables Plots](https://user-images.githubusercontent.com/106351334/193084160-faf7428d-a5b2-4a11-9208-c0f346e494d1.png)
<br>
<br>

**MODEL STRUCTURE**

In this project, the MIMO Auto-Regressive with eXogenous inputs (ARX) model structure is considered for modelling the 15 Stage 1 Combiner output measurements.

ARX time series models are a linear representation of a dynamic system in discrete time. Putting a model into ARX form is the basis for many methods in process dynamics and control analysis. A description of the ARX model can be found [here](https://en.wikipedia.org/wiki/Autoregressive_model). The Single-Input-Single-Output (SISO) form of the ARX model in discrete time is expressed as:

![MIMO ARX Model](https://user-images.githubusercontent.com/106351334/193307256-1a9d3fc9-c3c8-45f6-9336-1ce72eec35d3.png)
To implement the model training, the *.sysid()* system identification function in the python *gekko* library is utilized on the training portion of the dataset. *sysid()* will attempt to fit optimal values of the $A$ and $B$ matrices in MIMO ARX model to the dataset, based on hyperparameters - $n_{a}$, $n_{b}$, and $k$

To test the predictive capability of the MIMO ARX model identified by *.sysid()*, the *.arx()* function is applied to simulate the validation portion of the dataset. Detailed information about the *gekko* library can be found [here](https://gekko.readthedocs.io/en/latest/index.html). The arguments for the *.sysid()* and the *.arx()* functions are described [here](https://gekko.readthedocs.io/en/latest/model_methods.html?highlight=sysid#pre-built-objects).
<br>
<br>

**MODEL PERFORMANCE EVALUATION**

The dataset is split into the training and validation datasets. The training dataset is used for model identification, while the validation dataset is used to generate model predictions to compare against the actual targets' values. To evauate the performance, the Mean-Squared-Error (MSE) is calculated using the predictions and the validation dataset:

![MSE](https://user-images.githubusercontent.com/106351334/193311954-22583738-1c3d-4785-8cd3-1ba090a772e1.png)
A baseline MSE is initially calculated for a MIMO ARX model identified based on hyperparameter values - $n_{a}, n_{b}, k$ - suggested by the EDA. The baseline Training MSE and Validation MSE obtained are **0.0726** and **0.6893** respectively. Based on the following defined parameter grid, model training experiments are iteratively performed to obtain the model with the optimal values for the Training and Validation MSE's, relative to the baseline model:
```
{'na': [1, 2, 3, 4], 'nb': [1, 2, 3], 'nk': [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]}
```
<br>

**MODEL TUNING RESULT & PREDICTION PLOTS**

From iteratively implementing model training and performance evalaution over the model parameter grid space, the MIMO ARX model structure - $(n_{a}=1, n_{b}=1, k=9)$ is found to be the best-performing structure, with **Training MSE = 0.063 and Validation MSE = 0.497**. The details of the model coefficients for the $A$ and $B$ matrices can be found in the Jupyter notebook. The optimal model's prediction plots for the 15 Stage 1 output measuremenents, for both the training and validation datasets, are shown below:
<br>

![MIMO ARX Model Prediction](https://user-images.githubusercontent.com/106351334/193417856-d7e89cbe-c04e-498d-a18d-e51a427aa01b.png)
<br>
<br>

**CONCLUSION & SUGGESTED OPPORTUNITIES**

Following the application of ML techniques to the Liveline dataset, to attempt to train a linear time-invariant MIMO ARX model to predict the 15 measurements of the production line Stage 1 Combiner output, the following are suggested opportunities for future work to help further improve model accuracy:
* Considering other algorithms for the imputation of the spikes and missing values observed in several of the variables in the dataset. An example of an algorithm that could be explored is the Kalman filter for missing measurements;
* Model training for the 15 Stage 2 outputs 
* A linear time-invariant model structure had been assumed for this project's objective. Non-linearities in the target variables' dynamics could also be explored, and incorprated into the model.
* Identification of disturbance models for the target variables' residuals from their MIMO ARX model predictions. The ARMAX model could therefore be considered, instead of the ARX structure.






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




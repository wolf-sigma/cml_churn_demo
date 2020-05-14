# TKO Lab
## Telco churn with refactor code
This is the CML port of the Refractor prototype which is part of the [Interpretability
report from Cloudera Fast Forward Labs](https://clients.fastforwardlabs.com/ff06/report).

### Auto Deploy
To build all the project artifacts, run the `0_build_projet.py` file in a python3 session. 

### Manual Setup
If you wish to do this manually, follow the steps below.

### 0 Install Requirements
At the start of the manual build process, you need to open a workbench and run
`!pip3 install -r requirements.txt`


### 1 Ingest Data
Open `1_data_ingest.py` in a workbench: python3, 1 CPU, 2 GB.

Run the file. 


### 2 Explore Data
Open a Jupyter Notebook session: python3, 1 CPU, 2 GB and open the `2_data_exploration.ipynb` file.

At the top of the page click Cells > Run All

### 3 Train Models
A model has been pre-trained and placed in the models/test_model directory.  

If you want to retrain the model run the 3_train_models.py code in a pyton3 1 CPU, 2 GB session to train a new model.  

The model artifact will be saved in the models directory named telco_linear


### 4 Serve Models
Go to the **Models** section and create a new Explainer model with the following:

* **Name**: Explainer
* **Description**: Explain customer churn prediction
* **File**: 4_model_serve_explainer.py
* **Function**: explain
* **Input**: `{"StreamingTV":"No","MonthlyCharges":70.35,"PhoneService":"No","PaperlessBilling":"No","Partner":"No","OnlineBackup":"No","gender":"Female","Contract":"Month-to-month","TotalCharges":1397.475,"StreamingMovies":"No","DeviceProtection":"No","PaymentMethod":"Bank transfer (automatic)","tenure":29,"Dependents":"No","OnlineSecurity":"No","MultipleLines":"No","InternetService":"DSL","SeniorCitizen":"No","TechSupport":"No"}`
* **Kernel**: Python 3

In the deployed Explainer model -> Settings note (copy) the "Access Key" (ie. mukd9sit7tacnfq2phhn3whc4unq1f38)

### 5 Deploy Application

From the Project level click on "Open Workbench" (note you don't actually have to Launch a session) in order to edit a file.
Select the flask/single_view.html file and paste the Access Key in at line 19. 
Save and go back to the Project.  

Go to the **Applications** section and select "New Application" with the following:
* **Name**: Visual Churn Analysis
* **Subdomain**: telco-churn
* **Script**: 5_application.py
* **Kernel**: Python 3
* **Engine Profile**: 1vCPU / 2 GiB Memory  

After the Application deploys, click on the blue-arrow next to the name.  The initial view is a table of rows selected at  random from the dataset.  This shows a global view of which features are most important for the predictor model.  

Clicking on any single row will show a "local" interpretabilty of a particular instance.  Here you 
can see how adjusting any one of the features will change the instance's churn prediction.  

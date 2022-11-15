#  ML Ops Recepies - a small repo containing the learning of Ml OPs

## State of Ml Ops

Read [this](https://becominghuman.ai/no-you-dont-need-mlops-5e1ce9fdaa4b)  article - It summarises if you _really_ need MLOPs quite well

As long as your ML system is simple enough that an ops person can (1) find out when it isn’t working properly, (2) make small changes to it, and (3) redeploy the model, you are achieving the goal of MLOps.

Now, assuming you need Machine Learning in Production to support (automatic) decision making you can automate the whole process of training/testing and deployment 

## Steps in Ml Lifecycle

1. Data Collection & Analysis -> Which data do we have ? Which features can we build ?
2. Data Management -> How the data is being ingested into the training/testing step
3. ML Training Pipeline -> Train, Test and Build the models
4. Build and Validate Applications ->  Integrate models and build applications t
5. Performance Evaluation -> See how the product/service evaluates against human testing
6. Measuring Service Level Objectives (SLO's) -> Reliability of the Service (costs/scaling/performance to measure how the service is performing) - Kind of like the KPIs 
7. Launch -> Release of the Software into Prod - Update Monitoring and controlled Rollouts 
8. Monitoring and Feedback Loops


## Tools:

### Feast/Tecton

[feast](https://feast.dev) - Feature Store Solution - [Why do we need a feature store ? ](https://feast.dev/blog/what-is-a-feature-store/)
[tecton](https://feast.dev/blog/what-is-a-feature-store/) 


Open Source Feature store to automate ETL pipelelines into prod/staging/test environment for inference

Depending how quick your db is there are some different concerns: 
* Do you need do ETL quick ? How fast is your db ? Is there some alternative to ETL? 
* Can you batch process data and store it somewhere else for inference ? 

Feast, however, does not provide the ETL -> It gets support from airflow/dagger/dbt or other data engineering tools

Stores data offline/online and a feature server. 

Alternatives: Pull some from the data warehouse 

In General a feature store should provide raw/transformed data for training/inference 

#### Feast 

Feast provides processed data that is transformed from different data sources including streams, DataLakes/Warehouses or applications 

We can use it for serving live models or just for training/testing 



#### Other alternatives 

* Redis on Elasticache with Batch processed data 
* Persistent Storage somewhere on a instance -> read/sent on demand


### [DVC](https://www.dvc.org) - Data Version Control

DVC runs on top of any ml git repo - to store the artifacts we can use any possible stroage provider 

DVC allows to track any of the metrics we want to track for each experiment -> we can also set it back like Git 


### [mlflow](https://mlflow.org)

Experiment tracking and Model registry -> can be linked with a db/data lake/s3 to store models 

Microsoft was so nice to provide a taxonomy of [4 levels of Ml Ops](https://learn.microsoft.com/en-us/azure/architecture/example-scenario/mlops/mlops-maturity-model)

Like all definitions, you can find some other definitions for the levels or criterea for automation/manual tasks. Its mostly problem oriented. 

See where you want to be in this level of MlOps. 

### [Prefect](https://prefect.io)

Orchistration of experimentation and deployment - we can turn basic scripts into workflows (Optionally)


### Docker in combination with Fastapi/Flask/Django

Containerisation of a restful API which can be linked with one Prefect, mlflow, and observation tools like Grafana 

Deployment can be done either offline with batch service locally - or online by either being invoked via HTTP (API Gateway on AWS) or via Streaming

Tools to deploy the model include Flask/Django or Fastapi



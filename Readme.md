#  ML Ops Recepies - a small repo containing the learning of Ml OPs

## State of Ml Ops

Read [this](https://becominghuman.ai/no-you-dont-need-mlops-5e1ce9fdaa4b)  article - It summarises if you _really_ need MLOPs quite well

As long as your ML system is simple enough that an ops person can (1) find out when it isn’t working properly, (2) make small changes to it, and (3) redeploy the model, you are achieving the goal of MLOps.

Now, assuming you need Machine Learning in Production to support (automatic) decision making you can automate the whole process of training/testing and deployment 

## Project Design - ML Engineering 

* Learn from experienced ppl to overcome mistakes
* Problem definition -> Right Scope with the right targets defined with also the stakeholders of the OKR in business 
* Model approach: not xgboost ripped of from a poor written blog post that is cherry picked 
  * Invest time into doing the research and the analysis of the data (e.g. also statistical nature)
* Develop a deployment stategy 
* Develop a strategy to store artifacts and track experimentations 


### Communication - Make Demos more often - get SMEs involved 

* Focusing cross-functional team communication on objective, nontechnical, solution-based, and jargon-free speech will aid in creating a collaborative and inclusive environment that ensures an ML project meets its goals.
* Establishing specific milestones for project functionality demonstrations to a broad team of SMEs and internal customers will dramatically reduce rework and unexpected functionality shortcomings in ML projects
* Approaching the complexities of research, experimentation, and prototyping work with the same rigor that is applied to Agile development can reduce the time to arrive at a viable option for development.
* Understanding, defining, and incorporating business rules and expectations early in a project will help ensure that ML implementations are adapted and designed around these requirements, rather than shoehorning them in after a solution is already built. 
* Avoiding discussion about implementation details, esoteric ML-related topics, and explanations about how the internals of an algorithm work will help deliver a clear and focused discussion of the performance of a solution, allowing for creative discourse from all team members.

### Experiment Planning




## Steps in Ml Lifecycle - 

1. Data Collection & Analysis -> Which data do we have ? Which features can we build ?
2. Data Management -> How the data is being ingested into the training/testing step
3. ML Training Pipeline -> Train, Test and Build the models
4. Build and Validate Applications ->  Integrate models and build applications t
5. Performance Evaluation -> See how the product/service evaluates against human testing
6. Measuring Service Level Objectives (SLO's) -> Reliability of the Service (costs/scaling/performance to measure how the service is performing) - Kind of like the KPIs 
7. Launch -> Release of the Software into Prod - Update Monitoring and controlled Rollouts 
8. Monitoring and Feedback Loops - Show when and where the pipeline fails! 
 
### 2 Data Management 

More data and more features -> Usually good idea but also think about the curse of dimensionalities. 

Privace Issues with User data: the data needs to be anonymised in case of linkable personal data

- Could be done with random noise on normal data with a seed only known to the lords of data 
- Could be doen by synthesising data with usual Synthetic data generators
- Could be a highly over engineered GAN 
- Even more sophistication but who needs and would pay for it 
- being able to reliably host data, ingest it and feed it for the model
- ACID rules do not hold compleltely (especially consistency!)
- Data can be either fully from production or be engineered (feature Engineering) -> data versioning with hashing and meta data could be super usefull once it is super dependent on the state of the training data  
 - Prod data can come directly from the db to the API via contract
 - feature engineered data needs to be on time either transformed or stored somwhere (S3 bucket or even locally (cheaper))
 - ETL pipeline and data engineers can play a substatial role in this tastk
- Humans annotating data require their own systems to facilitate rapid, accurate, and verified annotations, which ultimately needs to be integrated into the feature store.
-

#### Tools:

##### [https://www.snorkel.org/get-started/](Snorkel) 

Snorkel is a system for programmatically building and managing training datasets without manual labeling. In Snorkel, users can develop large training datasets in hours or days rather than hand-labeling them over weeks or months.

##### Feast/Tecton

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

###### Other alternatives 

* Redis on Elasticache with Batch processed data 
* Persistent Storage somewhere on a instance -> read/sent on demand


##### [DVC](https://www.dvc.org) - Data Version Control

DVC runs on top of any ml git repo - to store the artifacts we can use any possible stroage provider 

DVC allows to track any of the metrics we want to track for each experiment -> we can also set it back like Git 


### [mlflow](https://mlflow.org)

Experiment tracking and Model registry -> can be linked with a db/data lake/s3 to store models 

Microsoft was so nice to provide a taxonomy of [4 levels of Ml Ops](https://learn.microsoft.com/en-us/azure/architecture/example-scenario/mlops/mlops-maturity-model)

Like all definitions, you can find some other definitions for the levels or criterea for automation/manual tasks. Its mostly problem oriented. 

See where you want to be in this level of MlOps. 

### [Prefect](Prefect)

Orchistration of experimentation and deployment - we can turn basic scripts into workflows (Optionally)


### Docker in combination with Fastapi/Flask/Django

Containerisation of a restful API which can be linked with one Prefect, mlflow, and observation tools like Grafana 

Deployment can be done either offline with batch service locally - or online by either being invoked via HTTP (API Gateway on AWS) or via Streaming

Tools to deploy the model include Flask/Django or Fastapi



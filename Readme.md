#  ML Ops Recepies - a small repo containing the learning of Ml OPs

## State of Ml Ops

Assuming you need Machine Learning in Production to support (automatic) decision making you can automate the whole process of training/testing and deployment 

## Tools:

### Ml flow

Experiment tracking and Model registry -> can be linked with a db/data lake/s3 to store models 

Microsoft was so nice to provide a taxonomy of [4 levels of Ml Ops](https://learn.microsoft.com/en-us/azure/architecture/example-scenario/mlops/mlops-maturity-model)

Like all definitions, you can find some other definitions for the levels or criterea for automation/manual tasks. Its mostly problem oriented. 

See where you want to be in this level of MlOps. 

### Prefect

Orchistration of experimentation and deployment 


### Docker in combination with Fastapi/Flask/Django

Containerisation of a restful API which can be linked with one Prefect, mlflow, and observation tools like Grafana 

Deployment can be done either offline with batch service locally - or online by either being invoked via HTTP (API Gateway on AWS) or via Streaming



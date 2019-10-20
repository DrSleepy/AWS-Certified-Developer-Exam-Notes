# Continuous Integration & Continuous Delivery/Deployment

**Continuous Integration:**

Continuous Integration is about integrating or merging the code changes frequently
at least once per day, enabling multiple devs to work on the same application

**Continuous Delivery:**

Continuous Delivery is all about automating the build, test and deyployment functions

**Continuous Deployment:**

Continuous Deploymenty fully automates the entire release process,
code is deployed into Production as soon as it has successfully passed through the release pipeline

## CodeCommit

- Source conttrol service
- Git repositry system like Github

## CodeBuild

- Compiles source code, runs tests and packages code
- A build management system like Bitbucket pipelines

## CodeDeploy

- Automated deployment to EC2, on premise servers and Lambda
- Helps deploy your code (into AWS services like EC2 instances)

**In-Place deployment approach:**

- Application is stopped, instances are out of service during deployment
- If the instances are behind a load balancer, you can configure the load balancer to stop sending requests to the instances which are being updated
- Also known as a Rolling Update
- Can only be used for EC2 and on-premise servers, not supported for Lambda
- If you need to roll back your changes, the previous version of the application will need to be re-deployed

**Blue-Green deployment approach:** 

- Applcation is not stopped
- New instances are provisioned in seperate, containing the latest code
- "Blue" represents the current environment
- "Green" represents the new environment
- Once the Green instances have been successfully provisioned, the Blue instances will be terminated

**Terminology:**

- Deployment Group: A set of EC2 instance or Lambda functions which a new revision of the software is to be deployed
- Deployment: The process and components used to apply a new revision
- Deployment Configuration: A set of deployment rules as well as success / failure conditions used during a deployment
- AppSpec File: Defines the deployment actions you want AWS CodeDeploy to execute (like bitbucket-pipline.yml)
- Revision: Everything needed to deploy the new version: AppSpec file, application files, executables, config files
- Application: Unique idefntifier of revision, deployment configuration and deployment group are referenced during a deployment

## CodePipeline

- CI/CD workflow tool (build, test, deploy)
- Helps you automate your entire release process

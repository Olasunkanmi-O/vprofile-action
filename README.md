#  VProfile Application – CI/CD with Maven, Sonar, Docker, ECR & Helm (GitOps Workflow)

This repository contains the source code and CI/CD pipeline for the **Vprofile Java application**,(which I forked off an open source repo) built using Maven, tested with SonarCloud, containerized using Docker, and deployed to **Amazon EKS** using **Helm** charts and a GitOps workflow.

---

## Prerequisites
#####
- JDK 11
- Maven 3
- MySQL 8 


## Database
Here,we used Mysql DB 
MSQL DB Installation Steps for Linux ubuntu 14.04:
- $ sudo apt-get update
- $ sudo apt-get install mysql-server

Then look for the file :
- /src/main/resources/db_backup.sql
- db_backup.sql file is a mysql dump file.we have to import this dump to mysql db server
- > mysql -u <user_name> -p accounts < db_backup.sql

---
## Architectural diagram
![](/img/app-deploy.drawio.png)
*NB: Please use this [link](https://github.com/Olasunkanmi-O/vprofile-action/raw/main/img/architectural%20setup.png) to view the other detailed diagram of the infrastructure*

##  Tech Stack Overview

| Tool                  | Purpose                                      |
|-----------------------|----------------------------------------------|
| **Maven (Checkstyle)**| Code linting and formatting              |
| **SonarCloud**        | Static code analysis and quality gate        |
| **Docker**            | Compiling and containerizing the Java app    |
| **Amazon ECR**        | Hosting of container images                  |
| **Helm**              | Kubernetes deployment templating              |
| **GitHub Actions**    | CI/CD pipeline (lint, scan, build, deploy)   |
| **Amazon EKS**        | Kubernetes cluster to run the application    |

---

##  Repository Structure

### Repository Setup 
1.  create a New Repository and clone it into your local machine
2. use the same AWS credentials setup for the IAC-Vprofile project since it is the same project.
3. create an ECR repo and store the URI as a Github secret

### SonarQube Setup
1. log into [sonarcloud](https://www.sonarcloud.io)  
2. generate a token to be used to authenticate your Github account
2. create a new organization and store the key as a Github secret
3. set up the sonargate for the project

## Github Secrets
| Secret Name | Description |
| --- | --- |
| `AWS_ACCESS_KEY_ID` | IAM user access key ID |
| `AWS_SECRET_ACCESS_KEY` | IAM user secret access key |
| `REGISTRY` | uri of your ECR repo |
| `SONAR_ORGANIZATION` | your sonar organization's name |
| `SONAR_PROJECT_KEY` | key to your organization |
| `SONAR_TOKEN` | token for authentication |
| `SONAR_URL` | url of the sonar-cloud |

## Github Action Workflow
1. Directory Structure
- Create a `.github/workflows/` root  directory in the root of your repository.

  ![](/img/workflow.png)

2. Create your workflow and set your environment variables. For this testing phase, I used a manual trigger
sample workflow [here](/files/main.yml)

  ```yaml
  name: vprofile actions
  on: workflow_dispatch
  env: 
      AWS_REGION: us-east-1
      ECR_REPOSIROTY: vprofileapp
      EKS_CLUSTER: vprofile-eks

  ```
3. Confirm through the github actions tab of your repository
![](/img/manual.png)
![](/img/app-workflow.png)





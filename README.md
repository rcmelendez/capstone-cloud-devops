# Cloud DevOps Engineer Capstone project

Capstone project from Udacity's __[Cloud DevOps Engineer
Nanodegree](https://www.udacity.com/course/cloud-dev-ops-nanodegree--nd9991)__ 
program. I developed a Continuous Integration and Continuous Deployment pipeline for a microservices application with a rolling deployment into a Kubernetes cluster. 


## Overview
In this project I applied the skills and knowledge which were developed throughout the Cloud DevOps Nanodegree program. These included:

- Working in AWS
- Using Jenkins to implement Continuous Integration and Continuous Deployment
- Building pipelines
- Working with Ansible and CloudFormation to deploy clusters
- Building Kubernetes clusters
- Building Docker containers in pipelines


## Project Specification
|                        | CRITERIA                                                       | MEETS SPECIFICATIONS                                                                                                                                                                                               |
|------------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| __Set Up Pipeline__        | Create Github repository with project code                     | All project code is stored in a GitHub repository and a link to the repository has been provided for reviewers.                                                                                                    |
|                        | Use image repository to store Docker images                    | The project uses a centralized image repository to manage images built in the project. After a clean build, images are pushed to the repository.                                                                   |
| __Build Docker Container__ | Execute linting step in code pipeline                          | Code is checked against a linter as part of a Continuous Integration step (demonstrated w/ two screenshots).                                                                                                        |
|                        | Build a Docker container in a pipeline                         | The project takes a Dockerfile and creates a Docker container in the pipeline.                                                                                                                                     |
| __Successful Deployment__  | The Docker container is deployed to a Kubernetes cluster       | The cluster is deployed with CloudFormation or Ansible. This should be in the source code of the student’s submission.                                                                                             |
|                        | Use Blue/Green Deployment or a Rolling Deployment successfully | The project performs the correct steps to do a blue/green or a rolling deployment into the environment selected. Student demonstrates the successful completion of chosen deployment methodology with screenshots. |


## Containerized application
For the Docker application, I used an existing Flask app that displays a GIF of a cute cat randomly. Go to [docker-curriculum](https://docker-curriculum.com/#our-first-image) for further details. 


## AWS EKS cluster
Per project directions, I developed an independent Jenkins pipeline that creates an AWS EKS cluster. For the source code, go to the [eks-cluster](https://github.com/rcmelendez/eks-cluster) repo.


## Jenkins pipeline
This is a CI/CD pipeline that deploys a Docker image to a Kubernetes cluster on Amazon EKS using Jenkins. For the Continuous Integration steps, it lints the Dockerfile and performs a security scan using Aqua Microscanner. For Continuous Deployment, it builds the Docker image, verifies if the Docker container responds to an HTTP request, then it pushes the image to Docker Hub. To avoid filling up the disk, it removes the local image. Then, it deploys the image to a AWS EKS cluster. Finally, it updates the pods to use the latest image with no downtime. 

These are all the stages of the pipeline:


## Validation


## License
Project licensed under the terms of the MIT License. See the `LICENSE` file for details.


## Contact
Find me as __rcmelendez__ on [LinkedIn](https://www.linkedin.com/in/rcmelendez/), 
[Medium](https://medium.com/@rcmelendez), and of course [GitHub](https://github.com/rcmelendez/).


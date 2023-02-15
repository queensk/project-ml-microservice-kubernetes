[![CircleCI](https://dl.circleci.com/status-badge/img/gh/queensk/project-ml-microservice-kubernetes/tree/main.svg?style=svg)](https://dl.circleci.com/status-badge/redirect/gh/queensk/project-ml-microservice-kubernetes/tree/main)

## Project Overview

This project involves operationalizing a Machine Learning Microservice API using a pre-trained sklearn model that predicts housing prices in Boston based on various features. The project aims to test the ability to operationalize a Python flask app that serves predictions about housing prices through API calls. The file structure includes the app.py file that contains the Flask app, a model_data folder with the pre-trained model and data files, and several bash scripts (run_docker.sh, run_kubernetes.sh, and make_prediction.sh) that build Docker images and run the application in Docker containers and Kubernetes clusters. The project demonstrates how to containerize and deploy a machine learning application using Docker and Kubernetes, making it scalable and easily accessible via API calls.

### Project Tasks

Your project goal is to operationalize this working, machine learning microservice using [kubernetes](https://kubernetes.io/), which is an open-source system for automating the management of containerized applications. In this project you will:
* Test your project code using linting
* Complete a Dockerfile to containerize this application
* Deploy your containerized application using Docker and make a prediction
* Improve the log statements in the source code for this application
* Configure Kubernetes and create a Kubernetes cluster
* Deploy a container using Kubernetes and make a prediction
* Upload a complete Github repo with CircleCI to indicate that your code has been tested

You can find a detailed [project rubric, here](https://review.udacity.com/#!/rubrics/2576/view).

**The final implementation of the project will showcase your abilities to operationalize production microservices.**

---
## file structure
| File Name         | Description                                                                                 |
|-------------------|---------------------------------------------------------------------------------------------|
| .circleci         | For the CircleCI build server                                                               |
| model_data        | Contains the pretrained sklearn model and housing csv files                                 |
| output_txt_files  | Contains sample output logs from running ./run_docker.sh and ./run_kubernetes.sh            |
| app.py            | Contains the flask app                                                                      |
| Dockerfile        | Contains instructions to containerize the application                                       |
| Makefile          | Contains instructions for environment setup and lint tests                                  |
| requirements.txt  | List of required dependencies                                                               |
| run_docker.sh     | Bash script to build Docker image and run the application in a Docker container             |
| upload_docker.sh  | Bash script to upload the built Docker image to Dockerhub                                   |
| run_kubernetes.sh | Bash script to run the application in a Kubernetes cluster                                  |
| make_prediction.sh| Bash script to make predictions against the Docker container and k8s cluster                |
| README.md         | This README file                                                                            |

## Setup the Environment

* Create a virtualenv with Python 3.7 and activate it. Refer to this link for help on specifying the Python version in the virtualenv. 
```bash
python3 -m pip install --user virtualenv
# You should have Python 3.7 available in your host. 
# Check the Python path using `which python3`
# Use a command similar to this one:
python3 -m virtualenv --python=<path-to-Python3.7> .devops
source .devops/bin/activate
```
* Run `make install` to install the necessary dependencies

### Running `app.py`

1. Standalone:  `python app.py`
2. Run in Docker:  `./run_docker.sh`
3. Run in Kubernetes:  `./run_kubernetes.sh`

### Kubernetes Steps

* Setup and Configure Docker locally
    1. run `make lint` to ensure the docker file is well formatted

    2. `bash run_docker.sh` or `./run_docker.sh` to run the docker container

    3. test endpoint using `./make_prediction.sh`

* Setup and Configure Kubernetes locally
1. stat pods by running `minikube start`

2. upload docker container to the pods using `./run_kubernetes.sh`

* Create Flask app in Container
1. Create a docker container `docker build --tag=ID/path`
2. List docker images `docker image ls`
3. Run docker image `docker run -p 8000:80 ID/path`
* Run via kubectl
Run the Docker Hub container with kubernetes
```
kubectl run ml-api\
	--image=ID/path\
	--port=80 --labels app=ml-api
```

List kubernetes pods `kubectl get pods`

Forward the container port to a host `kubectl port-forward ml-api 8000:80`

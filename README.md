# Udacity - Cloud Developer Nanodegree (Project 4 - k8s, docker, CI/CD)
***


## 1. CI/CD, Github & Code Quality

### 1.1. The project demonstrates an understanding of CI/CD and Github

Please, check the .travis.yml file into project root folder. We have in the file the code below

```yaml
install:
  - docker-compose -f udacity-c3-deployment/docker/docker-compose-build.yaml build --parallel 
  - docker login --username=${DOCKER_USERNAME} --password=${DOCKER_PASSWORD}
  - docker-compose -f udacity-c3-deployment/docker/docker-compose-build.yaml push

# safelist
branches:
  only:
  - master
```

It means when any change is made in the master branch, a new version of docker images is sent to the public repository 
after building. Please, verify the CI/CD building process images in the __./ci-cd screenshots__ folder. 
These new images can be deployed to our cluster


## 2. Container

### 2.1. The app is containerized

Prior execution of the system, you have to:

1. Provide valid AWS credentials to a S3 Bucket. You can use the awscli to set credentials.
2. Define the environment variables to your environment into docker-compose.yaml file to be used by the system. 
(__Look at the docker-compose.yaml file into ./udacity-c3-deployment/docker folder__)

```yaml
    environment:
      POSTGRESS_USERNAME: $POSTGRESS_USERNAME
      POSTGRESS_PASSWORD: $POSTGRESS_PASSWORD 
      POSTGRESS_DB: $POSTGRESS_DB 
      POSTGRESS_HOST: $POSTGRESS_HOST 
      AWS_REGION: $AWS_REGION 
      AWS_PROFILE: $AWS_PROFILE 
      AWS_BUCKET: $AWS_BUCKET
      JWT_SECRET: $JWT_SECRET
      URL: "http://localhost:8100"
```

#### Setup Docker Environment
You'll need to install docker https://docs.docker.com/install/. Open a new terminal within the project directory and run:

**1. Build the images:**

```bash
docker-compose -f docker-compose-build.yaml build --parallel
```

**2. Run the container:**

```bash
docker-compose up
```


### 2.2. The project have public docker images

The Dockerhub images are available in the following links: [Reverse Proxy image](https://hub.docker.com/r/fthiagomedeiros/reverseproxy), [Frontend image](https://hub.docker.com/r/fthiagomedeiros/udacity-frontend), [REST API User](https://hub.docker.com/r/fthiagomedeiros/udacity-restapi-user), [REST API Feed](https://hub.docker.com/r/fthiagomedeiros/udacity-restapi-feed)


### 2.3. The applications runs in a container without errors

To run the application locally, you have to set the environment variables and credentials for access to AWS S3 bucket as shown in
2.1 step.


## 3. Deployment

### 3.1. The application runs on a cluster in the cloud

All the files to deploy in the cloud are located into k8s folder.
Deployments and Services.

backend-feed-deployment.yaml
 
backend-feed-service.yaml

backend-user-deployment.yaml

backend-user-service.yaml

reverseproxy-deployment.yaml

reverseproxy-service.yaml

frontend-deployment.yaml

frontend-service.yaml


The image showing the running pods after the following statement 

```shell script
kubectl get pods
```
is available pods screenshot folder.

You will be able to run using minikube.
Install minikube and run the script deployment.sh located into folder k8s.
Please, provide the secrets and environment variables as necessary into the files **__aws-secret.yaml__** to point to credentials for s3 bucket. I have provided credentials for **__env-configmap.yaml and env-secret.yaml__**.

You should change the bucket name (AWS_BUCKET) in [env-configmap.yaml](https://github.com/fthiagomedeiros/udacity-cloud-project4/blob/master/udacity-c3-deployment/k8s/env-configmap.yaml) and [docker-compose.yaml](https://github.com/fthiagomedeiros/udacity-cloud-project4/blob/master/udacity-c3-deployment/docker/docker-compose.yaml) and credentials for access to S3 bucket in order to have valid credentials to access your s3 bucket



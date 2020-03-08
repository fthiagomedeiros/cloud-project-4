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

1. Copy to the folder ./udacity-c3-deployment/docker/ the file _docker-compose.yaml_ provided into zip file
2. Include AWS credentials to file credentials to allow AWS S3 bucket access. 
**(credentials file is into copied to folder ./udacity-c3-deployment/docker/aws)**

```typescript
export const config = {
  "dev": {
    "username": process.env.POSTGRESS_USERNAME,
    "password": process.env.POSTGRESS_PASSWORD,
    "database": process.env.POSTGRESS_DB,
    "host": process.env.POSTGRESS_HOST,
    "dialect": "postgres",
    "aws_region": process.env.AWS_REGION,
    "aws_profile": process.env.AWS_PROFILE,
    "aws_media_bucket": process.env.AWS_BUCKET,
    "url": process.env.URL
  }
};
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

> _tip_: To facilitate code execution, I have provided the file docker-compose.yaml ans aws credentials 
> file to be changed into the folder _/docker/_


### 2.2. The project have public docker images

The Dockerhub images are available in the following links: [Reverse Proxy image](https://hub.docker.com/r/fthiagomedeiros/reverseproxy), [Frontend image](https://hub.docker.com/r/fthiagomedeiros/udacity-frontend), [REST API User](https://hub.docker.com/r/fthiagomedeiros/udacity-restapi-user), [REST API Feed](https://hub.docker.com/r/fthiagomedeiros/udacity-restapi-feed)


### 2.3. The applications runs in a container without errors

To run the application locally, you have to set some environment variables and credentials for access to AWS S3 resource before run the step 2.1 above.
In order to facilitate the code execution, I have provided the files config.ts that has harcoded the required variables. 

The config.ts files are into the folders _**./udacity-c3-restapi-feed/src/config/config.ts**_ and _**./udacity-c3-restapi-user/src/config/config.ts**_

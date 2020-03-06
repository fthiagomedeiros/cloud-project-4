# Udagram Image Filtering Microservice

Udagram is a simple cloud application developed alongside the Udacity Cloud Engineering Nanodegree. It allows users to register and log into a web client, post photos to the feed, and process photos using an image filtering microservice.

The project is split into three parts:
1. [The Simple Frontend](/udacity-c3-frontend)
A basic Ionic client web application which consumes the RestAPI Backend. 
2. [The RestAPI Feed Backend](/udacity-c3-restapi-feed), a Node-Express feed microservice.
3. [The RestAPI User Backend](/udacity-c3-restapi-user), a Node-Express user microservice.

## Getting Setup

> _tip_: this frontend is designed to work with the RestAPI backends). It is recommended you stand up the backend first, test using Postman, and then the frontend should integrate.

### Installing Node and NPM
This project depends on Nodejs and Node Package Manager (NPM). Before continuing, you must download and install Node (NPM is included) from [https://nodejs.com/en/download](https://nodejs.org/en/download/).

### Installing Ionic Cli
The Ionic Command Line Interface is required to serve and build the frontend. Instructions for installing the CLI can be found in the [Ionic Framework Docs](https://ionicframework.com/docs/installation/cli).

### Installing project dependencies

This project uses NPM to manage software dependencies. NPM Relies on the package.json file located in the root of this repository. After cloning, open your terminal and run:
```bash
npm install
```
>_tip_: **npm i** is shorthand for **npm install**

### Setup Backend Node Environment
You'll need to create a new node server. Open a new terminal within the project directory and run:
1. Initialize a new project: `npm init`
2. Install express: `npm i express --save`
3. Install typescript dependencies: `npm i ts-node-dev tslint typescript  @types/bluebird @types/express @types/node --save-dev`
4. Look at the `package.json` file from the RestAPI repo and copy the `scripts` block into the auto-generated `package.json` in this project. This will allow you to use shorthand commands like `npm run dev`


### Configure The Backend Endpoint
Ionic uses enviornment files located in `./src/enviornments/enviornment.*.ts` to load configuration variables at runtime. By default `environment.ts` is used for development and `enviornment.prod.ts` is used for produciton. The `apiHost` variable should be set to your server url either locally or in the cloud.

***
### Running the Development Server
Ionic CLI provides an easy to use development server to run and autoreload the frontend. This allows you to make quick changes and see them in real time in your browser. To run the development server, open terminal and run:

```bash
ionic serve
```

### Building the Static Frontend Files
Ionic CLI can build the frontend into static HTML/CSS/JavaScript files. These files can be uploaded to a host to be consumed by users on the web. Build artifacts are located in `./www`. To build from source, open terminal and run:
```bash
ionic build
```
***

# Project Rubric (Execution)
***

## 2. Container

### 2.1. The app is containerized

To run the services locally, you have to set the environment variables to be provided to the system.

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

> _tip_: I have provided the file _config.ts_ to be changed into the folder _/src/config_ in both projects. _/udacity-c3-restapi-user/src/config_ and _/udacity-c3-restapi-feed/src/config_


### 2.2. The project have public docker images

The Dockerhub images are available in the following links: [Reverse Proxy image](https://hub.docker.com/r/fthiagomedeiros/reverseproxy), [Frontend image](https://hub.docker.com/r/fthiagomedeiros/udacity-frontend), [REST API User](https://hub.docker.com/r/fthiagomedeiros/udacity-restapi-user), [REST API Feed](https://hub.docker.com/r/fthiagomedeiros/udacity-restapi-feed)


### 2.3. The applications runs in a container without errors

To run the application locally, you have to set some environment variables and credentials for access to AWS S3 resource before run the step 2.1 above.
In order to facilitate the code execution, I have provided the files config.ts that has harcoded the required variables. 

The config.ts files are into the folders _**./udacity-c3-restapi-feed/src/config/config.ts**_ and _**./udacity-c3-restapi-user/src/config/config.ts**_

# Choose the Best Fitting for Your DevOps Plumbing: Red Hat OpenShift CI/CD Pipelines with JFrog Artifactory and Xray

This repository contains the code for the _Choose the Best Fitting for Your DevOps Plumbing: Red Hat OpenShift CI/CD Pipelines with JFrog Artifactory and Xray SwampUp 2021 Session_. This session is jointly presented by Red Hat and JFrog and discusses how to develop a CI/CD pipeline with [OpenShift](https://www.openshift.com/) and [the JFrog Platform](https://jfrog.com/platform/). It contains a npm application, dockerfile and openshift pipeline/tekton pipelines, resources and tasks to build and deploy the application.

## DevOps Pipeline Workflow
![openshift-jfrog-pipeline](https://user-images.githubusercontent.com/6440106/104625814-0700e580-564a-11eb-94af-7e37d6d9b279.png)

## High-level Architecture
![openshift-jfrog-arch](https://user-images.githubusercontent.com/6440106/104613433-137e4180-563c-11eb-8714-2ff424785c8e.png)

# DevOps Pipeline
The build and deployment of our DevOps pipelines is achieved through the use of [OpenShift Pipelines](https://www.openshift.com/learn/topics/pipelines) (Tekton) for CI/CD and the JFrog CLI. The JFrog CLI is used to build and upload the artifacts and the build information. Openshift Pipelines is used to automate this process. The pipeline and the tasks that use the JFrog CLI are defined in [pipeline.yaml](./pipeline.yaml). 

![pipeline](https://user-images.githubusercontent.com/6440106/105406537-68dcc480-5be1-11eb-82a3-c0042b63c1bb.png)

# Applying and Executing the Pipeline

1. Apply the [project-clusterrolebinding](project-clusterrolebinding.yaml) to allow OpenShift Pipelines to use the default ServiceAccount to create K8s resources.

```
kubectl apply -f project-clusterrolebinding.yaml -n demo
```

2. Apply the pipeline YAML with the following command to create the Task and Pipeline resources.

```
kubectl apply -f pipeline.yaml -n demo
```

3. Then create the PipelineRun resource to execute the pipeline. You can use the pipeline-run.yaml as an demo and apply it.

```
kubectl apply -f pipeline-run.yaml -n demo
```

or you can use the OpenShift Pipeline UI to create the PipelineRun resource via Pipeline > Start.

![Pipeline Run](https://user-images.githubusercontent.com/6440106/105402807-b9055800-5bdc-11eb-93b1-36d77d61b302.png)

4. The pipeline creates a [K8s Deployment and a Service](./deployment.yaml) to deploy the application. To view the application, create an OpenShift Route under Networking > Routes. Specify the service as seen here.

![Pipeline Route](https://user-images.githubusercontent.com/6440106/105403178-3fba3500-5bdd-11eb-95a7-2429578f1fd8.png)

5. Click on the URL to view your application!

# The Demo App

<img width="1747" alt="Screen Shot 2021-04-20 at 10 04 19 AM" src="https://user-images.githubusercontent.com/6440106/115436432-d89e2380-a1bf-11eb-9979-0b636f55aa6b.png">

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 10.1.7.

## Build and Run Docker Image Locally

```
$ docker build -t demo-app . 
$ docker run -p 443:443 -p 80:80 docker.io/library/demo-app
```

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `--prod` flag for a production build.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI README](https://github.com/angular/angular-cli/blob/master/README.md).

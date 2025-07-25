# Kubernetes Example
---

This repo contains the scripts to create a cluster on AWS EKS and deploy a docker image of the color-picker app as part of this [repo](https://github.com/SamEdwardsWEG/angular-theme-picker)


## Prerequisutes

1. You must have aws-cli installed on your machine, it can be downloaded from [here](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
2. You must have eksctl installed on your machine, it can be downloaded from [here](https://eksctl.io/installation/)
3. You must have kubectl installed on your machine, it can be downloaded from [here](https://kubernetes.io/docs/tasks/tools/)
4. You must have awscli configured with an access key and the appropriate permissions on AWS

## To create a cluster and deploy an app

Run the following commands

1. Clone this repo and `cd` into the directory
2. `eksctl create cluster -f cluster-config.yaml` (this can take a while to create on AWS so bear with it)
3. `kubectl apply -f ingressclass.yaml`
4. `kubectl create namespace colour-picker --save-config`
5. `kubectl apply -n colour-picker -f deploy.yaml`
6. `kubectl get services -n colour-picker`
7. Copy the EXTERNAL-IP from the above command and paste into browser (if it returns an error, give it a little while and refresh or run `kubectl get deployments -n colour-picker` to check if the deployment is available)

You should be presented with the below

![Screenshot](./screenshot.JPG)

## To update the app

1. Update deploy.yaml (e.g. change the image tag)
2. Run `kubectl apply -n colour-picker -f deploy.yaml`

## To delete the cluster

1. Run `eksctl delete cluster -f ./cluster-config.yaml`

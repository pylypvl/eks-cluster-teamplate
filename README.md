# eks-cluster-teamplate

Here is an example repository that contains configuration which can be used to deploy a Kubernetes EKS cluster.

To run, you need to execute the following commands:

Run terraform init and terraform apply.
Update your kubeconfig to the name of the cluster. In our case, it is the "Gamania-prod" cluster:

aws eks update-kubeconfig --region us-east-1 --name Gamania-prod

All these commands can be executed assuming that you have kubeconfig and AWS CLI installed on your local machine.

This repository contains configurations for the development cluster under the "prod" branch, and configurations for the production cluster under the "prod" branch.

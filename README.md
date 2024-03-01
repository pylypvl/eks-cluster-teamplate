EKS Cluster Template
Here is an example repository that contains configuration which can be used to deploy a Kubernetes EKS cluster.

To run, you need to execute the following commands:

Run terraform init and terraform apply.
Update your kubeconfig to the name of the cluster. In our case, it is the "gamania-dev" cluster:
css
Copy code
aws eks update-kubeconfig --region us-east-1 --name gamania-dev
All these commands can be executed assuming that you have kubeconfig and AWS CLI, along with Docker, installed on your local machine.

This repository contains configurations for the development cluster under the "alpha" branch, and configurations for the production cluster under the "prod" branch.

Also, this repository contains a small Dockerfile, which creates a Docker image for us. Whenever a container is created based on this image, it displays the value "Hello SRE!"

In order to create an image, here are the standard commands:

To pull the image to your local machine:

docker pull vladpylypenko/custom-nginx:latest
I stored the image inside the Docker repo: Vlad Pylypenko Docker Hub Repository.
https://hub.docker.com/repositories/vladpylypenko
To view images, run:

docker images
The following command will help to create a Docker image based on the current Dockerfile:

docker build -t custom-nginx:latest .
The following command will create a Docker container:

docker run -d -p 7777:80 custom-nginx:latest

Note: 7777 is not a mandatory port; it is just an example.

Docker will start a new container based on the custom-nginx:latest image, running the NGINX web server inside it. The container will run in the background, and port 80 of the NGINX server inside the container will be accessible via port 7777 on the host machine.

You can then check the sign "Hello SRE!" when you try to access it at http://localhost:7777/.

Additionally, inside the repository, I have "gamania-dev" Helm charts which contain an updated LoadBalancer service for us.

To expose it, use the following command:


helm install gamania-dev ./gamania-dev --set service.port=80 --set service.targetPort=80 --set service.type=LoadBalancer
Make sure that you are located in the correct directory.

After executing the command, you can check the pods and services deployed on the cluster:


kubectl get pods
kubectl get services
Then, you can retrieve the URL of the load balancer and paste it into a web browser to check the results of the container, which will output "Hello SRE!" since we are still using my custom vladpylypenko/custom-nginx:latest image for this.
# Azure Spring Boot Application and MySQL Deployment on Kubernetes

## Install NGINX Ingress Controller - [View Documentation on GitHub](https://github.com/kubernetes/ingress-nginx)

Step 1: Create the ingress-nginx Namespace

    kubectl create namespace ingress-nginx

Step 2: Install the Ingress Controller

    kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.12.0-beta.0/deploy/static/provider/cloud/deploy.yaml

Step 3: Verify the Installation
Check that the NGINX Ingress Controller is running by verifying the pods and services:

    kubectl get all -n ingress-nginx

That's it! You've installed the NGINX Ingress Controller using kubectl.

## To start the application

Step 1: Apply the deployment files

    kubectl apply -f .

Step 2: List deployment and services

    kubectl get all -A

Step 3: Port forward service to localhost or you can try LoadBalancer

    kubectl port-forward svc/springboot-mysql-aks 8080:8080

Step 4: List ingress

    kubectl get ingress

Step 5: Delete deployment and services

    kubectl delete -f .
    
## Test the Application

To test the application, you can use CURL.

Use the following `CURL` command to create a new "todo" item in the database name demo:

   ```bash
   curl --header "Content-Type: application/json" \
   --request POST \
   --data '{"description":"configuration","details":"congratulations, you have deployed your application correctly!","done": "true"}' \
   http://<loadbalnacer-ip>
  ```
We can all multiple data by using post request

Next, retrieve the data by using a new CURL request
   ```bash
   curl http://<loadbalnacer-ip>
   ```
Replace <loadbalnacer-ip> with the external IP address of the service from the previous step.

## Access Mysql pod

You can use the kubectl exec command to get into the MySQL pod 

pod name : mysql-deployment-1234 

passowrd of DB : password


   ```bash
   kubectl exec -it mysql-deployment-pod-name -- mysql -u root -p
  ```
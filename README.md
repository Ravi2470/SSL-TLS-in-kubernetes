# SSL-TLS-in-kubernetes

### Following command will setup cert-manager in your kubernetes cluster.

kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.11.0/cert-manager.yaml
### We can check the pods and services created by cert-manager by running following command:
Kubectl get all -n cert-manager       


### Following command will setup Nginx ingress controller in your kubernetes cluster.It will create a service with LoadBalancer IP that we will use later.
  
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.0.0/deploy/static/provider/cloud/deploy.yaml

### We can check the pods and services created by ingress controller by running following command:
Kubectl get all -n ingress-nginx
         
### Out of three pods created by ingress-nginx, 1 will be going to be in running state and other two will be going to be in completed state. 


### Following command will setup cluster issuer in our kubernetes cluster and help us to generate TLS/SSL certificate for our domain.We will use Let's Encrypt as CA.You can use other available options as well.
### We need to make changes in this file according to our requirements.

kubectl apply -f cluster-issuer.yml 

### Following command will issue a TLS/SSL certificate for our domain.We need to make changes in it according to our requirements.E.g. Domain name
### Before running this command you need to point your domain to the LoadBalancer IP address of your Ingress controller that was generated earlier.

kubectl apply -f certificate.yml   

### Following command will add TLS/SSL to our domain name. This will also use nginx-ingress controller as proxy in front of our service.
### We need to make changes in this file according to our requirements.E.g. We will add the service name to which we want ingress controller to redirect our user.

kubectl apply -f ingress.yml
        

## Prequest
1. Install Docker
2. Install Docker desktop
3. Install kubectl

## Dockerizing Web application and creating image
1. Go to the specific docker file folder
    ```bash
    cd lovevery/
2. Build docker image from Dockerfile
    ```bash
    docker build -t lovevery-test:v1 . 
3. Check if the image is created 
    ```bash
    docker ps 
4. Run the image and check if it build correctly or not
    ```bash
    docker run -d -p 8000:80 lovevery-test:v1

## Deploy image to kubernetes
1. Make sure kubectl is installed before this step. Go to k8s file folder.
    ```bash
    cd lovevery/
2. Create deployment under default namespace
    ```bash
    kubectl apply -f k8s-deployment.yaml
3. Check for the creation of deployment 
    ```bash
    kubectl get deployment 
4. Check for the creation of replicaset
    ```bash
    kubectl get replicaset 
5. Check for the creation of pods
    ```bash
    kubectl get pods
6. Create service under default namespace
    ```bash
    kubectl apply -f k8s-service.yaml
7. Check for the creation of service
    ```bash
    kubectl get service
8. Loadbalancer service is used in our usecase. check for  external-ip and validate the deployment.
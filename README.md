# **🚀 Kubernetes Container Orchestration**

🛠️ **This repository is used to deploy a microservices application on Kubernetes using Minikube, ensuring proper service communication and configuration.**. 
---

## **📌 Table of Contents**
- [📂 Microservices](#Microservices)
- [📂 k8](#k8)
- [📂 Outputs](#Outputs)
- [🤝 Contributing](#handshake-contributing)
- [📜 License](#scroll-license)

---
## 🔧 Steps to follow to deploy the applications up and running
1. Navigate to the Microservices folder to see the services.
2. Create a Dockerfile to containerize each microservice so they can run consistently in Kubernetes as isolated, portable containers.
3. After the Dockerfile is created successfully, build the Docker images using the following commands
   ```sh
   docker build -t <service-name>:latest ./<service-name>
   ex: docker build -t user-service:latest ./user-service #for user-service
   ```
4. Ensure to build images for all the services and run the below command to make sure the images are created successfully.
   ```sh
   docker images
   ```
5. Make sure to create YAML files to define Kubernetes Deployments and Services, which manage how each microservice is deployed, scaled, and exposed within the cluster, ensuring consistent and automated orchestration.
6. Now, to make sure to have a smooth deployment using Kubernetes, follow the below steps.
    
    1. Run the below command for deployments
       ```sh
       kubectl apply -f path to/deployment folder/
       ex: kubectl apply -f k8/deployment/ 
       ```
   2. You will output steps something like below
      ```sh
      deployment.apps/<service-name> created
      ```
   3. Run the below command for services.
      ```sh
      kubectl apply -f path to/ services folder/
      ex: kubectl apply -f k8/services/
      ```
   4. You will see output something like below.
      ```sh
      service/<service-name> created
      ```
   5. Now follow the steps below to check whether the pods are running as expected. Run the command below to check the status of pods.
      ```sh
      kubectl get pods
      ```
      ![image](https://github.com/user-attachments/assets/71850dea-102b-4b3c-81a0-50ea3e3ad61d)

   6. After running the above command if you face any issue saying "ImagePullBackOff" / "ErrImagePull",
      ```sh
      NAME                      READY   STATUS             RESTARTS   AGE
      <service-name>-image-id   0/1     ImagePullBackOff   0          30s
      ```
      this occurs due to Kubernetes is unable to pull your local Docker images. This happens in Minikube because it uses a separate Docker daemon from your host.
   7. To fix this:
       
       1. Rebuild images inside Minikube's Docker, run the below commands.
          ```sh
          minikube docker-env
          ```
       2. Now rebuild all of the images using the below command.
          ```sh
          docker build -t <service-name>:latest ./<service-name>
          ```
       3. Then reapply the deployments and services again using the commands below.
          ```sh
          kubectl apply -f k8/deployments/
          kubectl apply -f k8/services/
          ```
       4. Now, check again whether the pods are running using:
          ```sh
          kubectl get pods
          ```
7. If the pods are running successfully now run the below commands to port-forward the services(do it in each and separate terminal):
      ```sh
      kubectl port-forward svc/user-service 3000:3000
      kubectl port-forward svc/product-service 3001:3001
      kubectl port-forward svc/order-service 3002:3002
      kubectl port-forward svc/gateway-service 3003:80
      ``` 
## **Microserivces Testing**
1. After the ports are forwarded successfully, test them by using the endpoints below.

   [Gateway-Service](http://localhost:3003/health)
   ![Gateway-service](https://github.com/user-attachments/assets/21ef32ea-a3e1-4104-a2bf-571ee09cfcb9)
   [User-Service](http://localhost:3000/users)
   ![User-service](https://github.com/user-attachments/assets/6330083c-b3f2-4b06-93f2-880f4075791a)
   [Product-Service](http://localhost:3001/products)
   ![Product-service](https://github.com/user-attachments/assets/d8ced4e5-038a-4c60-a45c-8b1410cf04be)
   [Order-Service](http://localhost:3002/orders)
   ![Order-service](https://github.com/user-attachments/assets/a960c499-4208-48f1-a827-9c7274602096)
   [Ingress-/api/users](http://localhost:3003/api/users)
   ![api-users](https://github.com/user-attachments/assets/d5a7b3b4-c428-4898-8c33-b5858c68274c)
   [Ingress-/api/prdoucts](http://localhost:3003/api/products)
   ![api-products](https://github.com/user-attachments/assets/2a25b558-7d8d-4421-8dcf-92ab16fcadc6)
   [Ingress-/api/orders](http://localhost:3003/api/orders)
   ![api-orders](https://github.com/user-attachments/assets/9b2e9087-b020-47b9-b067-fbca21213e33)

## **🤝 Contributing**
🙌 Contributions are welcome! If you have suggestions for improvements:
- Fork this repository.
- Create a new branch (git branch new-branch).
- Commit your changes.(git commit -m "Commit Message")
- Push the code.(git push origin new-branch)
- Submit a pull request.
All contributions must follow standard code formatting and best practices.

## **📜 License**
📄 This repository is licensed under the MIT License. See the LICENSE file for details.

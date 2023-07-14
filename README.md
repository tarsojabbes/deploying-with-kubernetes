# Deploying with Kubernetes

This is a simple example of how to use Kubernetes to deploy applications using its different components (Deployment, Service, Secret and ConfigMap).

Here, we have a MongoDB server and a Mongo Express application that interact with each other. The MongoDB server is set up with an internal service, while the Mongo Express has an external service. To ensure security and good practices, some environmental variables are stored in mongodb-secret.yaml and mongodb-configmap.yaml.

The goal of this repository is to provide a basic template for deploying your application with Kubernetes. You can use it as a starting point or refer to it when you need guidance on how to perform specific tasks.

## How to deploy this application

- Copy the `example.mongodb-secret.yaml` file to `mongodb-secret.yaml` and include your username and password for the MongoDB server

```sh
cp example.mongodb-secret.yaml mongodb-secret.yaml
```
    
- By default, K8s uses Base64 encoded values in Secret, you can run the command below to encode your username and password and paste them in `mongodb-secret.yaml`
```sh
echo -n 'your_username_or_password' | base64
```

- Create the MongoDB Service

```sh
kubectl apply -f mongodb-service.yaml
```

- Create the MongoDB ConfigMap and Secret

```sh
kubectl apply -f mongodb-configmap.yaml
kubectl apply -f mongodb-secret.yaml
```

- Create the MongoDB deployment
```sh
kubectl apply -f mongodb-deployment.yaml
```

- Create the Mongo Express Service
```sh
kubectl apply -f mongoexpress-service.yaml
```

- Create the Mongo Express Deployment
```sh
kubectl apply -f mongoexpress-deployment.yaml
```

- Your Mongo Express application have a service which type is LoadBalancer, so you can access it through your browser. To do so, run:
```sh
kubectl get service
```

You may copy the EXTERNAL-IP and the PORT columns for the `mongo-express-service`. Feel free to modify and customize the deployment files according to your specific requirements.

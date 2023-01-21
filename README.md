
# Keda Java Consumber with RabbitMQ kubernetes cluster

A brief description of what this project does and who it's for

## Install Keda in our cluster using below command
```
kubectl apply -f https://github.com/kedacore/keda/releases/download/v2.0.0/keda-2.0.0.yaml
```
## Install RabbitMQ kubernetes cluster operator
A Kubernetes cluster operator is a specialized type of Kubernetes controller that extends the Kubernetes API to create, configure, and manage instances of a specific application or service on a Kubernetes cluster.<br>
There is a RabbitMQ cluster operator for Kubernetes, which allows you to deploy and manage RabbitMQ clusters on Kubernetes. This operator simplifies the process of creating and managing RabbitMQ clusters on Kubernetes by using Kubernetes resources to declaratively manage the configuration and scaling of RabbitMQ clusters.
```
kubectl apply -f https://github.com/kedacore/keda/releases/download/v2.0.0/keda-2.0.0.yaml
```

## Create java rabbitmq consumer deployment 
```
kubectl apply -f https://raw.githubusercontent.com/913165/rabbitmqexamples/main/java-rabbitmq-consumer.yaml
```

## Create keda scalerobject targeting java rabbitmq consumer deployment 
```
https://raw.githubusercontent.com/913165/rabbitmqexamples/main/keda-java-consumer.yaml
```

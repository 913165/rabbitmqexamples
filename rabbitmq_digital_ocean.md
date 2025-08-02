# RabbitMQ Installation on Digital Ocean Kubernetes

This guide walks you through setting up RabbitMQ on a Digital Ocean Kubernetes cluster with autoscaling enabled.

## Prerequisites

- Digital Ocean account
- kubectl installed on your local machine

## Step 1: Create Kubernetes Cluster

1. Create a Kubernetes cluster in Digital Ocean with autoscale enabled
2. Wait for the cluster to be fully provisioned

## Step 2: Configure kubectl

1. Download the kubeconfig file from your Digital Ocean Kubernetes cluster
2. Place the kubeconfig file in your desired folder (e.g., `C:\do\`)
3. Set the KUBECONFIG environment variable:

```bash
# Windows
set KUBECONFIG=C:\do\k8s-1-33-1-do-2-blr1-1754049835114-kubeconfig.yaml

# Linux/macOS
export KUBECONFIG=/path/to/your/kubeconfig.yaml
```

## Step 3: Install RabbitMQ Operator

Apply the RabbitMQ cluster operator to your Kubernetes cluster:

```bash
kubectl apply -f "https://github.com/rabbitmq/cluster-operator/releases/latest/download/cluster-operator.yml"
```

## Step 4: Deploy RabbitMQ Cluster

Deploy a simple RabbitMQ cluster with service:

```bash
kubectl apply -f "https://raw.githubusercontent.com/913165/rabbitmqexamples/main/simple-rabbitmq-cluster-service.yaml"
```

## Step 5: Access RabbitMQ Management Interface

1. Get your LoadBalancer IP address:
   ```bash
   kubectl get services
   ```

2. Replace `localhost` with your LoadBalancer IP address in the URL:
   ```
   http://YOUR_LOADBALANCER_IP:15672
   ```

## Default Credentials

- **Username:** `guest`
- **Password:** `guest`

## Verification

To verify your RabbitMQ installation is working:

1. Check if pods are running:
   ```bash
   kubectl get pods
   ```

2. Check services:
   ```bash
   kubectl get services
   ```

3. Access the management interface using the LoadBalancer IP and default credentials

## Step 6: Install KEDA (Kubernetes Event-Driven Autoscaler)

KEDA allows your applications to scale based on event sources like RabbitMQ queue length.

### Installing KEDA

1. Add the official KEDA Helm repository:
   ```bash
   helm repo add kedacore https://kedacore.github.io/charts  
   helm repo update
   ```

2. Install KEDA using Helm 3:
   ```bash
   helm install keda kedacore/keda --namespace keda --create-namespace
   ```

3. Verify KEDA installation:
   ```bash
   kubectl get pods -n keda
   ```

This command installs KEDA in a dedicated namespace (`keda`). You can customize the installation by passing additional configuration values with `--set`, allowing you to adjust parameters like replica counts, scaling metrics, or logging levels.

## Notes

- Make sure your Digital Ocean LoadBalancer is properly configured to allow traffic on port 15672
- Consider changing default credentials for production environments
- The autoscale feature will automatically adjust the number of nodes based on resource usage
- KEDA enables event-driven autoscaling based on RabbitMQ queue metrics and other event sources

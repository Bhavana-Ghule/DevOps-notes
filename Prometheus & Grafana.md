<img width="1358" height="741" alt="image" src="https://github.com/user-attachments/assets/852907ac-4ba0-43f2-bcd6-669df7b63a45" />


### What is Prometheus?
- Prometheus is an open-source monitoring and alerting tool used to collect, store, and query metrics from systems, applications, Jenkins, Kubernetes, and other services.
- Prometheus collects and stores monitoring data.

### What is Grafana?
- Grafana visualization and dashboard tool.
- Prometheus stores metrics, but Grafana helps humans understand them visually.
- Grafana displays that data in dashboards

### What is Helm?
- Helm is a package manager for Kubernetes.
- You already know how we deploy applications in Kubernetes using YAML files:
Deployment
Service
ConfigMap
Secret
PersistentVolumeClaim
StatefulSet
- Imagine installing Prometheus manually. You may need to manage many Kubernetes YAML resources and configurations.
- Helm simplifies this.
- Instead of manually creating many YAML files, you can install a packaged application using a Helm chart.

### How it start?
1. first of all you need to create an cluster in eks
2. so you need required installation like kind, kubectl, docker, eksctl, and further
####  Install kubectl
`kubectl` is a command-line tool used to communicate with and manage Kubernetes clusters.
```bash
sudo apt update
sudo apt install curl -y
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client
```
## 1.4 Install Helm

Helm is a package manager for Kubernetes. It helps install and manage applications using Helm charts.

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3

chmod 700 get_helm.sh

./get_helm.sh

helm version
```

## 1.5 Install kind (Optional)

`kind` is used to create local Kubernetes clusters using Docker containers.

**Note:** kind is optional for this EKS setup. You do not need kind to create an AWS EKS cluster.

```bash
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/latest/kind-linux-amd64

chmod +x ./kind

sudo mv ./kind /usr/local/bin/kind

kind version
```

---

# 2. Configure AWS Credentials

Check AWS CLI:

```bash
aws --version
```

Check AWS configuration:

```bash
aws configure list
```

Verify AWS identity:

```bash
aws sts get-caller-identity
```

> The EC2 instance must have an IAM role with the required permissions to create EKS clusters and associated AWS resources.

---

# 3. Create EKS Cluster Using eksctl

Create an EKS cluster with two worker nodes.

```bash
eksctl create cluster \
  --name project-cluster \
  --region us-east-1 \
  --node-type t3.medium \
  --nodes 2 \
  --nodes-min 2 \
  --nodes-max 2
```

This command creates:

- EKS cluster
- Managed worker node group
- Default networking resources
- Kubernetes configuration for kubectl

## 3.1 Verify EKS Cluster

```bash
eksctl get cluster --region us-east-1
```

## 3.2 Check Kubernetes Context

```bash
kubectl config current-context
```

## 3.3 Check Worker Nodes

```bash
kubectl get nodes -o wide
```

## 3.4 Check System Pods

```bash
kubectl get pods -n kube-system
```

---

# 4. Add Prometheus Community Helm Repository

Add the Prometheus Community repository:

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
```

Update Helm repositories:

```bash
helm repo update
```

Verify repository:

```bash
helm repo list
```

---

# 5. Create Monitoring Namespace

Create a separate namespace for monitoring resources.

```bash
kubectl create namespace monitoring
```

Verify namespace:

```bash
kubectl get namespaces
```

---

# 6. Install Prometheus and Grafana Using Helm

Install the `kube-prometheus-stack` Helm chart.

This chart installs multiple monitoring components, including:

- Prometheus
- Grafana
- Alertmanager
- Node Exporter
- Kube State Metrics
- Prometheus Operator

```bash
helm install monitoring prometheus-community/kube-prometheus-stack \
  --namespace monitoring
```

## 6.1 Verify Helm Installation

```bash
helm list -n monitoring
```

## 6.2 Check Monitoring Pods

```bash
kubectl get pods -n monitoring
```

## 6.3 Check Monitoring Services

```bash
kubectl get svc -n monitoring
```

## 6.4 Check Prometheus Endpoints

```bash
kubectl get endpoints monitoring-kube-prometheus-prometheus -n monitoring
```

## 6.5 Check Grafana Service

```bash
kubectl get svc monitoring-grafana -n monitoring
```

---

# 7. Retrieve Grafana Admin Password

The default Grafana username is:

```text
admin
```

Retrieve the generated password from the Kubernetes Secret:

```bash
kubectl get secret monitoring-grafana -n monitoring \
  -o jsonpath="{.data.admin-password}" | base64 --decode

echo
```

Use the retrieved password to log in to Grafana.

**Important:** Do not upload your actual Grafana password or Kubernetes Secret values to GitHub.

---

# 8. Port Forwarding

Port forwarding creates a temporary connection between a port on the EC2 instance and a Kubernetes service.

## 8.1 Prometheus Port Forwarding

Open Terminal 1 and run:

```bash
kubectl port-forward -n monitoring \
  svc/monitoring-kube-prometheus-prometheus \
  9090:9090 \
  --address 0.0.0.0
```

Expected output:

```text
Forwarding from 0.0.0.0:9090 -> 9090
```

Keep this terminal running.

## 8.2 Grafana Port Forwarding

Open another SSH terminal and run:

```bash
kubectl port-forward -n monitoring \
  svc/monitoring-grafana \
  3000:80 \
  --address 0.0.0.0
```

Expected output:

```text
Forwarding from 0.0.0.0:3000 -> 3000
```

Keep this terminal running too.

**Note:** Port-forward commands remain active and do not return to the command prompt until stopped using `Ctrl + C`. This is normal.

---

# 9. Configure EC2 Security Group

To access Grafana and Prometheus through the EC2 public IP, configure inbound rules in the EC2 Security Group.

Navigate to:

```text
AWS Console
    |
    v
EC2
    |
    v
Instances
    |
    v
Select EC2 Instance
    |
    v
Security
    |
    v
Security Groups
    |
    v
Edit Inbound Rules
```

Add the following rules:

| Type | Protocol | Port | Source |
|---|---|---|---|
| Custom TCP | TCP | 3000 | My IP |
| Custom TCP | TCP | 9090 | My IP |

> Security Note: Restrict access to your own IP. Do not expose monitoring ports publicly using `0.0.0.0/0` for this learning setup.

---

# 10. Access Grafana and Prometheus Through Browser

Get the EC2 public IP:

```bash
curl -s https://checkip.amazonaws.com
```

Suppose the public IP is:

```text
3.88.233.225
```

## 10.1 Prometheus URL

```text
http://3.88.233.225:9090
```

## 10.2 Grafana URL

```text
http://3.88.233.225:3000
```

## 10.3 Grafana Login Credentials

```text
Username: admin
Password: Retrieved from Kubernetes Secret
```

Replace the example IP with your current EC2 public IP.

---

# 11. Verify Monitoring Components

## Check All Monitoring Pods

```bash
kubectl get pods -n monitoring
```

## Check All Monitoring Services

```bash
kubectl get svc -n monitoring
```

## Check Deployments

```bash
kubectl get deployments -n monitoring
```

## Check StatefulSets

```bash
kubectl get statefulsets -n monitoring
```

## Check Prometheus Logs

```bash
kubectl logs -n monitoring <prometheus-pod-name>
```

## Check Grafana Logs

```bash
kubectl logs -n monitoring <grafana-pod-name>
```

---

# 12. Basic Prometheus Query

Open the Prometheus web interface.

Enter the following query:

```promql
up
```

This shows the status of monitored targets.

- `1` means the target is up.
- `0` means the target is down.

---

# 13. Cleanup Resources

## Uninstall Monitoring Helm Release

```bash
helm uninstall monitoring -n monitoring
```

## Delete Monitoring Namespace

```bash
kubectl delete namespace monitoring
```

## Delete EKS Cluster

```bash
eksctl delete cluster \
  --name project-cluster \
  --region us-east-1 \
  --wait
```

> AWS charges may apply for EKS and associated resources. Delete resources when they are no longer required.

---

# 14. Important Concepts

| Component | Purpose |
|---|---|
| kubectl | Communicates with Kubernetes |
| eksctl | Creates and manages EKS clusters |
| kind | Creates local Kubernetes clusters |
| Helm | Installs and manages Kubernetes applications |
| EKS | Managed Kubernetes service provided by AWS |
| Prometheus | Collects and stores monitoring metrics |
| Grafana | Visualizes metrics using dashboards |
| Node Exporter | Exposes Linux node metrics |
| Kube State Metrics | Exposes Kubernetes object information |
| Alertmanager | Handles alerts generated by Prometheus |
| Port Forwarding | Temporarily forwards a local port to a Kubernetes resource |
| ClusterIP | Exposes a service internally within the Kubernetes cluster |


   

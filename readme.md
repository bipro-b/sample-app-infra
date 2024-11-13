# Argo CD Installation and Setup on Local Kubernetes Cluster and Connecttion Argo CD to Infrastructure Repository

This guide provides instructions to set up Argo CD on a local Kubernetes cluster (using Minikube) and access its UI to manage deployments.
Here’s a README.md file that documents the steps to install Argo CD on a local Kubernetes cluster, expose the UI, and log in:

# Argo CD Installation and Setup on Local Kubernetes Cluster

This guide provides instructions to set up Argo CD on a local Kubernetes cluster (using Minikube) and access its UI to manage deployments.

## Prerequisites

- A local Kubernetes cluster (e.g., Minikube, Kind, or k3s)
- `kubectl` configured to interact with your cluster

## Step 1: Start the Kubernetes Cluster

Ensure your local Kubernetes cluster is up and running. For example, if using Minikube:

```bash
minikube start
Step 2: Install Argo CD
Create a namespace for Argo CD:

kubectl create namespace argocd
Install Argo CD by applying the official manifest:

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
This command deploys all Argo CD components in the argocd namespace.

Verify that Argo CD components are running:

kubectl get pods -n argocd
You should see output similar to this:

NAME                                                READY   STATUS            RESTARTS   AGE
argocd-application-controller-0                     1/1     Running           0          5m58s
argocd-applicationset-controller-7c77597d54-c84vs   1/1     Running           0          6m4s
argocd-dex-server-5d86b78484-5w48x                  0/1     PodInitializing   0          6m4s
argocd-notifications-controller-78f5bf5947-hjd56    1/1     Running           0          6m4s
argocd-redis-757c9855f5-shwz4                       1/1     Running           0          6m4s
argocd-repo-server-75c657669b-7mkgg                 1/1     Running           0          6m2s
argocd-server-7bbfdb874-2s5pr                       1/1     Running           0          6m1s
Step 3: Expose the Argo CD UI
To access the Argo CD UI, forward the Argo CD server service to a local port:

kubectl port-forward svc/argocd-server -n argocd 8080:443
This command forwards traffic from localhost:8080 to the Argo CD server.

Step 4: Access the Argo CD UI
Open your web browser and go to https://localhost:8080.
You may need to accept the self-signed certificate warning to proceed.
Step 5: Log in to Argo CD
Retrieve the initial password for the admin user:

kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 -d
In this example, the initial password is:

NR4-Zy-rG7HEx4QA
Log in using the following credentials:

Username: admin
Password: NR4-Zy-rG7HEx4QA (or the password obtained above)


![Connection Argo CD to Infrastructure Repository](https://github.com/bipro-b/sample-app-infra/blob/main/sample-app/images/arg.png?raw=true)



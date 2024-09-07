# Saleor Platform Deployment on Google Kubernetes Engine (GKE)

This repository contains the necessary configuration files and instructions for deploying the Saleor platform on Google Kubernetes Engine (GKE). The deployment includes multiple components such as the API, Storefront, Dashboard, PostgreSQL, and Redis.

## Overview
This setup deploys the Saleor platform using Kubernetes on GKE, leveraging cloud-native tools for scalability, reliability, and ease of management. The deployment consists of the following services:

- **Saleor API**: Backend for the Saleor platform.
- **Mailpit**: The default communication through mails for the e-commerce site.
- **Saleor Dashboard**: Admin interface for managing the Saleor platform.
- **PostgreSQL**: Managed database for data storage.
- **Redis**: In-memory data store for caching and message brokering.

## Prerequisites

Before you begin, ensure you have:

- **A Google Cloud Platform (GCP) account**: Make sure your GCP account has billing enabled.
- **Google Cloud SDK**: Installed and authenticated. Follow the instructions [here](https://cloud.google.com/sdk) to install and configure the Google Cloud SDK.
- **kubectl CLI**: Installed. You can install `kubectl` following the instructions [here](https://kubernetes.io/docs/tasks/tools/).
- **Basic knowledge of Kubernetes and GKE**: Familiarity with Kubernetes concepts and GKE is recommended for managing the deployment.
- **Trivy**: Security measure to scan the image vulnerabilities.Follow the instructions [here](https://aquasecurity.github.io/trivy/v0.18.3/installation/) to install trivy on your pc.

## Setup

1. Clone the Repository

```bash
git clone https://github.com/rossan/saleor-platform.git
cd saleor-platform

```
2. Create GKE Cluster

```bash
gcloud container clusters create-auto saleor-cluster-1 \
--location=us-central1

```

3.Get authentication credentials for the cluster

```bash 
gcloud container clusters get-credentials saleor-cluster-1 \
--location us-central1
```

## Deployment

- **Deploy Saleor Services,Postgres and Redis**
```bash
kubectl apply -f deployment.yaml
```

## Usage

```python
kubectl get services
```

### Access the services

- **Saleor Dashboard**: <http://34.69.42.253/9002>
- **Saleor API**: <http://34.44.12.9/8000>
- **Mailpit**: <http://34.41.244.164/8025>
- **Postgres**: <ClusterIP:5432>
- **Redis**: <ClusterIP:6379>

## Troubleshooting

- **Check Pod and Service Status**
```bash
kubectl get pods -n saleor
kubectl get services
```
- **Check logs of pods**
```bash
kubectl logs <pod-name> -n saleor

```

## Scan Vulnerability

```bash
trivy image <your image to be scanned>
```

## Contributing

Pull requests are welcome. For major changes, please open an issue first
to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

Disclaimer: Everything you see here is open and free to use as long as you comply with the license. There are no hidden charges. We promise to do our best to fix bugs and improve the code.

Some situations do call for extra code; we can cover exotic use cases or build you a custom e-commerce appliance.
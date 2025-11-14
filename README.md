# Three-Tier Application Infrastructure on Google Cloud Platform

## Overview

This repository contains Infrastructure as Code (IaC) for deploying a scalable three-tier application architecture on Google Cloud Platform. The project demonstrates modern cloud-native practices including automated infrastructure provisioning, containerized applications, and CI/CD pipelines.

## Architecture

The solution implements a classic three-tier architecture pattern:

### 1. Presentation Tier
- NGINX-based frontend serving static content
- WordPress web interface
- Exposed via Kubernetes Ingress with path-based routing

### 2. Application Tier
- Go-based backend service running as DaemonSet
- WordPress application server
- Deployed on Google Kubernetes Engine (GKE)

### 3. Data Tier
- MySQL database for WordPress
- Persistent storage for application data
- Deployed as StatefulSet in Kubernetes

## Technology Stack

- **Infrastructure Provisioning**: Terraform
- **Container Orchestration**: Google Kubernetes Engine (GKE)
- **Compute**: Google Compute Engine (GCE)
- **Networking**: Custom VPC with subnets and firewall rules
- **CI/CD**: Google Cloud Build
- **State Management**: Google Cloud Storage (GCS) backend
- **Containerization**: Docker

## Project Structure

```
.
├── main.tf                 # Root module orchestrating infrastructure
├── variables.tf            # Variable definitions
├── terraform.tfvars        # Variable values (not tracked in git)
├── provider.tf             # GCP provider configuration
├── backend.tf              # Terraform state backend configuration
├── cloudbuild.yaml         # CI/CD pipeline definition
├── modules/
│   ├── network/            # VPC, subnets, and firewall rules
│   ├── gke/                # Kubernetes cluster configuration
│   └── gce/                # Compute instance provisioning
├── docker/
│   ├── hello-frontend/     # Frontend application container
│   ├── hello-backend/      # Backend service container
│   ├── wordpress/          # WordPress container
│   └── wordpress-mysql/    # MySQL database container
└── yaml-gke/
    ├── hello-app/          # Hello app Kubernetes manifests
    ├── wordpress/          # WordPress Kubernetes resources
    └── ingress.yaml        # Ingress controller configuration
```

## Key Features

### Infrastructure as Code
- Fully automated infrastructure provisioning using Terraform
- Modular design for reusability and maintainability
- Parameterized configuration for different environments

### Networking
- Custom VPC with configurable subnet ranges
- Firewall rules for SSH and HTTP access
- Private GKE cluster option with authorized networks
- Network isolation and security controls

### Kubernetes Configuration
- Auto-scaling node pools with configurable min/max nodes
- Support for preemptible nodes for cost optimization
- Node auto-repair and auto-upgrade capabilities
- Multiple node pool configurations

### CI/CD Pipeline
- Automated Terraform workflow (init, validate, plan, apply)
- Automatic Kubernetes deployment
- Integration with Google Cloud Build
- Infrastructure and application deployment in single pipeline

### High Availability
- Multi-zone GKE cluster deployment
- Auto-scaling capabilities
- Self-healing infrastructure with auto-repair
- Load balancing via Kubernetes Ingress

## Deployment

The deployment is fully automated through Cloud Build:

1. **Infrastructure Provisioning**: Terraform creates VPC, subnets, GKE cluster, and GCE instances
2. **Application Deployment**: Kubernetes manifests deploy containerized applications
3. **Ingress Configuration**: Routes are configured for external access

### Routing
- `/hello` - Routes to the hello frontend application
- `/wordpress` - Routes to the WordPress application

## Security Considerations

- Private cluster configuration support
- Master authorized networks for API server access
- Firewall rules for controlled ingress
- Service accounts with least privilege access
- SSH access control via firewall rules

## Scalability

The architecture supports horizontal scaling through:
- GKE node pool autoscaling
- Kubernetes HorizontalPodAutoscaler ready
- Regional deployment for high availability
- Configurable node counts and machine types

## Configuration

Key configurable parameters include:
- GCP project and region
- VPC and subnet CIDR ranges
- GKE cluster version and node pool specifications
- Machine types and disk sizes
- Autoscaling thresholds
- Private/public cluster configuration

## Prerequisites

- Google Cloud Platform account
- Terraform >= 1.0.0
- kubectl CLI
- gcloud CLI
- Appropriate GCP IAM permissions

## Use Cases

This template is suitable for:
- Development and testing environments
- Learning cloud-native architecture patterns
- Proof-of-concept deployments
- Microservices architecture foundation
- CI/CD pipeline demonstration

## Cost Optimization

The infrastructure includes cost-saving features:
- Support for preemptible nodes
- Configurable machine types
- Autoscaling to match demand
- Resource tagging and labeling

## Future Enhancements

Potential improvements:
- Multi-region deployment
- Advanced monitoring and logging
- Service mesh integration
- GitOps workflow with ArgoCD
- Enhanced security with Binary Authorization
- Database replication and backup automation

## License

This project is available as a template for educational and professional development purposes.

## Contact

For questions or collaboration opportunities, please reach out through GitHub.
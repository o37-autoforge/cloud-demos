# Sample Cloudscript Code

This repository contains three examples of infrastructure configurations using Cloudscript to simplify the deployment process for cloud-based applications. Each example includes:

1. The `.cloud` code, located in the `cloud` folder.
2. Additional files required by the `.cloud` code, such as configuration files, stored in the same `cloud` folder.
3. The generated Infrastructure-as-Code (IaC) output in the `IaC` folder.

## Examples

### 1. AWS VPC, EKS Cluster, and Containerized Web App
- **Code Location**: `sample_cloud/sample1/cloud/main.cloud`
- **Description**:
  - Configures an AWS-based infrastructure with a VPC, subnets, an Internet Gateway, and a route table.
  - Provisions an EKS cluster for Kubernetes-based container orchestration.
  - Deploys a t2.micro EC2 instance pre-configured with NGINX.
  - Includes a Kubernetes Deployment with 3 replicas of an NGINX-based containerized web application.
  - Auto-scaling is configured with a Network Load Balancer (NLB) for traffic distribution.

#### Special Notes:
- The `.cloud` file in `sample1/cloud/main.cloud` references additional files such as `role.json` using the `file("role.json")` function.
- For example:
  ```plaintext
  iam "eks_cluster" {
      assume_role_policy = file("role.json")
  }
  ```
- This referencing approach avoids hardcoding the file content into the `.cloud` code. Instead, the file content is automatically parsed and included during conversion, as seen in the IaC folder for sample1.
- Ensure that referenced files like `role.json` are placed in the same `cloud` folder to allow seamless conversion.

---

### 2. GCP GKE Cluster with CronJob Container
- **Code Location**: `sample_cloud/sample2/cloud/main.cloud`
- **Description**:
  - Configures a GKE cluster with a primary node pool.
  - Deploys a MySQL server instance on a standalone compute instance.
  - Includes a CronJob container for regular database backups and an NGINX-based admin tool for internal communication.
  - Features Kubernetes-based auto-scaling and seamless database management.

---

### 3. Azure Storage, VM, and ConfigMap
- **Code Location**: `sample_cloud/sample3/cloud/main.cloud`
- **Description**:
  - Configures Azure infrastructure with a storage account for file and data storage.
  - Deploys a virtual machine (VM) pre-configured with prerequisites for hosting an application.
  - Uses a Kubernetes ConfigMap to store application configuration settings.
  - Includes a one-time setup job container for initialization tasks.

---

## Folder Structure
Each example is structured as follows:
- **`cloud` folder**:
  - Contains the `.cloud` code and any additional files referenced by the `.cloud` code.
- **`IaC` folder**:
  - Contains the Infrastructure-as-Code (IaC) output generated from the `.cloud` code.


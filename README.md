# **🚀 Deploying Super Mario on AWS EKS using Terraform**  

Super Mario is a legendary game we all cherish! In this project, we will deploy **Super Mario** on **Amazon EKS (Elastic Kubernetes Service)** using **Terraform** and manage infrastructure with AWS resources.  

![Super Mario](https://imgur.com/Njqsei9.gif)  

---

## 📌 **Project Overview**

This project provisions an **EKS cluster** on AWS and deploys the **Super Mario game** using **Terraform** and **Kubernetes manifests**. The deployment includes:

- ✅ **Amazon EKS Cluster** (v1.29) with latest features
- ✅ **Terraform Infrastructure as Code** (v1.8+)
- ✅ **Kubernetes Deployment & Service** with best practices
- ✅ **AWS S3 Backend** for Terraform state management
- ✅ **IAM roles & policies** with least-privilege access
- ✅ **CloudWatch logging** and monitoring
- ✅ **Horizontal Pod Autoscaling** for automatic scaling
- ✅ **Network policies** for enhanced security
- ✅ **ServiceMonitor** for Prometheus integration
- ✅ **AWS Load Balancer Controller** support
- ✅ **Health checks** and rolling updates

---

## **📁 Project Structure**  

```bash
📂 DEPLOYMENT-OF-SUPER-MARIO
│── 📂 EKS-TF               # Terraform configuration files for AWS EKS
│   ├── backend.tf          # S3 backend for Terraform state management
│   ├── main.tf             # AWS EKS Cluster and Node Group definition
│   ├── provider.tf         # AWS provider configuration
│   ├── variables.tf        # Input variables for configuration
│   ├── outputs.tf          # Output values after deployment
│   ├── terraform.tfvars.example # Example configuration file
│   ├── deployment.yaml     # Kubernetes Deployment for Super Mario
│   ├── service.yaml        # Kubernetes Service for exposing Super Mario app
│   ├── horizontal-pod-autoscaler.yaml  # HPA for automatic scaling
│   ├── network-policy.yaml # Network security policies
│   └── service-monitor.yaml # Prometheus monitoring configuration
│── 📄 README.md            # Project documentation
```

---

## **📌 Prerequisites**  

Before proceeding, ensure you have the following installed:

- ✅ **Terraform** (>=1.8.0)  
- ✅ **AWS CLI** (Configured with proper credentials)  
- ✅ **kubectl** (For managing Kubernetes resources)  
- ✅ **Docker** (For containerization)  
- ✅ **AWS Key Pair** named `eks-key` (for node access)  

---

## **🛠️ Setup & Deployment**  

### **1️⃣ Clone the Repository**  

```bash
git clone <your-repository-url>
cd <your-repository-name>/EKS-TF
```

### **2️⃣ Configure Terraform Variables**  

Copy the example variables file and customize as needed:

```bash
cp terraform.tfvars.example terraform.tfvars
# Edit terraform.tfvars with your preferred configuration
```

**Cost Optimization Tips:**
- Use `t3.small` instead of `t3.medium` for lower cost
- Set `desired_size = 1` and `max_size = 2` for development
- Reduce `disk_size` to 20GB if storage requirements are low
- Set `log_retention_days` to 7 for production or 3 for development

### **3️⃣ Initialize & Apply Terraform**  

```bash
terraform init      # Initialize Terraform backend
terraform plan      # Preview infrastructure changes
terraform apply -auto-approve  # Deploy to AWS
```

### **4️⃣ Configure Kubernetes Context**  

```bash
aws eks update-kubeconfig --name EKS_CLOUD --region ap-south-1
```

### **5️⃣ Deploy Super Mario Application**  

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f horizontal-pod-autoscaler.yaml
kubectl apply -f network-policy.yaml
# Optional: Apply if you have Prometheus installed
kubectl apply -f service-monitor.yaml
```

### **6️⃣ Access the Application**  

Once deployed, get the external LoadBalancer URL:  

```bash
kubectl get services mario-service
```

Access **Super Mario** in your browser using the displayed URL.

### **7️⃣ Monitor the Deployment**  

```bash
# Check deployment status
kubectl get deployment mario-deployment

# Check pods
kubectl get pods -l app=mario

# Check HPA status
kubectl get hpa mario-hpa

# Check logs
kubectl logs -l app=mario --tail=50

# Check autoscaling events
kubectl describe hpa mario-hpa
```

---

## **🎯 Project Highlights**

- **AWS EKS v1.29**: Latest managed Kubernetes cluster with enhanced features  
- **Terraform v1.8+**: Modern Infrastructure as Code with improved provider versions  
- **Kubernetes Best Practices**: Security contexts, resource limits, and health checks  
- **AWS S3 Backend**: Remote state management with DynamoDB locking  
- **CloudWatch Logging**: Centralized log collection and monitoring  
- **Auto Scaling**: Horizontal Pod Autoscaler for dynamic resource management  
- **Network Security**: Network policies for traffic control  
- **Load Balancer**: NLB with health checks and session affinity  
- **Monitoring Ready**: Prometheus integration via ServiceMonitor  
- **Security Hardened**: IAM roles with least-privilege access  

---

## **� Configuration Details**

### **EKS Cluster Configuration**
- **Version**: 1.29 (Latest stable)
- **Node Group**: t3.medium instances with 30GB disk
- **Scaling**: 1-4 nodes with desired size of 2
- **Logging**: All control plane logs enabled
- **Security**: Private and public endpoint access

### **Kubernetes Resources**
- **Replicas**: 3 pods with auto-scaling up to 10
- **Resources**: CPU requests 100m, limits 500m; Memory requests 128Mi, limits 512Mi
- **Health Checks**: Liveness, readiness, and startup probes
- **Security**: Security contexts and capability dropping

### **Monitoring & Observability**
- **CloudWatch**: 14-day log retention
- **Prometheus**: Ready for metrics collection
- **HPA**: CPU and memory-based scaling
- **Network Policies**: Traffic control and security

### **Cost Optimization**
- **On-Demand Instances**: Predictable pricing
- **Auto Scaling**: Scale down during low traffic
- **Resource Limits**: Prevent resource over-allocation
- **Log Retention**: 14-day retention to manage storage costs  

---

## **🔗 Resources & Documentation**

- **Terraform Docs**: [https://developer.hashicorp.com/terraform/docs](https://developer.hashicorp.com/terraform/docs)  
- **AWS EKS Docs**: [https://docs.aws.amazon.com/eks/latest/userguide](https://docs.aws.amazon.com/eks/latest/userguide)  
- **Kubernetes Docs**: [https://kubernetes.io/docs/home/](https://kubernetes.io/docs/home/)  
- **AWS Load Balancer Controller**: [https://kubernetes-sigs.github.io/aws-load-balancer-controller/](https://kubernetes-sigs.github.io/aws-load-balancer-controller/)  
- **Prometheus Monitoring**: [https://prometheus.io/docs/](https://prometheus.io/docs/)  

---

## **📢 Credits & Acknowledgments**  

This project demonstrates real-world **DevOps practices** using AWS, Terraform, and Kubernetes.  

🚀 *Happy Gaming & DevOps-ing!* 🎮

---

## 🤝 **Contributing**  

Contributions are welcome! If you'd like to improve this project, feel free to submit a pull request.  

---

## **Hit the Star!** ⭐

**If you find this repository helpful and plan to use it for learning, please give it a star. Your support is appreciated!**
## 🛠️ **Author & Community**  

This project demonstrates **DevOps practices** using AWS, Terraform, and Kubernetes.  

---

### 📧 **Connect:**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/your-profile) [![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/your-username)  [![Dev.to](https://img.shields.io/badge/Dev.to-0A0A0A?style=for-the-badge&logo=dev.to&logoColor=white)](https://dev.to/your-username) [![Hashnode](https://img.shields.io/badge/Hashnode-2962FF?style=for-the-badge&logo=hashnode&logoColor=white)](https://hashnode.com/@your-username)  

---

### 📢 **Stay Connected**  

![Follow Me](https://imgur.com/2j7GSPs.png)

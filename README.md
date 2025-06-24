# AWS ECS Deployment with GitHub Actions CI/CD

## 🚀 Project Overview

This project demonstrates how to deploy a web application to AWS ECS (Elastic Container Service) using GitHub Actions for Continuous Deployment. The setup creates a fully automated pipeline that builds, containerizes, and deploys your application to AWS cloud infrastructure.

## 🏗️ Architecture

```
Developer Code → GitHub → GitHub Actions → Docker Build → AWS ECR → AWS ECS → Live Website
```

### Key Components:
- **Source Code**: Travel website (Tejas Travels)
- **Container**: Docker with Nginx
- **Cloud Storage**: AWS ECR (Elastic Container Registry)
- **Cloud Hosting**: AWS ECS Fargate
- **Automation**: GitHub Actions CI/CD
- **Infrastructure**: Terraform (Infrastructure as Code)

## 📁 Project Structure

```
├── .github/
│   └── workflows/
│       └── deploy.yml          # GitHub Actions workflow
├── src/
│   └── index.html             # Website source code
├── terraform/
│   ├── main.tf                # Main infrastructure configuration
│   ├── variables.tf           # Terraform variables
│   ├── outputs.tf             # Terraform outputs
│   └── provider.tf            # AWS provider configuration
├── Dockerfile                 # Container configuration
├── .gitignore                # Git ignore rules
└── README.md                 # This file
```

## 🛠️ Prerequisites

- AWS Account with appropriate permissions
- GitHub Account
- Terraform installed locally
- AWS CLI configured
- Docker installed (optional for local testing)

## ⚙️ Setup Instructions

### 1. Clone Repository
```bash
git clone <your-repo-url>
cd ECS
```

### 2. Configure AWS Credentials
Set up your AWS credentials locally:
```bash
aws configure
```

### 3. Deploy Infrastructure
Navigate to terraform folder and run:
```bash
cd terraform
terraform init
terraform plan
terraform apply
```

### 4. Configure GitHub Secrets
Go to your GitHub repository → Settings → Secrets and variables → Actions

Add the following secrets:
- `AWS_ACCESS_KEY_ID`: Your AWS Access Key
- `AWS_SECRET_ACCESS_KEY`: Your AWS Secret Key

### 5. Push Code to GitHub
```bash
git add .
git commit -m "Initial deployment setup"
git push origin main
```

## 🏗️ Infrastructure Components

### AWS Resources Created:
- **VPC**: Virtual Private Cloud with DNS support
- **Subnets**: 2 public subnets across different AZs
- **Internet Gateway**: For internet access
- **Security Groups**: HTTP traffic (port 80) allowed
- **ECR Repository**: Docker image storage
- **ECS Cluster**: Container orchestration
- **ECS Service**: Application deployment
- **CloudWatch Logs**: Application logging
- **IAM Roles**: ECS task execution permissions

## 🔄 CI/CD Pipeline

The GitHub Actions workflow automatically:

1. **Triggers** on push to `main` branch
2. **Checks out** the repository code
3. **Configures** AWS credentials
4. **Logs in** to Amazon ECR
5. **Builds** Docker image
6. **Pushes** image to ECR
7. **Updates** ECS service with new deployment

## 🌐 Accessing Your Website

After successful deployment:

1. Go to AWS Console → ECS
2. Navigate to your cluster → Tasks
3. Click on the running task
4. Find the **Public IP** in the Configuration section
5. Open the IP address in your browser

## 📋 Terraform Configuration

### Variables (terraform/variables.tf):
- `aws_region`: AWS deployment region (default: us-west-2)
- `project_name`: Project identifier (default: hello-world)
- `environment`: Environment type (default: dev)

### Outputs (terraform/outputs.tf):
- `ecr_repository_url`: ECR repository URL
- `ecs_cluster_name`: ECS cluster name
- `ecs_service_name`: ECS service name

## 🐳 Docker Configuration

The Dockerfile uses:
- **Base Image**: `nginx:alpine` (lightweight)
- **Content**: Copies HTML files to Nginx directory
- **Port**: Exposes port 80 for HTTP traffic

## 🔧 Customization

### To modify the website:
1. Edit `src/index.html`
2. Commit and push changes
3. GitHub Actions will automatically deploy updates

### To change infrastructure:
1. Modify Terraform files in `terraform/` directory
2. Run `terraform plan` and `terraform apply`

## 🚨 Troubleshooting

### Common Issues:

1. **Pipeline Fails**: Check GitHub Secrets are configured correctly
2. **ECS Service Not Starting**: Verify security groups allow port 80
3. **Website Not Accessible**: Check ECS task has public IP assigned
4. **Docker Build Fails**: Ensure Dockerfile syntax is correct

### Useful Commands:
```bash
# Check ECS service status
aws ecs describe-services --cluster hello-world-cluster --services hello-world-service

# View ECS logs
aws logs describe-log-groups --log-group-name-prefix "/ecs/hello-world"

# Force new deployment
aws ecs update-service --cluster hello-world-cluster --service hello-world-service --force-new-deployment
```

## 🧹 Cleanup

To avoid AWS charges, destroy the infrastructure:
```bash
cd terraform
terraform destroy
```

## 📚 Technologies Used

- **AWS ECS Fargate**: Serverless container hosting
- **AWS ECR**: Container image registry
- **GitHub Actions**: CI/CD automation
- **Terraform**: Infrastructure as Code
- **Docker**: Containerization
- **Nginx**: Web server

## 🎯 Benefits

- **Automated Deployment**: Push code → Live website
- **Scalable Infrastructure**: ECS Fargate auto-scaling
- **Cost Effective**: Pay only for running containers
- **Version Control**: All infrastructure and code versioned
- **Zero Downtime**: Rolling deployments

## 📝 License

This project is open source and available under the [MIT License](LICENSE).

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## 📞 Support

For issues and questions:
- Create an issue in this repository
- Check AWS ECS documentation
- Review GitHub Actions logs

---

**Happy Deploying! 🚀**

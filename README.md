# n8n Terraform Starter Kit

This repository contains Terraform configuration starter kit to deploy a self-hosted n8n instance on AWS. 
The infrastructure automatically provisions an EC2 instance, configures security groups, optionally sets up DNS records and SSL, and deploys n8n using Docker Compose with the AI starter kit.

## 🚀 Features

- **Automated AWS Infrastructure**: Complete Terraform configuration for n8n deployment
- **Self-Hosted n8n with AI**: Uses the official n8n AI starter kit for enhanced AI capabilities
- **Security Configuration**: Properly configured security groups with restricted SSH access
- **DNS Integration**: Optional Route53 DNS record creation
- **HTTPS/SSL Integration**: Setup free https with certbot (letsencrypt)
- **Docker-based Deployment**: Automated container deployment with environment configuration

## 📋 Prerequisites

- [Terraform](https://www.terraform.io/downloads.html) (>= 1.0)
- [AWS CLI](https://aws.amazon.com/cli/) configured with appropriate credentials
- An AWS account with permissions to create EC2 instances, security groups, and Route53 records
- An SSH key pair for EC2 instance access 

## ⚙️ Configuration

### Required Variables

Rename `terraform.tfvars.example` to `terraform.tfvars` and modify the variable according to your setup.

### Variable Descriptions

| Variable | Description | Default |
|----------|-------------|---------|
| `aws_region` | AWS region for deployment | `us-east-1` |
| `instance_type` | EC2 instance type | `t3.small` |
| `key_name` | SSH key pair name | Required |
| `public_key_path` | Path to public SSH key | `~/.ssh/id_rsa.pub` |
| `my_ip_cidr` | Your IP address for SSH access | `0.0.0.0/0` |
| `domain_name` | Root domain for DNS records | Required |
| `domain_name` | Sub domain for DNS records | `n8n` |
| `create_dns_record` | Whether to create Route53 DNS record | `true` |
| `ssl_email` | Email for registering your ssl (letsencrypt) | `your@email.com` |
| `basic_auth_user` | n8n admin username | `admin` |
| `basic_auth_password` | n8n admin password | Required |
| `n8n_encryption_key` | n8n encryption key (32 chars) | Required |
| `n8n_user_management_jwt_secret` | JWT secret for user management | Required |

## 🚀 Deployment

### 1. Initialize Terraform

```bash
terraform init
```

### 2. Review the Plan

```bash
terraform plan
```

### 3. Apply the Configuration

```bash
terraform apply
```

### 4. Access n8n

After successful deployment, you can access n8n at:

- **Direct IP**: `http://<instance-public-ip>:5678`
- **Domain** (if DNS configured): `https://n8n.yourdomain.com:5678`

### 5. Login

Use the credentials specified in your `terraform.tfvars`:
- Username: `admin` (or your custom `basic_auth_user`)
- Password: Your `basic_auth_password`

## 🔧 Customization

### Instance Type

Modify the `instance_type` variable in `terraform.tfvars` to change the EC2 instance size:

```hcl
instance_type = "t3.medium"  # For better performance
```

## 🧹 Cleanup

To destroy the infrastructure:

```bash
terraform destroy
```

⚠️ **Warning**: This will permanently delete all created resources and data.
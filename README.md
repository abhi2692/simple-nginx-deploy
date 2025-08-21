# 🧰 Simple Nginx Web App Deployment on AWS EC2 using GitHub Actions

## ⚠️ Prerequisites

Before running this CI/CD pipeline, you must:

- **Enable EC2 in your main infrastructure repo** ([terraform-aws-infra](https://github.com/abhi2692/terraform-aws-infra.git)) by setting `enable_ec2 = true` in `environments/dev/variables.tf` and applying the changes with Terraform. This will provision the required EC2 instance for your app.
- Wait for the EC2 instance to be created and ensure it is reachable (public IP, SSH and HTTP open).
- Make sure you have the correct SSH keypair configured in both your infra and this repo's GitHub secrets.

If EC2 is not enabled and provisioned, this deployment will fail because there will be no target instance for Nginx.

This is a beginner-friendly DevOps project that deploys a static HTML page to an Nginx web server on an AWS EC2 instance using GitHub Actions.

## 🚀 Project Overview

- ✅ Launches an EC2 instance using Terraform
- ✅ Installs Nginx on Amazon Linux 2
- ✅ Serves a simple HTML homepage
- ✅ Uses GitHub Actions to deploy via SSH

## 🏗️ EC2 Infrastructure

This project assumes an EC2 instance is already created. You can:

- ✅ Manually create an EC2 instance (Amazon Linux 2, with public IP)
- 🔧 Or provision infrastructure using Terraform from this repo: [terraform-aws-infra](https://github.com/abhi2692/terraform-aws-infra.git)

Make sure you:

- Allow inbound HTTP (port 80) and SSH (port 22)
- Upload the public key of your SSH keypair to EC2
- Store the private key in your GitHub repo secrets

## 🗂️ Folder Structure

```
simple-nginx-deploy/
├── .github/
│   └── workflows/
│       └── deploy.yml         # GitHub Actions workflow
├── scripts/
│   └── deploy.sh              # Script to SSH and configure EC2 instance
├── app/
│   └── index.html             # HTML page served by Nginx
└── README.md
```


## ⚙️ How It Works

1. Terraform launches an EC2 instance (not included in this repo).
2. HTML file is pushed to GitHub.
3. GitHub Actions triggers `deploy.yml`.
4. `deploy.sh` connects to EC2 via SSH and:
   - Installs Nginx
   - Sets up the homepage
   - Starts the service

## 🔐 Secrets Required in GitHub

Set the following GitHub Secrets:

- `EC2_SSH_KEY` – Your EC2 private key (in OpenSSH format)
- `EC2_HOST` – Public IP of your EC2 instance
- `EC2_USER` – SSH user, usually `ec2-user` for Amazon Linux 2

## 🏁 To Deploy

Push to the `main` branch. GitHub Actions will do the rest.

## 📦 Tech Stack

- AWS EC2 (Amazon Linux 2)
- Nginx
- GitHub Actions
- Bash

## 🏷️ Project Tag

> ✅ Level: Beginner  
> 🔧 Focus: SSH + EC2 + GitHub Actions  
> 🧱 Category: Cloud Basics

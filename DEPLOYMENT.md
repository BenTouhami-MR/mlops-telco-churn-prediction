# MLOps Telco Churn Prediction - EC2 Deployment

This repository contains an MLOps application for telco churn prediction with automated deployment to AWS EC2 using GitHub Actions.

## 🚀 Quick Deploy

**Total time: ~70 minutes**

1. **AWS Setup** (30 min) - Create IAM user and launch EC2 instance
2. **EC2 Configuration** (20 min) - Install Docker, Docker Compose, Git
3. **GitHub Setup** (10 min) - Add repository secrets
4. **Deploy** (5 min) - Push code to trigger deployment
5. **Verify** (5 min) - Access your services

📋 **Follow the [Quick Start Checklist](../../.gemini/antigravity/brain/f617f4f1-9576-4948-95c4-24cfc22dec7e/quick_start_checklist.md)**

📖 **Detailed guide: [Deployment Guide](../../.gemini/antigravity/brain/f617f4f1-9576-4948-95c4-24cfc22dec7e/deployment_guide.md)**

## 📦 Application Stack

- **Airflow** - Workflow orchestration (Port 8080)
- **MLflow** - Experiment tracking (Port 5000)
- **Prometheus** - Metrics collection (Port 9090)
- **Grafana** - Visualization (Port 3001)
- **Evidently** - Data quality monitoring (Port 8020)
- **PostgreSQL** - Database
- **Redis** - Message broker

## 🔧 Prerequisites

- AWS Account
- GitHub Account
- SSH client (for EC2 access)

## 📝 Required GitHub Secrets

Add these in **Settings → Secrets and variables → Actions**:

- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `EC2_HOST`
- `EC2_USERNAME`
- `EC2_SSH_KEY`
- `AIRFLOW_UID`

## 🌐 Access Services

After deployment, access at:

```
Airflow:    http://YOUR_EC2_IP:8080  (airflow/airflow)
MLflow:     http://YOUR_EC2_IP:5000
Grafana:    http://YOUR_EC2_IP:3001  (admin/admin)
Prometheus: http://YOUR_EC2_IP:9090
Evidently:  http://YOUR_EC2_IP:8020
```

## 🔄 CI/CD Pipeline

Automated deployment triggers on push to `main` branch:

1. Checkout code
2. Configure AWS credentials
3. SSH to EC2
4. Pull latest code
5. Rebuild and restart containers
6. Verify deployment

## 💰 Cost Estimate

- **t3.large** (8 GB): ~$60/month
- **t3.xlarge** (16 GB): ~$120/month
- **Storage**: ~$5/month

## 🛠️ Manual Commands

```bash
# SSH to EC2
ssh -i your-key.pem ubuntu@YOUR_EC2_IP

# View logs
docker-compose logs -f

# Restart services
docker-compose restart

# Update application
git pull origin main
docker-compose up -d --build
```

## 🔒 Security Notes

⚠️ **Change default passwords immediately!**

- Airflow: Update in environment variables
- Grafana: Change on first login
- Restrict SSH access to your IP only
- Set up SSL/TLS for production

## 📚 Documentation

- [Quick Start Checklist](../../.gemini/antigravity/brain/f617f4f1-9576-4948-95c4-24cfc22dec7e/quick_start_checklist.md) - Step-by-step deployment
- [Deployment Guide](../../.gemini/antigravity/brain/f617f4f1-9576-4948-95c4-24cfc22dec7e/deployment_guide.md) - Detailed instructions
- [EC2 Setup Script](./scripts/ec2-setup.sh) - Automated EC2 configuration

## 🐛 Troubleshooting

**Deployment fails?**
- Check GitHub Actions logs
- Verify all secrets are set correctly
- Ensure EC2 security group allows required ports

**Can't access services?**
- Verify EC2 instance is running
- Check security group rules
- Run `docker-compose ps` on EC2

**Out of memory?**
- Upgrade to larger instance type
- Setup script includes 4GB swap

## 📞 Support

For issues or questions, check the detailed deployment guide or review:
- GitHub Actions workflow logs
- EC2 system logs: `journalctl -xe`
- Docker logs: `docker-compose logs`

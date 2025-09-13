# DevSecOps Pipeline Configuration Prompts

## GitHub Actions CI/CD Workflow Configuration

**Date:** September 13, 2025
**Role:** DevSecOps Engineer

### Task Description:
Configure the GitHub Actions workflow in `.github/workflows/ci.yml` to implement a complete CI/CD pipeline.

### Requirements:
After a Pull-request to the main branch, the workflow should:
1. Run the backend tests
2. Build the backend
3. Deploy the application in an EC2 server

### Configuration Needed:
- GitHub Secrets configuration
- EC2 deployment setup
- Backend testing and building pipeline

### Answers Provided:

#### EC2 Configuration:
- **OS**: Amazon Linux 2 ✅
- **Backend Port**: 8080 in production (3010 locally) ✅
- **Deployment Directory**: `/home/ec2-user/lti-app` ✅
- **Database**: PostgreSQL directly on EC2 (easier setup) ✅
- **Process Manager**: PM2 ✅
- **Prisma Migrations**: Yes, run during deployment ✅

#### Deployment Strategy:
- **Frontend**: Include React frontend build and deployment ✅
- **Serving**: Use easiest method (Express static serving) ✅
- **Environment**: Use provided .env file with production credentials ✅

#### Database Credentials:
- **DB_USER**: LTIdbUser
- **DB_PASSWORD**: D1ymf8wyQEGthFR1E9xhCq
- **DB_NAME**: LTIdb
- **DB_PORT**: 5432

#### Security & Access:
- **EC2 Username**: LidrAI_David ✅
- **SSH Key**: Required for deployment ✅
- **GitHub Secrets**: AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, EC2_HOST, EC2_USERNAME, EC2_SSH_KEY, DB_PASSWORD ✅

#### Testing:
- **Test Database**: Mock values for existing tests ✅
- **Test Files**: Use existing candidateService.test.ts and positionService.test.ts ✅

#### Deployment Process:
- **Application Management**: Stop existing app before deployment ✅
- **Post-deployment**: Run migrations and seed script ✅

---

## GitHub Secrets Configuration Instructions

### Required Secrets:
1. **AWS_ACCESS_KEY_ID**: AWS Access Key ID
2. **AWS_SECRET_ACCESS_KEY**: AWS Secret Access Key  
3. **EC2_HOST**: EC2 instance public IP or DNS
4. **EC2_USERNAME**: LidrAI_David
5. **EC2_SSH_KEY**: Private SSH key for EC2 access
6. **DB_PASSWORD**: D1ymf8wyQEGthFR1E9xhCq

### How to Find Information in AWS:

#### AWS Access Keys:
1. Go to AWS Console → IAM → Users
2. Select your user → Security credentials tab
3. Create access key if you don't have one
4. Copy Access Key ID and Secret Access Key

#### EC2 Instance Information:
1. Go to AWS Console → EC2 → Instances
2. Select your instance
3. Copy **Public IPv4 address** or **Public IPv4 DNS** for EC2_HOST

#### SSH Key:
1. Use the private key file (.pem) you downloaded when creating the EC2 instance
2. Copy the entire content of the .pem file for EC2_SSH_KEY

### Setting Up GitHub Secrets:
1. Go to your GitHub repository
2. Click Settings → Secrets and variables → Actions
3. Click "New repository secret"
4. Add each secret with the exact names listed above

### EC2 Prerequisites Update:
**New Requirement (September 13, 2025):** The EC2 server is completely empty and requires automatic setup.

The workflow must install all necessary components automatically:
- Node.js 18+ 
- PM2 globally (`npm install -g pm2`)
- PostgreSQL server
- Database `LTIdb` with user `LTIdbUser`
- All system dependencies

**Previous assumption:** EC2 instance was pre-configured
**Current reality:** Clean EC2 instance requiring full automated setup

---

## Final Configuration Summary:

### Workflow Features:
- ✅ Run backend tests on every PR
- ✅ Build both backend and frontend
- ✅ Deploy to EC2 only on main branch pushes
- ✅ Handle database migrations and seeding
- ✅ Use PM2 for process management
- ✅ Serve frontend static files through Express
- ✅ Zero-downtime deployment with backup strategy

### Security Features:
- ✅ SSH-based deployment
- ✅ Environment variables management
- ✅ GitHub Secrets integration
- ✅ Production database credentials protection

---
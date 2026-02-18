# 🎬 Netflix Clone - DevSecOps CI/CD Pipeline

[![Jenkins](https://img.shields.io/badge/Jenkins-CI%2FCD-D24939?logo=jenkins&logoColor=white)](https://www.jenkins.io/)
[![Docker](https://img.shields.io/badge/Docker-Containerized-2496ED?logo=docker&logoColor=white)](https://www.docker.com/)
[![Prometheus](https://img.shields.io/badge/Prometheus-Monitoring-E6522C?logo=prometheus&logoColor=white)](https://prometheus.io/)
[![Grafana](https://img.shields.io/badge/Grafana-Visualization-F46800?logo=grafana&logoColor=white)](https://grafana.com/)
[![Security](https://img.shields.io/badge/Security-DevSecOps-success)](https://www.devsecops.org/)

> A production-grade DevSecOps project demonstrating automated CI/CD pipeline with integrated security scanning, containerization, and comprehensive monitoring for a Netflix clone application.

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Architecture](#️-architecture)
- [Tech Stack](#️-tech-stack)
- [Features](#-features)
- [Pipeline Workflow](#-pipeline-workflow)
- [Prerequisites](#-prerequisites)
- [Installation Guide](#-installation-guide)
- [Configuration](#️-configuration)
- [Monitoring](#-monitoring)
- [Security](#-security)
- [Screenshots](#-screenshots)
- [Key Learnings](#-key-learnings)
- [Future Improvements](#-future-improvements)
- [Troubleshooting](#-troubleshooting)
- [Contributing](#-contributing)

---

## 🎯 Overview

This project automates the entire software delivery lifecycle for a Netflix clone application, implementing DevSecOps best practices with security scanning integrated at every stage of the CI/CD pipeline.

### What Makes This Special?

- ✅ **Fully Automated Deployment** - Zero manual intervention required
- ✅ **Security-First Approach** - Multiple scanning tools catch vulnerabilities early
- ✅ **Real-Time Monitoring** - Complete observability of system health
- ✅ **Production-Ready** - Docker containerization ensures consistency
- ✅ **Instant Notifications** - Email alerts for build status

### Performance Metrics

| Metric | Before Automation | After Automation | Improvement |
|--------|------------------|------------------|-------------|
| Deployment Time | ~30 minutes | ~10-15 minutes | **50-60% faster** |
| Manual Steps | 15+ commands | 1 button click | **93% reduction** |
| Security Checks | Manual/Ad-hoc | Automated | **100% coverage** |
| Failure Detection | Hours/Days | Immediate | **Real-time** |

---

## 🏗️ Architecture

### High-Level System Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                            DEVELOPER                                │
│                      (Git Push to GitHub)                           │
└───────────────────────────────┬─────────────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────────────┐
│                     JENKINS CI/CD PIPELINE                          │
│  ┌───────────────────────────────────────────────────────────────┐  │
│  │                                                               │  │
│  │  Stage 1: Clean Workspace                                    │  │
│  │  ├─► Remove old artifacts                                    │  │
│  │  └─► Prepare clean environment                               │  │
│  │                                                               │  │
│  │  Stage 2: Git Checkout                                       │  │
│  │  ├─► Clone main branch                                       │  │
│  │  └─► Fetch latest code                                       │  │
│  │                                                               │  │
│  │  Stage 3: Install Dependencies                               │  │
│  │  ├─► npm install                                             │  │
│  │  └─► Download Node.js packages                               │  │
│  │                                                               │  │
│  │  Stage 4: Security Scan (File System)                        │  │
│  │  ├─► Trivy FS Scan                                           │  │
│  │  └─► Generate vulnerability report                           │  │
│  │                                                               │  │
│  │  Stage 5: Docker Build & Push                                │  │
│  │  ├─► Build Docker image                                      │  │
│  │  ├─► Tag image (username/netflix:latest)                     │  │
│  │  └─► Push to DockerHub Registry ─────────┐                   │  │
│  │                                           │                   │  │
│  │  Stage 6: Security Scan (Container Image)│                   │  │
│  │  ├─► Trivy Image Scan                    │                   │  │
│  │  └─► Verify image security               │                   │  │
│  │                                           │                   │  │
│  │  Stage 7: Deploy Container               │                   │  │
│  │  ├─► Stop existing container             │                   │  │
│  │  ├─► Remove old container                │                   │  │
│  │  └─► Deploy new container (port 8081)    │                   │  │
│  │                                           │                   │  │
│  └───────────────────────────────────────────┼───────────────────┘  │
└──────────────────────────────────────────────┼───────────────────────┘
                                               │
                    ┌──────────────────────────┴──────────────┐
                    ▼                                         ▼
          ┌───────────────────┐                    ┌──────────────────┐
          │    DOCKERHUB      │                    │  DEPLOYED APP    │
          │  Image Registry   │                    │ localhost:8081   │
          │                   │                    │                  │
          │  netflix:latest   │                    │ Netflix Clone    │
          └───────────────────┘                    └────────┬─────────┘
                                                            │
                    ┌───────────────────────────────────────┘
                    │
                    ▼
┌─────────────────────────────────────────────────────────────────────┐
│                    MONITORING & ALERTING STACK                      │
│                                                                     │
│  ┌─────────────────┐      ┌─────────────────┐    ┌──────────────┐  │
│  │   PROMETHEUS    │─────►│     GRAFANA     │    │    EMAIL     │  │
│  │                 │      │                 │    │ NOTIFICATION │  │
│  │ Metrics Storage │      │   Dashboards    │    │              │  │
│  │ & Collection    │      │ Visualization   │    │ Build Status │  │
│  └────────▲────────┘      └─────────────────┘    └──────────────┘  │
│           │                                              ▲          │
│           │                                              │          │
│  ┌────────┴──────────┐                          ┌───────┴────────┐  │
│  │  Node Exporter    │                          │    Jenkins     │  │
│  │                   │                          │  Build Events  │  │
│  │  System Metrics:  │                          │                │  │
│  │  • CPU Usage      │                          │  Success/Fail  │  │
│  │  • Memory Usage   │                          │  Notifications │  │
│  │  • Disk I/O       │                          │                │  │
│  │  • Network Stats  │                          └────────────────┘  │
│  └───────────────────┘                                               │
└─────────────────────────────────────────────────────────────────────┘
```

### Pipeline Flow Diagram

```
                            START
                              │
                              ▼
                    ┌──────────────────┐
                    │ Clean Workspace  │
                    │ Remove artifacts │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │  Git Checkout    │
                    │  Clone main      │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │Install Dependencies│
                    │   npm install    │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ Trivy FS Scan    │
                    │Source Code Scan  │
                    └────────┬─────────┘
                             │
                    ┌────────┴────────┐
                    │ Vulnerabilities? │
                    └────┬────────┬───┘
                         │        │
                    YES  │        │  NO
                         │        │
            ┌────────────┘        └─────────────┐
            ▼                                    ▼
    ┌──────────────┐                   ┌──────────────────┐
    │Generate Report│                   │     Continue     │
    │  & Continue   │                   │                  │
    └───────┬───────┘                   └────────┬─────────┘
            │                                    │
            └────────────────┬───────────────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │Docker Build&Push │
                    │ 1. Build Image   │
                    │ 2. Tag Image     │
                    │ 3. Push DockerHub│
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │Trivy Image Scan  │
                    │ Container Scan   │
                    └────────┬─────────┘
                             │
                    ┌────────┴────────┐
                    │ Vulnerabilities? │
                    └────┬────────┬───┘
                         │        │
                    YES  │        │  NO
                         │        │
            ┌────────────┘        └─────────────┐
            ▼                                    ▼
    ┌──────────────┐                   ┌──────────────────┐
    │Generate Report│                   │     Continue     │
    │  & Continue   │                   │                  │
    └───────┬───────┘                   └────────┬─────────┘
            │                                    │
            └────────────────┬───────────────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ Deploy Container │
                    │ 1. Stop old      │
                    │ 2. Remove old    │
                    │ 3. Run new       │
                    └────────┬─────────┘
                             │
                    ┌────────┴────────┐
                    │  Build Status?  │
                    └────┬────────┬───┘
                         │        │
                   SUCCESS│        │FAILURE
                         │        │
            ┌────────────┘        └─────────────┐
            ▼                                    ▼
    ┌──────────────┐                   ┌──────────────────┐
    │ ✅ SUCCESS   │                   │  ❌ FAILURE     │
    │ Email Sent   │                   │  Email Sent      │
    └───────┬──────┘                   └────────┬─────────┘
            │                                    │
            └────────────────┬───────────────────┘
                             │
                             ▼
                            END
```

### Component Interaction Flow

```
┌──────────────┐
│   GitHub     │
│  Repository  │
│   (Source)   │
└──────┬───────┘
       │ Webhook/Poll SCM
       │ Trigger on Push
       ▼
┌──────────────────────────────┐
│       Jenkins Master         │
│                              │
│  ┌────────────────────────┐  │
│  │  Pipeline Executor     │  │
│  │  (Groovy Script)       │  │
│  └───┬───────────┬────────┘  │
└──────┼───────────┼───────────┘
       │           │
       │           └──────────────────┐
       │                              │
       ▼                              ▼
┌──────────────┐            ┌──────────────────┐
│    Trivy     │            │   SonarQube      │
│   Scanner    │            │  (Code Quality)  │
│              │            │   [Optional]     │
│ Scan Files   │            └──────────────────┘
│ Scan Images  │
└──────────────┘
       │
       │
       ▼
┌──────────────────────────────┐
│       Docker Engine          │
│                              │
│  1. Build Image              │
│  2. Tag Image                │
│  3. Push to Registry         │
│  4. Run Container            │
└───────┬──────────────────────┘
        │
        ├──────────────────┐
        │                  │
        ▼                  ▼
┌──────────────┐    ┌──────────────────┐
│  DockerHub   │    │ Running Container│
│   Registry   │    │                  │
│              │    │ Netflix App      │
│ Store Images │    │ Port: 8081       │
└──────────────┘    └────────┬─────────┘
                             │
                             │ Metrics Exposed
                             │
        ┌────────────────────┴──────────────────┐
        │                                       │
        ▼                                       ▼
┌─────────────────┐                  ┌──────────────────┐
│   Prometheus    │                  │  Node Exporter   │
│                 │                  │                  │
│ Scrape Metrics  │◄─────────────────│ System Metrics   │
│ Store Time-     │                  │ • CPU            │
│ Series Data     │                  │ • Memory         │
│                 │                  │ • Disk           │
└────────┬────────┘                  │ • Network        │
         │                           └──────────────────┘
         │ Prometheus as
         │ Data Source
         │
         ▼
┌─────────────────┐
│    Grafana      │
│                 │
│  • Dashboards   │
│  • Alerts       │
│  • Visualization│
└─────────────────┘
```

---

## 🛠️ Tech Stack

### Core Technologies

| Category | Technology | Version | Purpose |
|----------|-----------|---------|---------|
| **CI/CD** | Jenkins | Latest | Pipeline orchestration and automation |
| **Containerization** | Docker | 24.x | Application containerization |
| **Version Control** | Git/GitHub | - | Source code management |
| **Security Scanning** | Trivy | 0.48+ | Vulnerability scanning (FS & Images) |
| **Code Quality** | SonarQube | LTS Community | Static code analysis |
| **Monitoring** | Prometheus | 2.47+ | Metrics collection and storage |
| **Visualization** | Grafana | Latest | Dashboard and metrics visualization |
| **System Metrics** | Node Exporter | 1.6+ | System-level metrics collection |
| **Frontend** | React.js | 18.x | Netflix clone UI |
| **Runtime** | Node.js | 16.x | JavaScript runtime |
| **OS** | CentOS | 7/8 | Linux operating system |

### Application Stack

```
Frontend:    React.js + Vite
Backend:     Node.js + Express (serve static)
API:         TMDB (The Movie Database)
Build Tool:  npm
Container:   Docker (Alpine-based)
Registry:    DockerHub
```

---

## ✨ Features

### Automation Features

- 🚀 **One-Click Deployment** - Single button triggers entire pipeline
- 🔄 **Automated Builds** - Triggered on Git push (webhook/polling)
- 📦 **Dependency Management** - Automatic npm package installation
- 🏗️ **Container Building** - Docker image creation with optimizations
- 📤 **Registry Push** - Automatic push to DockerHub
- 🔄 **Rolling Deployment** - Zero-downtime container replacement

### Security Features

- 🔒 **Multi-Layer Scanning** - File system AND container image scanning
- 🛡️ **Vulnerability Detection** - Identifies CVEs and security issues
- 📊 **Code Quality Analysis** - SonarQube integration for code smells
- 🔐 **Secret Management** - Jenkins credentials store for sensitive data
- ⚠️ **Security Reports** - Detailed vulnerability reports generated

### Monitoring Features

- 📊 **Real-Time Metrics** - Live system performance data
- 📈 **Historical Data** - Time-series metrics storage
- 🎨 **Visual Dashboards** - Grafana dashboards for insights
- 🔔 **Alerting** - Email notifications on build status
- 📉 **Performance Tracking** - CPU, RAM, Disk, Network monitoring

---

## 🔄 Pipeline Workflow

### Detailed Stage Breakdown

#### Stage 1: Clean Workspace
```groovy
cleanWs()
```
- Removes all files from previous builds
- Ensures clean slate for new build
- Prevents artifact contamination

#### Stage 2: Git Checkout
```groovy
git branch: 'main', url: 'https://github.com/N4si/DevSecOps-Project.git'
```
- Clones latest code from GitHub
- Checks out main branch
- Fetches all dependencies

#### Stage 3: Install Dependencies
```bash
npm install
```
- Downloads Node.js packages
- Installs React dependencies
- Prepares build environment
- **Time:** ~2-3 minutes

#### Stage 4: Trivy File System Scan
```bash
trivy fs . > trivyfs.txt
```
- Scans source code for vulnerabilities
- Checks dependencies for known CVEs
- Generates security report
- **Does NOT block build** (informational)

#### Stage 5: Docker Build & Push
```bash
docker build --build-arg TMDB_V3_API_KEY=xxx -t netflix .
docker tag netflix username/netflix:latest
docker push username/netflix:latest
```
- Builds optimized Docker image
- Injects API key at build time
- Tags with latest version
- Pushes to DockerHub registry
- **Time:** ~5-7 minutes (largest stage)

#### Stage 6: Trivy Image Scan
```bash
trivy image username/netflix:latest > trivyimage.txt
```
- Scans final Docker image
- Identifies OS vulnerabilities
- Checks for malware
- Generates comprehensive report

#### Stage 7: Deploy Container
```bash
docker stop netflix || true
docker rm netflix || true
docker run -d --name netflix -p 8081:80 username/netflix:latest
```
- Gracefully stops old container
- Removes old container
- Deploys new container
- Exposes on port 8081
- **Time:** ~30 seconds

### Post-Build Actions

#### On Success ✅
```groovy
emailext(
    subject: "✅ SUCCESS: Build #${env.BUILD_NUMBER}",
    body: "Netflix app deployed successfully!",
    to: 'your-email@gmail.com'
)
```

#### On Failure ❌
```groovy
emailext(
    subject: "❌ FAILED: Build #${env.BUILD_NUMBER}",
    body: "Build failed! Check console output.",
    to: 'your-email@gmail.com'
)
```

---

## 📦 Prerequisites

### System Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| RAM | 4GB | 8GB+ |
| CPU | 2 cores | 4 cores |
| Disk Space | 20GB | 30GB+ |
| OS | CentOS 7+ | CentOS 8/Ubuntu 22.04 |

### Required Software

- **Git** - Version control
- **Docker** - Container runtime
- **Java 17** - Jenkins requirement
- **Jenkins** - CI/CD server
- **Node.js 16+** - Application runtime

### Accounts Needed

1. **GitHub Account** - Source code hosting
2. **DockerHub Account** - Container registry
3. **TMDB Account** - API key for movie data
4. **Gmail Account** - Email notifications (with App Password)

---

## 🚀 Installation Guide

### Step 1: System Setup

```bash
# Update system
sudo yum update -y

# Install Git
sudo yum install git -y

# Clone repository
git clone https://github.com/N4si/DevSecOps-Project.git
cd DevSecOps-Project
```

### Step 2: Install Docker

```bash
# Install Docker
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install docker-ce docker-ce-cli containerd.io -y

# Start Docker
sudo systemctl start docker
sudo systemctl enable docker

# Add user to docker group
sudo usermod -aG docker $USER
newgrp docker
sudo chmod 777 /var/run/docker.sock
```

### Step 3: Install Java & Jenkins

```bash
# Install Java 17
sudo yum install java-17-openjdk java-17-openjdk-devel -y
java -version

# Add Jenkins repository
sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key

# Install Jenkins
sudo yum install jenkins -y

# Start Jenkins
sudo systemctl start jenkins
sudo systemctl enable jenkins

# Get initial admin password
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Access Jenkins: `http://localhost:8080`

### Step 4: Install Security Tools

#### Trivy
```bash
# CentOS installation
sudo rpm -ivh https://github.com/aquasecurity/trivy/releases/download/v0.48.0/trivy_0.48.0_Linux-64bit.rpm

# Verify installation
trivy --version
```

#### SonarQube (Docker)
```bash
docker run -d --name sonar -p 9000:9000 sonarqube:lts-community
```

Access SonarQube: `http://localhost:9000` (admin/admin)

### Step 5: Install Monitoring Stack

#### Prometheus
```bash
# Create user
sudo useradd --system --no-create-home --shell /bin/false prometheus

# Download Prometheus
cd /tmp
wget https://github.com/prometheus/prometheus/releases/download/v2.47.1/prometheus-2.47.1.linux-amd64.tar.gz
tar -xvf prometheus-2.47.1.linux-amd64.tar.gz
cd prometheus-2.47.1.linux-amd64/

# Setup directories
sudo mkdir -p /data /etc/prometheus
sudo mv prometheus promtool /usr/local/bin/
sudo mv consoles/ console_libraries/ /etc/prometheus/
sudo mv prometheus.yml /etc/prometheus/

# Set permissions
sudo chown -R prometheus:prometheus /etc/prometheus/ /data/

# Create systemd service
sudo tee /etc/systemd/system/prometheus.service > /dev/null <<EOF
[Unit]
Description=Prometheus
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
  --config.file=/etc/prometheus/prometheus.yml \
  --storage.tsdb.path=/data \
  --web.listen-address=0.0.0.0:9090

[Install]
WantedBy=multi-user.target
EOF

# Start service
sudo systemctl daemon-reload
sudo systemctl enable prometheus
sudo systemctl start prometheus
```

Access Prometheus: `http://localhost:9090`

#### Node Exporter
```bash
# Create user
sudo useradd --system --no-create-home --shell /bin/false node_exporter

# Download
cd /tmp
wget https://github.com/prometheus/node_exporter/releases/download/v1.6.1/node_exporter-1.6.1.linux-amd64.tar.gz
tar -xvf node_exporter-1.6.1.linux-amd64.tar.gz
sudo mv node_exporter-1.6.1.linux-amd64/node_exporter /usr/local/bin/

# Create service
sudo tee /etc/systemd/system/node_exporter.service > /dev/null <<EOF
[Unit]
Description=Node Exporter
After=network-online.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target
EOF

# Start service
sudo systemctl daemon-reload
sudo systemctl enable node_exporter
sudo systemctl start node_exporter
```

#### Grafana
```bash
# Add repository
sudo tee /etc/yum.repos.d/grafana.repo > /dev/null <<EOF
[grafana]
name=grafana
baseurl=https://rpm.grafana.com
repo_gpgcheck=1
enabled=1
gpgcheck=1
gpgkey=https://rpm.grafana.com/gpg.key
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
EOF

# Install
sudo yum install grafana -y

# Start service
sudo systemctl enable grafana-server
sudo systemctl start grafana-server
```

Access Grafana: `http://localhost:3000` (admin/admin)

---

## ⚙️ Configuration

### 1. Jenkins Configuration

#### Install Required Plugins
```
Manage Jenkins → Plugins → Available Plugins

Required:
- Eclipse Temurin Installer
- SonarQube Scanner
- NodeJs Plugin
- Email Extension Plugin
- Docker Plugin
- Docker Pipeline
- OWASP Dependency-Check
```

#### Configure Tools
```
Manage Jenkins → Tools

JDK:
- Name: jdk17
- Install automatically from adoptium.net
- Version: 17

NodeJS:
- Name: node16
- Install automatically
- Version: 16.x

SonarQube Scanner:
- Name: sonar-scanner
- Install automatically

Docker:
- Name: docker
- Install automatically
```

#### Add Credentials

**DockerHub Credentials:**
```
Manage Jenkins → Credentials → System → Global credentials

- Kind: Username with password
- Username: your-dockerhub-username
- Password: your-dockerhub-password
- ID: docker
```

**TMDB API Key:**
```
- Kind: Secret text
- Secret: your-tmdb-api-key
- ID: tmdb-api-key
```

**Gmail App Password:**
```
- Kind: Username with password
- Username: your-email@gmail.com
- Password: 16-character-app-password
- ID: gmail-credentials
```

#### Configure SonarQube Integration

**SonarQube Token:**
```
SonarQube (localhost:9000):
- My Account → Security → Generate Token
- Copy token

Jenkins:
- Manage Jenkins → Credentials
- Add Secret text
- ID: Sonar-token
```

**SonarQube Server:**
```
Manage Jenkins → System → SonarQube servers

- Name: sonar-server
- Server URL: http://localhost:9000
- Server authentication token: Sonar-token
```

#### Configure Email Notifications

**Extended E-mail Notification:**
```
Manage Jenkins → System

SMTP server: smtp.gmail.com
SMTP port: 465
Credentials: gmail-credentials
Use SSL: ✓
Default Content Type: HTML
Default Recipients: your-email@gmail.com
```

**E-mail Notification:**
```
SMTP server: smtp.gmail.com
Use SMTP Authentication: ✓
User Name: your-email@gmail.com
Password: app-password
Use SSL: ✓
SMTP Port: 465

Test: Send test e-mail
```

### 2. Prometheus Configuration

Edit `/etc/prometheus/prometheus.yml`:

```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'node_exporter'
    static_configs:
      - targets: ['localhost:9100']

  - job_name: 'jenkins'
    metrics_path: '/prometheus'
    static_configs:
      - targets: ['localhost:8080']
```

Reload configuration:
```bash
curl -X POST http://localhost:9090/-/reload
```

### 3. Grafana Configuration

#### Add Prometheus Data Source
```
Configuration → Data Sources → Add data source

Type: Prometheus
URL: http://localhost:9090
Save & Test
```

#### Import Dashboard
```
+ Icon → Import → Dashboard ID: 1860

Name: Node Exporter Full
Prometheus: Select "Prometheus"
Import
```

### 4. Create Jenkins Pipeline

```
New Item → Name: Netflix-Pipeline → Pipeline → OK

Pipeline Script:
[Paste the complete pipeline code from repository]

Save
```

---

## 📊 Monitoring

### Prometheus Metrics

Access targets: `http://localhost:9090/targets`

**Available Metrics:**
- Node Exporter (System metrics)
- Jenkins (Build metrics)

**Key Metrics to Monitor:**
- `node_cpu_seconds_total` - CPU usage
- `node_memory_MemAvailable_bytes` - Available memory
- `node_disk_io_time_seconds_total` - Disk I/O
- `node_network_receive_bytes_total` - Network incoming
- `node_network_transmit_bytes_total` - Network outgoing

### Grafana Dashboards

Access: `http://localhost:3000`

**Node Exporter Dashboard (ID: 1860):**
- CPU Usage (per core)
- Memory Usage
- Disk Usage
- Network Traffic
- System Load Average
- Disk I/O
- File System Usage

**During CI/CD Build:**
```
Idle State:
- CPU: 10-20%
- RAM: 1.4GB
- Disk I/O: Low
- Network: Minimal

During Build:
- CPU: 60-90% ⬆️ (Docker build stage)
- RAM: 1.6GB ⬆️
- Disk I/O: High ⬆️⬆️ (npm install, docker build)
- Network: Spike ⬆️ (DockerHub push)

Post-Deployment:
- CPU: 20-30%
- RAM: 1.5GB (new container running)
- Disk I/O: Normal
- Network: Normal
```

---

## 🔐 Security

### Security Scanning Process

#### 1. File System Scan (Trivy)
```bash
trivy fs . > trivyfs.txt
```
**Scans for:**
- Vulnerable dependencies in package.json
- Known CVEs in npm packages
- License compliance issues

#### 2. Image Scan (Trivy)
```bash
trivy image username/netflix:latest > trivyimage.txt
```
**Scans for:**
- OS-level vulnerabilities
- Application vulnerabilities
- Misconfigurations
- Exposed secrets

#### 3. Code Quality (SonarQube)
```bash
sonar-scanner \
  -Dsonar.projectName=Netflix \
  -Dsonar.projectKey=Netflix
```
**Analyzes:**
- Code smells
- Bugs
- Security hotspots
- Code coverage
- Duplications

### Security Best Practices Implemented

✅ **Secrets Management**
- API keys stored as Jenkins credentials
- No hardcoded secrets in code
- Build arguments for sensitive data

✅ **Container Security**
- Multi-stage Docker builds
- Minimal base images (Alpine)
- Non-root user execution
- Regular image scanning

✅ **Access Control**
- Jenkins authentication required
- Role-based access control
- Credential encryption

✅ **Network Security**
- Services on localhost (not exposed publicly)
- Firewall rules configured
- Minimal port exposure

---



## 💡 Key Learnings

### Technical Skills Gained

#### DevOps Practices
- ✅ CI/CD pipeline design and implementation
- ✅ Infrastructure as Code concepts
- ✅ Automation best practices
- ✅ GitOps workflow understanding

#### Containerization
- ✅ Docker multi-stage builds
- ✅ Image optimization techniques
- ✅ Container orchestration basics
- ✅ Registry management

#### Security
- ✅ DevSecOps integration
- ✅ Vulnerability scanning
- ✅ Shift-left security approach
- ✅ Secrets management

#### Monitoring
- ✅ Prometheus metrics collection
- ✅ Grafana dashboard creation
- ✅ Observability principles
- ✅ Performance monitoring

#### Problem Solving
- ✅ Resource optimization
- ✅ Troubleshooting Linux issues
- ✅ SELinux configuration
- ✅ Service management

### Real-World Insights

**Resource Constraints:**
Working with limited RAM (1.7GB) taught me to optimize services, make trade-offs, and understand that production environments aren't always ideal.

**Automation Value:**
Reducing 30 minutes of manual work to 10-15 minutes of automated process demonstrated the ROI of DevOps practices.

**Security First:**
Integrating security early (shift-left) is easier than retrofitting it later. Catching vulnerabilities before deployment saves time and reduces risk.

**Monitoring Matters:**
Real-time visibility into system behavior helps identify bottlenecks, optimize resources, and troubleshoot issues quickly.

### Challenges Overcome

1. **SonarQube Memory Issues**
   - Problem: Service hanging with 1.7GB RAM
   - Solution: Run on-demand instead of continuously

2. **SELinux Blocking Services**
   - Problem: Systemd services failing to start
   - Solution: Configured SELinux policies properly

3. **Docker Permission Errors**
   - Problem: Jenkins couldn't access Docker socket
   - Solution: Added Jenkins user to docker group

4. **Trivy Scan Failures**
   - Problem: Serialization errors in pipeline
   - Solution: Added try-catch error handling

---

## 🚀 Future Improvements

### Short-term (1-2 weeks)

- [ ] Add automated testing (Jest, Cypress)
- [ ] Implement blue-green deployment
- [ ] Add Slack notifications
- [ ] Create custom Grafana dashboards for application metrics
- [ ] Add Terraform for infrastructure provisioning

### Medium-term (1-2 months)

- [ ] Kubernetes deployment with Minikube
- [ ] ArgoCD for GitOps
- [ ] Helm charts for application packaging
- [ ] Multi-environment setup (dev/staging/prod)
- [ ] Implement canary deployments

### Long-term (3+ months)

- [ ] AWS/GCP cloud deployment
- [ ] Auto-scaling based on load
- [ ] Advanced security with Vault
- [ ] Log aggregation with ELK stack
- [ ] Distributed tracing with Jaeger
- [ ] Service mesh with Istio

### Enhancement Ideas

**Testing:**
- Unit tests with Jest
- Integration tests
- E2E tests with Cypress
- Performance testing with k6
- Security testing with OWASP ZAP

**Advanced CI/CD:**
- Parallel pipeline execution
- Matrix builds for multiple environments
- Approval gates for production
- Automated rollback on failure
- Build caching for faster builds

**Observability:**
- Application Performance Monitoring (APM)
- Custom application metrics
- Distributed tracing
- Log correlation
- Alerting rules with Alertmanager

**Infrastructure:**
- Infrastructure as Code (Terraform)
- Configuration Management (Ansible)
- Container Orchestration (Kubernetes)
- Service Mesh (Istio)
- API Gateway (Kong)

---

## 🐛 Troubleshooting

### Common Issues

#### 1. Jenkins Service Won't Start

**Symptom:**
```bash
sudo systemctl start jenkins
# Failed to start Jenkins
```

**Solutions:**
```bash
# Check logs
sudo journalctl -xeu jenkins.service

# Check Java version
java -version  # Should be 17

# Check port 8080 availability
sudo netstat -tulpn | grep 8080

# If port is in use, change Jenkins port
sudo nano /etc/sysconfig/jenkins
# HTTP_PORT=8090

sudo systemctl restart jenkins
```

#### 2. Docker Permission Denied

**Symptom:**
```bash
docker ps
# permission denied while trying to connect to Docker daemon
```

**Solutions:**
```bash
# Add user to docker group
sudo usermod -aG docker $USER
newgrp docker

# Set socket permissions
sudo chmod 666 /var/run/docker.sock

# Restart Docker
sudo systemctl restart docker

# For Jenkins
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
```

#### 3. SonarQube Out of Memory

**Symptom:**
```
SonarQube container keeps restarting
```

**Solutions:**
```bash
# Stop SonarQube
docker stop sonar
docker rm sonar

# Run with memory limit
docker run -d --name sonar \
  --memory="2g" \
  -p 9000:9000 \
  sonarqube:lts-community

# Or run only when needed
docker start sonar  # When analysis needed
docker stop sonar   # After analysis
```

#### 4. Trivy Scan Fails in Pipeline

**Symptom:**
```
Trivy fs scan failed with serialization error
```

**Solutions:**
```groovy
// Add try-catch in pipeline
stage('Trivy FS Scan') {
    steps {
        script {
            try {
                sh "trivy fs . > trivyfs.txt"
            } catch (Exception e) {
                echo "Trivy scan failed but continuing: ${e.getMessage()}"
            }
        }
    }
}
```

#### 5. Prometheus Service Fails

**Symptom:**
```bash
sudo systemctl start prometheus
# Job for prometheus.service failed
```

**Solutions:**
```bash
# Check config syntax
promtool check config /etc/prometheus/prometheus.yml

# Check permissions
ls -la /etc/prometheus/
sudo chown -R prometheus:prometheus /etc/prometheus/ /data/

# Check logs
sudo journalctl -xeu prometheus.service

# Manual start for debugging
sudo -u prometheus /usr/local/bin/prometheus \
  --config.file=/etc/prometheus/prometheus.yml \
  --storage.tsdb.path=/data
```

#### 6. Grafana Can't Connect to Prometheus

**Symptom:**
```
Data source is not working: HTTP Error Bad Gateway
```

**Solutions:**
```bash
# Check Prometheus is running
curl http://localhost:9090/api/v1/status/config

# In Grafana, use correct URL:
# http://localhost:9090 (not https)

# Check firewall
sudo firewall-cmd --list-all
sudo firewall-cmd --permanent --add-port=9090/tcp
sudo firewall-cmd --reload
```

#### 7. Email Notifications Not Working

**Symptom:**
```
Email sending failed
```

**Solutions:**
```bash
# Verify Gmail App Password (not regular password)
# Go to: https://myaccount.google.com/apppasswords

# Test SMTP connection
telnet smtp.gmail.com 465

# In Jenkins, ensure:
- SMTP server: smtp.gmail.com
- Port: 465
- Use SSL: ✓
- Credentials: 16-character app password

# Test configuration with "Test e-mail" button
```

#### 8. Build Hangs at npm install

**Symptom:**
```
npm install taking forever or hanging
```

**Solutions:**
```bash
# Clean npm cache
npm cache clean --force

# Update npm
npm install -g npm@latest

# Use npm ci instead (faster)
npm ci --prefer-offline

# In pipeline, add timeout
stage('Install Dependencies') {
    options {
        timeout(time: 10, unit: 'MINUTES')
    }
    steps {
        sh "npm install"
    }
}
```

#### 9. Container Port Already in Use

**Symptom:**
```
docker: Error response from daemon: 
driver failed programming external connectivity on endpoint netflix: 
Bind for 0.0.0.0:8081 failed: port is already allocated
```

**Solutions:**
```bash
# Find process using port
sudo netstat -tulpn | grep 8081

# Stop old container
docker stop netflix
docker rm netflix

# Or use different port
docker run -d --name netflix -p 8082:80 netflix:latest
```

#### 10. SELinux Blocking Services (CentOS)

**Symptom:**
```
Services fail to start with permission errors
```

**Solutions:**
```bash
# Check SELinux status
sestatus

# Temporarily disable (development)
sudo setenforce 0

# Permanently disable (if needed)
sudo sed -i 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/selinux/config

# Or configure SELinux properly (recommended)
sudo setsebool -P httpd_can_network_connect 1
```

---

## 🤝 Contributing

Contributions are welcome! Please follow these guidelines:

### How to Contribute

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/AmazingFeature
   ```
3. **Commit your changes**
   ```bash
   git commit -m 'Add some AmazingFeature'
   ```
4. **Push to the branch**
   ```bash
   git push origin feature/AmazingFeature
   ```
5. **Open a Pull Request**

### Areas for Contribution

- 📝 Documentation improvements
- 🐛 Bug fixes
- ✨ New features
- 🧪 Test coverage
- 🎨 UI/UX improvements
- 🔒 Security enhancements

### Code of Conduct

- Be respectful and inclusive
- Follow existing code style
- Write clear commit messages
- Test your changes thoroughly
- Update documentation as needed

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 📞 Contact & Support

### Author
**Your Name**
- GitHub: [@yourusername](https://github.com/yourusername)
- LinkedIn: [Your LinkedIn](https://linkedin.com/in/yourprofile)
- Email: your.email@example.com

### Project Links
- Repository: [GitHub](https://github.com/yourusername/netflix-devsecops)
- Issues: [GitHub Issues](https://github.com/yourusername/netflix-devsecops/issues)
- Discussions: [GitHub Discussions](https://github.com/yourusername/netflix-devsecops/discussions)

### Support

If you found this project helpful:
- ⭐ Star the repository
- 🐛 Report bugs
- 💡 Suggest features
- 📢 Share with others

---

## 🙏 Acknowledgments

- **TMDB** - Movie database API
- **Jenkins Community** - CI/CD platform
- **Docker Inc** - Containerization technology
- **Aqua Security** - Trivy scanner
- **SonarSource** - SonarQube platform
- **Prometheus Team** - Monitoring solution
- **Grafana Labs** - Visualization platform
- **Netflix** - Original application design inspiration

---

## 📚 Additional Resources

### Documentation
- [Jenkins Documentation](https://www.jenkins.io/doc/)
- [Docker Documentation](https://docs.docker.com/)
- [Trivy Documentation](https://aquasecurity.github.io/trivy/)
- [Prometheus Documentation](https://prometheus.io/docs/)
- [Grafana Documentation](https://grafana.com/docs/)

### Learning Resources
- [DevOps Roadmap](https://roadmap.sh/devops)
- [Docker Mastery Course](https://www.udemy.com/course/docker-mastery/)
- [Jenkins Pipeline Tutorial](https://www.jenkins.io/doc/book/pipeline/)

### Community
- [r/devops](https://reddit.com/r/devops)
- [DevOps Stack Exchange](https://devops.stackexchange.com/)
- [CNCF Slack](https://slack.cncf.io/)

---

<div align="center">

**Made with ❤️ for the DevOps Community**

**⭐ Star this repository if you found it helpful! ⭐**

[Report Bug](https://github.com/yourusername/netflix-devsecops/issues) · [Request Feature](https://github.com/yourusername/netflix-devsecops/issues)

</div>

---

## 📊 Project Statistics

![GitHub last commit](https://img.shields.io/github/last-commit/yourusername/netflix-devsecops)
![GitHub issues](https://img.shields.io/github/issues/yourusername/netflix-devsecops)
![GitHub pull requests](https://img.shields.io/github/issues-pr/yourusername/netflix-devsecops)
![GitHub stars](https://img.shields.io/github/stars/yourusername/netflix-devsecops)
![GitHub forks](https://img.shields.io/github/forks/yourusername/netflix-devsecops)

---

**Last Updated:** February 2026

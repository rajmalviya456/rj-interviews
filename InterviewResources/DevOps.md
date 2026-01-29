# DevOps, Cloud & Infrastructure Interview Handbook

**Target Role:** DevOps Engineer, SRE, Cloud Architect, Platform Engineer  
**Focus:** Fundamentals to Advanced Production-Level Concepts

---

## Table of Contents

### Section 1 — DevOps Fundamentals
- What is DevOps
- DevOps Culture & Principles
- DevOps Lifecycle
- DevOps vs SRE vs Platform Engineering
- Key Metrics (DORA Metrics)

### Section 2 — Linux & Shell Scripting
- Essential Linux Commands
- File Permissions & Ownership
- Process Management
- Process Signals (SIGTERM vs SIGKILL)
- Shell Scripting Basics
- Cron Jobs & Scheduling
- System Monitoring Commands

### Section 3 — Version Control (Git)
- Git Fundamentals
- Branching Strategies
- Git Workflows (GitFlow, Trunk-Based)
- Merge vs Rebase
- Git Hooks
- Common Git Scenarios

### Section 4 — CI/CD Pipelines
- What is CI/CD
- CI vs CD vs CD (Continuous Delivery vs Deployment)
- Pipeline Stages
- Build Artifacts
- Testing Strategies in CI/CD
- Pipeline as Code
- Blue-Green & Canary Deployments
- Rollback Strategies

### Section 5 — Jenkins
- Jenkins Architecture
- Master-Agent Setup
- Jenkinsfile & Declarative Pipelines
- Shared Libraries
- Jenkins Plugins
- Security & Credentials Management
- Distributed Builds
- Jenkins Best Practices

### Section 6 — Docker & Containerization
- What is Containerization
- Docker Architecture
- Docker Images & Containers
- Dockerfile Best Practices
- Docker Networking
- Docker Volumes & Storage
- Docker Compose
- Multi-Stage Builds
- Image Optimization
- Container Security

### Section 7 — Kubernetes (K8s)
- Kubernetes Architecture
- Master & Worker Node Components
- Pods, ReplicaSets, Deployments
- Services & Networking
- ConfigMaps & Secrets
- Persistent Volumes & Claims
- StatefulSets vs Deployments
- DaemonSets & Jobs
- CronJobs & Scheduled Jobs
- Ingress Controllers
- Helm Charts
- RBAC & Security
- Resource Management (Requests/Limits)
- Horizontal Pod Autoscaler (HPA)
- Kubernetes Troubleshooting

### Section 8 — Infrastructure as Code (IaC)
- What is IaC
- Declarative vs Imperative
- IaC Benefits & Best Practices
- State Management
- Drift Detection

### Section 9 — Terraform
- Terraform Architecture
- Providers & Resources
- Variables & Outputs
- State Files & Remote Backends
- Modules
- Workspaces
- Multi-Cloud Architecture
- Multi-Environment Handling
- Terraform Import
- Best Practices
- Common Interview Scenarios

### Section 10 — Ansible
- Ansible Architecture
- Inventory Files
- Playbooks & Plays
- Modules & Tasks
- Roles & Collections
- Variables & Facts
- Handlers & Templates
- Ansible Vault
- Idempotency
- Ansible vs Terraform

### Section 11 — AWS Cloud
- AWS Global Infrastructure
- IAM (Identity & Access Management)
- EC2 (Compute)
- VPC (Networking)
- S3 (Storage)
- RDS & DynamoDB (Databases)
- Lambda (Serverless)
- ECS & EKS (Containers)
- ECR (Elastic Container Registry)
- CloudFormation
- CloudWatch & Monitoring
- Route 53 (DNS)
- Load Balancers (ALB, NLB)
- CloudFront CDN
- Auto Scaling
- Security Best Practices

### Section 12 — Azure Cloud
- Azure Resource Model
- Azure Active Directory (Entra ID)
- Virtual Machines & Scale Sets
- Azure Virtual Network
- Azure Storage
- Azure SQL & Cosmos DB
- Azure Functions
- AKS (Azure Kubernetes Service)
- Azure DevOps
- Azure Monitor & Log Analytics
- ARM Templates & Bicep

### Section 13 — GCP (Google Cloud Platform)
- GCP Resource Hierarchy
- IAM & Service Accounts
- Compute Engine & GKE
- VPC & Networking
- Cloud Storage (Blob Storage)
- Cloud SQL & BigQuery
- Cloud Functions & Cloud Run
- Cloud Build
- Stackdriver Monitoring

### Section 14 — Monitoring & Observability
- Observability Pillars (Logs, Metrics, Traces)
- Prometheus
- Grafana
- ELK Stack (Elasticsearch, Logstash, Kibana)
- DataDog
- New Relic
- APM Tools Comparison
- Alerting Strategies
- SLI, SLO, SLA
- Incident Management

### Section 15 — Performance & Optimization
- Performance Testing Types
- Load Testing Tools
- Capacity Planning
- Bottleneck Identification
- Caching Strategies
- CDN & Edge Computing
- Database Optimization

### Section 16 — Scenario-Based Questions
- Production Incident Scenarios
- Deployment Failures
- Scaling Challenges
- Security Incidents
- Cost Optimization
- Migration Scenarios

---

## Section 1 — DevOps Fundamentals

### What is DevOps?

> **ELI5**: DevOps is like a relay race where developers and operations teams pass the baton smoothly instead of throwing it over a wall. Everyone works together so software goes from idea to production faster and more reliably.

**Definition**: DevOps is a set of practices, cultural philosophies, and tools that increase an organization's ability to deliver applications and services at high velocity.

**The Problem DevOps Solves**:
- **Before DevOps (Silos)**: Developers wrote code and "threw it over the wall" to Operations. Ops would struggle to deploy it. Blame games ensued.
- **After DevOps**: Dev and Ops collaborate throughout the entire lifecycle. Same team owns building AND running the software.

**Core Principles (CALMS)**:
| Principle | Description |
| :--- | :--- |
| **C**ulture | Breaking down silos, shared responsibility |
| **A**utomation | Automate repetitive tasks (builds, tests, deployments) |
| **L**ean | Eliminate waste, continuous improvement |
| **M**easurement | Track metrics to improve (deployment frequency, lead time) |
| **S**haring | Share knowledge, tools, and responsibilities |

---

### DevOps Lifecycle

The DevOps lifecycle is an infinite loop representing continuous improvement:

```
Plan → Code → Build → Test → Release → Deploy → Operate → Monitor → (back to Plan)
```

| Phase | Activities | Tools |
| :--- | :--- | :--- |
| **Plan** | Requirements, sprint planning | Jira, Azure Boards |
| **Code** | Writing code, code review | VS Code, Git, GitHub |
| **Build** | Compile, create artifacts | Maven, Gradle, npm |
| **Test** | Unit, integration, security testing | JUnit, Selenium, SonarQube |
| **Release** | Version, approve for production | Jenkins, GitLab CI |
| **Deploy** | Push to production environments | Kubernetes, Ansible, Terraform |
| **Operate** | Run, scale, maintain | Docker, K8s, AWS |
| **Monitor** | Observe, alert, analyze | Prometheus, Grafana, ELK |

---

### DevOps vs SRE vs Platform Engineering

| Aspect | DevOps | SRE | Platform Engineering |
| :--- | :--- | :--- | :--- |
| **Focus** | Culture & automation | Reliability & availability | Internal developer platforms |
| **Origin** | Agile movement | Google | Evolution of DevOps |
| **Key Metric** | Deployment frequency | SLO/Error budgets | Developer productivity |
| **Responsibility** | CI/CD, automation | Incident response, capacity | Self-service infrastructure |
| **Approach** | Breaking silos | Software engineering for ops | Building internal products |

---

### DORA Metrics

The DevOps Research and Assessment (DORA) team identified 4 key metrics that predict software delivery performance:

| Metric | Definition | Elite Performance |
| :--- | :--- | :--- |
| **Deployment Frequency** | How often code is deployed to production | On-demand (multiple per day) |
| **Lead Time for Changes** | Time from commit to production | Less than 1 hour |
| **Mean Time to Recover (MTTR)** | Time to recover from a failure | Less than 1 hour |
| **Change Failure Rate** | Percentage of deployments causing failures | 0-15% |

---

## Section 2 — Linux & Shell Scripting

### Essential Linux Commands

**File Operations**:
```bash
ls -la          # List all files with details
cp -r src dest  # Copy recursively
mv old new      # Move/rename
rm -rf dir      # Remove directory (DANGEROUS)
find /path -name "*.log" -mtime +7 -delete  # Find and delete old logs
```

**Text Processing**:
```bash
cat file.txt              # Display file
grep -r "pattern" /path   # Search recursively
awk '{print $1}' file     # Print first column
sed 's/old/new/g' file    # Find and replace
tail -f /var/log/app.log  # Follow log file
head -n 100 file          # First 100 lines
wc -l file                # Count lines
```

**System Information**:
```bash
df -h           # Disk usage
free -m         # Memory usage
top / htop      # Process monitoring
ps aux          # All processes
netstat -tulpn  # Network connections
lsof -i :8080   # What's using port 8080
```

---

### File Permissions & Ownership

```
-rwxr-xr-- 1 user group 1234 Jan 28 10:00 script.sh
│└┬┘└┬┘└┬┘
│ │  │  └── Others: read only (4)
│ │  └───── Group: read + execute (5)
│ └──────── Owner: read + write + execute (7)
└────────── File type (- = file, d = directory)
```

**Permission Values**: r=4, w=2, x=1

```bash
chmod 755 script.sh   # rwxr-xr-x
chmod u+x script.sh   # Add execute for owner
chown user:group file # Change ownership
```

---

### Shell Scripting Basics

```bash
#!/bin/bash

# Variables
NAME="DevOps"
echo "Hello, $NAME"

# Conditionals
if [ -f "/path/to/file" ]; then
    echo "File exists"
elif [ -d "/path/to/dir" ]; then
    echo "Directory exists"
else
    echo "Not found"
fi

# Loops
for server in web1 web2 web3; do
    ssh $server "uptime"
done

# Functions
deploy() {
    local env=$1
    echo "Deploying to $env..."
}
deploy "production"

# Error handling
set -e  # Exit on error
set -o pipefail  # Catch pipe errors
```

---

### Process Signals (SIGTERM vs SIGKILL)

### Understanding Process Signals

> **ELI5**: Signals are like messages sent to a running program. SIGTERM is a polite "please stop" that lets the program clean up, while SIGKILL is an immediate "STOP NOW" that doesn't give the program any choice.

```
┌────────────┬────────┬────────────┬────────────────┬──────────────┐
│  Signal    │ Number │ Can Catch? │ Default Action │ Use Case     │
├────────────┼────────┼────────────┼────────────────┼──────────────┤
│  SIGTERM   │   15   │    Yes     │   Terminate    │ Graceful     │
│  SIGKILL   │    9   │    No      │   Kill         │ Force stop   │
│  SIGINT    │    2   │    Yes     │   Interrupt    │ Ctrl+C       │
│  SIGHUP    │    1   │    Yes     │   Hangup       │ Config reload│
│  SIGQUIT   │    3   │    Yes     │   Quit + core  │ Debug dump   │
│  SIGSTOP   │   19   │    No      │   Stop process │ Pause        │
│  SIGCONT   │   18   │    Yes     │   Continue     │ Resume       │
└────────────┴────────┴────────────┴────────────────┴──────────────┘
```

---

### SIGTERM (Signal 15) - Graceful Termination

**Characteristics**:
- **Default termination signal** sent by `kill` command
- **Can be caught and handled** by applications
- Allows process to perform cleanup operations
- Used by Kubernetes for pod termination

**What Happens**:
```
Application receives SIGTERM
        │
        ▼
┌───────────────────────────────────┐
│  Signal Handler Executes:         │
│  • Close database connections     │
│  • Flush buffers to disk          │
│  • Complete in-flight requests    │
│  • Release file locks             │
│  • Notify dependent services      │
│  • Save state if needed           │
└───────────────────────────────────┘
        │
        ▼
    Process Exits Gracefully
```

**Example - Handling SIGTERM in Python**:
```python
import signal
import sys
import time

def graceful_shutdown(signum, frame):
    print("Received SIGTERM, shutting down gracefully...")
    # Close database connections
    db.close()
    # Flush any pending writes
    cache.flush()
    # Complete in-flight requests
    server.stop(grace_period=30)
    print("Cleanup complete, exiting.")
    sys.exit(0)

# Register the signal handler
signal.signal(signal.SIGTERM, graceful_shutdown)

# Main application logic
while True:
    process_requests()
```

**Example - Handling SIGTERM in Node.js**:
```javascript
process.on('SIGTERM', async () => {
  console.log('SIGTERM received, starting graceful shutdown...');
  
  // Stop accepting new connections
  server.close();
  
  // Wait for existing connections to complete
  await new Promise(resolve => setTimeout(resolve, 5000));
  
  // Close database connections
  await database.disconnect();
  
  console.log('Graceful shutdown complete');
  process.exit(0);
});
```

---

### SIGKILL (Signal 9) - Forced Termination

**Characteristics**:
- **Cannot be caught, blocked, or ignored**
- Kernel immediately terminates the process
- No cleanup operations possible
- Used as last resort when SIGTERM fails

**Why SIGKILL is Dangerous**:
```
┌──────────────────────────────────────────────────────────────────┐
│                     SIGKILL Consequences                         │
├──────────────────────────────────────────────────────────────────┤
│  ❌ Data loss: In-memory data not written to disk                │
│  ❌ Corrupted files: Partial writes may corrupt data             │
│  ❌ Resource leaks: File handles, sockets not released           │
│  ❌ Transaction failures: Database transactions left incomplete  │
│  ❌ Lock files: May leave stale lock files                       │
│  ❌ Child processes: Orphaned processes may continue running     │
└──────────────────────────────────────────────────────────────────┘
```

**When to Use SIGKILL**:
- Process is not responding to SIGTERM
- Process is in uninterruptible sleep (D state)
- Zombie processes (though won't help)
- Malicious processes that ignore signals

---

### Kubernetes Pod Termination Lifecycle

```
┌────────────────────────────────────────────────────────────────────┐
│               Kubernetes Pod Termination Flow                      │
└────────────────────────────────────────────────────────────────────┘

1. Pod receives delete request
        │
        ▼
2. Pod marked as "Terminating"
   • Removed from Service endpoints
   • No new traffic sent to pod
        │
        ▼
3. PreStop hook executes (if defined)
   • Custom commands/HTTP calls
   • Blocks until complete or timeout
        │
        ▼
4. SIGTERM sent to main container process (PID 1)
        │
        ▼
5. terminationGracePeriodSeconds countdown starts (default: 30s)
        │
        ▼
6. If process still running after grace period:
   SIGKILL sent (forced termination)
        │
        ▼
7. Pod removed from API server
```

**Pod Spec with Grace Period**:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: graceful-app
spec:
  terminationGracePeriodSeconds: 60  # Allow 60s for graceful shutdown
  containers:
    - name: app
      image: myapp:v1
      lifecycle:
        preStop:
          exec:
            command: ["/bin/sh", "-c", "sleep 5"]  # Allow LB to drain
```

---

### Best Practices for Signal Handling

| Practice | Description |
| :--- | :--- |
| **Always handle SIGTERM** | Implement graceful shutdown in all applications |
| **Set appropriate grace periods** | Match `terminationGracePeriodSeconds` to your cleanup time |
| **Use preStop hooks** | Allow load balancers to drain connections |
| **Complete in-flight requests** | Don't drop active requests |
| **Close connections properly** | Database, cache, message queue connections |
| **Log shutdown progress** | Help debugging if shutdown hangs |
| **Test shutdown behavior** | Verify cleanup works as expected |

---

### Sending Signals in Linux

```bash
# Send SIGTERM (default, graceful)
kill <PID>
kill -15 <PID>
kill -SIGTERM <PID>

# Send SIGKILL (force, last resort)
kill -9 <PID>
kill -SIGKILL <PID>

# Send to all processes by name
pkill -TERM myapp
pkill -9 myapp

# Send to process group
kill -TERM -<PGID>

# View process signals
kill -l  # List all signals

# Check process state
ps aux | grep <PID>
# States: R=running, S=sleeping, D=disk sleep, Z=zombie, T=stopped
```

---

## Section 3 — Version Control (Git)

### Git Fundamentals

**Core Concepts**:
- **Repository**: Project folder tracked by Git
- **Commit**: Snapshot of changes with unique SHA
- **Branch**: Independent line of development
- **HEAD**: Pointer to current branch/commit

**Essential Commands**:
```bash
git init                    # Initialize repo
git clone <url>             # Clone remote repo
git add .                   # Stage all changes
git commit -m "message"     # Commit with message
git push origin main        # Push to remote
git pull origin main        # Pull latest changes
git status                  # Check current state
git log --oneline -10       # View recent commits
```

---

### Branching Strategies

**GitFlow**:
```
main ──────●──────────────●──────────●──── (production releases)
            \            /          /
develop ─────●──●──●──●──●──●──●──●──── (integration branch)
              \      /    \    /
feature ───────●──●──      ●──●
```
- `main`: Production-ready code
- `develop`: Integration branch
- `feature/*`: New features
- `release/*`: Prepare releases
- `hotfix/*`: Emergency fixes

**Trunk-Based Development**:
- Single `main` branch
- Short-lived feature branches (< 1 day)
- Feature flags for incomplete work
- Better for CI/CD

---

### Merge vs Rebase

**Merge**:
```bash
git checkout main
git merge feature-branch
```
- Creates a merge commit
- Preserves complete history
- Safe for shared branches

**Rebase**:
```bash
git checkout feature-branch
git rebase main
```
- Replays commits on top of main
- Creates linear history
- **Never rebase shared/public branches**

**Golden Rule**: Rebase local branches, merge shared branches.

---

## Section 4 — CI/CD Pipelines

### What is CI/CD?

| Term | Full Name | Description |
| :--- | :--- | :--- |
| **CI** | Continuous Integration | Automatically build and test code on every commit |
| **CD** | Continuous Delivery | Automatically prepare release; manual approval for production |
| **CD** | Continuous Deployment | Automatically deploy every change to production |

```
Code Commit → Build → Unit Tests → Integration Tests → Deploy to Staging → (Approval) → Deploy to Prod
              └────────── CI ──────────────┘ └───────────── CD ─────────────────────────────┘
```

---

### Pipeline Stages

A typical CI/CD pipeline includes:

| Stage | Purpose | Example Tools |
| :--- | :--- | :--- |
| **Source** | Trigger on code changes | GitHub, GitLab, Bitbucket |
| **Build** | Compile code, create artifacts | Maven, Gradle, Docker |
| **Test** | Unit, integration, security tests | JUnit, pytest, OWASP ZAP |
| **Analyze** | Code quality, vulnerability scan | SonarQube, Snyk |
| **Deploy** | Push to environments | Kubernetes, Terraform |
| **Verify** | Smoke tests, health checks | Selenium, curl |

---

### Deployment Strategies

**Blue-Green Deployment**:
```
                    Load Balancer
                         │
          ┌──────────────┴──────────────┐
          ▼                             ▼
     ┌─────────┐                  ┌─────────┐
     │  Blue   │                  │  Green  │
     │ (v1.0)  │                  │ (v1.1)  │
     │ ACTIVE  │                  │  IDLE   │
     └─────────┘                  └─────────┘
```
- Two identical environments
- Switch traffic instantly
- Easy rollback (switch back)

**Canary Deployment**:
```
Traffic: 90% → v1.0 (Stable)
         10% → v1.1 (Canary)
```
- Gradually shift traffic
- Monitor for errors
- Roll back if issues detected

**Rolling Deployment**:
- Update instances one at a time
- No downtime
- Mixed versions during deployment

---

## Section 5 — Jenkins

### Jenkins Architecture

```
┌─────────────────────────────────────────────────────┐
│                   Jenkins Master                    │
│  ┌─────────────┐  ┌───────────┐  ┌───────────────┐  │
│  │  Scheduler  │  │  Web UI   │  │  Plugin Mgmt  │  │
│  └─────────────┘  └───────────┘  └───────────────┘  │
└────────────────────────┬────────────────────────────┘
                         │
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
     ┌─────────┐    ┌─────────┐    ┌─────────┐
     │ Agent 1 │    │ Agent 2 │    │ Agent 3 │
     │ (Linux) │    │(Windows)│    │(Docker) │
     └─────────┘    └─────────┘    └─────────┘
```

**Components**:
- **Master**: Schedules jobs, serves UI, manages agents
- **Agent**: Executes build jobs
- **Executor**: Thread on agent that runs a build
- **Job/Project**: Runnable task

---

### Jenkinsfile (Declarative Pipeline)

```groovy
pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE = 'myapp:${BUILD_NUMBER}'
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/org/repo.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        
        stage('Test') {
            parallel {
                stage('Unit Tests') {
                    steps {
                        sh 'mvn test'
                    }
                }
                stage('Integration Tests') {
                    steps {
                        sh 'mvn verify -Pintegration'
                    }
                }
            }
        }
        
        stage('Docker Build') {
            steps {
                sh 'docker build -t ${DOCKER_IMAGE} .'
            }
        }
        
        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                sh 'kubectl apply -f k8s/'
            }
        }
    }
    
    post {
        success {
            slackSend message: "Build succeeded: ${env.JOB_NAME}"
        }
        failure {
            slackSend message: "Build failed: ${env.JOB_NAME}"
        }
    }
}
```

---

## Section 6 — Docker & Containerization

### What is Containerization?

> **ELI5**: A container is like a lunchbox. Everything your app needs (code, libraries, settings) is packed together. It works the same whether you're at school, work, or home.

**Containers vs VMs**:

| Aspect | Container | Virtual Machine |
| :--- | :--- | :--- |
| **Size** | MBs | GBs |
| **Startup** | Seconds | Minutes |
| **Isolation** | Process-level | Hardware-level |
| **OS** | Shares host kernel | Full OS per VM |
| **Overhead** | Minimal | Significant |
| **Use Case** | Microservices, CI/CD | Legacy apps, different OS |

---

### Docker Architecture

```
┌──────────────────────────────────────────────────────┐
│                     Docker Host                      │
│  ┌──────────────────────────────────────────────┐    │
│  │           Docker Daemon (dockerd)            │    │
│  │  ┌───────────┐ ┌───────────┐ ┌───────────┐   │    │
│  │  │ Container │ │ Container │ │ Container │   │    │
│  │  │  (App1)   │ │  (App2)   │ │   (DB)    │   │    │
│  │  └───────────┘ └───────────┘ └───────────┘   │    │
│  └──────────────────────────────────────────────┘    │
│  ┌──────────────────────────────────────────────┐    │
│  │               Host OS Kernel                 │    │
│  └──────────────────────────────────────────────┘    │
└──────────────────────────────────────────────────────┘
        ▲
        │ Docker CLI / API
        ▼
   ┌──────────┐
   │  Client  │
   └──────────┘
```

**Key Components**:
- **Docker Client**: CLI to interact with daemon
- **Docker Daemon**: Builds, runs, manages containers
- **Docker Registry**: Stores images (Docker Hub, ECR, ACR)
- **Image**: Read-only template for containers
- **Container**: Running instance of an image

---

### Dockerfile Best Practices

```dockerfile
# Use specific version, not 'latest'
FROM python:3.11-slim

# Set working directory
WORKDIR /app

# Copy dependency files first (layer caching)
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY . .

# Create non-root user
RUN useradd -m appuser && chown -R appuser:appuser /app
USER appuser

# Expose port (documentation)
EXPOSE 8000

# Health check
HEALTHCHECK --interval=30s --timeout=3s \
    CMD curl -f http://localhost:8000/health || exit 1

# Use exec form for signal handling
CMD ["python", "app.py"]
```

**Best Practices**:
1. Use specific base image versions
2. Minimize layers (combine RUN commands)
3. Leverage layer caching (copy dependencies first)
4. Use `.dockerignore` to exclude files
5. Run as non-root user
6. Use multi-stage builds for smaller images

---

### Multi-Stage Builds

```dockerfile
# Stage 1: Build
FROM golang:1.21 AS builder
WORKDIR /app
COPY . .
RUN CGO_ENABLED=0 go build -o myapp

# Stage 2: Runtime
FROM alpine:3.18
RUN apk add --no-cache ca-certificates
COPY --from=builder /app/myapp /myapp
CMD ["/myapp"]
```

**Benefits**:
- Build image: ~1GB → Production image: ~20MB
- No build tools in production (security)
- Smaller attack surface

---

### Docker Networking

| Network Type | Description | Use Case |
| :--- | :--- | :--- |
| **bridge** | Default. Containers on same bridge can communicate | Single host, development |
| **host** | Container uses host's network directly | Performance-critical apps |
| **none** | No networking | Security isolation |
| **overlay** | Multi-host networking | Docker Swarm, clusters |

```bash
# Create custom network
docker network create mynetwork

# Run container on network
docker run --network mynetwork --name web nginx

# Containers can reach each other by name
docker run --network mynetwork alpine ping web
```

---

### Docker Compose

```yaml
version: '3.8'

services:
  web:
    build: .
    ports:
      - "8000:8000"
    environment:
      - DATABASE_URL=postgres://db:5432/app
    depends_on:
      - db
    networks:
      - app-network
    restart: unless-stopped

  db:
    image: postgres:15
    volumes:
      - postgres_data:/var/lib/postgresql/data
    environment:
      - POSTGRES_PASSWORD=secret
    networks:
      - app-network

networks:
  app-network:
    driver: bridge

volumes:
  postgres_data:
```

**Commands**:
```bash
docker-compose up -d       # Start all services
docker-compose down        # Stop and remove
docker-compose logs -f     # Follow logs
docker-compose ps          # List services
docker-compose exec web sh # Shell into container
```

---

## Section 7 — Kubernetes (K8s)

### What is Kubernetes?

> **ELI5**: Kubernetes is like an airport traffic controller for containers. It decides where containers land (which server), makes sure enough are running, and routes passengers (traffic) to them.

**Key Features**:
- **Container Orchestration**: Manages container lifecycle
- **Self-Healing**: Restarts failed containers
- **Scaling**: Horizontal auto-scaling
- **Load Balancing**: Distributes traffic
- **Rolling Updates**: Zero-downtime deployments
- **Secret Management**: Secure configuration

---

### Kubernetes Architecture

```
┌──────────────────────────────────────────────────────────────────┐
│                     Control Plane (Master)                       │
│  ┌─────────────┐  ┌────────────┐  ┌────────────┐  ┌────────────┐ │
│  │ API Server  │  │ Scheduler  │  │ Controller │  │    etcd    │ │
│  │             │  │            │  │  Manager   │  │  (state)   │ │
│  └─────────────┘  └────────────┘  └────────────┘  └────────────┘ │
└──────────────────────────────┬───────────────────────────────────┘
                               │
         ┌─────────────────────┼─────────────────────┐
         ▼                     ▼                     ▼
 ┌───────────────┐     ┌───────────────┐     ┌───────────────┐
 │  Worker Node  │     │  Worker Node  │     │  Worker Node  │
 │ ┌───────────┐ │     │ ┌───────────┐ │     │ ┌───────────┐ │
 │ │  kubelet  │ │     │ │  kubelet  │ │     │ │  kubelet  │ │
 │ └───────────┘ │     │ └───────────┘ │     │ └───────────┘ │
 │ ┌───────────┐ │     │ ┌───────────┐ │     │ ┌───────────┐ │
 │ │kube-proxy │ │     │ │kube-proxy │ │     │ │kube-proxy │ │
 │ └───────────┘ │     │ └───────────┘ │     │ └───────────┘ │
 │ ┌────┐ ┌────┐ │     │ ┌────┐ ┌────┐ │     │ ┌────┐ ┌────┐ │
 │ │Pod1│ │Pod2│ │     │ │Pod3│ │Pod4│ │     │ │Pod5│ │Pod6│ │
 │ └────┘ └────┘ │     │ └────┘ └────┘ │     │ └────┘ └────┘ │
 └───────────────┘     └───────────────┘     └───────────────┘
```

**Control Plane Components**:
- **API Server**: Gateway to cluster, handles all REST requests
- **etcd**: Distributed key-value store for cluster state
- **Scheduler**: Assigns pods to nodes based on resources
- **Controller Manager**: Runs controllers (ReplicaSet, Deployment, etc.)

**Node Components**:
- **kubelet**: Agent ensuring containers run in pods
- **kube-proxy**: Network proxy, implements Services
- **Container Runtime**: Docker, containerd, CRI-O

---

### Core Workload Resources

**Pod** (Smallest deployable unit):
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
spec:
  containers:
    - name: nginx
      image: nginx:1.25
      ports:
        - containerPort: 80
```

**Deployment** (Manages ReplicaSets):
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:1.25
          ports:
            - containerPort: 80
          resources:
            requests:
              cpu: "100m"
              memory: "128Mi"
            limits:
              cpu: "200m"
              memory: "256Mi"
```

---

### Services & Networking

**Service Types**:

| Type | Description | Use Case |
| :--- | :--- | :--- |
| **ClusterIP** | Internal IP, only accessible within cluster | Internal microservices |
| **NodePort** | Exposes on each node's IP at static port | Development, testing |
| **LoadBalancer** | Creates external load balancer (cloud) | Production external access |
| **ExternalName** | Maps to external DNS name | External database access |

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: LoadBalancer
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
```

**Ingress** (HTTP/HTTPS routing):
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: app-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
    - host: app.example.com
      http:
        paths:
          - path: /api
            pathType: Prefix
            backend:
              service:
                name: api-service
                port:
                  number: 80
          - path: /
            pathType: Prefix
            backend:
              service:
                name: frontend-service
                port:
                  number: 80
```

---

### ConfigMaps & Secrets

**ConfigMap** (Non-sensitive configuration):
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  DATABASE_HOST: "postgres.default.svc.cluster.local"
  LOG_LEVEL: "info"
  config.json: |
    {
      "feature_flags": {
        "new_ui": true
      }
    }
```

**Secret** (Sensitive data, base64 encoded):
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: app-secret
type: Opaque
data:
  DB_PASSWORD: cGFzc3dvcmQxMjM=  # base64 encoded
  API_KEY: c2VjcmV0a2V5MTIz
```

**Using in Pod**:
```yaml
spec:
  containers:
    - name: app
      envFrom:
        - configMapRef:
            name: app-config
        - secretRef:
            name: app-secret
      volumeMounts:
        - name: config-volume
          mountPath: /etc/config
  volumes:
    - name: config-volume
      configMap:
        name: app-config
```

---

### Persistent Storage

```yaml
# PersistentVolumeClaim
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: postgres-pvc
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: gp2
  resources:
    requests:
      storage: 10Gi

---
# Using PVC in Deployment
spec:
  containers:
    - name: postgres
      image: postgres:15
      volumeMounts:
        - name: postgres-storage
          mountPath: /var/lib/postgresql/data
  volumes:
    - name: postgres-storage
      persistentVolumeClaim:
        claimName: postgres-pvc
```

**Access Modes**:
- `ReadWriteOnce` (RWO): Single node read-write
- `ReadOnlyMany` (ROX): Many nodes read-only
- `ReadWriteMany` (RWX): Many nodes read-write

---

### Horizontal Pod Autoscaler (HPA)

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: app-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: app-deployment
  minReplicas: 2
  maxReplicas: 10
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 70
    - type: Resource
      resource:
        name: memory
        target:
          type: Utilization
          averageUtilization: 80
```

---

### Kubernetes Troubleshooting Commands

```bash
# Cluster info
kubectl cluster-info
kubectl get nodes

# View resources
kubectl get pods -A                    # All namespaces
kubectl get pods -o wide               # More details
kubectl describe pod <pod-name>        # Full details

# Logs
kubectl logs <pod-name>                # Current logs
kubectl logs <pod-name> --previous     # Previous container logs
kubectl logs -f <pod-name>             # Follow logs

# Debug
kubectl exec -it <pod-name> -- sh      # Shell into pod
kubectl port-forward svc/my-svc 8080:80  # Local port forward

# Events
kubectl get events --sort-by=.metadata.creationTimestamp

# Resource usage
kubectl top nodes
kubectl top pods
```

---

### CronJobs & Scheduled Jobs

### Job vs CronJob

| Aspect | Job | CronJob |
| :--- | :--- | :--- |
| **Execution** | Runs once | Runs on schedule |
| **Trigger** | Manual or programmatic | Time-based (cron expression) |
| **Use Case** | One-time tasks, migrations | Recurring tasks, backups |
| **Creates** | Pod(s) directly | Job objects on schedule |

---

### Kubernetes Job

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: database-migration
spec:
  ttlSecondsAfterFinished: 3600  # Clean up after 1 hour
  backoffLimit: 3                 # Retry 3 times on failure
  activeDeadlineSeconds: 600      # Timeout after 10 minutes
  parallelism: 1                  # Run 1 pod at a time
  completions: 1                  # Need 1 successful completion
  template:
    spec:
      restartPolicy: OnFailure    # or Never
      containers:
        - name: migration
          image: myapp:migrate
          command: ["./migrate.sh"]
          env:
            - name: DATABASE_URL
              valueFrom:
                secretKeyRef:
                  name: db-secret
                  key: url
```

**Job Patterns**:
```
┌────────────────────────────────────────────────────────────────────┐
│                     Job Execution Patterns                         │
├────────────────────────────────────────────────────────────────────┤
│  Pattern          │ parallelism │ completions │ Use Case           │
├───────────────────┼─────────────┼─────────────┼────────────────────┤
│  Single Job       │      1      │      1      │ One-time task      │
│  Fixed Completion │      N      │      M      │ Process M items    │
│  Work Queue       │      N      │    unset    │ Queue processing   │
└────────────────────────────────────────────────────────────────────┘
```

---

### Kubernetes CronJob

```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: database-backup
  namespace: production
spec:
  schedule: "0 2 * * *"           # Daily at 2 AM
  timeZone: "America/New_York"     # K8s 1.27+
  concurrencyPolicy: Forbid        # Don't overlap
  successfulJobsHistoryLimit: 3    # Keep last 3 successful
  failedJobsHistoryLimit: 3        # Keep last 3 failed
  startingDeadlineSeconds: 300     # Miss deadline = skip
  suspend: false                   # Set true to pause
  jobTemplate:
    spec:
      ttlSecondsAfterFinished: 86400
      backoffLimit: 2
      template:
        spec:
          restartPolicy: OnFailure
          containers:
            - name: backup
              image: postgres:15
              command:
                - /bin/sh
                - -c
                - |
                  pg_dump $DATABASE_URL | gzip > /backup/db-$(date +%Y%m%d).sql.gz
                  aws s3 cp /backup/db-*.sql.gz s3://my-backups/
              envFrom:
                - secretRef:
                    name: backup-credentials
              volumeMounts:
                - name: backup-volume
                  mountPath: /backup
          volumes:
            - name: backup-volume
              emptyDir: {}
```

---

### Cron Expression Syntax

```
┌───────────────────────── minute (0 - 59)
│ ┌─────────────────────── hour (0 - 23)
│ │ ┌───────────────────── day of month (1 - 31)
│ │ │ ┌─────────────────── month (1 - 12)
│ │ │ │ ┌───────────────── day of week (0 - 6, Sun=0)
│ │ │ │ │
* * * * *
```

**Common Schedules**:
| Expression | Description |
| :--- | :--- |
| `*/5 * * * *` | Every 5 minutes |
| `0 * * * *` | Every hour |
| `0 0 * * *` | Daily at midnight |
| `0 2 * * *` | Daily at 2 AM |
| `0 0 * * 0` | Weekly on Sunday midnight |
| `0 0 1 * *` | Monthly on 1st at midnight |
| `0 9-17 * * 1-5` | Weekdays 9 AM - 5 PM, hourly |
| `0 0 1 1 *` | Yearly on Jan 1st |

---

### CronJob Concurrency Policies

```yaml
spec:
  concurrencyPolicy: Allow    # Default: allow concurrent jobs
  # concurrencyPolicy: Forbid   # Skip if previous still running
  # concurrencyPolicy: Replace  # Cancel previous, start new
```

| Policy | Behavior | Use Case |
| :--- | :--- | :--- |
| **Allow** | Multiple jobs can run simultaneously | Independent tasks |
| **Forbid** | Skip new job if previous still running | Prevent overlap |
| **Replace** | Cancel running job, start new one | Always run latest |

---

### CronJob Monitoring & Troubleshooting

```bash
# List CronJobs
kubectl get cronjobs

# Describe CronJob (see last schedule time)
kubectl describe cronjob database-backup

# List Jobs created by CronJob
kubectl get jobs --selector=job-name=database-backup-*

# View logs of most recent job
kubectl logs job/database-backup-28429452

# Manually trigger a CronJob
kubectl create job --from=cronjob/database-backup manual-backup

# Suspend a CronJob
kubectl patch cronjob database-backup -p '{"spec":{"suspend":true}}'

# Resume a CronJob
kubectl patch cronjob database-backup -p '{"spec":{"suspend":false}}'
```

---

### CronJob Best Practices

| Practice | Description |
| :--- | :--- |
| **Set `startingDeadlineSeconds`** | Prevent running stale jobs after downtime |
| **Use `concurrencyPolicy: Forbid`** | Avoid overlapping jobs for DB operations |
| **Set `activeDeadlineSeconds`** | Prevent runaway jobs |
| **Configure history limits** | Keep cluster clean |
| **Add monitoring/alerting** | Alert on job failures |
| **Use `ttlSecondsAfterFinished`** | Auto-cleanup completed jobs |
| **Specify timezone** | Ensure consistent scheduling |

---

## Section 8 — Infrastructure as Code (IaC)

### What is IaC?

> **ELI5**: Instead of clicking buttons in a web console to create servers, you write code that describes what infrastructure you want. The tool reads the code and creates everything automatically.

**Benefits**:
- **Version Control**: Track changes like application code
- **Consistency**: Same code = same infrastructure every time
- **Automation**: No manual clicking, reduce human error
- **Documentation**: Code IS the documentation
- **Speed**: Provision infrastructure in minutes

**Declarative vs Imperative**:

| Approach | Description | Example |
| :--- | :--- | :--- |
| **Declarative** | Define desired end state; tool figures out how | Terraform, CloudFormation |
| **Imperative** | Define step-by-step instructions | Ansible, Shell scripts |

---

## Section 9 — Terraform

### Terraform Architecture

```
┌─────────────────────────────────────────────────────┐
│             Terraform Configuration                 │
│   (main.tf, variables.tf, outputs.tf, etc.)         │
└────────────────────────┬────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────┐
│                  Terraform Core                     │
│  ┌─────────────┐  ┌──────────────┐  ┌────────────┐  │
│  │ State Mgmt  │  │ Plan Engine  │  │  Executor  │  │
│  └─────────────┘  └──────────────┘  └────────────┘  │
└────────────────────────┬────────────────────────────┘
                         │
         ┌───────────────┼───────────────┐
         ▼               ▼               ▼
    ┌─────────┐     ┌─────────┐     ┌─────────┐
    │   AWS   │     │  Azure  │     │   GCP   │
    │Provider │     │Provider │     │Provider │
    └─────────┘     └─────────┘     └─────────┘
```

---

### Terraform Workflow

```bash
terraform init      # Download providers, initialize backend
terraform plan      # Preview changes (dry run)
terraform apply     # Apply changes to infrastructure
terraform destroy   # Destroy all resources
```

---

### Complete Terraform Example

```hcl
# provider.tf
terraform {
  required_version = ">= 1.5"
  
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
  
  backend "s3" {
    bucket         = "my-terraform-state"
    key            = "prod/terraform.tfstate"
    region         = "us-east-1"
    encrypt        = true
    dynamodb_table = "terraform-locks"
  }
}

provider "aws" {
  region = var.aws_region
}

# variables.tf
variable "aws_region" {
  description = "AWS region"
  type        = string
  default     = "us-east-1"
}

variable "environment" {
  description = "Environment name"
  type        = string
}

variable "instance_type" {
  description = "EC2 instance type"
  type        = string
  default     = "t3.micro"
}

# main.tf
resource "aws_vpc" "main" {
  cidr_block           = "10.0.0.0/16"
  enable_dns_hostnames = true
  
  tags = {
    Name        = "${var.environment}-vpc"
    Environment = var.environment
  }
}

resource "aws_subnet" "public" {
  count             = 2
  vpc_id            = aws_vpc.main.id
  cidr_block        = "10.0.${count.index + 1}.0/24"
  availability_zone = data.aws_availability_zones.available.names[count.index]
  
  tags = {
    Name = "${var.environment}-public-${count.index + 1}"
  }
}

resource "aws_instance" "web" {
  ami           = data.aws_ami.amazon_linux.id
  instance_type = var.instance_type
  subnet_id     = aws_subnet.public[0].id
  
  tags = {
    Name = "${var.environment}-web"
  }
}

# outputs.tf
output "vpc_id" {
  description = "VPC ID"
  value       = aws_vpc.main.id
}

output "instance_public_ip" {
  description = "Public IP of web server"
  value       = aws_instance.web.public_ip
}
```

---

### Terraform State Management

**State File** (`terraform.tfstate`):
- Tracks real-world resources
- Maps config to actual infrastructure
- Contains sensitive data (encrypt!)

**Remote Backend Best Practices**:
```hcl
backend "s3" {
  bucket         = "my-terraform-state"
  key            = "env/prod/terraform.tfstate"
  region         = "us-east-1"
  encrypt        = true
  dynamodb_table = "terraform-locks"  # State locking
}
```

**State Commands**:
```bash
terraform state list                    # List resources in state
terraform state show aws_instance.web   # Show resource details
terraform state mv old.name new.name    # Rename resource
terraform state rm aws_instance.web     # Remove from state (not cloud!)
terraform import aws_instance.web i-12345  # Import existing resource
```

---

### Terraform Modules

```hcl
# modules/vpc/main.tf
variable "cidr_block" {}
variable "environment" {}

resource "aws_vpc" "this" {
  cidr_block = var.cidr_block
  tags = { Name = "${var.environment}-vpc" }
}

output "vpc_id" {
  value = aws_vpc.this.id
}

# Root main.tf
module "vpc" {
  source      = "./modules/vpc"
  cidr_block  = "10.0.0.0/16"
  environment = "prod"
}

# Use module output
resource "aws_subnet" "public" {
  vpc_id = module.vpc.vpc_id
  # ...
}
```

---

### Multi-Cloud Architecture

### Multi-Cloud Strategy

> **Why Multi-Cloud?**
> - Avoid vendor lock-in
> - Leverage best services from each provider
> - Geographic redundancy
> - Regulatory compliance
> - Cost optimization

```
┌────────────────────────────────────────────────────────────────────┐
│                    Multi-Cloud Architecture                        │
├────────────────────────────────────────────────────────────────────┤
│                                                                    │
│                    ┌─────────────────┐                             │
│                    │   Terraform     │                             │
│                    │   State (S3)    │                             │
│                    └────────┬────────┘                             │
│                             │                                      │
│         ┌───────────────────┼───────────────────┐                  │
│         ▼                   ▼                   ▼                  │
│   ┌───────────┐       ┌───────────┐       ┌───────────┐            │
│   │    AWS    │       │   Azure   │       │    GCP    │            │
│   ├───────────┤       ├───────────┤       ├───────────┤            │
│   │ • EKS     │       │ • AKS     │       │ • GKE     │            │
│   │ • RDS     │       │ • CosmosDB│       │ • BigQuery│            │
│   │ • S3      │       │ • Blob    │       │ • GCS     │            │
│   └───────────┘       └───────────┘       └───────────┘            │
│                                                                    │
└────────────────────────────────────────────────────────────────────┘
```

---

### Multi-Cloud Provider Configuration

```hcl
# providers.tf

terraform {
  required_version = ">= 1.5.0"
  
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "~> 3.0"
    }
    google = {
      source  = "hashicorp/google"
      version = "~> 5.0"
    }
  }
  
  backend "s3" {
    bucket         = "terraform-multicloud-state"
    key            = "global/terraform.tfstate"
    region         = "us-east-1"
    encrypt        = true
    dynamodb_table = "terraform-locks"
  }
}

# AWS Provider
provider "aws" {
  region = var.aws_region
  
  default_tags {
    tags = {
      Environment = var.environment
      ManagedBy   = "Terraform"
      Project     = var.project_name
    }
  }
}

# Azure Provider
provider "azurerm" {
  features {}
  
  subscription_id = var.azure_subscription_id
  tenant_id       = var.azure_tenant_id
}

# GCP Provider
provider "google" {
  project = var.gcp_project_id
  region  = var.gcp_region
}
```

---

### Multi-Cloud Module Structure

```
terraform/
├── modules/
│   ├── aws/
│   │   ├── vpc/
│   │   ├── eks/
│   │   ├── rds/
│   │   └── s3/
│   ├── azure/
│   │   ├── vnet/
│   │   ├── aks/
│   │   ├── sql/
│   │   └── storage/
│   ├── gcp/
│   │   ├── vpc/
│   │   ├── gke/
│   │   ├── cloudsql/
│   │   └── gcs/
│   └── common/
│       ├── dns/
│       └── monitoring/
├── environments/
│   ├── dev/
│   ├── staging/
│   └── prod/
└── main.tf
```

---

### Cross-Cloud Networking Example

```hcl
# AWS VPC
module "aws_vpc" {
  source  = "./modules/aws/vpc"
  
  cidr_block  = "10.0.0.0/16"
  environment = var.environment
}

# Azure VNet
module "azure_vnet" {
  source = "./modules/azure/vnet"
  
  address_space   = ["10.1.0.0/16"]
  resource_group  = azurerm_resource_group.main.name
  environment     = var.environment
}

# GCP VPC
module "gcp_vpc" {
  source = "./modules/gcp/vpc"
  
  network_name = "${var.project_name}-vpc"
  project      = var.gcp_project_id
}

# Cross-cloud VPN connections
resource "aws_vpn_connection" "aws_to_azure" {
  vpn_gateway_id      = aws_vpn_gateway.main.id
  customer_gateway_id = aws_customer_gateway.azure.id
  type                = "ipsec.1"
  static_routes_only  = true
}

resource "azurerm_virtual_network_gateway_connection" "azure_to_aws" {
  name                       = "azure-to-aws"
  resource_group_name        = azurerm_resource_group.main.name
  location                   = azurerm_resource_group.main.location
  type                       = "IPsec"
  virtual_network_gateway_id = azurerm_virtual_network_gateway.main.id
  local_network_gateway_id   = azurerm_local_network_gateway.aws.id
  shared_key                 = var.vpn_shared_key
}
```

---

### Multi-Environment Handling

### Environment Strategies Comparison

| Strategy | Pros | Cons | Best For |
| :--- | :--- | :--- | :--- |
| **Workspaces** | Simple, single codebase | Shared state file risks | Small teams |
| **Directory Structure** | Clear separation, flexibility | Code duplication | Most organizations |
| **Terragrunt** | DRY, powerful inheritance | Learning curve | Large enterprises |
| **Feature Flags** | Runtime flexibility | Complex conditionals | Dynamic configs |

---

### Strategy 1: Terraform Workspaces

```bash
# Create and switch workspaces
terraform workspace new dev
terraform workspace new staging
terraform workspace new prod

# List workspaces
terraform workspace list

# Switch workspace
terraform workspace select prod

# Current workspace
terraform workspace show
```

**Using Workspaces in Code**:
```hcl
# variables.tf
variable "environment_configs" {
  type = map(object({
    instance_type = string
    min_capacity  = number
    max_capacity  = number
  }))
  
  default = {
    dev = {
      instance_type = "t3.small"
      min_capacity  = 1
      max_capacity  = 2
    }
    staging = {
      instance_type = "t3.medium"
      min_capacity  = 2
      max_capacity  = 4
    }
    prod = {
      instance_type = "t3.large"
      min_capacity  = 3
      max_capacity  = 10
    }
  }
}

# main.tf
locals {
  environment = terraform.workspace
  config      = var.environment_configs[local.environment]
}

resource "aws_instance" "app" {
  instance_type = local.config.instance_type
  
  tags = {
    Environment = local.environment
  }
}
```

---

### Strategy 2: Directory Structure (Recommended)

```
terraform/
├── modules/                    # Reusable modules
│   ├── vpc/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── eks/
│   ├── rds/
│   └── app/
│
├── environments/
│   ├── dev/
│   │   ├── main.tf            # Module calls
│   │   ├── variables.tf
│   │   ├── terraform.tfvars   # Dev-specific values
│   │   ├── backend.tf         # Dev state config
│   │   └── outputs.tf
│   │
│   ├── staging/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── terraform.tfvars
│   │   ├── backend.tf
│   │   └── outputs.tf
│   │
│   └── prod/
│       ├── main.tf
│       ├── variables.tf
│       ├── terraform.tfvars
│       ├── backend.tf
│       └── outputs.tf
│
└── global/                     # Shared resources
    ├── iam/
    ├── dns/
    └── s3-state/
```

**Environment Main.tf Example**:
```hcl
# environments/prod/main.tf

module "vpc" {
  source = "../../modules/vpc"
  
  environment  = var.environment
  cidr_block   = var.vpc_cidr
  az_count     = 3
  enable_nat   = true
}

module "eks" {
  source = "../../modules/eks"
  
  cluster_name    = "${var.project_name}-${var.environment}"
  vpc_id          = module.vpc.vpc_id
  subnet_ids      = module.vpc.private_subnet_ids
  node_count      = var.eks_node_count
  instance_types  = var.eks_instance_types
}

module "rds" {
  source = "../../modules/rds"
  
  identifier     = "${var.project_name}-${var.environment}"
  engine_version = "15.4"
  instance_class = var.rds_instance_class
  multi_az       = true  # Always true for prod
  
  vpc_id             = module.vpc.vpc_id
  subnet_ids         = module.vpc.database_subnet_ids
  security_group_ids = [module.vpc.database_sg_id]
}
```

**Environment-Specific tfvars**:
```hcl
# environments/dev/terraform.tfvars
environment        = "dev"
vpc_cidr           = "10.0.0.0/16"
eks_node_count     = 2
eks_instance_types = ["t3.medium"]
rds_instance_class = "db.t3.small"

# environments/prod/terraform.tfvars
environment        = "prod"
vpc_cidr           = "10.100.0.0/16"
eks_node_count     = 5
eks_instance_types = ["m5.xlarge", "m5.2xlarge"]
rds_instance_class = "db.r5.xlarge"
```

---

### Strategy 3: Terragrunt (DRY Configuration)

```
infrastructure/
├── terragrunt.hcl              # Root config
├── dev/
│   ├── terragrunt.hcl
│   ├── vpc/
│   │   └── terragrunt.hcl
│   ├── eks/
│   │   └── terragrunt.hcl
│   └── rds/
│       └── terragrunt.hcl
├── staging/
│   └── ...
└── prod/
    └── ...
```

**Root terragrunt.hcl**:
```hcl
# terragrunt.hcl
remote_state {
  backend = "s3"
  generate = {
    path      = "backend.tf"
    if_exists = "overwrite"
  }
  config = {
    bucket         = "my-terraform-state"
    key            = "${path_relative_to_include()}/terraform.tfstate"
    region         = "us-east-1"
    encrypt        = true
    dynamodb_table = "terraform-locks"
  }
}

inputs = {
  project_name = "myapp"
  aws_region   = "us-east-1"
}
```

**Environment terragrunt.hcl**:
```hcl
# prod/terragrunt.hcl
include "root" {
  path = find_in_parent_folders()
}

inputs = {
  environment = "prod"
  vpc_cidr    = "10.100.0.0/16"
}
```

**Component terragrunt.hcl**:
```hcl
# prod/vpc/terragrunt.hcl
include "root" {
  path = find_in_parent_folders()
}

include "env" {
  path = "${dirname(find_in_parent_folders())}/prod/terragrunt.hcl"
}

terraform {
  source = "../../../modules/vpc"
}

inputs = {
  enable_nat_gateway = true
  az_count          = 3
}
```

---

### CI/CD Pipeline for Multi-Environment

```yaml
# .github/workflows/terraform.yml
name: Terraform Multi-Environment

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

env:
  TF_VERSION: "1.6.0"

jobs:
  determine-environment:
    runs-on: ubuntu-latest
    outputs:
      environment: ${{ steps.set-env.outputs.environment }}
    steps:
      - id: set-env
        run: |
          if [[ "${{ github.ref }}" == "refs/heads/main" ]]; then
            echo "environment=prod" >> $GITHUB_OUTPUT
          elif [[ "${{ github.ref }}" == "refs/heads/develop" ]]; then
            echo "environment=staging" >> $GITHUB_OUTPUT
          else
            echo "environment=dev" >> $GITHUB_OUTPUT
          fi

  terraform:
    needs: determine-environment
    runs-on: ubuntu-latest
    environment: ${{ needs.determine-environment.outputs.environment }}
    
    steps:
      - uses: actions/checkout@v4
      
      - uses: hashicorp/setup-terraform@v3
        with:
          terraform_version: ${{ env.TF_VERSION }}
      
      - name: Terraform Init
        working-directory: environments/${{ needs.determine-environment.outputs.environment }}
        run: terraform init
      
      - name: Terraform Plan
        working-directory: environments/${{ needs.determine-environment.outputs.environment }}
        run: terraform plan -out=tfplan
      
      - name: Terraform Apply
        if: github.ref == 'refs/heads/main' || github.ref == 'refs/heads/develop'
        working-directory: environments/${{ needs.determine-environment.outputs.environment }}
        run: terraform apply -auto-approve tfplan
```

---

## Section 10 — Ansible

### Ansible Architecture

```
┌─────────────────────────────────────────────────────┐
│                   Control Node                      │
│  ┌───────────┐  ┌────────────┐  ┌────────────────┐  │
│  │ Playbook  │  │  Inventory │  │  ansible.cfg   │  │
│  └───────────┘  └────────────┘  └────────────────┘  │
└────────────────────────┬────────────────────────────┘
                         │ SSH (agentless)
         ┌───────────────┼───────────────┐
         ▼               ▼               ▼
    ┌─────────┐     ┌─────────┐     ┌─────────┐
    │ Managed │     │ Managed │     │ Managed │
    │  Host 1 │     │  Host 2 │     │  Host 3 │
    └─────────┘     └─────────┘     └─────────┘
```

**Key Characteristics**:
- **Agentless**: Uses SSH, no agent installation
- **Idempotent**: Running twice = same result
- **YAML-based**: Easy to read and write
- **Push-based**: Control node pushes configs

---

### Inventory File

```ini
# inventory/production.ini
[webservers]
web1.example.com
web2.example.com

[dbservers]
db1.example.com ansible_user=admin

[production:children]
webservers
dbservers

[all:vars]
ansible_python_interpreter=/usr/bin/python3
```

---

### Ansible Playbook

```yaml
# playbooks/deploy_app.yml
---
- name: Deploy Web Application
  hosts: webservers
  become: yes
  vars:
    app_version: "1.2.3"
    app_port: 8080
  
  tasks:
    - name: Install required packages
      apt:
        name:
          - nginx
          - python3
          - python3-pip
        state: present
        update_cache: yes
    
    - name: Create application directory
      file:
        path: /opt/myapp
        state: directory
        owner: www-data
        mode: '0755'
    
    - name: Copy application files
      copy:
        src: files/app/
        dest: /opt/myapp/
        owner: www-data
      notify: Restart Application
    
    - name: Configure nginx
      template:
        src: templates/nginx.conf.j2
        dest: /etc/nginx/sites-available/myapp
      notify: Restart Nginx
    
    - name: Enable nginx site
      file:
        src: /etc/nginx/sites-available/myapp
        dest: /etc/nginx/sites-enabled/myapp
        state: link
  
  handlers:
    - name: Restart Nginx
      service:
        name: nginx
        state: restarted
    
    - name: Restart Application
      service:
        name: myapp
        state: restarted
```

---

### Ansible Roles

```
roles/
└── webserver/
    ├── tasks/
    │   └── main.yml
    ├── handlers/
    │   └── main.yml
    ├── templates/
    │   └── nginx.conf.j2
    ├── files/
    ├── vars/
    │   └── main.yml
    └── defaults/
        └── main.yml
```

**Using Roles**:
```yaml
- name: Configure web servers
  hosts: webservers
  roles:
    - common
    - webserver
    - role: monitoring
      vars:
        grafana_port: 3000
```

### Ansible Vault (Secret Management)
**Goal**: Encrypt sensitive data (passwords, API keys) so they aren't stored in plain text in Git.

**Commands**:
```bash
ansible-vault create secret.yml      # Create new encrypted file
ansible-vault view secret.yml        # View content
ansible-vault edit secret.yml        # Edit content
ansible-vault encrypt plain.yml      # Encrypt existing file
ansible-vault decrypt secret.yml     # Decrypt file
```

**Using in Playbook**:
```yaml
# Run playbook asking for password
ansible-playbook site.yml --ask-vault-pass

# Or use a password file
ansible-playbook site.yml --vault-password-file ~/.vault_pass
```

---

### Idempotency (The Core Concept)
**Definition**: An operation is idempotent if running it multiple times yields the **same result** as running it once, without intended side effects.

**Example**:
- *Non-Idempotent*: `echo "line" >> file.txt` (Run twice -> duplicates line).
- *Idempotent (Ansible)*: `lineinfile` module ensures the line exists. If it's already there, do nothing.

**Why it matters**:
- You can safely re-run an Ansible playbook on a server that is partially configured.
- If a network glitch stops execution halfway, you just run it again.

---

### Ansible vs Terraform

| Aspect | Terraform | Ansible |
| :--- | :--- | :--- |
| **Type** | Declarative IaC | Imperative Configuration Mgmt |
| **Best For** | Provisioning infrastructure | Configuring servers |
| **State** | Maintains state file | Stateless |
| **Agent** | None | None (SSH-based) |
| **Mutable** | Immutable (recreate resources) | Mutable (in-place changes) |
| **Typical Use** | Create EC2, VPC, RDS | Install packages, configure apps |

**Common Pattern**: Use Terraform to provision infrastructure, Ansible to configure it.

---

## Section 11 — AWS Cloud

### AWS Global Infrastructure

```
AWS Global
├── Regions (us-east-1, eu-west-1, ap-south-1, ...)
│   ├── Availability Zones (us-east-1a, us-east-1b, ...)
│   │   └── Data Centers
│   └── Edge Locations (CloudFront, Route 53)
```

- **Region**: Geographic area (25+ regions)
- **Availability Zone (AZ)**: Isolated data centers within a region
- **Edge Location**: CDN cache locations (400+ worldwide)

---

### IAM (Identity & Access Management)

**Core Concepts**:
- **User**: Individual identity with credentials
- **Group**: Collection of users (apply policies to groups)
- **Role**: Temporary identity assumed by services/users
- **Policy**: JSON document defining permissions

**Policy Example**:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Resource": "arn:aws:s3:::my-bucket/*"
    },
    {
      "Effect": "Deny",
      "Action": "s3:DeleteObject",
      "Resource": "*"
    }
  ]
}
```

**Best Practices**:
- Least privilege principle
- Use roles instead of long-term credentials
- Enable MFA for all users
- Rotate access keys regularly

---

### EC2 (Elastic Compute Cloud)

**Instance Types**:
| Family | Use Case | Example |
| :--- | :--- | :--- |
| **t** | General purpose, burstable | t3.micro, t3.large |
| **m** | General purpose, balanced | m6i.xlarge |
| **c** | Compute optimized | c6i.2xlarge |
| **r** | Memory optimized | r6i.large |
| **i** | Storage optimized | i3.xlarge |
| **g/p** | GPU instances | p4d.24xlarge |

**Pricing Models**:
- **On-Demand**: Pay per hour/second, no commitment
- **Reserved**: 1-3 year commitment, up to 72% discount
- **Spot**: Unused capacity, up to 90% discount, can be interrupted
- **Savings Plans**: Flexible commitment across instance families

---

### VPC (Virtual Private Cloud)

```
┌───────────────────────────────────────────────────────────────────┐
│                        VPC (10.0.0.0/16)                          │
│  ┌─────────────────────────┐  ┌─────────────────────────┐         │
│  │        AZ-1a            │  │        AZ-1b            │         │
│  │  ┌───────────────────┐  │  │  ┌───────────────────┐  │         │
│  │  │ Public Subnet     │──┼──┼──│ Public Subnet     │  │         │
│  │  │ 10.0.1.0/24       │  │  │  │ 10.0.2.0/24       │  │         │
│  │  │   [Web Servers]   │  │  │  │   [Web Servers]   │  │         │
│  │  └─────────┬─────────┘  │  │  └─────────┬─────────┘  │         │
│  │            │NAT GW      │  │            │            │         │
│  │  ┌─────────▼─────────┐  │  │  ┌─────────▼─────────┐  │         │
│  │  │ Private Subnet    │  │  │  │ Private Subnet    │  │         │
│  │  │ 10.0.3.0/24       │  │  │  │ 10.0.4.0/24       │  │         │
│  │  │   [App Servers]   │  │  │  │   [App Servers]   │  │         │
│  │  └───────────────────┘  │  │  └───────────────────┘  │         │
│  └─────────────────────────┘  └─────────────────────────┘         │
│                        │                                          │
│                   Internet Gateway                                │
└────────────────────────┼──────────────────────────────────────────┘
                         │
                    Internet
```

**Components**:
- **Subnet**: Range of IP addresses (public/private)
- **Internet Gateway**: Connect VPC to internet
- **NAT Gateway**: Allow private subnets to access internet
- **Route Table**: Rules for traffic routing
- **Security Group**: Stateful firewall at instance level
- **NACL**: Stateless firewall at subnet level

---

### S3 (Simple Storage Service)

**Storage Classes**:
| Class | Use Case | Retrieval |
| :--- | :--- | :--- |
| **Standard** | Frequently accessed | Instant |
| **Intelligent-Tiering** | Unknown access patterns | Instant |
| **Standard-IA** | Infrequent access | Instant |
| **One Zone-IA** | Infrequent, non-critical | Instant |
| **Glacier Instant** | Archive, instant retrieval | Instant |
| **Glacier Flexible** | Archive, hours retrieval | 1-12 hours |
| **Glacier Deep Archive** | Long-term archive | 12-48 hours |

**Best Practices**:
- Enable versioning for critical buckets
- Use lifecycle policies to transition/delete objects
- Enable server-side encryption
- Block public access by default
- Use VPC endpoints for private access

---

### ECS vs EKS

| Aspect | ECS | EKS |
| :--- | :--- | :--- |
| **Type** | AWS-native container service | Managed Kubernetes |
| **Learning Curve** | Lower | Higher |
| **Portability** | AWS-locked | Multi-cloud portable |
| **Launch Types** | EC2, Fargate | EC2, Fargate |
| **Best For** | AWS-only workloads | K8s expertise, multi-cloud |

---

### ECR (Elastic Container Registry)

### ECR Overview

> **ELI5**: ECR is like a private photo album for your Docker images. Only people you authorize can view or add photos (images), and AWS keeps them safe and organized for you.

```
┌───────────────────────────────────────────────────────────────────┐
│                        ECR Architecture                           │
├───────────────────────────────────────────────────────────────────┤
│                                                                   │
│   ┌───────────────────────────────────────────────────────────┐   │
│   │                      ECR Registry                         │   │
│   │  ┌────────────────┐  ┌────────────────┐  ┌─────────────┐  │   │
│   │  │  Repository 1  │  │  Repository 2  │  │ Repository N│  │   │
│   │  │  (frontend)    │  │  (backend)     │  │ (worker)    │  │   │
│   │  │  ┌──────────┐  │  │  ┌──────────┐  │  │             │  │   │
│   │  │  │ Image:v1 │  │  │  │ Image:v1 │  │  │   ...       │  │   │
│   │  │  │ Image:v2 │  │  │  │ Image:v2 │  │  │             │  │   │
│   │  │  │ Image:v3 │  │  │  │ Image:v3 │  │  │             │  │   │
│   │  │  └──────────┘  │  │  └──────────┘  │  │             │  │   │
│   │  └────────────────┘  └────────────────┘  └─────────────┘  │   │
│   └───────────────────────────────────────────────────────────┘   │
│                               │                                   │
│                               ▼                                   │
│   ┌───────────────────────────────────────────────────────────┐   │
│   │   Consumers: ECS, EKS, Lambda, EC2, CodeBuild             │   │
│   └───────────────────────────────────────────────────────────┘   │
│                                                                   │
└───────────────────────────────────────────────────────────────────┘
```

---

### ECR Repository Types

| Type | Description | Use Case |
| :--- | :--- | :--- |
| **Private** | Only accessible within your AWS account | Production applications |
| **Public** | Accessible by anyone (ECR Public Gallery) | Open source projects |

---

### ECR Operations

**Create Repository**:
```bash
# Create private repository
aws ecr create-repository \
    --repository-name my-app \
    --image-scanning-configuration scanOnPush=true \
    --encryption-configuration encryptionType=KMS \
    --tags Key=Environment,Value=prod

# Create with lifecycle policy
aws ecr put-lifecycle-policy \
    --repository-name my-app \
    --lifecycle-policy-text file://lifecycle-policy.json
```

**Authentication & Push**:
```bash
# Get login password (valid for 12 hours)
aws ecr get-login-password --region us-east-1 | \
    docker login --username AWS --password-stdin \
    123456789012.dkr.ecr.us-east-1.amazonaws.com

# Tag and push image
docker tag my-app:latest \
    123456789012.dkr.ecr.us-east-1.amazonaws.com/my-app:latest

docker push 123456789012.dkr.ecr.us-east-1.amazonaws.com/my-app:latest

# Push with specific tag
docker tag my-app:latest \
    123456789012.dkr.ecr.us-east-1.amazonaws.com/my-app:v1.2.3

docker push 123456789012.dkr.ecr.us-east-1.amazonaws.com/my-app:v1.2.3
```

**Pull Images**:
```bash
# Pull image
docker pull 123456789012.dkr.ecr.us-east-1.amazonaws.com/my-app:latest

# List images in repository
aws ecr describe-images --repository-name my-app

# List repositories
aws ecr describe-repositories
```

---

### ECR Lifecycle Policies

```json
{
  "rules": [
    {
      "rulePriority": 1,
      "description": "Keep last 10 production images",
      "selection": {
        "tagStatus": "tagged",
        "tagPrefixList": ["prod-"],
        "countType": "imageCountMoreThan",
        "countNumber": 10
      },
      "action": {
        "type": "expire"
      }
    },
    {
      "rulePriority": 2,
      "description": "Delete untagged images older than 7 days",
      "selection": {
        "tagStatus": "untagged",
        "countType": "sinceImagePushed",
        "countUnit": "days",
        "countNumber": 7
      },
      "action": {
        "type": "expire"
      }
    },
    {
      "rulePriority": 3,
      "description": "Keep only last 30 images",
      "selection": {
        "tagStatus": "any",
        "countType": "imageCountMoreThan",
        "countNumber": 30
      },
      "action": {
        "type": "expire"
      }
    }
  ]
}
```

---

### ECR Image Scanning

```bash
# Enable scan on push for repository
aws ecr put-image-scanning-configuration \
    --repository-name my-app \
    --image-scanning-configuration scanOnPush=true

# Manually trigger scan
aws ecr start-image-scan \
    --repository-name my-app \
    --image-id imageTag=latest

# Get scan findings
aws ecr describe-image-scan-findings \
    --repository-name my-app \
    --image-id imageTag=latest
```

**Scan Findings Severity Levels**:
| Severity | Description | Action |
| :--- | :--- | :--- |
| **CRITICAL** | Immediate exploitation risk | Block deployment, fix immediately |
| **HIGH** | Serious vulnerability | Fix before production |
| **MEDIUM** | Moderate risk | Fix in next release |
| **LOW** | Minor risk | Fix as time permits |
| **INFORMATIONAL** | Best practice suggestions | Consider addressing |

---

### ECR Cross-Account Access

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowCrossAccountPull",
      "Effect": "Allow",
      "Principal": {
        "AWS": [
          "arn:aws:iam::111111111111:root",
          "arn:aws:iam::222222222222:root"
        ]
      },
      "Action": [
        "ecr:GetDownloadUrlForLayer",
        "ecr:BatchGetImage",
        "ecr:BatchCheckLayerAvailability"
      ]
    }
  ]
}
```

---

### ECR with Terraform

```hcl
resource "aws_ecr_repository" "app" {
  name                 = "my-app"
  image_tag_mutability = "MUTABLE"  # or IMMUTABLE for strict versioning

  image_scanning_configuration {
    scan_on_push = true
  }

  encryption_configuration {
    encryption_type = "KMS"
    kms_key         = aws_kms_key.ecr.arn
  }

  tags = {
    Environment = var.environment
  }
}

resource "aws_ecr_lifecycle_policy" "app" {
  repository = aws_ecr_repository.app.name

  policy = jsonencode({
    rules = [
      {
        rulePriority = 1
        description  = "Keep last 30 images"
        selection = {
          tagStatus   = "any"
          countType   = "imageCountMoreThan"
          countNumber = 30
        }
        action = {
          type = "expire"
        }
      }
    ]
  })
}

# Output repository URL
output "repository_url" {
  value = aws_ecr_repository.app.repository_url
}
```

---

### ECR Best Practices

| Practice | Description |
| :--- | :--- |
| **Enable image scanning** | Detect vulnerabilities automatically |
| **Use lifecycle policies** | Control storage costs, clean old images |
| **Immutable tags for prod** | Prevent overwriting production images |
| **Cross-region replication** | Improve pull performance globally |
| **Use KMS encryption** | Encrypt images at rest |
| **Implement IAM policies** | Least privilege access |
| **Tag images semantically** | Use version numbers, commit hashes |

---

### CloudFront CDN

### CloudFront Overview

> **ELI5**: CloudFront is like having copies of your website stored in small warehouses (edge locations) all around the world. When someone visits your site, they get content from the nearest warehouse instead of traveling all the way to your main factory (origin server).

```
┌────────────────────────────────────────────────────────────────────┐
│                     CloudFront Architecture                        │
├────────────────────────────────────────────────────────────────────┤
│                                                                    │
│    ┌─────────┐     ┌─────────┐     ┌─────────┐     ┌───────────┐   │
│    │  User   │     │  User   │     │  User   │     │   User    │   │
│    │  (US)   │     │  (EU)   │     │ (Asia)  │     │(S.America)│   │
│    └────┬────┘     └────┬────┘     └────┬────┘     └────┬──────┘   │
│         │               │               │               │          │
│         ▼               ▼               ▼               ▼          │
│    ┌─────────┐     ┌─────────┐     ┌─────────┐     ┌───────────┐   │
│    │  Edge   │     │  Edge   │     │  Edge   │     │  Edge     │   │
│    │Location │     │Location │     │Location │     │Location   │   │
│    │ (NYC)   │     │(Frankfurt)│   │ (Tokyo) │     │(São Paulo)│   │
│    └────┬────┘     └────┬────┘     └────┬────┘     └────┬──────┘   │
│         │               │               │               │          │
│         └───────────────┴───────┬───────┴───────────────┘          │
│                                 ▼                                  │
│                    ┌──────────────────────┐                        │
│                    │  Regional Edge Cache │                        │
│                    └──────────┬───────────┘                        │
│                               ▼                                    │
│         ┌─────────────────────┼─────────────────────┐              │
│         ▼                     ▼                     ▼              │
│    ┌─────────┐           ┌─────────┐           ┌─────────┐         │
│    │   S3    │           │   ALB   │           │ Custom  │         │
│    │ Bucket  │           │         │           │ Origin  │         │
│    └─────────┘           └─────────┘           └─────────┘         │
│                                                                    │
└────────────────────────────────────────────────────────────────────┘
```

---

### CloudFront Components

| Component | Description |
| :--- | :--- |
| **Distribution** | Configuration for content delivery |
| **Origin** | Source of content (S3, ALB, EC2, custom) |
| **Edge Location** | Data center that caches content (400+) |
| **Regional Edge Cache** | Larger cache between edge and origin |
| **Behavior** | URL pattern matching and cache settings |
| **Cache Policy** | TTL and cache key configuration |
| **Origin Request Policy** | Headers/cookies sent to origin |

---

### CloudFront Distribution Types

| Type | Protocol | Use Case |
| :--- | :--- | :--- |
| **Web** | HTTP/HTTPS | Websites, APIs, static content |
| **RTMP** | RTMP (deprecated) | Legacy media streaming |

---

### Creating CloudFront Distribution

```bash
# Create distribution with S3 origin
aws cloudfront create-distribution \
    --origin-domain-name my-bucket.s3.amazonaws.com \
    --default-root-object index.html

# List distributions
aws cloudfront list-distributions

# Invalidate cache
aws cloudfront create-invalidation \
    --distribution-id EDFDVBD6EXAMPLE \
    --paths "/*"

# Invalidate specific paths
aws cloudfront create-invalidation \
    --distribution-id EDFDVBD6EXAMPLE \
    --paths "/images/*" "/css/*" "/index.html"
```

---

### CloudFront with Terraform

```hcl
# S3 bucket for static content
resource "aws_s3_bucket" "website" {
  bucket = "my-website-${var.environment}"
}

resource "aws_s3_bucket_policy" "website" {
  bucket = aws_s3_bucket.website.id
  policy = jsonencode({
    Version = "2012-10-17"
    Statement = [
      {
        Sid       = "AllowCloudFrontOAC"
        Effect    = "Allow"
        Principal = {
          Service = "cloudfront.amazonaws.com"
        }
        Action   = "s3:GetObject"
        Resource = "${aws_s3_bucket.website.arn}/*"
        Condition = {
          StringEquals = {
            "AWS:SourceArn" = aws_cloudfront_distribution.website.arn
          }
        }
      }
    ]
  })
}

# Origin Access Control
resource "aws_cloudfront_origin_access_control" "website" {
  name                              = "website-oac"
  origin_access_control_origin_type = "s3"
  signing_behavior                  = "always"
  signing_protocol                  = "sigv4"
}

# CloudFront Distribution
resource "aws_cloudfront_distribution" "website" {
  enabled             = true
  is_ipv6_enabled     = true
  default_root_object = "index.html"
  aliases             = ["www.example.com", "example.com"]
  price_class         = "PriceClass_100"  # US, Canada, Europe only
  
  # S3 Origin
  origin {
    domain_name              = aws_s3_bucket.website.bucket_regional_domain_name
    origin_id                = "S3-${aws_s3_bucket.website.id}"
    origin_access_control_id = aws_cloudfront_origin_access_control.website.id
  }
  
  # API Origin (ALB)
  origin {
    domain_name = aws_lb.api.dns_name
    origin_id   = "ALB-API"
    
    custom_origin_config {
      http_port              = 80
      https_port             = 443
      origin_protocol_policy = "https-only"
      origin_ssl_protocols   = ["TLSv1.2"]
    }
  }
  
  # Default behavior (static content)
  default_cache_behavior {
    allowed_methods  = ["GET", "HEAD", "OPTIONS"]
    cached_methods   = ["GET", "HEAD"]
    target_origin_id = "S3-${aws_s3_bucket.website.id}"
    
    forwarded_values {
      query_string = false
      cookies {
        forward = "none"
      }
    }
    
    viewer_protocol_policy = "redirect-to-https"
    min_ttl                = 0
    default_ttl            = 86400      # 1 day
    max_ttl                = 31536000   # 1 year
    compress               = true
  }
  
  # API behavior (no caching)
  ordered_cache_behavior {
    path_pattern     = "/api/*"
    allowed_methods  = ["DELETE", "GET", "HEAD", "OPTIONS", "PATCH", "POST", "PUT"]
    cached_methods   = ["GET", "HEAD"]
    target_origin_id = "ALB-API"
    
    forwarded_values {
      query_string = true
      headers      = ["Authorization", "Host"]
      cookies {
        forward = "all"
      }
    }
    
    viewer_protocol_policy = "https-only"
    min_ttl                = 0
    default_ttl            = 0
    max_ttl                = 0
  }
  
  # Custom error responses (SPA routing)
  custom_error_response {
    error_code         = 404
    response_code      = 200
    response_page_path = "/index.html"
  }
  
  custom_error_response {
    error_code         = 403
    response_code      = 200
    response_page_path = "/index.html"
  }
  
  # SSL Certificate
  viewer_certificate {
    acm_certificate_arn      = aws_acm_certificate.website.arn
    ssl_support_method       = "sni-only"
    minimum_protocol_version = "TLSv1.2_2021"
  }
  
  # Geographic restrictions
  restrictions {
    geo_restriction {
      restriction_type = "none"
      # Or whitelist/blacklist specific countries
      # restriction_type = "whitelist"
      # locations        = ["US", "CA", "GB"]
    }
  }
  
  tags = {
    Environment = var.environment
  }
}

# Route 53 alias record
resource "aws_route53_record" "website" {
  zone_id = aws_route53_zone.main.zone_id
  name    = "www.example.com"
  type    = "A"
  
  alias {
    name                   = aws_cloudfront_distribution.website.domain_name
    zone_id                = aws_cloudfront_distribution.website.hosted_zone_id
    evaluate_target_health = false
  }
}
```

---

### CloudFront Cache Behaviors

| Setting | Description | Recommendation |
| :--- | :--- | :--- |
| **Path Pattern** | URL pattern to match | `/api/*`, `/static/*`, `*.jpg` |
| **TTL** | How long to cache | Static: long, Dynamic: short/0 |
| **Query Strings** | Include in cache key | Yes for dynamic, No for static |
| **Headers** | Forward to origin | Minimal for better caching |
| **Cookies** | Forward to origin | None for static content |
| **Compression** | Compress responses | Always enable |

---

### CloudFront Security Features

| Feature | Description |
| :--- | :--- |
| **HTTPS** | SSL/TLS encryption |
| **AWS WAF** | Web application firewall integration |
| **Field-Level Encryption** | Encrypt sensitive form fields |
| **Signed URLs/Cookies** | Restrict access to authorized users |
| **Origin Access Control** | Secure S3 access |
| **Geo-Restriction** | Block/allow by country |

---

### CloudFront Best Practices

| Practice | Description |
| :--- | :--- |
| **Use OAC for S3** | Prevent direct S3 access |
| **Enable compression** | Reduce bandwidth costs |
| **Set appropriate TTLs** | Balance freshness and performance |
| **Use cache policies** | Managed policies for common patterns |
| **Implement WAF rules** | Protect against attacks |
| **Monitor with CloudWatch** | Track cache hit ratio, errors |
| **Use invalidations sparingly** | First 1000/month free, then $0.005 each |

---

## Section 12 — Azure Cloud

### Azure Resource Hierarchy

```
Azure AD Tenant (Organization)
└── Management Groups
    └── Subscriptions (Billing boundary)
        └── Resource Groups (Logical container)
            └── Resources (VMs, Storage, etc.)
```

---

### Key Azure Services

| Category | Service | Description |
| :--- | :--- | :--- |
| **Compute** | Virtual Machines | IaaS VMs |
| | VM Scale Sets | Auto-scaling VM groups |
| | App Service | PaaS web hosting |
| | Azure Functions | Serverless compute |
| | AKS | Managed Kubernetes |
| **Storage** | Blob Storage | Object storage |
| | Azure Files | Managed file shares |
| | Disk Storage | Block storage for VMs |
| **Database** | Azure SQL | Managed SQL Server |
| | Cosmos DB | Multi-model NoSQL |
| | Azure Database for PostgreSQL | Managed PostgreSQL |
| **Networking** | Virtual Network | Private networks |
| | Load Balancer | L4 load balancing |
| | Application Gateway | L7 load balancing + WAF |
| | Azure DNS | DNS hosting |

---

### Azure DevOps

**Components**:
- **Azure Repos**: Git repositories
- **Azure Pipelines**: CI/CD pipelines
- **Azure Boards**: Work tracking (Agile, Scrum)
- **Azure Artifacts**: Package management
- **Azure Test Plans**: Testing tools

**Azure Pipeline YAML**:
```yaml
trigger:
  - main

pool:
  vmImage: 'ubuntu-latest'

stages:
  - stage: Build
    jobs:
      - job: BuildJob
        steps:
          - task: NodeTool@0
            inputs:
              versionSpec: '18.x'
          - script: npm install && npm run build
          - publish: $(Build.ArtifactStagingDirectory)
            artifact: drop

  - stage: Deploy
    dependsOn: Build
    condition: succeeded()
    jobs:
      - deployment: DeployWeb
        environment: 'production'
        strategy:
          runOnce:
            deploy:
              steps:
                - script: echo Deploying to production
```

---

## Section 13 — GCP (Google Cloud Platform)

### Cloud SQL & BigQuery

**Cloud SQL**:
- Fully managed relational database service (MySQL, PostgreSQL, SQL Server).
- **Use Case**: OLTP applications, web backends, general-purpose relational storage.
- **Features**: Automatic backups, replication, high availability, vertical scaling.

**BigQuery**:
- Serverless, highly scalable, and cost-effective multi-cloud data warehouse.
- **Use Case**: OLAP, data analytics, business intelligence, large-scale data processing.
- **Architecture**: Separates compute (slots) from storage (Colossus). Query using standard SQL.

---

### Cloud Functions & Cloud Run

**Cloud Functions**:
- Event-driven serverless compute (FaaS).
- **Triggered by**: HTTP requests, Cloud Storage events, Pub/Sub messages.
- **Best for**: Single-purpose code glue, ETL triggers, lightweight APIs.

**Cloud Run**:
- Managed compute platform for running containerized applications.
- **Triggered by**: HTTP requests, gRPC, Eventarc.
- **Best for**: Stateless microservices, containerized web apps, language-agnostic workloads.
- **Knative**: Built on the Knative open-source standard.

---

### GCP Resource Hierarchy

```
Organization
└── Folders (optional, for departments)
    └── Projects (billing/resource boundary)
        └── Resources
```

---

### Key GCP Services

| Category | Service | AWS Equivalent |
| :--- | :--- | :--- |
| **Compute** | Compute Engine | EC2 |
| | GKE | EKS |
| | Cloud Run | Fargate |
| | Cloud Functions | Lambda |
| **Storage** | Cloud Storage | S3 |
| | Persistent Disk | EBS |
| **Database** | Cloud SQL | RDS |
| | Cloud Spanner | Aurora (global) |
| | BigQuery | Redshift + Athena |
| **Networking** | VPC | VPC |
| | Cloud Load Balancing | ALB/NLB |
| **DevOps** | Cloud Build | CodeBuild |
| | Artifact Registry | ECR |

---

### Cloud Storage (Blob Storage)

### Cloud Storage Overview

> **ELI5**: Cloud Storage is like a giant filing cabinet in the cloud where you can store any file of any size. Google takes care of making copies to keep your files safe and delivers them quickly wherever you need them.

```
┌────────────────────────────────────────────────────────────────────┐
│                  GCP Cloud Storage Architecture                    │
├────────────────────────────────────────────────────────────────────┤
│                                                                    │
│   ┌──────────────────────────────────────────────────────────────┐ │
│   │                         Project                              │ │
│   │  ┌─────────────────┐  ┌─────────────────┐  ┌──────────────┐  │ │
│   │  │   Bucket A      │  │   Bucket B      │  │  Bucket C    │  │ │
│   │  │  (Standard)     │  │  (Nearline)     │  │  (Archive)   │  │ │
│   │  │                 │  │                 │  │              │  │ │
│   │  │ ┌─────────────┐ │  │ ┌─────────────┐ │  │ ┌──────────┐ │  │ │
│   │  │ │   Object    │ │  │ │   Object    │ │  │ │ Object   │ │  │ │
│   │  │ │  (files)    │ │  │ │  (backups)  │ │  │ │(archives)│ │  │ │   
│   │  │ └─────────────┘ │  │ └─────────────┘ │  │ └──────────┘ │  │ │
│   │  └─────────────────┘  └─────────────────┘  └──────────────┘  │ │
│   └──────────────────────────────────────────────────────────────┘ │
│                                                                    │
└────────────────────────────────────────────────────────────────────┘
```

---

### Storage Classes Comparison

| Class | Access | Min Duration | Use Case | Price (per GB/month) |
| :--- | :--- | :--- | :--- | :--- |
| **Standard** | Frequent | None | Hot data, websites | $0.020 |
| **Nearline** | Monthly | 30 days | Backups, DR | $0.010 |
| **Coldline** | Quarterly | 90 days | Disaster recovery | $0.004 |
| **Archive** | Yearly | 365 days | Long-term compliance | $0.0012 |

---

### Cloud Storage Operations

**gsutil Commands**:
```bash
# Create bucket
gsutil mb -l us-central1 -c standard gs://my-bucket-name

# Upload files
gsutil cp file.txt gs://my-bucket/
gsutil cp -r ./folder gs://my-bucket/

# Download files
gsutil cp gs://my-bucket/file.txt .
gsutil cp -r gs://my-bucket/folder ./

# List objects
gsutil ls gs://my-bucket/
gsutil ls -l gs://my-bucket/  # With details

# Sync directories
gsutil -m rsync -r ./local-folder gs://my-bucket/folder

# Set object metadata
gsutil setmeta -h "Content-Type:text/html" gs://my-bucket/index.html

# Make object public
gsutil acl ch -u AllUsers:R gs://my-bucket/public-file.txt

# Copy between buckets
gsutil cp gs://bucket1/file.txt gs://bucket2/

# Delete objects
gsutil rm gs://my-bucket/file.txt
gsutil rm -r gs://my-bucket/folder/  # Recursive
```

**gcloud Commands**:
```bash
# List buckets
gcloud storage buckets list

# Create bucket with settings
gcloud storage buckets create gs://my-bucket \
    --location=us-central1 \
    --default-storage-class=standard \
    --uniform-bucket-level-access

# Get bucket info
gcloud storage buckets describe gs://my-bucket

# Update bucket
gcloud storage buckets update gs://my-bucket \
    --versioning
```

---

### Bucket Configuration

```bash
# Enable versioning
gsutil versioning set on gs://my-bucket

# Enable uniform bucket-level access
gsutil uniformbucketlevelaccess set on gs://my-bucket

# Set lifecycle policy
gsutil lifecycle set lifecycle.json gs://my-bucket

# Enable requester pays
gsutil requesterpays set on gs://my-bucket

# Set CORS configuration
gsutil cors set cors.json gs://my-bucket
```

**Lifecycle Policy** (`lifecycle.json`):
```json
{
  "lifecycle": {
    "rule": [
      {
        "action": {
          "type": "SetStorageClass",
          "storageClass": "NEARLINE"
        },
        "condition": {
          "age": 30,
          "matchesStorageClass": ["STANDARD"]
        }
      },
      {
        "action": {
          "type": "SetStorageClass",
          "storageClass": "COLDLINE"
        },
        "condition": {
          "age": 90,
          "matchesStorageClass": ["NEARLINE"]
        }
      },
      {
        "action": {
          "type": "Delete"
        },
        "condition": {
          "age": 365,
          "isLive": true
        }
      },
      {
        "action": {
          "type": "Delete"
        },
        "condition": {
          "numNewerVersions": 3
        }
      }
    ]
  }
}
```

---

### Cloud Storage with Terraform

```hcl
# Create bucket
resource "google_storage_bucket" "website" {
  name          = "${var.project_id}-website"
  location      = "US"
  storage_class = "STANDARD"
  
  uniform_bucket_level_access = true
  
  versioning {
    enabled = true
  }
  
  # Lifecycle rules
  lifecycle_rule {
    condition {
      age = 30
    }
    action {
      type          = "SetStorageClass"
      storage_class = "NEARLINE"
    }
  }
  
  lifecycle_rule {
    condition {
      age = 365
    }
    action {
      type = "Delete"
    }
  }
  
  # CORS configuration
  cors {
    origin          = ["https://example.com"]
    method          = ["GET", "HEAD", "PUT", "POST", "DELETE"]
    response_header = ["*"]
    max_age_seconds = 3600
  }
  
  # Website configuration
  website {
    main_page_suffix = "index.html"
    not_found_page   = "404.html"
  }
  
  labels = {
    environment = var.environment
  }
}

# Make bucket public for website hosting
resource "google_storage_bucket_iam_member" "public" {
  bucket = google_storage_bucket.website.name
  role   = "roles/storage.objectViewer"
  member = "allUsers"
}

# Upload objects
resource "google_storage_bucket_object" "index" {
  name   = "index.html"
  bucket = google_storage_bucket.website.name
  source = "website/index.html"
  
  content_type = "text/html"
  
  metadata = {
    cache-control = "max-age=3600"
  }
}

# Signed URL for private access
resource "google_storage_bucket_iam_member" "admin" {
  bucket = google_storage_bucket.private.name
  role   = "roles/storage.admin"
  member = "serviceAccount:${google_service_account.app.email}"
}
```

---

### Signed URLs for Secure Access

```python
# Python example for generating signed URLs
from google.cloud import storage
from datetime import timedelta

def generate_signed_url(bucket_name, blob_name, expiration_minutes=15):
    """Generate a signed URL for downloading an object."""
    storage_client = storage.Client()
    bucket = storage_client.bucket(bucket_name)
    blob = bucket.blob(blob_name)
    
    url = blob.generate_signed_url(
        version="v4",
        expiration=timedelta(minutes=expiration_minutes),
        method="GET"
    )
    
    return url

# For uploads
def generate_upload_signed_url(bucket_name, blob_name, expiration_minutes=15):
    """Generate a signed URL for uploading an object."""
    storage_client = storage.Client()
    bucket = storage_client.bucket(bucket_name)
    blob = bucket.blob(blob_name)
    
    url = blob.generate_signed_url(
        version="v4",
        expiration=timedelta(minutes=expiration_minutes),
        method="PUT",
        content_type="application/octet-stream"
    )
    
    return url
```

---

### Cloud Storage vs AWS S3 vs Azure Blob

| Feature | GCP Cloud Storage | AWS S3 | Azure Blob |
| :--- | :--- | :--- | :--- |
| **Hot Storage** | Standard | Standard | Hot |
| **Warm Storage** | Nearline | Standard-IA | Cool |
| **Cold Storage** | Coldline | Glacier Instant | Cold |
| **Archive** | Archive | Glacier Deep Archive | Archive |
| **Object Size Limit** | 5 TB | 5 TB | 4.75 TB (block blob) |
| **Versioning** | Yes | Yes | Yes |
| **Lifecycle Policies** | Yes | Yes | Yes |
| **CDN Integration** | Cloud CDN | CloudFront | Azure CDN |

---

### Cloud Storage Best Practices

| Practice | Description |
| :--- | :--- |
| **Use uniform bucket-level access** | Simplify IAM permissions |
| **Enable versioning** | Protect against accidental deletion |
| **Implement lifecycle policies** | Optimize costs automatically |
| **Use signed URLs** | Secure temporary access |
| **Enable audit logging** | Track access for compliance |
| **Use Cloud CDN** | Improve global performance |
| **Set appropriate CORS** | Enable web application access |
| **Encrypt sensitive data** | Use CMEK for compliance |

---

## Section 14 — Monitoring & Observability

### Three Pillars of Observability

| Pillar | What It Captures | Tools |
| :--- | :--- | :--- |
| **Logs** | Discrete events (errors, requests) | ELK, Loki, CloudWatch Logs |
| **Metrics** | Numeric measurements over time | Prometheus, CloudWatch, Datadog |
| **Traces** | Request flow across services | Jaeger, Zipkin, X-Ray |

---

### Prometheus & Grafana

**Prometheus Architecture**:
```
┌─────────────────────────────────────────────────┐
│                 Prometheus Server               │
│  ┌────────────┐  ┌────────────┐  ┌───────────┐  │
│  │  Scraper   │  │   TSDB     │  │ Alert Mgr │  │
│  └────────────┘  └────────────┘  └───────────┘  │
└────────────────────────┬────────────────────────┘
                         │ Pull metrics
        ┌────────────────┼────────────────┐
        ▼                ▼                ▼
   ┌─────────┐      ┌─────────┐      ┌─────────┐
   │ App 1   │      │ App 2   │      │ Node    │
   │ :9090   │      │ :9090   │      │ Exporter│
   └─────────┘      └─────────┘      └─────────┘
```

**PromQL Examples**:
```promql
# CPU usage per pod
sum(rate(container_cpu_usage_seconds_total[5m])) by (pod)

# Memory usage percentage
(node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes) 
/ node_memory_MemTotal_bytes * 100

# HTTP error rate
sum(rate(http_requests_total{status=~"5.."}[5m])) 
/ sum(rate(http_requests_total[5m])) * 100
```

---

### SLI, SLO, SLA

| Term | Definition | Example |
| :--- | :--- | :--- |
| **SLI** | Service Level Indicator (metric) | Request latency, error rate |
| **SLO** | Service Level Objective (target) | 99.9% availability, p99 < 200ms |
| **SLA** | Service Level Agreement (contract) | 99.95% uptime or credit refund |

**Error Budget**: `100% - SLO = Error Budget`
- If SLO is 99.9%, error budget is 0.1%
- Use error budget for risky deployments
- If budget exhausted, focus on reliability

---
### APM (Application Performance Monitoring) Overview

### APM Overview

> **ELI5**: APM is like having a doctor constantly monitoring your application's vital signs. It tells you not just if your app is sick (slow or broken), but exactly where the problem is and helps you fix it before users notice.

```
┌─────────────────────────────────────────────────────────────────────┐
│                    APM Monitoring Layers                            │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│   ┌─────────────────────────────────────────────────────────────┐   │
│   │  User Experience (Real User Monitoring - RUM)               │   │
│   │  • Page load times • Click tracking • Error rates           │   │
│   └─────────────────────────────────────────────────────────────┘   │
│                              │                                      │
│   ┌─────────────────────────▼───────────────────────────────────┐   │
│   │  Application Layer (APM Agents)                             │   │
│   │  • Request traces • Function timings • Database queries     │   │
│   └─────────────────────────────────────────────────────────────┘   │
│                              │                                      │
│   ┌─────────────────────────▼───────────────────────────────────┐   │
│   │  Infrastructure (Host Metrics)                              │   │
│   │  • CPU/Memory • Disk I/O • Network • Container metrics      │   │
│   └─────────────────────────────────────────────────────────────┘   │
│                              │                                      │
│   ┌─────────────────────────▼───────────────────────────────────┐   │
│   │  Dependencies (External Services)                           │   │
│   │  • Database health • Cache performance • API endpoints      │   │
│   └─────────────────────────────────────────────────────────────┘   │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

---

### APM Tools Comparison

| Feature | DataDog | New Relic | Grafana | Dynatrace |
| :--- | :--- | :--- | :--- | :--- |
| **Pricing Model** | Per host/metric | Per GB ingested | Free/Enterprise | Per host |
| **APM** | ✅ Excellent | ✅ Excellent | ⚠️ Via plugins | ✅ Excellent |
| **Infrastructure** | ✅ Built-in | ✅ Built-in | ✅ Via Prometheus | ✅ Built-in |
| **Logs** | ✅ Built-in | ✅ Built-in | ✅ Via Loki | ✅ Built-in |
| **RUM** | ✅ Built-in | ✅ Built-in | ⚠️ Limited | ✅ Built-in |
| **AI/ML** | ✅ Watchdog | ✅ AI Ops | ⚠️ Limited | ✅ Davis AI |
| **Open Source** | ❌ Proprietary | ❌ Proprietary | ✅ Yes | ❌ Proprietary |

---

### DataDog

### DataDog Architecture

```
┌────────────────────────────────────────────────────────────────────┐
│                      DataDog Architecture                          │
├────────────────────────────────────────────────────────────────────┤
│                                                                    │
│   ┌──────────────┐    ┌──────────────┐    ┌──────────────┐         │
│   │  Your App    │    │  Your App    │    │  Your App    │         │
│   │  + Agent     │    │  + Agent     │    │  + Agent     │         │
│   └──────┬───────┘    └──────┬───────┘    └──────┬───────┘         │
│          │                   │                   │                 │
│          └───────────────────┼───────────────────┘                 │
│                              ▼                                     │
│                    ┌─────────────────┐                             │
│                    │  DataDog Agent  │ (collects & forwards)       │
│                    │  (DaemonSet)    │                             │
│                    └────────┬────────┘                             │
│                             │ HTTPS                                │
│                             ▼                                      │
│  ┌──────────────────────────────────────────────────────────────┐  │
│  │                     DataDog Cloud                            │  │
│  │  ┌─────────┐ ┌────────┐ ┌──────┐ ┌────────┐ ┌─────────────┐  │  │
│  │  │ Metrics │ │  APM   │ │ Logs │ │  RUM   │ │ Synthetics  │  │  │
│  │  └─────────┘ └────────┘ └──────┘ └────────┘ └─────────────┘  │  │
│  └──────────────────────────────────────────────────────────────┘  │
│                                                                    │
└────────────────────────────────────────────────────────────────────┘
```

---

### DataDog Agent Installation

**Docker**:
```bash
docker run -d --name dd-agent \
    -v /var/run/docker.sock:/var/run/docker.sock:ro \
    -v /proc/:/host/proc/:ro \
    -v /sys/fs/cgroup/:/host/sys/fs/cgroup:ro \
    -e DD_API_KEY=<YOUR_API_KEY> \
    -e DD_SITE="datadoghq.com" \
    -e DD_APM_ENABLED=true \
    -e DD_LOGS_ENABLED=true \
    gcr.io/datadoghq/agent:latest
```

**Kubernetes (Helm)**:
```bash
helm repo add datadog https://helm.datadoghq.com
helm repo update

helm install datadog-agent datadog/datadog \
    --set datadog.apiKey=<YOUR_API_KEY> \
    --set datadog.site='datadoghq.com' \
    --set datadog.apm.portEnabled=true \
    --set datadog.logs.enabled=true \
    --set datadog.logs.containerCollectAll=true \
    --set datadog.processAgent.enabled=true \
    --set datadog.networkMonitoring.enabled=true
```

**Kubernetes Manifest**:
```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: datadog-agent
  namespace: monitoring
spec:
  selector:
    matchLabels:
      app: datadog-agent
  template:
    metadata:
      labels:
        app: datadog-agent
    spec:
      containers:
        - name: datadog-agent
          image: gcr.io/datadoghq/agent:latest
          env:
            - name: DD_API_KEY
              valueFrom:
                secretKeyRef:
                  name: datadog-secret
                  key: api-key
            - name: DD_SITE
              value: "datadoghq.com"
            - name: DD_APM_ENABLED
              value: "true"
            - name: DD_LOGS_ENABLED
              value: "true"
            - name: DD_KUBERNETES_POD_LABELS_AS_TAGS
              value: '{"app":"kube_app","environment":"env"}'
          volumeMounts:
            - name: dockersocket
              mountPath: /var/run/docker.sock
            - name: procdir
              mountPath: /host/proc
              readOnly: true
          resources:
            limits:
              memory: 512Mi
            requests:
              cpu: 200m
              memory: 256Mi
      volumes:
        - name: dockersocket
          hostPath:
            path: /var/run/docker.sock
        - name: procdir
          hostPath:
            path: /proc
```

---

### DataDog APM Instrumentation

**Python (Flask)**:
```python
# pip install ddtrace

from ddtrace import tracer, patch_all
from flask import Flask

# Auto-instrument all supported libraries
patch_all()

# Configure tracer
tracer.configure(
    hostname='localhost',
    port=8126,
    env='production',
    service='my-flask-app',
    version='1.0.0'
)

app = Flask(__name__)

@app.route('/api/users/<user_id>')
def get_user(user_id):
    # Create custom span
    with tracer.trace('user.fetch', service='my-flask-app') as span:
        span.set_tag('user.id', user_id)
        user = fetch_user_from_db(user_id)
        span.set_tag('user.found', user is not None)
    return jsonify(user)
```

**Node.js**:
```javascript
// npm install dd-trace

const tracer = require('dd-trace').init({
  env: 'production',
  service: 'my-node-app',
  version: '1.0.0',
  logInjection: true,
  runtimeMetrics: true
});

const express = require('express');
const app = express();

app.get('/api/users/:id', async (req, res) => {
  // Create custom span
  const span = tracer.startSpan('user.fetch');
  span.setTag('user.id', req.params.id);
  
  try {
    const user = await fetchUser(req.params.id);
    span.setTag('user.found', !!user);
    res.json(user);
  } catch (error) {
    span.setTag('error', true);
    span.setTag('error.message', error.message);
    throw error;
  } finally {
    span.finish();
  }
});
```

---

### DataDog Custom Metrics

```python
from datadog import initialize, statsd

initialize(statsd_host='localhost', statsd_port=8125)

# Counter - track occurrences
statsd.increment('orders.completed', tags=['region:us-east', 'tier:premium'])

# Gauge - current value
statsd.gauge('queue.size', get_queue_size(), tags=['queue:orders'])

# Histogram - distribution of values
statsd.histogram('request.latency', response_time_ms, tags=['endpoint:/api/users'])

# Distribution - global percentiles
statsd.distribution('payment.amount', amount, tags=['currency:usd'])

# Set - unique values
statsd.set('users.unique', user_id)
```

---

### DataDog Monitors & Alerting

```hcl
# Terraform DataDog Monitor
resource "datadog_monitor" "high_error_rate" {
  name    = "High Error Rate on API"
  type    = "metric alert"
  message = <<-EOF
    Error rate is above 5% on {{service.name}}
    
    @slack-alerts
    @pagerduty-oncall
  EOF

  query = "sum(last_5m):sum:trace.http.request.errors{service:api-gateway}.as_count() / sum:trace.http.request.hits{service:api-gateway}.as_count() * 100 > 5"

  monitor_thresholds {
    warning  = 2
    critical = 5
  }

  notify_no_data    = false
  renotify_interval = 60

  tags = ["service:api-gateway", "team:platform", "env:production"]
}

resource "datadog_monitor" "pod_crashloop" {
  name    = "Pod CrashLoopBackOff"
  type    = "query alert"
  message = <<-EOF
    Pod {{pod_name.name}} is in CrashLoopBackOff
    
    @slack-k8s-alerts
  EOF

  query = "max(last_5m):max:kubernetes_state.container.status_report.count.waiting{reason:crashloopbackoff} by {kube_namespace,pod_name} > 0"

  tags = ["team:platform", "source:kubernetes"]
}
```

---

### DataDog Dashboards

```json
{
  "title": "Application Performance Dashboard",
  "widgets": [
    {
      "definition": {
        "type": "timeseries",
        "title": "Request Rate by Service",
        "requests": [
          {
            "q": "sum:trace.http.request.hits{*} by {service}.as_rate()",
            "display_type": "line"
          }
        ]
      }
    },
    {
      "definition": {
        "type": "timeseries",
        "title": "P99 Latency",
        "requests": [
          {
            "q": "p99:trace.http.request.duration{*} by {service}",
            "display_type": "line"
          }
        ]
      }
    },
    {
      "definition": {
        "type": "query_value",
        "title": "Error Rate",
        "requests": [
          {
            "q": "sum:trace.http.request.errors{*}.as_count() / sum:trace.http.request.hits{*}.as_count() * 100"
          }
        ],
        "precision": 2
      }
    },
    {
      "definition": {
        "type": "toplist",
        "title": "Slowest Endpoints",
        "requests": [
          {
            "q": "avg:trace.http.request.duration{*} by {resource_name}"
          }
        ]
      }
    }
  ]
}
```

---

### New Relic

### New Relic Architecture

```
┌────────────────────────────────────────────────────────────────────┐
│                     New Relic One Platform                         │
├────────────────────────────────────────────────────────────────────┤
│                                                                    │
│   ┌────────────┐  ┌────────────┐  ┌──────────────┐  ┌───────────┐  │
│   │    APM     │  │   Logs     │  │Infrastructure│  │  Browser  │  │
│   └────────────┘  └────────────┘  └──────────────┘  └───────────┘  │
│                                                                    │
│   ┌────────────┐  ┌────────────┐  ┌─────────────┐  ┌───────────┐   │
│   │  Mobile    │  │ Synthetic  │  │   Errors    │  │  Alerts   │   │
│   └────────────┘  └────────────┘  └─────────────┘  └───────────┘   │
│                                                                    │
│   ┌────────────────────────────────────────────────────────────┐   │
│   │             NRDB (New Relic Database) - NRQL               │   │
│   └────────────────────────────────────────────────────────────┘   │
│                                                                    │
└────────────────────────────────────────────────────────────────────┘
```

---

### New Relic Agent Installation

**Python**:
```bash
pip install newrelic

# Generate config file
newrelic-admin generate-config YOUR_LICENSE_KEY newrelic.ini

# Run with agent
NEW_RELIC_CONFIG_FILE=newrelic.ini newrelic-admin run-program gunicorn app:app
```

**Node.js**:
```javascript
// Add at very top of entry file
require('newrelic');

// newrelic.js config file
exports.config = {
  app_name: ['My Application'],
  license_key: process.env.NEW_RELIC_LICENSE_KEY,
  distributed_tracing: {
    enabled: true
  },
  logging: {
    level: 'info'
  },
  allow_all_headers: true,
  attributes: {
    exclude: [
      'request.headers.cookie',
      'request.headers.authorization'
    ]
  }
}
```

**Kubernetes**:
```yaml
# New Relic Kubernetes Integration
apiVersion: v1
kind: ConfigMap
metadata:
  name: nri-bundle-config
data:
  NEW_RELIC_LICENSE_KEY: "YOUR_LICENSE_KEY"
  CLUSTER_NAME: "production-cluster"

---
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: newrelic-infrastructure
spec:
  selector:
    matchLabels:
      name: newrelic-infrastructure
  template:
    metadata:
      labels:
        name: newrelic-infrastructure
    spec:
      containers:
        - name: newrelic-infrastructure
          image: newrelic/infrastructure-k8s:latest
          env:
            - name: NRIA_LICENSE_KEY
              valueFrom:
                configMapKeyRef:
                  name: nri-bundle-config
                  key: NEW_RELIC_LICENSE_KEY
            - name: CLUSTER_NAME
              valueFrom:
                configMapKeyRef:
                  name: nri-bundle-config
                  key: CLUSTER_NAME
            - name: NRIA_VERBOSE
              value: "0"
          volumeMounts:
            - name: host-volume
              mountPath: /host
              readOnly: true
      volumes:
        - name: host-volume
          hostPath:
            path: /
```

---

### NRQL (New Relic Query Language)

```sql
-- Request rate over time
SELECT rate(count(*), 1 minute) 
FROM Transaction 
WHERE appName = 'MyApp' 
SINCE 1 hour ago 
TIMESERIES

-- Average response time by endpoint
SELECT average(duration) 
FROM Transaction 
WHERE appName = 'MyApp' 
FACET request.uri 
SINCE 1 hour ago

-- Error rate percentage
SELECT percentage(count(*), WHERE error IS true) 
FROM Transaction 
WHERE appName = 'MyApp' 
SINCE 24 hours ago 
TIMESERIES

-- P95 latency
SELECT percentile(duration, 95) as 'P95 Latency'
FROM Transaction 
WHERE appName = 'MyApp' 
SINCE 1 hour ago 
TIMESERIES

-- Slow transactions
SELECT * 
FROM Transaction 
WHERE appName = 'MyApp' AND duration > 2 
SINCE 1 hour ago 
LIMIT 100

-- Apdex score
SELECT apdex(duration, 0.5) 
FROM Transaction 
WHERE appName = 'MyApp' 
SINCE 1 day ago 
TIMESERIES

-- Container metrics
SELECT average(cpuPercent), average(memoryUsedPercent) 
FROM ContainerSample 
FACET containerName 
SINCE 1 hour ago 
TIMESERIES
```

---

### New Relic Alerts (NRQL Conditions)

```hcl
# Terraform New Relic Alert
resource "newrelic_nrql_alert_condition" "high_error_rate" {
  policy_id = newrelic_alert_policy.app_policy.id
  name      = "High Error Rate"
  type      = "static"
  enabled   = true

  nrql {
    query = <<-NRQL
      SELECT percentage(count(*), WHERE error IS true) 
      FROM Transaction 
      WHERE appName = 'MyApp'
    NRQL
  }

  critical {
    operator              = "above"
    threshold             = 5
    threshold_duration    = 300
    threshold_occurrences = "at_least_once"
  }

  warning {
    operator              = "above"
    threshold             = 2
    threshold_duration    = 300
    threshold_occurrences = "at_least_once"
  }
}

resource "newrelic_nrql_alert_condition" "high_latency" {
  policy_id = newrelic_alert_policy.app_policy.id
  name      = "High P95 Latency"
  type      = "static"

  nrql {
    query = "SELECT percentile(duration, 95) FROM Transaction WHERE appName = 'MyApp'"
  }

  critical {
    operator              = "above"
    threshold             = 2.0  # 2 seconds
    threshold_duration    = 300
    threshold_occurrences = "all"
  }
}
```

---

### Grafana

### Grafana Architecture

```
┌────────────────────────────────────────────────────────────────────┐
│                       Grafana Ecosystem                            │
├────────────────────────────────────────────────────────────────────┤
│                                                                    │
│                    ┌─────────────────────┐                        │
│                    │     Grafana UI      │                        │
│                    │  (Visualization)    │                        │
│                    └──────────┬──────────┘                        │
│                               │                                    │
│        ┌──────────────────────┼──────────────────────┐            │
│        ▼                      ▼                      ▼            │
│   ┌──────────┐          ┌──────────┐          ┌──────────┐       │
│   │Prometheus│          │   Loki   │          │  Tempo   │       │
│   │ (Metrics)│          │  (Logs)  │          │ (Traces) │       │
│   └──────────┘          └──────────┘          └──────────┘       │
│        │                      │                      │            │
│        ▼                      ▼                      ▼            │
│   ┌─────────────────────────────────────────────────────────────┐ │
│   │                     Your Applications                       │ │
│   └─────────────────────────────────────────────────────────────┘ │
│                                                                    │
└────────────────────────────────────────────────────────────────────┘
```

---

### Grafana Installation

**Docker Compose**:
```yaml
version: '3.8'

services:
  grafana:
    image: grafana/grafana:latest
    container_name: grafana
    ports:
      - "3000:3000"
    environment:
      - GF_SECURITY_ADMIN_USER=admin
      - GF_SECURITY_ADMIN_PASSWORD=admin123
      - GF_USERS_ALLOW_SIGN_UP=false
      - GF_SERVER_ROOT_URL=https://grafana.example.com
      - GF_SMTP_ENABLED=true
      - GF_SMTP_HOST=smtp.gmail.com:587
    volumes:
      - grafana-data:/var/lib/grafana
      - ./provisioning:/etc/grafana/provisioning
    restart: unless-stopped

  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
      - prometheus-data:/prometheus
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.path=/prometheus'
      - '--storage.tsdb.retention.time=30d'
    restart: unless-stopped

  loki:
    image: grafana/loki:latest
    container_name: loki
    ports:
      - "3100:3100"
    volumes:
      - ./loki-config.yaml:/etc/loki/config.yaml
      - loki-data:/loki
    command: -config.file=/etc/loki/config.yaml
    restart: unless-stopped

volumes:
  grafana-data:
  prometheus-data:
  loki-data:
```

**Kubernetes (Helm)**:
```bash
# Add Grafana repo
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update

# Install Grafana
helm install grafana grafana/grafana \
    --namespace monitoring \
    --set persistence.enabled=true \
    --set persistence.size=10Gi \
    --set adminPassword=admin123 \
    --set ingress.enabled=true \
    --set ingress.hosts[0]=grafana.example.com

# Install Prometheus stack (includes Grafana)
helm install prometheus prometheus-community/kube-prometheus-stack \
    --namespace monitoring \
    --set grafana.enabled=true \
    --set prometheus.prometheusSpec.retention=30d
```

---

### Grafana Data Source Provisioning

```yaml
# provisioning/datasources/datasources.yaml
apiVersion: 1

datasources:
  - name: Prometheus
    type: prometheus
    access: proxy
    url: http://prometheus:9090
    isDefault: true
    editable: false

  - name: Loki
    type: loki
    access: proxy
    url: http://loki:3100
    jsonData:
      maxLines: 1000

  - name: Tempo
    type: tempo
    access: proxy
    url: http://tempo:3200
    jsonData:
      tracesToLogs:
        datasourceUid: loki
        tags: ['job', 'namespace']

  - name: PostgreSQL
    type: postgres
    url: postgres:5432
    database: metrics
    user: grafana
    secureJsonData:
      password: ${POSTGRES_PASSWORD}
    jsonData:
      sslmode: disable
```

---

### Grafana Dashboard JSON

```json
{
  "dashboard": {
    "title": "Application Metrics",
    "uid": "app-metrics",
    "panels": [
      {
        "title": "Request Rate",
        "type": "timeseries",
        "gridPos": { "x": 0, "y": 0, "w": 12, "h": 8 },
        "targets": [
          {
            "expr": "sum(rate(http_requests_total[5m])) by (service)",
            "legendFormat": "{{service}}"
          }
        ]
      },
      {
        "title": "P99 Latency",
        "type": "timeseries",
        "gridPos": { "x": 12, "y": 0, "w": 12, "h": 8 },
        "targets": [
          {
            "expr": "histogram_quantile(0.99, sum(rate(http_request_duration_seconds_bucket[5m])) by (le, service))",
            "legendFormat": "{{service}}"
          }
        ]
      },
      {
        "title": "Error Rate",
        "type": "stat",
        "gridPos": { "x": 0, "y": 8, "w": 6, "h": 4 },
        "targets": [
          {
            "expr": "sum(rate(http_requests_total{status=~\"5..\"}[5m])) / sum(rate(http_requests_total[5m])) * 100"
          }
        ],
        "fieldConfig": {
          "defaults": {
            "unit": "percent",
            "thresholds": {
              "mode": "absolute",
              "steps": [
                { "value": 0, "color": "green" },
                { "value": 1, "color": "yellow" },
                { "value": 5, "color": "red" }
              ]
            }
          }
        }
      }
    ]
  }
}
```

---

### Grafana Alerting

```yaml
# provisioning/alerting/alerts.yaml
apiVersion: 1

groups:
  - name: Application Alerts
    folder: Production
    interval: 1m
    rules:
      - uid: high-error-rate
        title: High Error Rate
        condition: C
        data:
          - refId: A
            relativeTimeRange:
              from: 300
              to: 0
            datasourceUid: prometheus
            model:
              expr: sum(rate(http_requests_total{status=~"5.."}[5m])) / sum(rate(http_requests_total[5m])) * 100
          - refId: C
            datasourceUid: __expr__
            model:
              type: threshold
              conditions:
                - evaluator:
                    type: gt
                    params: [5]
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: Error rate above 5%
          description: "Current error rate is {{ $value }}%"

      - uid: high-latency
        title: High P99 Latency
        condition: C
        data:
          - refId: A
            datasourceUid: prometheus
            model:
              expr: histogram_quantile(0.99, sum(rate(http_request_duration_seconds_bucket[5m])) by (le))
          - refId: C
            datasourceUid: __expr__
            model:
              type: threshold
              conditions:
                - evaluator:
                    type: gt
                    params: [2]
        for: 5m
        labels:
          severity: warning
```

---

### Prometheus (Deep Dive)

### Prometheus Architecture

```
┌────────────────────────────────────────────────────────────────────┐
│                     Prometheus Architecture                        │
├────────────────────────────────────────────────────────────────────┤
│                                                                    │
│   ┌──────────────────────────────────────────────────────────┐     │
│   │                    Prometheus Server                     │     │
│   │  ┌────────────┐  ┌────────────┐  ┌────────────────────┐  │     │
│   │  │  Scraper   │  │    TSDB    │  │   HTTP Server      │  │     │
│   │  │(pull model)│  │(storage)   │  │  (PromQL queries)  │  │     │
│   │  └────────────┘  └────────────┘  └────────────────────┘  │     │
│   └────────────────────────┬─────────────────────────────────┘     │
│                            │                                       │
│        ┌───────────────────┼───────────────────┐                   │
│        ▼                   ▼                   ▼                   │
│   ┌─────────────┐   ┌─────────────┐   ┌─────────────────┐          │
│   │ Application │   │    Node     │   │   Kubernetes    │          │
│   │  /metrics   │   │  Exporter   │   │  State Metrics  │          │
│   └─────────────┘   └─────────────┘   └─────────────────┘          │
│                                                                    │
│   ┌─────────────────────────────────────────────────────────────┐  │
│   │                    Alertmanager                             │  │
│   │  Routes alerts to: Slack, PagerDuty, Email, Webhook         │  │
│   └─────────────────────────────────────────────────────────────┘  │
│                                                                    │
└────────────────────────────────────────────────────────────────────┘
```

---

### Prometheus Configuration

```yaml
# prometheus.yml
global:
  scrape_interval: 15s
  evaluation_interval: 15s
  external_labels:
    cluster: production
    region: us-east-1

alerting:
  alertmanagers:
    - static_configs:
        - targets: ['alertmanager:9093']

rule_files:
  - '/etc/prometheus/rules/*.yml'

scrape_configs:
  # Prometheus self-monitoring
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']

  # Node Exporter
  - job_name: 'node'
    static_configs:
      - targets: ['node-exporter:9100']

  # Application metrics
  - job_name: 'app'
    metrics_path: /metrics
    static_configs:
      - targets: ['app:8080']
    relabel_configs:
      - source_labels: [__address__]
        target_label: instance

  # Kubernetes pods with annotations
  - job_name: 'kubernetes-pods'
    kubernetes_sd_configs:
      - role: pod
    relabel_configs:
      - source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_scrape]
        action: keep
        regex: true
      - source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_path]
        action: replace
        target_label: __metrics_path__
        regex: (.+)
      - source_labels: [__address__, __meta_kubernetes_pod_annotation_prometheus_io_port]
        action: replace
        regex: ([^:]+)(?::\d+)?;(\d+)
        replacement: $1:$2
        target_label: __address__
      - source_labels: [__meta_kubernetes_namespace]
        target_label: namespace
      - source_labels: [__meta_kubernetes_pod_name]
        target_label: pod
```

---

### PromQL Examples

```promql
# Basic queries
http_requests_total                           # All HTTP requests
http_requests_total{status="200"}             # Only successful requests
http_requests_total{status=~"5.."}            # 5xx errors (regex)

# Rate and increase
rate(http_requests_total[5m])                 # Per-second rate over 5 min
irate(http_requests_total[5m])                # Instant rate (more sensitive)
increase(http_requests_total[1h])             # Total increase over 1 hour

# Aggregations
sum(http_requests_total) by (service)         # Sum by service
avg(http_requests_total) by (instance)        # Average by instance
max(http_requests_total) by (endpoint)        # Max by endpoint
count(http_requests_total) by (status)        # Count by status

# Percentiles (histograms)
histogram_quantile(0.99, sum(rate(http_request_duration_seconds_bucket[5m])) by (le))
histogram_quantile(0.95, sum(rate(http_request_duration_seconds_bucket[5m])) by (le, service))
histogram_quantile(0.50, sum(rate(http_request_duration_seconds_bucket[5m])) by (le))

# CPU and Memory
100 - (avg(irate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)  # CPU usage %
(node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes) / node_memory_MemTotal_bytes * 100

# Error rate
sum(rate(http_requests_total{status=~"5.."}[5m])) / sum(rate(http_requests_total[5m])) * 100

# SLI: Availability
1 - (sum(rate(http_requests_total{status=~"5.."}[30d])) / sum(rate(http_requests_total[30d])))

# Kubernetes specific
kube_pod_container_status_restarts_total      # Container restarts
kube_deployment_status_replicas_available     # Available replicas
kube_node_status_condition{condition="Ready"} # Node readiness
```

---

### Prometheus Alert Rules

```yaml
# rules/application.yml
groups:
  - name: application
    rules:
      - alert: HighErrorRate
        expr: |
          sum(rate(http_requests_total{status=~"5.."}[5m])) by (service)
          / sum(rate(http_requests_total[5m])) by (service) * 100 > 5
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "High error rate on {{ $labels.service }}"
          description: "Error rate is {{ $value | printf \"%.2f\" }}% (threshold: 5%)"

      - alert: HighLatency
        expr: |
          histogram_quantile(0.99, sum(rate(http_request_duration_seconds_bucket[5m])) by (le, service)) > 2
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "High P99 latency on {{ $labels.service }}"
          description: "P99 latency is {{ $value | printf \"%.2f\" }}s"

      - alert: PodCrashLooping
        expr: |
          increase(kube_pod_container_status_restarts_total[1h]) > 3
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Pod {{ $labels.pod }} is crash looping"
          description: "Pod has restarted {{ $value }} times in the last hour"

      - alert: HighMemoryUsage
        expr: |
          (container_memory_usage_bytes / container_spec_memory_limit_bytes) * 100 > 90
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "High memory usage in {{ $labels.container }}"
          description: "Memory usage is {{ $value | printf \"%.2f\" }}%"
```

---

### Alertmanager Configuration

```yaml
# alertmanager.yml
global:
  resolve_timeout: 5m
  slack_api_url: 'https://hooks.slack.com/services/xxx/xxx/xxx'

route:
  group_by: ['alertname', 'service']
  group_wait: 10s
  group_interval: 5m
  repeat_interval: 4h
  receiver: 'default'
  routes:
    - match:
        severity: critical
      receiver: 'pagerduty-critical'
      continue: true
    - match:
        severity: critical
      receiver: 'slack-critical'
    - match:
        severity: warning
      receiver: 'slack-warning'

receivers:
  - name: 'default'
    slack_configs:
      - channel: '#alerts'
        send_resolved: true

  - name: 'slack-critical'
    slack_configs:
      - channel: '#alerts-critical'
        send_resolved: true
        title: '{{ .Status | toUpper }}: {{ .CommonAnnotations.summary }}'
        text: '{{ .CommonAnnotations.description }}'

  - name: 'slack-warning'
    slack_configs:
      - channel: '#alerts-warning'
        send_resolved: true

  - name: 'pagerduty-critical'
    pagerduty_configs:
      - service_key: 'your-pagerduty-key'
        severity: critical

inhibit_rules:
  - source_match:
      severity: 'critical'
    target_match:
      severity: 'warning'
    equal: ['alertname', 'service']
```

---

### ELK Stack (Elasticsearch, Logstash, Kibana)

### ELK Stack Architecture

```
┌────────────────────────────────────────────────────────────────────┐
│                      ELK Stack Architecture                        │
├────────────────────────────────────────────────────────────────────┤
│                                                                    │
│   ┌──────────────────────────────────────────────────────────┐     │
│   │                         Kibana                           │     │
│   │  (Visualization, Dashboards, Discover, Alerting)         │     │
│   └──────────────────────────────────────────────────────────┘     │
│                              ▲                                     │
│                              │                                     │
│   ┌──────────────────────────────────────────────────────────┐     │
│   │                     Elasticsearch                        │     │
│   │  (Search, Analytics, Storage)                            │     │
│   │  ┌─────────┐ ┌─────────┐ ┌─────────┐                     │     │
│   │  │  Node 1 │ │  Node 2 │ │  Node 3 │ (Cluster)           │     │
│   │  └─────────┘ └─────────┘ └─────────┘                     │     │
│   └──────────────────────────────────────────────────────────┘     │
│                              ▲                                     │
│                              │                                     │
│   ┌──────────────────────────────────────────────────────────┐     │
│   │                       Logstash                           │     │
│   │  (Ingest, Transform, Enrich)                             │     │
│   └──────────────────────────────────────────────────────────┘     │
│                              ▲                                     │
│        ┌─────────────────────┼─────────────────────┐               │
│        │                     │                     │               │
│   ┌─────────┐          ┌──────────┐         ┌─────────┐            │
│   │Filebeat │          │Metricbeat│         │  Agents │            │
│   └─────────┘          └──────────┘         └─────────┘            │
│                                                                    │
└────────────────────────────────────────────────────────────────────┘
```

---

### Docker Compose Setup

```yaml
version: '3.8'

services:
  elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:8.11.0
    container_name: elasticsearch
    environment:
      - node.name=es01
      - cluster.name=docker-cluster
      - discovery.type=single-node
      - bootstrap.memory_lock=true
      - xpack.security.enabled=false
      - "ES_JAVA_OPTS=-Xms2g -Xmx2g"
    ulimits:
      memlock:
        soft: -1
        hard: -1
    volumes:
      - elasticsearch-data:/usr/share/elasticsearch/data
    ports:
      - "9200:9200"
    healthcheck:
      test: ["CMD-SHELL", "curl -s http://localhost:9200 | grep -q 'cluster_name'"]
      interval: 10s
      timeout: 10s
      retries: 120

  logstash:
    image: docker.elastic.co/logstash/logstash:8.11.0
    container_name: logstash
    volumes:
      - ./logstash/pipeline:/usr/share/logstash/pipeline
      - ./logstash/config/logstash.yml:/usr/share/logstash/config/logstash.yml
    ports:
      - "5044:5044"    # Beats input
      - "5000:5000"    # TCP input
      - "9600:9600"    # API
    environment:
      - "LS_JAVA_OPTS=-Xms512m -Xmx512m"
    depends_on:
      elasticsearch:
        condition: service_healthy

  kibana:
    image: docker.elastic.co/kibana/kibana:8.11.0
    container_name: kibana
    environment:
      - ELASTICSEARCH_HOSTS=http://elasticsearch:9200
    ports:
      - "5601:5601"
    depends_on:
      elasticsearch:
        condition: service_healthy

  filebeat:
    image: docker.elastic.co/beats/filebeat:8.11.0
    container_name: filebeat
    user: root
    volumes:
      - ./filebeat/filebeat.yml:/usr/share/filebeat/filebeat.yml:ro
      - /var/lib/docker/containers:/var/lib/docker/containers:ro
      - /var/run/docker.sock:/var/run/docker.sock:ro
    depends_on:
      elasticsearch:
        condition: service_healthy

volumes:
  elasticsearch-data:
```

---

### Logstash Pipeline Configuration

```ruby
# logstash/pipeline/logstash.conf

input {
  beats {
    port => 5044
  }
  
  tcp {
    port => 5000
    codec => json_lines
  }
}

filter {
  # Parse JSON logs
  if [message] =~ /^\{/ {
    json {
      source => "message"
      target => "parsed"
    }
    
    mutate {
      rename => { "[parsed][level]" => "log_level" }
      rename => { "[parsed][message]" => "log_message" }
      rename => { "[parsed][timestamp]" => "@timestamp" }
    }
  }
  
  # Parse Apache/Nginx access logs
  if [type] == "nginx" {
    grok {
      match => { "message" => '%{IPORHOST:client_ip} - %{USER:ident} \[%{HTTPDATE:timestamp}\] "%{WORD:method} %{URIPATHPARAM:request} HTTP/%{NUMBER:http_version}" %{NUMBER:status} %{NUMBER:bytes} "%{DATA:referrer}" "%{DATA:user_agent}"' }
    }
    
    date {
      match => [ "timestamp", "dd/MMM/yyyy:HH:mm:ss Z" ]
    }
    
    geoip {
      source => "client_ip"
      target => "geoip"
    }
  }
  
  # Add environment metadata
  mutate {
    add_field => {
      "environment" => "${ENVIRONMENT:production}"
      "cluster" => "${CLUSTER:default}"
    }
  }
  
  # Remove unnecessary fields
  mutate {
    remove_field => ["agent", "ecs", "host", "input", "log"]
  }
}

output {
  elasticsearch {
    hosts => ["http://elasticsearch:9200"]
    index => "logs-%{+YYYY.MM.dd}"
    
    # Index lifecycle management
    ilm_enabled => true
    ilm_rollover_alias => "logs"
    ilm_pattern => "{now/d}-000001"
    ilm_policy => "logs-policy"
  }
  
  # Debug output
  # stdout { codec => rubydebug }
}
```

---

### Filebeat Configuration

```yaml
# filebeat/filebeat.yml
filebeat.inputs:
  # Container logs
  - type: container
    paths:
      - '/var/lib/docker/containers/*/*.log'
    processors:
      - add_docker_metadata:
          host: "unix:///var/run/docker.sock"
      - decode_json_fields:
          fields: ["message"]
          target: "json"
          overwrite_keys: true

  # Application logs
  - type: log
    enabled: true
    paths:
      - /var/log/app/*.log
    fields:
      type: application
    multiline.pattern: '^[0-9]{4}-[0-9]{2}-[0-9]{2}'
    multiline.negate: true
    multiline.match: after

# Kubernetes autodiscover
filebeat.autodiscover:
  providers:
    - type: kubernetes
      node: ${NODE_NAME}
      hints.enabled: true
      hints.default_config:
        type: container
        paths:
          - /var/log/containers/*${data.kubernetes.container.id}.log

processors:
  - add_host_metadata: ~
  - add_cloud_metadata: ~
  - add_kubernetes_metadata:
      host: ${NODE_NAME}
      matchers:
        - logs_path:
            logs_path: "/var/log/containers/"

output.elasticsearch:
  hosts: ["http://elasticsearch:9200"]
  indices:
    - index: "filebeat-app-%{+yyyy.MM.dd}"
      when.contains:
        fields.type: "application"
    - index: "filebeat-system-%{+yyyy.MM.dd}"
      when.contains:
        fields.type: "system"

# Or send to Logstash
# output.logstash:
#   hosts: ["logstash:5044"]

setup.kibana:
  host: "http://kibana:5601"

setup.dashboards.enabled: true
```

---

### Elasticsearch Index Lifecycle Management

```json
PUT _ilm/policy/logs-policy
{
  "policy": {
    "phases": {
      "hot": {
        "min_age": "0ms",
        "actions": {
          "rollover": {
            "max_age": "1d",
            "max_size": "50gb"
          },
          "set_priority": {
            "priority": 100
          }
        }
      },
      "warm": {
        "min_age": "7d",
        "actions": {
          "shrink": {
            "number_of_shards": 1
          },
          "forcemerge": {
            "max_num_segments": 1
          },
          "set_priority": {
            "priority": 50
          }
        }
      },
      "cold": {
        "min_age": "30d",
        "actions": {
          "set_priority": {
            "priority": 0
          }
        }
      },
      "delete": {
        "min_age": "90d",
        "actions": {
          "delete": {}
        }
      }
    }
  }
}
```

---

### Kibana Query Examples (KQL)

```
# Basic queries
status:200                              # Exact match
status:>=400                            # Comparison
message:*error*                         # Wildcard
not status:200                          # Negation

# Field existence
_exists_:error                          # Field exists
not _exists_:user_id                    # Field doesn't exist

# Logical operators
status:200 and method:GET               # AND
status:404 or status:500                # OR
status:200 and not method:OPTIONS       # Combined

# Phrase search
message:"connection refused"            # Exact phrase
message:"connection * refused"          # With wildcard

# Range queries
@timestamp >= "2024-01-01"
response_time:[100 TO 500]              # Inclusive range
bytes:>1000                             # Greater than

# Nested and complex
kubernetes.namespace:production and (status:500 or status:503)
service.name:api and response_time>1000 and not path:/health
```

---

### ELK Best Practices

| Area | Practice |
| :--- | :--- |
| **Indexing** | Use date-based indices, implement ILM |
| **Sharding** | 20-50GB per shard, avoid over-sharding |
| **Mapping** | Define explicit mappings, use keyword for filters |
| **Retention** | Implement lifecycle policies, archive old data |
| **Security** | Enable authentication, encrypt in transit |
| **Performance** | Use SSD storage, allocate 50% heap to ES |
| **Monitoring** | Monitor cluster health, disk usage, queue sizes |

---

### Observability Comparison Summary

### When to Use Which Tool

| Scenario | Recommended Tool |
| :--- | :--- |
| **Full-stack APM** | DataDog, New Relic, Dynatrace |
| **Cost-conscious metrics** | Prometheus + Grafana |
| **Log aggregation** | ELK Stack, Loki |
| **Cloud-native K8s** | Prometheus Operator |
| **Quick start/SaaS** | DataDog, New Relic |
| **Open source preference** | Grafana Stack (LGTM) |
| **Enterprise compliance** | Splunk, Dynatrace |

### The LGTM Stack (Open Source Alternative)

```
┌────────────────────────────────────────────────────────────────────┐
│                      Grafana LGTM Stack                            │
├────────────────────────────────────────────────────────────────────┤
│                                                                    │
│   L - Loki      (Logs)                                             │
│   G - Grafana   (Visualization)                                    │
│   T - Tempo     (Traces)                                           │
│   M - Mimir     (Metrics - Prometheus compatible)                  │
│                                                                    │
│   All unified in Grafana with correlation between pillars          │
│                                                                    │
└────────────────────────────────────────────────────────────────────┘
```

---

## Section 15 — Performance & Optimization

### Performance Testing Types

| Type | Purpose | When |
| :--- | :--- | :--- |
| **Load Testing** | Expected traffic | Pre-production |
| **Stress Testing** | Beyond limits | Capacity planning |
| **Spike Testing** | Sudden traffic bursts | Event preparation |
| **Soak Testing** | Extended duration | Memory leak detection |
| **Chaos Testing** | Failure injection | Resilience validation |

**Tools**: JMeter, Locust, k6, Gatling, Chaos Monkey

---

### Caching Strategies

| Strategy | Description | Use Case |
| :--- | :--- | :--- |
| **Cache-Aside** | App checks cache, then DB | General purpose |
| **Write-Through** | Write to cache AND DB | Consistency critical |
| **Write-Behind** | Write to cache, async to DB | Write-heavy workloads |
| **Read-Through** | Cache fetches from DB on miss | Simplify app code |

**Tools**: Redis, Memcached, Varnish, CloudFront

---

## Section 16 — Scenario-Based Questions

### Scenario 1: Production Outage

**Question**: Your application is returning HTTP 503 errors. How do you troubleshoot?

**Systematic Approach**:
1. **Verify the issue**: Check from multiple sources (monitoring, different clients)
2. **Check load balancer**: Are backend targets healthy?
3. **Check application pods**: `kubectl get pods` - are pods running?
4. **Check logs**: `kubectl logs <pod>` - application errors?
5. **Check resources**: `kubectl top pods` - CPU/memory exhaustion?
6. **Check dependencies**: Database, Redis, external APIs healthy?
7. **Check recent changes**: Was there a deployment? Rollback if needed.
8. **Check infrastructure**: Node health, network connectivity

---

### Scenario 2: Database Connection Issues

**Question**: Application logs show "Connection pool exhausted". What's wrong?

**Root Causes**:
1. **Connection leaks**: Connections not being returned to pool
2. **Pool too small**: Not enough connections for traffic
3. **Long queries**: Queries holding connections too long
4. **Database overloaded**: DB can't accept more connections

**Solutions**:
1. Check code for connection leaks (missing `close()`)
2. Increase pool size with limits
3. Add query timeouts
4. Scale database or add read replicas

---

### Scenario 3: Slow Deployments

**Question**: Deployments take 30+ minutes. How would you speed them up?

**Optimization Areas**:
1. **Docker builds**:
   - Use multi-stage builds
   - Optimize layer caching
   - Use smaller base images
   
2. **CI/CD pipeline**:
   - Parallelize tests
   - Cache dependencies
   - Use incremental builds
   
3. **Kubernetes**:
   - Pre-pull images to nodes
   - Use rolling updates with appropriate surge
   - Optimize readiness/liveness probes

---

### Scenario 4: Cost Optimization

**Question**: AWS bill spiked 40% this month. How do you investigate?

**Approach**:
1. **Cost Explorer**: Identify which services increased
2. **Resource tagging**: Find untagged/orphaned resources
3. **Right-sizing**: Are instances over-provisioned?
4. **Reserved capacity**: Could savings plans reduce costs?
5. **Storage**: Old snapshots, unused EBS volumes?
6. **Data transfer**: Unexpected egress charges?
7. **Automation**: Turn off dev/test environments after hours

---

### Scenario 5: Security Incident

**Question**: Security team detected suspicious API calls. How do you respond?

**Incident Response**:
1. **Contain**: Revoke compromised credentials immediately
2. **Identify**: Which credentials? What access scope?
3. **Investigate**: CloudTrail/audit logs - what did attacker do?
4. **Eradicate**: Remove any backdoors, malicious resources
5. **Recover**: Rotate all potentially compromised secrets
6. **Post-mortem**: How did credentials leak? Prevent recurrence

---

### Scenario 6: Scaling Challenge

**Question**: Application handles 1000 RPS but needs to scale to 10,000 RPS. How?

**Scaling Strategy**:
1. **Identify bottlenecks**: Profile to find constraints
2. **Horizontal scaling**: Add more instances/pods
3. **Database**: Read replicas, connection pooling, caching
4. **Caching**: Redis for hot data, CDN for static assets
5. **Async processing**: Queue long-running tasks
6. **Architecture**: Consider microservices for independent scaling

---

## Quick Reference Commands

### Docker
```bash
docker build -t app:v1 .
docker run -d -p 8080:80 app:v1
docker exec -it container_id sh
docker logs -f container_id
docker-compose up -d
```

### Kubernetes
```bash
kubectl apply -f manifest.yaml
kubectl get pods -o wide
kubectl describe pod <pod>
kubectl logs -f <pod>
kubectl exec -it <pod> -- sh
kubectl rollout restart deployment/<name>
kubectl rollout undo deployment/<name>
```

### Terraform
```bash
terraform init
terraform plan -out=plan.tfplan
terraform apply plan.tfplan
terraform destroy
terraform state list
```

### Ansible
```bash
ansible-playbook -i inventory playbook.yml
ansible all -m ping
ansible-playbook playbook.yml --check
ansible-vault encrypt secrets.yml
```

### AWS CLI
```bash
aws s3 ls s3://bucket/
aws ec2 describe-instances
aws logs tail /aws/lambda/my-function --follow
aws sts get-caller-identity
```

---


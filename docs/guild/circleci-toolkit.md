# Pioneer Agent v2 CircleCI Toolkit

## Overview

This toolkit provides implementation-focused procedures for monitoring, troubleshooting, and managing the CircleCI production build pipeline for Pioneer Agent v2. All commands are executable and validated.

## Installation & Setup

### Step 1: Configure CircleCI API Access

```bash
# Set up CircleCI environment
cd /Users/highlander/WebstormProjects/pioneer-agent-v2
bash skills/untested/circleci/auto-setup.sh
```

This will:
- Create `~/.circleci/` directory
- Store your CircleCI token securely
- Configure project settings for API access

### Step 2: Verify Setup

```bash
# Test API access
cd /Users/highlander/WebstormProjects/pioneer-agent-v2
bash skills/untested/circleci/circle status

# Expected output: Details about the most recent build on your current branch
```

## Build Pipeline Diagnostics

### Quick Status Check

```bash
# Check build status on current branch
cd /Users/highlander/WebstormProjects/pioneer-agent-v2
bash skills/untested/circleci/circle status

# Check status on a specific branch
bash skills/untested/circleci/circle status main
```

### Configuration Validation

```bash
# Analyze config for potential issues
cd /Users/highlander/WebstormProjects/pioneer-agent-v2
bash skills/untested/circleci/analyze-config.sh

# Expected output: Detailed analysis of your .circleci/config.yml file
```

### Retrieve Build Logs

```bash
# Get logs from the most recent build
cd /Users/highlander/WebstormProjects/pioneer-agent-v2
bash skills/untested/circleci/circle logs

# Get logs for a specific job on a specific branch
bash skills/untested/circleci/circle logs main build-and-push
```

### Verify Build Hash

```bash
# Verify your local code matches what's in CircleCI
cd /Users/highlander/WebstormProjects/pioneer-agent-v2
bash skills/untested/circleci/circle verify

# Expected output: Confirmation that your local git hash matches the one in CircleCI
```

## Common Issues & Fixes

### 1. Docker Version Compatibility

**Issue**: `Job was rejected because this version of Docker is not supported on this resource class`

**Solution**:
```bash
# Check Docker configuration in CircleCI
cd /Users/highlander/WebstormProjects/pioneer-agent-v2
grep -A 10 "setup_remote_docker" .circleci/config.yml

# Fix: Remove Docker version specification
sed -i '' '/version:/d' .circleci/config.yml

# Verify fix
grep -A 10 "setup_remote_docker" .circleci/config.yml
```

### 2. Node.js Image Compatibility 

**Issue**: Incompatible Node.js version

**Solution**:
```bash
# Check current Node image
cd /Users/highlander/WebstormProjects/pioneer-agent-v2
grep -A 2 "image: cimg/node" .circleci/config.yml

# Fix: Update to compatible version
sed -i '' 's/image: cimg\/node:.*$/image: cimg\/node:18.19/' .circleci/config.yml
```

### 3. Build Timeout Issues

**Issue**: Builds timing out during Docker operations

**Solution**:
```bash
# Apply timeout fix
bash skills/untested/circleci/apply_fixes.sh timeout
```

## Deployment Verification

After CircleCI successfully builds and deploys:

```bash
# Verify Docker image was pushed correctly
cd /Users/highlander/WebstormProjects/pioneer-agent-v2
bash skills/untested/circleci/check_image.sh

# Verify deployment is healthy
bash skills/untested/circleci/check_deployment.sh
```

## Build Monitoring

### Manual Build Monitoring

```bash
# Monitor ongoing build
cd /Users/highlander/WebstormProjects/pioneer-agent-v2
bash skills/untested/circleci/monitor_build.sh

# Monitor specific workflow
WORKFLOW_ID=$(bash skills/untested/circleci/circle status | grep -o "workflow_id: [a-f0-9-]*" | cut -d' ' -f2)
bash skills/untested/circleci/monitor_workflow.sh $WORKFLOW_ID
```

### Automatic Build Monitoring

```bash
# Set up automated build monitoring (runs every 5 minutes)
cd /Users/highlander/WebstormProjects/pioneer-agent-v2
bash skills/untested/circleci/monitor-pipeline.sh &

# To stop monitoring
pkill -f "bash.*monitor-pipeline.sh"
```

## Trigger Builds Manually

```bash
# Trigger a build on the current branch
cd /Users/highlander/WebstormProjects/pioneer-agent-v2
bash skills/untested/circleci/circle trigger

# Trigger a build on a specific branch
bash skills/untested/circleci/trigger-build.sh main
```

## Sprint Wrap-Up Reporting

Generate a report of all CircleCI builds during the sprint:

```bash
# Generate sprint report (last 2 weeks)
cd /Users/highlander/WebstormProjects/pioneer-agent-v2
bash skills/untested/circleci/sprint-wrap.sh > docs/sprint-reports/circleci-sprint-report.md

# Expected output: Complete report with build statistics, success rates, and failure analysis
```

## Port Configuration Verification

Verify that your Docker container is exposing the correct ports:

```bash
# Check port configuration in Dockerfile
cd /Users/highlander/WebstormProjects/pioneer-agent-v2
grep -A 3 "EXPOSE" apps/server/Dockerfile

# Verify port matches CircleCI health check
grep -A 10 "health" .circleci/config.yml
```

## Health Check Verification

```bash
# Test health endpoint on local Docker container
docker run -d --name pioneer-test -p 3000:3000 pioneer-agent:latest
curl http://localhost:3000/health
docker stop pioneer-test && docker rm pioneer-test
```

## Emergency Actions

### Stop Current Build

```bash
# Get current build number
BUILD_NUM=$(bash skills/untested/circleci/circle status | grep -o "build_num: [0-9]*" | cut -d' ' -f2)

# Cancel build
curl -X POST -H "Circle-Token: ${CIRCLE_TOKEN}" \
  https://circleci.com/api/v1.1/project/${CIRCLE_PROJECT_SLUG}/${BUILD_NUM}/cancel
```

### Clean Up Docker Resources

If builds are failing due to Docker resource issues:

```bash
# Clean up Docker resources on CircleCI
bash skills/untested/circleci/cleanup_docker.sh
```

## Advanced Features

### Continuous Integration Alerts

Set up Slack notifications for failed builds:

```bash
# Configure Slack notifications
cd /Users/highlander/WebstormProjects/pioneer-agent-v2/skills/untested/circleci
cp config.json.example config.json
# Edit config.json to add your Slack webhook URL
```

### Build Analytics

Generate build analytics for the last month:

```bash
# Get build analytics
cd /Users/highlander/WebstormProjects/pioneer-agent-v2
bash skills/untested/circleci/circle analytics > docs/build-analytics.md
```

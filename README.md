Jenkins README — CI/CD Quickstart

Overview
- Purpose: concise Jenkins guide for Node.js + Docker projects and a ready-to-use `Jenkinsfile` sample.

Prerequisites
- Ubuntu server (example: 24.04)
- Java (JDK 17+ or 21)
- Jenkins installed and running on port 8080
- Docker installed on Jenkins host or Docker-enabled agent
- GitHub repo with project and `Dockerfile`

Install & initial setup (high level)
1. Update system:
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```
2. Install Java (Temurin/OpenJDK) and verify:
   ```bash
   java -version
   ```
3. Add Jenkins repo, install, and start:
   ```bash
   # follow official Jenkins docs to add repo/GPG key
   sudo apt update
   sudo apt install jenkins -y
   sudo systemctl enable --now jenkins
   sudo systemctl status jenkins
   ```
4. Open UI: `http://<jenkins-host-ip>:8080` and use `/var/lib/jenkins/secrets/initialAdminPassword` to unlock.

Permissions
- If Jenkins must run Docker locally, add the Jenkins user to the `docker` group:
  ```bash
  sudo usermod -aG docker jenkins && sudo systemctl restart jenkins
  ```

GitHub webhook
- Configure your GitHub repo > Settings > Webhooks to POST to: `http://<jenkins-host>/github-webhook/` (or use Jenkins GitHub plugin integration).

Credentials
- Store Docker Hub credentials, SSH keys, and other secrets in Jenkins Credentials (avoid plaintext in pipelines).

Jenkinsfile (declarative) — Node + Docker example
```groovy
pipeline {
  agent any
  environment {
    IMAGE = "${env.JOB_NAME.toLowerCase()}:$BUILD_NUMBER"
  }
  stages {
    stage('Checkout') {
      steps { git branch: 'main', url: 'https://github.com/yourorg/yourrepo.git' }
    }
    stage('Build') {
      steps {
        sh 'docker build -t $IMAGE .'
      }
    }
    stage('Stop Old') {
      steps {
        sh "if docker ps -q --filter name=app_container; then docker stop app_container || true; docker rm app_container || true; fi"
      }
    }
    stage('Run') {
      steps {
        sh 'docker run -d --name app_container -p 8050:80 $IMAGE'
      }
    }
    stage('Verify') {
      steps { sh 'docker ps --filter name=app_container' }
    }
  }
  post {
    success { echo 'Deployed successfully' }
    failure { echo 'Pipeline failed' }
  }
}
```

Notes & best practices
- Use dedicated Docker agents or the Docker plugin for safer builds.
- Avoid running `docker` as root inside the Jenkins master.
- Use credentials binding for `docker login` when pushing images.
- Add cleanup steps for old images and containers to save disk space.
- For production pipelines consider CD via orchestration (Kubernetes, Docker Compose, or a deployment tool).

Common commands (Jenkins host)
```bash
# Build & run
docker build -t myapp .
docker stop myapp_container || true
docker rm myapp_container || true
docker run -d --name myapp_container -p 8050:80 myapp
# Logs
docker logs -f myapp_container
# Jenkins
sudo systemctl status jenkins
journalctl -u jenkins -n 200 --no-pager
```

Troubleshooting
- If Jenkins cannot run Docker: ensure `jenkins` user is in `docker` group and service restarted.
- Webhook not triggering: check GitHub webhook delivery logs and Jenkins Git plugin configuration.
- Permission errors: ensure ownership `chown -R jenkins:jenkins /var/lib/jenkins` for custom dirs.

Next steps I can do for you
- Add this `Jenkinsfile` to your repository and commit.
- Create a `deploy.sh` script for Jenkins to call (stop/remove/run).
- Add a sample Jenkins job configuration or a GitHub webhook example.

# DevOps 

This repository contains concise notes and commands practiced across six DevOps class.

---

**Day 1 — Basic Linux Commands**

- **Directory:** `pwd`, `ls`, `ls -l`, `ls -a`, `cd <dir>`, `cd ..`, `cd ~`, `mkdir <dir>`, `rmdir <dir>`
- **Files:** `touch file.txt`, `vim file.txt`, `cat file.txt`, `cp src dest`, `mv old new`, `rm file.txt`, `history`
- **Wildcards:** `ls *.txt`, `rm *.txt`, `ls file?.txt`
- **Packages (Ubuntu):** `sudo apt update`, `sudo apt upgrade -y`
- **SSH (server):** `sudo apt install openssh-server`, `sudo systemctl status ssh`, `sudo systemctl start ssh`, `sudo systemctl enable ssh`
- **Useful:** `clear` (Ctrl+L), `head file.txt`, `tail file.txt`, `tail -f file.txt`, `chmod +x script.sh`, `ps`, `top`, `ip a`, `ping <host>`

**Day 2 — Docker Basics**

- Install Docker (Ubuntu):

```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
docker --version
docker info
```

- Common commands: `docker images`, `docker pull <image>`, `docker run <image>`, `docker run -d <image>`, `docker ps`, `docker ps -a`, `docker stop <id>`, `docker rm <id>`, `docker rmi <image>`
- Run nginx with port mapping: `docker run -d -p 8080:80 nginx` → open `http://<host>:8080`

**Day 3 — Git & SSH (redacted)**

- Configure Git global identity (use your details):

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --list
```

- Generate SSH key and add to your Git host (redacted):

```bash
ssh-keygen -t ed25519 -C "you@example.com"
cat ~/.ssh/id_ed25519.pub
# Add the public key to your Git hosting account
```

- Clone repositories via SSH: `git clone <ssh-repo-url>`
- Branch workflow:
  - `git branch`
  - `git checkout -b <new-branch>`
  - `git add .`
  - `git commit -m "message"`
  - `git push origin <branch>`

**Day 4 — Jenkins CI/CD with Docker**

- Install Java and Jenkins (Ubuntu):

```bash
sudo apt update
sudo apt install openjdk-21-jre -y
sudo apt install jenkins -y
sudo systemctl start jenkins
sudo systemctl enable jenkins
sudo systemctl status jenkins
```

- Unlock Jenkins using the initial admin password: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`
- Install Docker and allow the `jenkins` user to run Docker by adding it to the `docker` group:

```bash
sudo apt install docker.io -y
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
```

- Typical pipeline stages for a Docker-based app:
  - Build Docker image
  - Stop old container
  - Remove old container
  - Run new container (map ports as required)

**Day 5 — AWS, EC2 & Terraform (summary)**

- Create AWS account and use EC2 to launch instances (Windows/Ubuntu). Create and download key pairs for SSH/RDP access.
- Install Terraform (Ubuntu): `sudo apt install terraform -y` and verify `terraform -version`.
- Terraform workflow: `terraform init`, `terraform validate`, `terraform plan`, `terraform apply`, `terraform destroy`.

**Day 6 — Ansible Apache Deployment (summary)**

- Install Ansible: `sudo apt update && sudo apt install ansible -y` and verify with `ansible --version`.
- Use an inventory file and SSH keys to connect to target hosts. Example connectivity test:

```bash
ansible -i inventory.ini all -m ping
```

- Run playbook to install/configure Apache:

```bash
ansible-playbook -i inventory.ini apache-playbook.yml
```

---

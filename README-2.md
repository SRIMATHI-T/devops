**Overview**
- **Purpose:** Quick reference for common Linux shell commands, wildcards, apt, IPv4 basics, Docker, system checks, and Git workflow.

**Shell Basics**
- **Remove Dir:** `rm -rf directory_name` — recursively and forcefully remove a directory.
- **Note:** `-rdf` is unnecessary; `-rf` is sufficient and flag order doesn't matter.

**Wildcards in `ls`**
- **`*` :** Matches any number of characters. Example: `ls *.txt` — lists all .txt files.
- **`?` :** Matches exactly one character. Example: `ls file?.txt` — matches `file1.txt` but not `file10.txt`.
- **`[ ]` :** Matches any one character inside brackets. Example: `ls file[12].txt` — matches `file1.txt` and `file2.txt`.
- **Example:** `ls *.??` — lists files with any name and exactly two-character extension (e.g., `file.sh`, `data.py`). Does not match `file.txt` or `a.c`.

**Apt — Update & Upgrade (Ubuntu/Debian)**
- **Purpose:** Keep system packages up-to-date.
- `sudo apt update` — refresh package lists.
- `sudo apt upgrade` — install available upgrades for installed packages.
- **Combined:** `sudo apt update && sudo apt upgrade -y` (`-y` auto-confirms prompts).

**IPv4 — Address Allocation**
- **Format:** 32-bit address, four octets (0–255), e.g., `192.168.1.10`.
- **Assignment methods:**
  - **Static (manual):** Admin assigns a fixed IP (common for printers, servers).
  - **Dynamic (DHCP):** Router/DHCP server assigns available IPs automatically (laptops, phones).
- **Purpose:** Unique address for sending/receiving network traffic.

**Docker — Quick Guide**
- **What is Docker:** Container platform packaging app, libraries, runtime, and config so it runs consistently across environments.
- **Key terms:**
  - **Image:** Immutable blueprint for a container.
  - **Container:** Running instance of an image.
  - **Dockerfile:** Recipe to build an image.
- **Why use Docker:** Portability, lightweight, consistency between dev/test/production.

**Docker — Common Commands**
- **Build image:** `docker build -t my-app-name .` (run where `Dockerfile` is located).
- **Run container:** `docker run -d -p 8080:80 --name my_app my-app-name` (`-d` runs detached, `-p` publishes ports).
- **List images:** `docker images`
- **List running containers:** `docker ps`
- **Build without cache:** `docker build --no-cache -t my-app-name .`

**Docker — Push/Pull (registry)**
- **Tag:** `docker tag my-app:latest myrepo/my-app:tag`
- **Push:** `docker push myrepo/my-app:tag`
- **Pull:** `docker pull myrepo/my-app:tag`

**System & Network Checks**
- `more /etc/os-release` — view OS/version info.
- `ifconfig` or `ip addr` / `ip a` — show network interfaces and IPs (install `net-tools` for `ifconfig`).
- `ping -c 3 google.com` — test connectivity.
- `sudo systemctl status ssh` — check ssh service status.
- `sudo ufw status` / `sudo ufw allow ssh` — firewall status and allow SSH.

**Git — Basics & Workflow**
- **What is Git:** Distributed version control for tracking code changes and collaboration.
- **Main concepts:**
  - **`main` branch:** Default stable branch.
  - **Feature branch:** Branch off `main` to work on a feature, then merge back.
  - **Commit:** Snapshot of changes with a message.
- **Common commands:**
  1. `mkdir myproject && cd myproject`
  2. `git init` — initialize repository.
  3. `git add .` — stage changes.
  4. `git commit -m "Initial commit"` — commit staged changes.
  5. `git remote add origin https://github.com/username/repo.git` — add remote.
  6. `git push -u origin main` — push commits to remote.
- **Edit & update cycle:** Edit file → `git add .` → `git commit -m "msg"` → `git push`.
- **View history:** `git log`.
- **HEAD vs Tail:** `HEAD` points to latest commit; the tail is the oldest commit in history.

**Example: Docker install & project history (short)**
- Sequence example used while setting up Docker and a project:
  - `sudo apt update && sudo apt upgrade -y`
  - Install Docker prerequisites and add Docker repo/gpg key
  - `sudo apt install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin`
  - `docker build -t docker-sample .` and `sudo docker run -d -p 3000:3000 --name docker_sample docker-sample`
  - Typical local Git steps: `git init`, `git add .`, `git commit -m "Initial commit"`, `git remote add origin <repo>`, `git push -u origin main`.

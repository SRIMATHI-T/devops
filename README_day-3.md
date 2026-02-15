**Docker — Quick Guide**
- **What is Docker:** Container platform packaging app, libraries, runtime, and config so it runs consistently across environments.
- **Key terms:**
  - **Image:** Immutable blueprint for a container.
  - **Container:** Running instance of an image.
  - **Dockerfile:** Recipe to build an image.
- **Why use Docker:** Portability, lightweight, consistency between dev/test/production.

---

## Docker Sample App (Node.js)

This small sample demonstrates a minimal Express app, `Dockerfile`, and commands to build/run locally.

Files added to workspace:
- `app.js` — example Express server
- `package.json` — project metadata and dependency
- `Dockerfile` — builds image using `node:18-alpine`

app.js
```js
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello from Docker!');
});

app.listen(3000, '0.0.0.0', () => {
  console.log('App running on port 3000');
});
```

package.json
```json
{
  "name": "docker-basic-app",
  "version": "1.0.0",
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  },
  "dependencies": {
    "express": "^4.18.2"
  }
}
```

Dockerfile
```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install --only=production
COPY . .
EXPOSE 3000
CMD ["node", "app.js"]
```

Build and run (from the project folder where `Dockerfile` lives):

```bash
docker build -t docker-basic-app .
docker run -d -p 3000:3000 --name docker_basic_app docker-basic-app
```

Open in browser:

- `http://localhost:3000` or `http://<your-vm-ip>:3000` — you should see `Hello from Docker!`.

Notes:
- `0.0.0.0` in `app.listen` makes the server reachable from outside the container.
- Use `docker logs docker_basic_app` to see output.

---

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

**How to use this README**
- Copy useful command snippets into your terminal.
- Edit examples (`my-app-name`, ports, repo URLs) to match your project.

**Files added**
- `app.js`
- `package.json`
- `Dockerfile`

---

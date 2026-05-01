<div align="center">

# BewohnerApp Demo

### Run a modern resident communication platform locally with Docker.

[![Docker](https://img.shields.io/badge/Requirement-Docker%20Desktop-2496ED?logo=docker&logoColor=white)](https://www.docker.com/products/docker-desktop/)
![Windows](https://img.shields.io/badge/Windows-PowerShell-0078D4?logo=windows&logoColor=white)
![macOS](https://img.shields.io/badge/macOS-Terminal-000000?logo=apple&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-Terminal-FCC624?logo=linux&logoColor=black)
![Image](https://img.shields.io/badge/Image-GHCR-orange)

[Quick Start](#quick-start) · [Demo Login](#demo-login) · [Try the Workflow](#try-the-workflow) · [Troubleshooting](#troubleshooting)

</div>

---

## Overview

**BewohnerApp** is a resident communication and staff management platform for accommodation or residential environments.

With the demo you can create residents, invite them into the system, send notifications, manage resident-facing content, and test the communication workflow from one admin dashboard.

The demo runs from this Docker image:

```text
ghcr.io/hosseinebi71/bewohner-app:latest
```

---

## Before You Start

Install Docker first, then come back and run the demo.

- **Windows:** [Install Docker Desktop for Windows](https://docs.docker.com/desktop/setup/install/windows-install/)
- **macOS:** [Install Docker Desktop for Mac](https://docs.docker.com/desktop/setup/install/mac-install/)
- **Linux:** [Install Docker Engine for Linux](https://docs.docker.com/engine/install/)

Check that Docker is available:

```bash
docker --version
```

---

## Quick Start

Use the same command on **Windows PowerShell**, **macOS Terminal**, or **Linux Terminal**:

```bash
docker rm -f bewohner-demo
docker pull ghcr.io/hosseinebi71/bewohner-app:latest
docker run -d --name bewohner-demo -p 8001:8000 ghcr.io/hosseinebi71/bewohner-app:latest
```

If Docker on Linux asks for root permissions, run the same commands with `sudo`:

```bash
sudo docker rm -f bewohner-demo
sudo docker pull ghcr.io/hosseinebi71/bewohner-app:latest
sudo docker run -d --name bewohner-demo -p 8001:8000 ghcr.io/hosseinebi71/bewohner-app:latest
```

---

## Open the Demo

**Admin panel**

```text
http://127.0.0.1:8001/secure-admin-panel/
```

**Public page**

```text
http://127.0.0.1:8001/
```

---

## Demo Login

The container creates a temporary admin user automatically:

```text
Username: demo-admin
Password: DemoAdmin123!
```

You can also check the credentials in the logs:

```bash
docker logs bewohner-demo
```

On Linux with sudo:

```bash
sudo docker logs bewohner-demo
```

---

## Try the Workflow

### 1. Log in to the admin panel

Open the admin panel and sign in with the demo admin account.

From there, you can create realistic test data and explore the management side of the app.

### 2. Create a resident

Create a resident with sample details such as name, room/house information, language, email, and profile information.

This resident becomes the center of the workflow: account activation, resident login, notifications, inbox messages, and confirmations.

### 3. Invite the resident

After the resident exists, use the available invitation or activation information.

The app supports an invite-style onboarding flow where staff can give the resident an activation code, invite link, or QR-based access path depending on the screen.

A good demo path is:

1. Create a resident.
2. Find the resident invite or activation information.
3. Open the invite link or use the QR/invitation code.
4. Complete the resident activation flow.
5. Log in as the resident and check what is available on the resident side.

### 4. Send a notification

Create a notification for the resident and then check the resident inbox.

This shows the communication part of the system: staff can send updates, reminders, appointments, or important messages, and residents can receive them in a structured place.

---

## Useful Commands

Check whether the container is running:

```bash
docker ps
```

View logs:

```bash
docker logs bewohner-demo
```

Stop and remove the demo container:

```bash
docker rm -f bewohner-demo
```

Restart from a fresh container:

```bash
docker rm -f bewohner-demo
docker pull ghcr.io/hosseinebi71/bewohner-app:latest
docker run -d --name bewohner-demo -p 8001:8000 ghcr.io/hosseinebi71/bewohner-app:latest
```

---

## Port Information

The command uses:

```text
-p 8001:8000
```

That means:

- `8000` is the internal container port.
- `8001` is the browser port on your machine.

Open the admin panel:

```text
http://127.0.0.1:8001/secure-admin-panel/
```

If port `8001` is already busy, use another local port:

```bash
docker run -d --name bewohner-demo -p 8002:8000 ghcr.io/hosseinebi71/bewohner-app:latest
```

Then open:

```text
http://127.0.0.1:8002/secure-admin-panel/
```

---

## Notes

- The demo uses SQLite inside the container for quick local testing.
- Data is temporary and resets when the container is removed.
- The `latest` tag points to the newest published demo image.

---

## Troubleshooting

### Image cannot be pulled

Make sure the Docker image is public and available:

```text
ghcr.io/hosseinebi71/bewohner-app:latest
```

### Port is already allocated

Stop the old container:

```bash
docker rm -f bewohner-demo
```

Or run it on another port, for example `8002`.

### Admin login does not work

Check the logs:

```bash
docker logs bewohner-demo
```

The demo admin credentials are printed when the container starts.

---

<div align="center">

**BewohnerApp Demo** · Docker-first · Reviewer-friendly · Local setup in minutes

</div>

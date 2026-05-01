<div align="center">

# BewohnerApp Demo

### Run a modern resident communication platform locally with Docker.

[![Docker](https://img.shields.io/badge/Requirement-Docker%20Desktop-2496ED?logo=docker&logoColor=white)](https://www.docker.com/products/docker-desktop/)
![Windows](https://img.shields.io/badge/Windows-Ready-0078D4?logo=windows&logoColor=white)
![macOS](https://img.shields.io/badge/macOS-Ready-000000?logo=apple&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-Ready-FCC624?logo=linux&logoColor=black)
![Docker Image](https://img.shields.io/badge/Docker%20Image-Ready-orange)

[Quick Start](#quick-start) · [Demo Access](#demo-access) · [Try the Workflow](#try-the-workflow) · [Troubleshooting](#troubleshooting)

</div>

---

## Overview

**BewohnerApp** is a resident communication and staff management platform for accommodation or residential environments.

The demo starts with ready-to-test data: a temporary admin account, a sample resident, invite/activation codes, resident-facing content, and sample notifications.

The demo runs from this Docker image:

```text
ghcr.io/hosseinebi71/bewohner-app:latest
```

---

## Before You Start

Install Docker and make sure it is running:

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) for Windows and macOS
- [Docker Engine](https://docs.docker.com/engine/install/) for Linux

```bash
docker --version
```

---

## Quick Start

Pull the latest image:

```bash
docker pull ghcr.io/hosseinebi71/bewohner-app:latest
```

Start the demo:

```bash
docker run -d --name bewohner-demo -p 8001:8000 ghcr.io/hosseinebi71/bewohner-app:latest
```

If Docker says the container name is already in use, remove the old demo container and run the start command again:

```bash
docker rm -f bewohner-demo
```

Linux permission issue? Use `sudo` with the same commands.

---

## Demo Access

**Admin panel**

```text
http://127.0.0.1:8001/secure-admin-panel/
```

**Admin login**

```text
Username: demo-admin
Password: DemoAdmin123!
```

**Public page**

```text
http://127.0.0.1:8001/
```

The container also prints the ready-to-test demo data in the logs:

```bash
docker logs bewohner-demo
```

You will see the demo resident, invite code, activation code, and demo URLs there.

---

## Try the Workflow

### 1. Log in to the admin panel

Open the admin panel and sign in with the demo admin account.

A sample resident is already available, so you can immediately inspect the management workflow without building everything from zero.

### 2. Review the demo resident

Use the pre-created resident:

```text
Resident: Mina Karimi
PKZ: DEMO-1001
Room: Haus A / 101
Invite code: DEMO1001
```

This resident is connected to the demo invite flow, activation code, notifications, inbox messages, and confirmation workflow.

### 3. Test invite and activation

Check the container logs for the generated demo URLs:

```bash
docker logs bewohner-demo
```

The demo output includes the invite/activation information that can be used to test resident onboarding.

### 4. Send or review notifications

Open the resident's notifications and review the sample messages.

The demo includes an important notification that requires confirmation, plus an appointment-style reminder. This shows how staff can send structured updates and how residents receive them in one place.

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
- Demo data is created automatically when the container starts.
- Data is temporary and resets when the container is removed.
- The `latest` tag points to the newest published demo image.

---

## Troubleshooting

### Image cannot be pulled

Make sure the Docker image is public and available:

```text
ghcr.io/hosseinebi71/bewohner-app:latest
```

### Container name is already in use

Remove the old demo container and start it again:

```bash
docker rm -f bewohner-demo
docker run -d --name bewohner-demo -p 8001:8000 ghcr.io/hosseinebi71/bewohner-app:latest
```

### Port is already allocated

Use another local port, for example `8002`:

```bash
docker run -d --name bewohner-demo -p 8002:8000 ghcr.io/hosseinebi71/bewohner-app:latest
```

### Admin login does not work

Check the logs:

```bash
docker logs bewohner-demo
```

The demo admin credentials and demo data are printed when the container starts.

---

<div align="center">

**BewohnerApp Demo** · Docker-first · Ready-to-test data · Local setup in minutes

</div>

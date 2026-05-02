<div align="center">

# BewohnerApp Demo

### Docker-based demo for resident communication, staff workflows, and administration.

[![Docker](https://img.shields.io/badge/Requirement-Docker%20Desktop-2496ED?logo=docker&logoColor=white)](https://www.docker.com/products/docker-desktop/)
![Windows](https://img.shields.io/badge/Windows-Ready-0078D4?logo=windows&logoColor=white)
![macOS](https://img.shields.io/badge/macOS-Ready-000000?logo=apple&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-Ready-FCC624?logo=linux&logoColor=black)
![Docker Image](https://img.shields.io/badge/Docker%20Image-GHCR-orange)

[Quick Start](#quick-start) · [Demo Accounts](#demo-accounts) · [Guided Test Flow](#guided-test-flow) · [Useful Commands](#useful-commands) · [Troubleshooting](#troubleshooting)

</div>

---

## Overview

**BewohnerApp** is a web platform for residential/accommodation environments. It helps staff manage residents, send messages, share appointments, provide resident-facing information, and support onboarding through invite codes.

This public repository is a **Docker demo**. You can test the app without cloning the private source code and without setting up Python, Poetry, a database, or environment variables.

The demo includes three roles:

| Role | What it shows |
| --- | --- |
| **Admin** | System administration and backend data structure |
| **Staff / Mitarbeiter** | Daily staff dashboard, residents, messages, invite codes, notifications, and content |
| **Resident / Bewohner** | Resident login, inbox, appointments, confirmations, and public information |

Docker image:

```text
ghcr.io/hosseinebi71/bewohner-app:latest
```

---

## Before you start

Install Docker and make sure it is running:

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) for Windows and macOS
- [Docker Engine](https://docs.docker.com/engine/install/) for Linux

Check Docker:

```bash
docker --version
```

---

## Quick Start

### 1. Pull the demo image

```bash
docker pull ghcr.io/hosseinebi71/bewohner-app:latest
```

This downloads the ready-to-run demo image from GitHub Container Registry.

Approximate time:

- first download: usually **1-5 minutes**, depending on internet speed
- later downloads: usually faster, because Docker reuses cached layers

---

### 2. Start the demo container

```bash
docker run -d --name bewohner-demo -p 8001:8000 ghcr.io/hosseinebi71/bewohner-app:latest
```

This creates and starts a local container named `bewohner-demo`.

Behind the scenes, the container:

- starts the web application
- maps container port `8000` to your local browser port `8001`
- prepares a temporary SQLite demo database
- creates demo users, residents, messages, appointments, invite data, and staff permissions

Approximate startup time after the image is already downloaded:

- usually **10-30 seconds**
- on slower machines, allow up to **1 minute**

Then open:

```text
http://127.0.0.1:8001/
```

---

### 3. Check startup logs

```bash
docker logs -f bewohner-demo
```

Use this if the app does not open immediately or if you want to see the generated demo information.

Stop watching logs with:

```text
CTRL + C
```

The demo keeps running.

---

## Demo Accounts

### Admin

```text
URL:      http://127.0.0.1:8001/secure-admin-panel/
Username: demo-admin
Password: DemoAdmin123!
```

Use this to inspect the backend/admin side: users, residents, messages, notifications, and content-related data.

---

### Staff / Mitarbeiter

```text
URL:      http://127.0.0.1:8001/login/
Username: demo-staff
Password: DemoAdmin123!
```

After login, open:

```text
http://127.0.0.1:8001/staff/
```

Use this to review the operational workflow: resident management, invite codes, messages, appointments, notifications, and help/contact examples.

---

### Resident / Bewohner

```text
URL:      http://127.0.0.1:8001/resident/login/
Username: demo-resident
Password: DemoAdmin123!
```

Resident home:

```text
http://127.0.0.1:8001/
```

Use this to review the resident-facing experience: inbox, appointments, confirmations, and public content sections.

---

## Guided Test Flow

For a clear review, test the app in this order:

1. **Resident app**
   - open `http://127.0.0.1:8001/`
   - log in as `demo-resident`
   - check inbox, appointments, confirmations, and content sections

2. **Staff dashboard**
   - log in as `demo-staff`
   - open `http://127.0.0.1:8001/staff/`
   - review residents, messages, invite codes, notifications, and staff workflow

3. **Admin panel**
   - open `http://127.0.0.1:8001/secure-admin-panel/`
   - log in as `demo-admin`
   - inspect the backend structure and seeded demo data

---

## Demo Data

The container creates ready-to-test data automatically:

```text
Resident: Mina Karimi
PKZ: DEMO-1001
Room: Haus A / 101
Invite code: DEMO1001
```

It also creates sample inbox messages, appointment messages, content sections, notification examples, help/contact sample data, and staff dashboard access permissions.

The data is temporary and resets when the container is removed.

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

Follow logs live:

```bash
docker logs -f bewohner-demo
```

Stop and remove the demo container:

```bash
docker rm -f bewohner-demo
```

Start fresh:

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

- `8000` is the internal app port inside Docker
- `8001` is the local browser port on your machine

If port `8001` is busy, use another local port:

```bash
docker run -d --name bewohner-demo -p 8002:8000 ghcr.io/hosseinebi71/bewohner-app:latest
```

Then open:

```text
http://127.0.0.1:8002/
```

---

## Troubleshooting

### Container name is already in use

```bash
docker rm -f bewohner-demo
docker run -d --name bewohner-demo -p 8001:8000 ghcr.io/hosseinebi71/bewohner-app:latest
```

### Port is already allocated

Use another local port, for example `8002`:

```bash
docker run -d --name bewohner-demo -p 8002:8000 ghcr.io/hosseinebi71/bewohner-app:latest
```

### Image pull is slow

The first pull usually takes **1-5 minutes**, depending on your internet connection. Later pulls are usually faster because Docker uses cached layers.

Check the local image:

```bash
docker images ghcr.io/hosseinebi71/bewohner-app
```

### App does not open immediately

The first container startup usually takes **10-30 seconds** after the image has been downloaded. On slower machines, allow up to **1 minute**.

Check logs:

```bash
docker logs -f bewohner-demo
```

### Login does not work

Check the logs and use the exact credentials from the [Demo Accounts](#demo-accounts) section:

```bash
docker logs bewohner-demo
```

### Linux permission issue

Use `sudo` with the same commands:

```bash
sudo docker pull ghcr.io/hosseinebi71/bewohner-app:latest
sudo docker run -d --name bewohner-demo -p 8001:8000 ghcr.io/hosseinebi71/bewohner-app:latest
```

---

<div align="center">

**BewohnerApp Demo** · Admin · Staff · Resident · Docker-based review environment

</div>

<div align="center">

# BewohnerApp Demo

### Run a resident communication and staff management demo locally with Docker.

[![Docker](https://img.shields.io/badge/Requirement-Docker%20Desktop-2496ED?logo=docker&logoColor=white)](https://www.docker.com/products/docker-desktop/)
![Windows](https://img.shields.io/badge/Windows-Ready-0078D4?logo=windows&logoColor=white)
![macOS](https://img.shields.io/badge/macOS-Ready-000000?logo=apple&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-Ready-FCC624?logo=linux&logoColor=black)
![Docker Image](https://img.shields.io/badge/Docker%20Image-Ready-orange)

[Quick Start](#quick-start) · [Demo Accounts](#demo-accounts) · [What-to-test](#what-to-test) · [Troubleshooting](#troubleshooting)

</div>

---

## Overview

**BewohnerApp** is a resident communication and staff management platform for accommodation or residential environments.

The demo includes three ready-to-test roles:

- **Admin** for full administration
- **Staff / Mitarbeiter** for the staff dashboard and daily workflows
- **Resident / Bewohner** for the resident-facing app, inbox, appointments, and invite flow

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

## Demo Accounts

The demo creates three users automatically.

### Admin

```text
URL:      http://127.0.0.1:8001/secure-admin-panel/
Username: demo-admin
Password: DemoAdmin123!
```

### Staff / Mitarbeiter

Use this account to test the staff dashboard, residents, invite codes, and message creation.

```text
URL:      http://127.0.0.1:8001/login/
Username: demo-staff
Password: DemoAdmin123!
```

After login, open:

```text
http://127.0.0.1:8001/staff/
```

### Resident / Bewohner

Use this account to test the resident-facing app, inbox, appointments, confirmations, and public content.

```text
URL:      http://127.0.0.1:8001/resident/login/
Username: demo-resident
Password: DemoAdmin123!
```

Resident home:

```text
http://127.0.0.1:8001/
```

You can also inspect the generated demo information in the logs:

```bash
docker logs bewohner-demo
```

---

## Demo Data

The demo container creates ready-to-test data automatically:

```text
Resident: Mina Karimi
PKZ: DEMO-1001
Room: Haus A / 101
Invite code: DEMO1001
```

It also creates sample inbox messages, appointment messages, resident-facing content sections, and demo invite information.

---

## What to Test

### 1. Admin panel

Log in as `demo-admin` and inspect the full administration area.

### 2. Staff dashboard

Log in as `demo-staff` and open the staff dashboard.

From there, test the operational workflow:

- review residents
- create a message for a resident
- check invite codes
- inspect notification types and app sections
- review help/contact requests

### 3. Resident app

Log in as `demo-resident` and test the resident-facing side:

- open the resident home page
- check Posteingang / inbox
- check Termine / appointments
- open resident-facing content sections
- confirm important messages

### 4. Invite / activation flow

Use the demo invite code or the generated URLs from the logs to test resident onboarding:

```bash
docker logs bewohner-demo
```

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

If port `8001` is already busy, use another local port:

```bash
docker run -d --name bewohner-demo -p 8002:8000 ghcr.io/hosseinebi71/bewohner-app:latest
```

Then open the app on port `8002`.

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

### Login does not work

Check the logs:

```bash
docker logs bewohner-demo
```

The demo users and generated demo information are printed when the container starts.

---

<div align="center">

**BewohnerApp Demo** · Admin · Staff · Resident · Ready-to-test data

</div>

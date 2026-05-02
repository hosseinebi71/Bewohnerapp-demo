<div align="center">

# BewohnerApp Demo

### A guided Docker demo for resident communication, staff workflows, and administration.

[![Docker](https://img.shields.io/badge/Requirement-Docker%20Desktop-2496ED?logo=docker&logoColor=white)](https://www.docker.com/products/docker-desktop/)
![Windows](https://img.shields.io/badge/Windows-Ready-0078D4?logo=windows&logoColor=white)
![macOS](https://img.shields.io/badge/macOS-Ready-000000?logo=apple&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-Ready-FCC624?logo=linux&logoColor=black)
![Docker Image](https://img.shields.io/badge/Docker%20Image-GHCR-orange)

[Start the Demo](#start-the-demo) · [What Happens Behind the Scenes](#what-happens-behind-the-scenes) · [Demo Accounts](#demo-accounts) · [Guided Test Flow](#guided-test-flow) · [Troubleshooting](#troubleshooting)

</div>

---

## What this demo shows

**BewohnerApp** is a web platform for residential/accommodation environments where staff need to manage residents, send information, handle appointments, and provide a simple resident-facing app.

This public demo is designed for reviewers, employers, and technical evaluators. It lets you test the product without cloning the private source code and without setting up Python, Poetry, a database, or environment variables manually.

The demo includes three realistic roles:

| Role | What you can review |
| --- | --- |
| **Admin** | Full administration area and backend data structure |
| **Staff / Mitarbeiter** | Daily operational dashboard, residents, invite codes, messages, notifications, and content management |
| **Resident / Bewohner** | Resident-facing login, inbox, appointments, confirmations, and public content |

The demo runs from this published Docker image:

```text
ghcr.io/hosseinebi71/bewohner-app:latest
```

The source repository remains private. The image contains a runnable demo build with prepared demo data.

---

## Before you start

Install Docker and make sure it is running:

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) for Windows and macOS
- [Docker Engine](https://docs.docker.com/engine/install/) for Linux

Check that Docker is available:

```bash
docker --version
```

If Docker is installed correctly, you should see a version number.

---

## Start the demo

### 1. Download the demo image

```bash
docker pull ghcr.io/hosseinebi71/bewohner-app:latest
```

What this does:

- downloads the latest prebuilt BewohnerApp demo image from GitHub Container Registry
- avoids any local source-code setup
- reuses cached Docker layers if you have already pulled the image before

Why this step can take a little time:

- on the first run, Docker needs to download the full image
- the image contains the web application, Python runtime, production dependencies, static files, and startup scripts
- later pulls are usually faster because Docker only downloads changed layers

---

### 2. Start the container

```bash
docker run -d --name bewohner-demo -p 8001:8000 ghcr.io/hosseinebi71/bewohner-app:latest
```

What this does:

- creates a container named `bewohner-demo`
- starts the application in the background
- maps the app from the container port `8000` to your local browser port `8001`
- prepares the local demo environment automatically

After this command, open:

```text
http://127.0.0.1:8001/
```

The first startup may take a few seconds. During that time the container is preparing the demo database, users, sample residents, messages, permissions, and resident-facing content.

---

### 3. Follow the startup progress

```bash
docker logs -f bewohner-demo
```

What this shows:

- whether the app started successfully
- demo user creation
- generated demo data
- invite/demo information
- any startup errors, if something went wrong

You can stop following the logs with:

```text
CTRL + C
```

The container will continue running.

---

## What happens behind the scenes

When you run the demo container, Docker is not just opening a static page. The container starts a real web application with a prepared demo state.

In simplified form, this is what happens:

1. **The application runtime starts**
   - the container launches the BewohnerApp web server
   - static files are served from inside the image
   - the app listens internally on port `8000`

2. **The demo database is prepared**
   - the demo uses SQLite inside the container for fast local testing
   - the database is temporary and belongs only to this container
   - removing the container resets the demo state

3. **Demo accounts are created**
   - admin user
   - staff user
   - resident user

4. **Rich demo content is seeded**
   - sample resident profile
   - room and PKZ/demo information
   - invite code
   - inbox messages
   - appointment messages
   - app/content sections
   - notification/help/contact examples
   - staff dashboard permissions

5. **The reviewer can test three perspectives**
   - admin controls the system
   - staff handles daily operations
   - resident sees the simplified end-user experience

This is why the first run can feel slower than opening a simple website: the demo is preparing a realistic product state, not just rendering a landing page.

---

## Demo accounts

All demo users are created automatically when the container starts.

### Admin

Use this account to inspect the backend/admin side.

```text
URL:      http://127.0.0.1:8001/secure-admin-panel/
Username: demo-admin
Password: DemoAdmin123!
```

What to look for:

- data models and administration structure
- users, residents, messages, notifications, and content-related data
- how the product is organized from the system/admin perspective

---

### Staff / Mitarbeiter

Use this account to test the operational staff dashboard.

```text
URL:      http://127.0.0.1:8001/login/
Username: demo-staff
Password: DemoAdmin123!
```

After login, open:

```text
http://127.0.0.1:8001/staff/
```

What to look for:

- resident overview
- staff dashboard navigation
- resident communication workflow
- invite code/onboarding support
- messages and appointment-related content
- notification and help/contact examples

This role is important because it shows the daily workflow of the application, not just the technical admin panel.

---

### Resident / Bewohner

Use this account to test the resident-facing experience.

```text
URL:      http://127.0.0.1:8001/resident/login/
Username: demo-resident
Password: DemoAdmin123!
```

Resident home:

```text
http://127.0.0.1:8001/
```

What to look for:

- simple resident login flow
- inbox / Posteingang
- appointments / Termine
- important message confirmations
- resident-facing content sections
- how information is presented to non-technical users

---

## Guided test flow

For the best review experience, test the demo in this order.

### Step 1: Confirm the container is running

```bash
docker ps
```

You should see a container named `bewohner-demo`.

This confirms that Docker has started the app and mapped it to your local machine.

---

### Step 2: Open the resident app

Open:

```text
http://127.0.0.1:8001/
```

This shows the public/resident-facing entry point. Start here to understand what the end user sees.

Then log in as `demo-resident` and check inbox, appointments, and content sections.

---

### Step 3: Open the staff dashboard

Log in at:

```text
http://127.0.0.1:8001/login/
```

Then open:

```text
http://127.0.0.1:8001/staff/
```

This is where the operational value of the app becomes clearer: staff can work with resident records, communication, invite codes, messages, and prepared demo data.

---

### Step 4: Open the admin panel

Open:

```text
http://127.0.0.1:8001/secure-admin-panel/
```

Log in as `demo-admin`.

This lets you inspect the structure behind the product: users, residents, seeded data, and administration models.

---

### Step 5: Inspect generated demo information

```bash
docker logs bewohner-demo
```

Use this when you want to see what was created during startup, especially invite/demo information.

---

## Demo data

The demo container creates ready-to-test data automatically, including:

```text
Resident: Mina Karimi
PKZ: DEMO-1001
Room: Haus A / 101
Invite code: DEMO1001
```

It also creates:

- demo admin, staff, and resident users
- resident profile data
- sample inbox messages
- appointment messages
- app/content sections
- notification examples
- help/contact sample data
- staff dashboard access permissions

This means reviewers do not need to create data from scratch before understanding the app.

---

## Useful commands

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

Restart from a fresh container:

```bash
docker rm -f bewohner-demo
docker pull ghcr.io/hosseinebi71/bewohner-app:latest
docker run -d --name bewohner-demo -p 8001:8000 ghcr.io/hosseinebi71/bewohner-app:latest
```

---

## Port information

The start command uses:

```text
-p 8001:8000
```

That means:

- `8000` is the internal application port inside Docker
- `8001` is the local port you open in your browser

If port `8001` is already busy, use another local port, for example `8002`:

```bash
docker run -d --name bewohner-demo -p 8002:8000 ghcr.io/hosseinebi71/bewohner-app:latest
```

Then open:

```text
http://127.0.0.1:8002/
```

---

## Resetting the demo

The demo data lives inside the container. To reset everything, remove the container and start again:

```bash
docker rm -f bewohner-demo
docker run -d --name bewohner-demo -p 8001:8000 ghcr.io/hosseinebi71/bewohner-app:latest
```

This gives you a fresh demo state.

---

## Troubleshooting

### Docker says the container name is already in use

A previous demo container already exists. Remove it and start again:

```bash
docker rm -f bewohner-demo
docker run -d --name bewohner-demo -p 8001:8000 ghcr.io/hosseinebi71/bewohner-app:latest
```

---

### Docker says the port is already allocated

Another application is already using port `8001`. Use a different local port:

```bash
docker run -d --name bewohner-demo -p 8002:8000 ghcr.io/hosseinebi71/bewohner-app:latest
```

Then open:

```text
http://127.0.0.1:8002/
```

---

### The image pull is slow

This is usually normal on the first run. Docker is downloading the complete application image. Later pulls should be faster because Docker reuses cached layers.

You can confirm the image exists locally with:

```bash
docker images ghcr.io/hosseinebi71/bewohner-app
```

---

### The app does not open immediately

Check the logs:

```bash
docker logs -f bewohner-demo
```

The first startup can take a few seconds because the container prepares demo users, demo content, permissions, and sample resident data.

---

### Login does not work

First confirm that the app started correctly:

```bash
docker logs bewohner-demo
```

Then use the exact demo credentials from the [Demo accounts](#demo-accounts) section.

---

### Linux permission issue

On some Linux systems, Docker commands require `sudo`:

```bash
sudo docker pull ghcr.io/hosseinebi71/bewohner-app:latest
sudo docker run -d --name bewohner-demo -p 8001:8000 ghcr.io/hosseinebi71/bewohner-app:latest
```

---

## Notes for reviewers

- This is a Docker-based demo, not a source-code release.
- The source repository is private.
- The demo image is published through GitHub Container Registry.
- The app runs locally on your machine inside Docker.
- The demo uses SQLite inside the container for quick review.
- Demo data is temporary and resets when the container is removed.
- The `latest` tag points to the newest published demo image.

---

<div align="center">

**BewohnerApp Demo** · Admin · Staff · Resident · Docker-based review environment

</div>

# GearGuard: The Ultimate Maintenance Tracker

> **Odoo Hackathon Project** - A comprehensive maintenance management system for tracking company assets and managing maintenance requests.

## 1. Module Overview

**Objective:** Develop a maintenance management system that allows a company to track its assets (machines, vehicles, computers) and manage maintenance requests for those assets.

**Core Philosophy:** The module seamlessly connects Equipment (what is broken), Teams (who fix it), and Requests (the work to be done).

## 2. Key Functional Areas

### A. Equipment

The system serves as a central database for all company assets with robust tracking capabilities.

#### Equipment Tracking
Use search or group by features for tracking requests:
- **By Department:** (e.g., A CNC Machine belongs to the "Production" department)
- **By Employee:** (e.g., A Laptop belongs to "Person name")

#### Responsibility
- Each equipment must have a dedicated **Maintenance Team**
- A **technician** is assigned to it by default

#### Key Fields
- Equipment Name & Serial Number
- Purchase Date & Warranty Information
- Location: Where is this machine physically located?

### B. Maintenance Team

The system supports multiple specialized teams for different types of maintenance work.

#### Team Structure
- **Team Name:** Define teams (e.g., Mechanics, Electricians, IT Support)
- **Team Member Name:** Link specific users (Technicians) to these teams
- **Workflow Logic:** When a request is created for a specific team, only team members should pick it up

### C. Maintenance Request

This is the transactional part of the module that handles the lifecycle of a repair job.

#### Request Types
- **Corrective:** Unplanned repair (Breakdown)
- **Preventive:** Planned maintenance (Routine Checkup)

#### Key Fields
- **Subject:** What is wrong? (e.g., "Leaking Oil")
- **Equipment:** Which machine is affected?
- **Scheduled Date:** When should the work happen?
- **Duration:** How long did the repair take?

## 3. The Functional Workflow

### Flow 1: The Breakdown

1. **Request:** Any user can create a request
2. **Auto-Fill Logic:** When the user selects an Equipment (e.g., "Printer 01"):
   - The system automatically fetches the Equipment category and Maintenance Team from the equipment record and fills them into the request
3. **Request State:** The request starts in the **New** stage
4. **Assignment:** A manager or technician assigns themselves to the ticket
5. **Execution:** The stage moves to **In Progress**
6. **Completion:** The technician records the Hours Spent (Duration) and moves the stage to **Repaired**

### Flow 2: The Routine Checkup

1. **Scheduling:** A manager creates a request with the type **Preventive**
2. **Date Setting:** The user sets a Scheduled Date (e.g., Next Monday)
3. **Visibility:** This request appears on the **Calendar View** on the specific date so the technician knows they have a job to do

## 4. User Interface & Views Requirements

### 1. The Maintenance Kanban Board

The primary workspace for technicians.

- **Group By:** Stages (New | In Progress | Repaired | Scrap)
- **Drag & Drop:** Users can drag a card from "New" to "In Progress"
- **Visual Indicators:**
  - **Technician:** Show the avatar of the assigned user
  - **Status Color:** Display a red strip or text if the request is Overdue

### 2. The Calendar View

- Display all **Preventive** maintenance requests
- Allow users to click a date to schedule a new maintenance request

### 3. The Pivot/Graph Report (Optional/Advanced)

- A report showing the **Number of Requests per Team** or **per Equipment Category**

## 5. Required Automation & Smart Features

These features distinguish a basic form from a smart "Odoo-like" module.

### Smart Buttons

- **On the Equipment Form:** Add a button labeled **"Maintenance"**
  - **Function:** Clicking this button opens a list of all requests related only to that specific machine
  - **Badge:** The button displays the count of open requests

### Scrap Logic

- If a request is moved to the **Scrap** stage, the system should logically indicate that the equipment is no longer usable (e.g., log a note or set a flag)

## 6. Design Mockup

View the complete design mockup here: [Excalidraw Mockup](https://link.excalidraw.com/l/65VNwvy7c4X/5y5Qt87q1Qp)

## Technology Stack

- ⚡ [**FastAPI**](https://fastapi.tiangolo.com) for the Python backend API
  - 🧰 [SQLModel](https://sqlmodel.tiangolo.com) for the Python SQL database interactions (ORM)
  - 🔍 [Pydantic](https://docs.pydantic.dev) for data validation and settings management
  - 💾 [PostgreSQL](https://www.postgresql.org) as the SQL database
- 🚀 [React](https://react.dev) for the frontend
  - 💃 Using TypeScript, hooks, [Vite](https://vitejs.dev)
  - 🎨 [Tailwind CSS](https://tailwindcss.com) and [shadcn/ui](https://ui.shadcn.com) for the frontend components
  - 🤖 Automatically generated frontend client
  - 🧪 [Playwright](https://playwright.dev) for End-to-End testing
  - 🦇 Dark mode support
- 🐋 [Docker Compose](https://www.docker.com) for development and production
- 🔒 Secure password hashing by default
- 🔑 JWT (JSON Web Token) authentication
- 📫 Email based password recovery
- ✅ Tests with [Pytest](https://pytest.org)

## Getting Started

### Configure

Update configs in the `.env` files to customize your configurations.

Before deploying, make sure you change at least the values for:

- `SECRET_KEY`
- `FIRST_SUPERUSER_PASSWORD`
- `POSTGRES_PASSWORD`

### Generate Secret Keys

Generate secret keys by running:

```bash
python -c "import secrets; print(secrets.token_urlsafe(32))"
```

## Development

### Backend Development

Backend docs: [backend/README.md](./backend/README.md)

### Frontend Development

Frontend docs: [frontend/README.md](./frontend/README.md)

### Local Development with Docker Compose

This includes using Docker Compose, custom local domains, `.env` configurations, etc.

## License

The GearGuard project is licensed under the terms of the MIT license.

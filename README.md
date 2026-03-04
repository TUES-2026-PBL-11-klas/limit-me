<div align="center">

  <h1>Screen Time Tracker with Streak System</h1>
  
  <p>
    Android app that tracks daily screen time and motivates users with a streak system based on personal limits.
  </p>
</div>

<br />

## Table of Contents

* [About the Project](#about-the-project)
  * [Screenshots](#screenshots)
  * [Tech Stack](#tech-stack)
  * [Features](#features)
  * [Environment Variables](#environment-variables)
* [Getting Started](#getting-started)
  * [Prerequisites](#prerequisites)
  * [Installation](#installation)
  * [Run Locally](#run-locally)
  * [Run with Docker Compose](#run-with-docker-compose)
* [CI/CD](#cicd)
* [Usage](#usage)
* [Roadmap](#roadmap)
* [License](#license)
* [Contact](#contact)

## About the Project

Screen Time Tracker with Streak System is a mobile app for Android and iOS that:

- Tracks daily screen time (with focus on social media and games).
- Lets each user set a personal daily limit.
- Builds a streak when the user stays under the limit.
- Resets the streak when the user exceeds the limit.

The goal is to help users form healthier digital habits through clear feedback and simple rules.

### Screenshots

TBD – mobile UI screenshots will be added later.

### Tech Stack

- **Client**: React Native (Expo)
- **Server**: Java, Spring Boot
- **Database**: PostgreSQL (Supabase)
- **DevOps**: Docker, Docker Compose, GitHub Actions, Docker Hub

### Features

- **User accounts**: registration and login.
- **Daily reports**: automatic creation of a daily screen time report per user.
- **User limits**: configurable daily screen time limit per user.
- **Streak system**:
  - Streak increases when the user stays under the limit.
  - Streak resets when the user exceeds the limit.
- **Remote backend & anti-cheat friendly design** (validation on the server side).

### Environment Variables

Backend (Spring Boot) expects these environment variables:

- `SPRING_DATASOURCE_URL`
- `SPRING_DATASOURCE_USERNAME`
- `SPRING_DATASOURCE_PASSWORD`
- `SPRING_JPA_HIBERNATE_DDL_AUTO` (optional, e.g. `update`)

For Docker Compose, create a root `.env` file (this repo provides an example template):

```bash
cp .env.example .env
```

Then fill in the values in `.env`. Do not commit `.env`.

## Getting Started

### Prerequisites

- Node.js and npm (for the Expo/React Native frontend).
- Java 17+ and Maven (for the backend, if not using Docker).
- Docker & Docker Compose (to run the backend container locally).

### Installation

Clone the repository:

```bash
git clone <your-repo-url>
cd limit-me
```

Install frontend dependencies:

```bash
cd frontend
npm install
```

Backend uses Maven and has no extra manual install step beyond JDK and Maven.

### Run Locally

**Frontend (Expo app):**

```bash
cd frontend
npx expo start
```

**Backend (Spring Boot, without Docker):**

1. Make sure you have PostgreSQL connection credentials (e.g. Supabase).
2. Export the required env vars or configure them in your IDE run configuration:
   - `SPRING_DATASOURCE_URL`
   - `SPRING_DATASOURCE_USERNAME`
   - `SPRING_DATASOURCE_PASSWORD`
3. Run:

```bash
cd backend
./mvnw spring-boot:run
```

### Run with Docker Compose

To run the backend container locally (it connects to PostgreSQL using the credentials from your root `.env`):

```bash
docker compose up --build
```

This will start the Spring Boot backend on port `8080`.

If you want to run with a prebuilt image (for example from Docker Hub), you can switch the `backend` service from `build:` to `image:` in `docker-compose.yml`.

## CI/CD

This project includes a GitHub Actions workflow that automatically builds and publishes the backend Docker image to Docker Hub on every push to `main`:

- Workflow: `.github/workflows/dockerhub-backend.yml`
- Tags:
  - `latest`
  - `<commit-sha>`

Docker Hub credentials are stored as GitHub repository secrets:

- `DOCKERHUB_USERNAME`
- `DOCKERHUB_TOKEN` (Docker Hub personal access token)

## Usage

- Create an account from the mobile app.
- Set your daily screen time limit.
- Let the app collect your daily usage data and generate reports.
- Watch your streak grow when you stay under your limit; it resets if you exceed it.

## Roadmap

- [ ] Implement user registration and login endpoints.
- [ ] Implement daily report ingestion from the mobile client.
- [ ] Implement streak calculation logic on the backend.
- [ ] Add anti-cheat checks and validations.
- [ ] Polish UI/UX and add charts for statistics.

## License

This project is currently for educational use for the OOP, RS, DB, and VOT courses.

## Contact

Team **Kekscheta** – Screen Time Tracker project.


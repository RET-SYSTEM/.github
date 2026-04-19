# RET System

**RET System** is an AI-powered expense tracking application that removes the need for manual expense entry.

Instead of typing every purchase into an app, the user simply scans the QR code printed on a fiscal receipt. The system then retrieves the receipt data from Montenegrin government tax portal, extracts purchased items, categorizes them with AI, stores everything in a database, and displays the results in a mobile app through statistics, charts, and AI-generated reports.

---

## Demo
🎥 **Demo Video**  
![Add YouTube link here](https://www.youtube.com/shorts/XydU75vXJJo)

---

### Architecture Diagram
![System architecture diagram](https://i.imgur.com/iyYpjDc.png)

---

## What Problem Does It Solve?

Most expense tracking apps still depend on manual input, which makes them frustrating to use consistently.

RET System automates the full process:

- scan a receipt QR code
- retrieve receipt data from the tax portal
- categorize purchased items with AI
- store the data in a database
- visualize spending in a mobile app
- generate AI-powered spending reports

The goal of the project is simple: make personal expense tracking fast, automatic, and actually useful.

---

## Main Features

- QR scanning of fiscal receipts through the mobile app
- automatic retrieval of receipt data
- AI-based item categorization using custom user-defined categories
- receipt history and monthly spending overview
- spending statistics and category-based charts
- AI-generated spending reports with monthly insights
- anomaly detection in spending patterns
- personalized financial recommendations
- duplicate receipt protection

---

## How It Works

1. **The user scans a receipt QR code** using the mobile app.  
2. The **backend** checks whether the receipt has already been imported.  
3. If the receipt is new, the request is forwarded to the **Python worker**.  
4. The worker retrieves receipt data from the montenegro tax portal and sends the purchased items to the AI model for categorization.  
5. The processed data is returned to the backend and stored in the database.  
6. The mobile app displays the updated expenses, categories, and AI reports.  

---

## Architecture

RET System is built as a distributed system with three separate repositories:

### Mobile App — [`ret-mobile`](https://github.com/RET-SYSTEM/ret-mobile)
**Tech:** React Native, Expo, TypeScript

The mobile app is used for:
- scanning receipt QR codes
- viewing expenses and receipts
- managing categories
- displaying charts and AI reports

### Backend API — [`ret-backend`](https://github.com/RET-SYSTEM/ret-backend)
**Tech:** Java, Spring Boot, PostgreSQL, Hibernate

The backend is responsible for:
- handling API requests
- validating and storing data
- managing categories and reports
- preventing duplicate receipt imports
- communicating with the Python worker

### AI / Worker Service — [`ret-worker`](https://github.com/RET-SYSTEM/ret-worker)
**Tech:** Python, FastAPI

The worker service is responsible for:
- retrieving receipt data from the tax portal
- processing receipt items
- AI-based product categorization
- generating AI spending reports

---

## AI Reports

In addition to automatic product categorization, the system also uses AI to analyze spending history.

AI reports can include:

- month-to-month spending comparisons
- category growth or decline detection
- anomaly detection for unusual expenses
- personalized recommendations based on spending habits

Reports are stored in the database and can be reopened later inside the app.

---

## Tech Stack

### Mobile
- React Native
- Expo
- TypeScript

### Backend
- Java
- Spring Boot
- PostgreSQL
- Hibernate / JPA

### Worker / AI
- Python
- FastAPI
- AI model integration

### DevOps / Deployment
- Docker
- VPS hosting
- CI/CD pipeline
- GitHub Actions

---

## Deployment

The system is hosted on a **VPS** using **Docker**, with a **CI/CD pipeline** configured to automatically deploy new updates after changes are pushed to GitHub.

---

## Why This Project Matters

RET System is more than a simple CRUD application.

It demonstrates:

- mobile app development
- backend development and database design
- Python service architecture
- AI integration in a real product workflow
- ingestion of data from external sources
- deployment and CI/CD automation
- system design across multiple connected services

---

## Project Status

RET System is an active portfolio project that is still evolving.

Planned improvements include:
- better report visualizations
- more advanced spending analysis
- improved receipt item normalization
- smarter anomaly detection
- stronger comparison logic in AI reports

---

## Repositories

- **Mobile App:** [`ret-mobile`](https://github.com/RET-SYSTEM/ret-mobile)
- **Backend API:** [`ret-backend`](https://github.com/RET-SYSTEM/ret-backend)
- **Worker Service:** [`ret-worker`](https://github.com/RET-SYSTEM/ret-worker)

---

## Author

Built as a full-stack portfolio project focused on automation, AI integration, and practical personal finance tooling.

# RET System

**RET System** is an AI-powered expense tracking application that removes the need for manual expense entry.

Instead of typing every purchase into an app, the user scans the QR code printed on a fiscal receipt. The system then retrieves the receipt data, extracts the purchased items, categorizes them with AI, stores everything in a database, and displays the results in a mobile dashboard.

The goal of the project is simple: make personal expense tracking automatic, fast, and actually usable.

🎥 **Demo Video (Coming Soon)**  
👉 *[Add YouTube link here]*

---

## Overview

Most expense tracking apps still depend on manual input, which makes them annoying to use consistently.

RET System solves that problem by automating the full flow:

- scan a receipt QR code
- retrieve receipt data
- categorize items with AI
- store the result
- visualize spending
- generate AI-powered spending reports

This makes the app feel less like a spreadsheet and more like a smart financial assistant.

---

## Core Idea

In Montenegro, store receipts include a QR code that links to a government tax portal containing receipt verification data.

RET System uses that QR code as the entry point for the entire process.

### How it works

1. **Scan**  
   The user scans the QR code on a receipt using the mobile app.

2. **Retrieve**  
   The backend sends the extracted receipt reference to a Python worker, which fetches the receipt data from the tax portal.

3. **Categorize with AI**  
   The purchased items are sent to an AI model, which categorizes them into user-defined spending categories such as:
   - Groceries
   - Drinks
   - Fast Food
   - Clothing

4. **Store**  
   The processed receipt is saved in the database together with all items and categories.

5. **Visualize**  
   The mobile app displays spending history, category totals, and charts.

6. **Analyze with AI**  
   Users can generate AI spending reports for selected months and receive summaries, anomaly detection, and personalized financial tips.

---

## Main Features

### Automated Receipt Scanning
- scan QR codes directly from the mobile app
- no manual receipt entry
- duplicate receipt protection

### AI-Based Item Categorization
- purchased items are categorized automatically
- categories are customizable
- reduces repetitive manual organization

### Expense Dashboard
- monthly totals
- category breakdown
- receipt history
- interactive charts and summaries

### AI Spending Reports
Users can generate saved AI reports based on selected months.

Each report can include:

- **Monthly comparison**
  - “You spent 18% more than last month”
  - “The biggest increase was in Food”

- **Anomaly detection**
  - unusually large purchases
  - spikes in a category
  - suspiciously similar receipts
  - unusual spending patterns

- **Personalized tips**
  - suggestions based on actual spending behavior
  - category-based optimization insights
  - habit and pattern observations

Reports are stored in the database so users can reopen older analyses later.

---

## Architecture

RET System is built as a small distributed system with three separate codebases.

### 1. Mobile App — [`ret-mobile`](https://github.com/RET-SYSTEM/ret-mobile)
**Tech:** React Native, Expo, TypeScript

The mobile app is the main user interface. It allows users to:

- scan receipts
- view spending data
- manage categories
- browse receipt history
- generate and read AI reports

---

### 2. Backend API — [`ret-backend`](https://github.com/RET-SYSTEM/ret-backend)
**Tech:** Java 17, Spring Boot 3, PostgreSQL, Hibernate

The backend is responsible for:

- handling mobile API requests
- validating and storing receipt data
- managing categories and reports
- preventing duplicate receipt imports
- aggregating spending data for AI analysis
- coordinating communication with the Python worker

---

### 3. AI / Scraping Worker — [`ret-worker`](https://github.com/RET-SYSTEM/ret-worker)
**Tech:** Python 3.12, FastAPI, Mistral (`open-mistral-nemo`)

The worker handles tasks that are better separated from the core backend:

- retrieving receipt data from the tax portal
- transforming raw receipt content
- categorizing receipt items with AI
- generating structured AI spending reports

---

## End-to-End Receipt Flow

When a user scans a receipt QR code, this is the full process:

1. The **mobile app** reads the QR URL from the receipt.
2. The **Spring Boot backend** receives the request and checks whether the receipt already exists.
3. If the receipt is new, the backend forwards the relevant data to the **Python worker**.
4. The **Python worker** retrieves the raw receipt content from the tax portal.
5. The worker sends the purchased items and available categories to the **Mistral AI model**.
6. The AI returns categorized items.
7. The **backend** maps the result into Java entities and saves it in PostgreSQL.
8. The **mobile app** refreshes and displays the new expense data.

---

## End-to-End AI Report Flow

When a user generates an AI spending report:

1. The user opens the **Reports** tab in the mobile app.
2. The user selects one or more months for analysis.
3. The **mobile app** sends the selected months to the **Spring Boot backend**.
4. The **backend** retrieves all relevant receipts and calculates structured spending statistics.
5. The backend sends those statistics to the **Python worker**.
6. The worker builds a prompt and sends the data to the **Mistral AI model**.
7. The AI returns a structured report containing:
   - title
   - summary
   - anomalies
   - tips
8. The **backend** stores the generated report in the database.
9. The **mobile app** displays the new report and allows it to be reopened later.

---

## Why This Project Is Interesting

RET System is more than a CRUD app.

It demonstrates:

- mobile development with React Native
- backend development with Spring Boot
- Python microservices with FastAPI
- PostgreSQL data modeling
- AI integration in a real product flow
- automated data ingestion from external sources
- end-to-end system design across multiple services

It combines real-world automation, AI-assisted classification, analytics, and a clean mobile experience in one project.

---

## Tech Stack

### Mobile
- React Native
- Expo
- TypeScript

### Backend
- Java 17
- Spring Boot 3
- PostgreSQL
- Hibernate / JPA

### Worker / AI
- Python 3.12
- FastAPI
- Mistral AI (`open-mistral-nemo`)

---

## Project Status

RET System is an actively evolving portfolio project focused on:

- automated receipt ingestion
- AI categorization
- spending visualization
- AI-generated financial insights

Planned improvements may include:
- better receipt analytics
- richer report visualizations
- improved item normalization
- smarter anomaly detection
- stronger report comparison logic

---

## Repositories

- **Mobile App:** [`ret-mobile`](https://github.com/RET-SYSTEM/ret-mobile)
- **Backend API:** [`ret-backend`](https://github.com/RET-SYSTEM/ret-backend)
- **Worker Service:** [`ret-worker`](https://github.com/RET-SYSTEM/ret-worker)

---

## Author

Built and designed by **RET-SYSTEM** as a full-stack portfolio project focused on automation, AI integration, and practical personal finance tooling.

# Montenegro Expense Tracker (RET System)
**Role:** Full Stack Software Engineer / Architect  
**Architecture:** Microservices (Java Spring Boot, Python FastAPI, React Native)  
**Deployment:** CI/CD via GitHub Actions, Docker Compose, Self-hosted Linux VPS  

---

## 🚀 Overview

The **RET System (Montenegro Expense Tracker)** is an end-to-end, automated AI expense-tracking platform. I architected and built this system from the ground up to solve a real-world problem: the tedious nature of manual expense tracking. 

In Montenegro, fiscal receipts contain QR codes linking to a government portal. The RET System allows users to simply snap a picture of that QR code via a mobile app, which then automatically scrapes the government database, uses an LLM to smartly categorize the purchased items using a custom taxonomy, and visualizes the user's spending habits on a dashboard.

---

## 🧠 Technical Achievements & Problem Solving

This project demonstrates my ability to design, build, and deploy a complete microservice architecture, spanning frontend UI/UX, backend data integrity, AI integration, and DevOps.

### 1. Reverse-Engineering & Web Scraping (Python / FastAPI)
The Montenegrin Tax API is protected heavily by an F5 BIG-IP Web Application Firewall (WAF) that aggressively blocks standard HTTP clients. 
*   **The Solution:** I built a dedicated Python FastAPI microservice utilizing `curl_cffi` to mimic Chrome TLS/JA3 fingerprints. This successfully bypassed the firewall, completed the complex WAF cookie-handshakes, and extracted the raw, heavily-nested JSON receipt data.

### 2. Dynamic AI Integration (Groq / Llama 3)
Receipt items are returned in the Montenegrin language. Hardcoding category mapping was impossible due to the infinite variety of potential items.
*   **The Solution:** I integrated the **Groq API (Llama-3.3-70b)** to process the scraped items. Instead of giving the AI hardcoded categories, the Spring Boot backend dynamically feeds the AI the user's *custom* database categories. The AI evaluates the items entirely in-context and returns a strict, mapable JSON payload.

### 3. Core Backend Infrastructure (Java / Spring Boot 3)
The system required a robust, transactional core to manage the database, handle mobile API requests, and coordinate with the Python AI worker.
*   **The Solution:** I developed a RESTful backend using **Java 21 and Spring Boot 3**, backed by a **PostgreSQL** database and Hibernate ORM. It exposes full CRUD capabilities, applies cascade-deletes for data integrity, and manages internal/external API Key security via custom Servlet Context Filters. 

### 4. Cross-Platform Mobile Development (React Native / Expo)
The user needed a seamless, native way to interact with the system on a daily basis.
*   **The Solution:** I built an Android mobile app using **React Native and Expo**. It features native Camera API integration for rapid QR processing, aggressive state management for instant UI updates during CRUD operations, and an interactive charting dashboard. The app runs completely standalone and connects directly to the self-hosted backend.

### 5. DevOps, Docker, & CI/CD Pipelines
Code sitting on a local laptop isn't a product. It needed to be highly available.
*   **The Solution:** I containerized the entire architecture using **Docker** and successfully deployed it to a remote Linux VPS using **Docker Compose**. 
Furthermore, I engineered a CI/CD pipeline using **GitHub Actions**. Whenever a new commit is pushed to the repository main branch, the pipeline automatically tests the build, signals the VPS via webhook, pulls the latest code, and conducts a zero-downtime rolling restart of the Docker containers.

---

## 🛠️ The Tech Stack

**Frontend (Mobile App)**
*   React Native, Expo (SDK 55), TypeScript
*   Axios, Expo Camera, Expo Router

**Backend Core (REST API)**
*   Java 21, Spring Boot 3
*   Spring Data JPA (Hibernate), PostgreSQL
*   Spring Web (RestClient)

**AI Worker (Scraping/Processing)**
*   Python 3.12, FastAPI, Uvicorn
*   `curl_cffi` (WAF Bypass), Groq SDK (Llama 3)

**DevOps & Deployment**
*   Linux VPS Hosting, Docker, Docker Compose
*   GitHub Actions CI/CD Pipeline
*   EAS (Expo Application Services) for automated `.apk` generation

---

## 🎯 Impact
By combining reverse-engineering, intelligent AI categorization, robust Java data persistence, and automated DevOps, I delivered a seamless, production-grade application that completely automates personal financial analytics.

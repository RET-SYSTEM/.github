# (RET) System

Welcome to the **RET System** organization. This project is NOT LIKE other EXPENSE TRACKING APPLICATIONS, this is a complete, automated end-to-end AI expense-tracking platform. I architected and built this microservice system from the ground up to solve a real-world problem: the tedious nature of manual personal finance tracking.

🎥 **Demo Video (Coming Soon)**
👉 *\[PLACE YOUR YOUTUBE LINK HERE\]*

---

## 🌟 The Problem & The Solution

**The Problem:**
In Montenegro, every store receipt contains a QR code that links to a government tax portal confirming the receipt. However, keeping track of how much you spend every month and on exactly what items is incredibly tedious if you have to manually enter everything into an app or a spreadsheet.

**The Solution:**
The RET System is an automated expense-tracking mobile app. 

1. **Scan:** You scan the QR code on your receipt using the mobile app's camera.
2. **Scrape:** The system instantly scrapes the raw receipt data directly from the Montenegrin government's heavily protected database.
3. **Analyze:** Artificial Intelligence (Groq Llama-3) reads every individual item (e.g., "Milk", "Bread", "T-Shirt") and automatically categorizes them based on your own custom categories that you can create inside mobile app (e.g., *Groceries*, *Clothing*).
4. **Visualize:** The app calculates everything and builds beautiful, interactive charts, showing you exactly how much you spent this month on each category.

---

## 💻 Technical Architecture & Repositories

The RET System is not a monolith; it is a distributed microservice architecture consisting of three distinct codebases working together seamlessly.

### [1. Mobile Frontend (`ret-mobile`)](https://github.com/your-org/ret-mobile)
*   **Built With:** React Native, Expo (SDK 55), TypeScript.
*   **Role:** The cross-platform user interface. It acts as a QR code scanner and interactive dashboard. It uses aggressive state-management for instant UI updates during CRUD operations.

### [2. Core Backend (`ret-backend`)](https://github.com/your-org/ret-backend)
*   **Built With:** Java 21, Spring Boot 3, PostgreSQL, Hibernate ORM.
*   **Role:** The brain and database manager. It handles all RESTful CRUD operations, applies cascade-deletes for data integrity, and coordinates the transaction flow between the mobile app and the AI worker.

### [3. AI & Scraping Worker (`ret-worker`)](https://github.com/your-org/ret-worker)
*   **Built With:** Python 3.12, FastAPI, Groq SDK, `curl_cffi`.
*   **Role:** The heavy lifter. It physically bypasses the government's Web Application Firewall (WAF) to extract receipt JSON, and then utilizes the Llama-3-70b LLM to process and format the scraped data.

---

## 🧠 Technical Achievements & Problem Solving

This system demonstrates my ability to design, build, and deploy a complete microservice architecture spanning frontend UI, backend data integrity, AI integration, and DevOps.

*   **Reverse-Engineering (WAF Bypass):** The Montenegrin Tax API is protected heavily by an F5 BIG-IP Firewall that aggressively blocks standard HTTP clients. I built the Python microservice utilizing `curl_cffi` to mimic Chrome TLS/JA3 fingerprints. This successfully bypassed the firewall, completed the complex cookie-handshakes, and extracted the raw JSON.
*   **Dynamic AI Integration:** Hardcoding category mapping was impossible due to the infinite variety of potential items in the Montenegrin language. I integrated the **Groq API (Llama-3)**. Instead of giving the AI hardcoded categories, the Spring Boot backend *dynamically* feeds the AI the user's custom database categories, effectively acting as an intelligent formatting engine.
*   **DevOps, Docker, & CI/CD Pipelines:** I containerized the entire architecture using **Docker** and successfully self-hosted it on a remote Linux VPS using **Docker Compose**. I engineered a CI/CD pipeline using **GitHub Actions**. Whenever a new commit is pushed to the main branch, the pipeline automatically pulls the latest code to the VPS and conducts a zero-downtime rolling restart of the Docker containers.
*   **Security Lock-down:** The database and internal APIs are strictly locked down. All communication from the Mobile App to Spring Boot demands a custom `MOBILE_API_KEY` validated by a Servlet Filter. Furthermore, the Python Worker is not publicly accessible; it requires an `INTERNAL_API_KEY` so only the Spring Boot backend can utilize its scraping and AI generation capabilities.

---

## 🔄 The Scanning Flow (End-to-End)

When a user points their phone camera at a receipt QR code, here is exactly what happens under the hood:

1. **Mobile App** reads the URL: `https://mapr.tax.gov.me/ic/#?iic=XYZ...` and sends a `POST` request to the **Spring Boot Backend**.
2. **Spring Boot** extracts the tracking numbers and checks PostgreSQL to see if the receipt was already cached. If not, it forwards the request to the **Python Worker**.
3. **Python Worker** bypasses the government firewall, downloads the raw receipt data securely, and strips out the headers.
4. **Python Worker** feeds the list of purchased items to the **Groq AI model**. Spring Boot dynamically provides the AI with the *custom categories straight from the database*. 
5. **Python Worker** returns the intelligently categorized receipt back to **Spring Boot**.
6. **Spring Boot** maps the JSON into Java Entities, saves everything to PostgreSQL, and returns the final data.
7. **Mobile App** refreshes the dashboard and the user sees their updated spending analytics.

---

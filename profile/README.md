# (RET) System

Welcome to the **RET System**. This project is NOT LIKE other EXPENSE TRACKING APPLICATIONS, this is a complete, automated end-to-end AI expense-tracking platform, without the need for any manual entry of your spendings. I architected and built this system from the ground up to solve a real-world problem: the tedious nature of manual personal finance tracking.

🎥 **Demo Video (Coming Soon)**
👉 *\[PLACE YOUR YOUTUBE LINK HERE\]*

---

## 🌟 The Problem & The Solution

**The Problem:**
Keeping track of how much you spend every month and on exactly what items is incredibly tedious if you have to manually enter everything into an app or a spreadsheet.

**The Solution:**
In Montenegro, every store receipt contains a QR code that links to a government tax portal confirming the receipt, showing total price and items purchased. The RET System utilizes that data and automatically enters the data into the app once you scan the receipt QR code. 

1. **Scan:** You scan the QR code on your receipt using the mobile app's camera.
2. **Scrape:** The system instantly scrapes the raw receipt data directly from the tax portal.
3. **Analyze:** Artificial Intelligence (open-mistral-nemo) reads every individual item (e.g., "Milk", "Bread", "T-Shirt") and automatically categorizes them based on your own custom categories that you can create inside mobile app (e.g., *Groceries*, *Clothing*).
4. **Visualize:** The app calculates everything and builds beautiful, interactive charts, showing you exactly how much you spent.

---

## 💻 Technical Architecture & Repositories

The RET System is not a monolith; it is a distributed microservice architecture consisting of three distinct codebases working together seamlessly.

### [1. Mobile Frontend (`ret-mobile`)](https://github.com/your-org/ret-mobile)
*   **Built With:** React Native, Expo (SDK 55), TypeScript.
*   **Role:** The cross-platform user interface. It acts as a QR code scanner and interactive dashboard. It uses aggressive state-management for instant UI updates during CRUD operations.

### [2. Core Backend (`ret-backend`)](https://github.com/your-org/ret-backend)
*   **Built With:** Java 17, Spring Boot 3, PostgreSQL, Hibernate ORM.
*   **Role:** The brain and database manager. It handles all RESTful CRUD operations, applies cascade-deletes for data integrity, and coordinates the transaction flow between the mobile app and the AI worker.

### [3. AI & Scraping Worker (`ret-worker`)](https://github.com/your-org/ret-worker)
*   **Built With:** Python 3.12, FastAPI
*   **Role:** The heavy lifter. It extracts receipt JSON from the tax portal, and then utilizes the Mistral's open-mistral-nemo LLM to process and format the scraped data.

---

## 🔄 The Scanning Flow (End-to-End)

When a user points their phone camera at a receipt QR code, here is exactly what happens under the hood:

1. **Mobile App** reads the URL: `https://mapr.tax.gov.me/ic/#?iic=XYZ...` and sends a `POST` request to the **Spring Boot Backend**.
2. **Spring Boot** extracts the tracking numbers and checks database to see if the receipt was already scanned. If not, it forwards the request to the **Python Worker**.
3. **Python Worker** scrapes the raw receipt data from tax portal, feeds the list of purchased items to the **Mistral's AI model**. Spring Boot dynamically provides the AI with the *custom categories straight from the database,* making customizable categories possible. 
5. **Python Worker** returns the intelligently categorized receipt back to **Spring Boot**.
6. **Spring Boot** maps the JSON into Java Entities, saves everything to PostgreSQL database, and returns the final data.
7. **Mobile App** refreshes the dashboard and the user sees their updated spending analytics.

---

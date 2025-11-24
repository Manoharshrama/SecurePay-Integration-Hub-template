# Software Requirements Specification
## for SecurePay Integration Hub
### using Design Patterns

**University:** Lewis University

---

### 3. Proposal Last Updated
**Date:** November 24, 2025

---

### 1. Application Overview
**End User Perspective**

The **SecurePay Integration Hub** is designed to solve the fragmentation problem e-commerce merchants face when dealing with multiple payment providers. Currently, switching between providers (e.g., from Stripe to PayPal) requires significant manual coding and downtime.

This application provides a unified "Write Once, Pay Anywhere" dashboard. Merchants can log in to a centralized web interface to manage their payment configurations without needing technical intervention. The system allows the user to:

* **Visualize Transactions:** View a real-time table of all payments processed, regardless of which banking provider handled them.
* **Dynamic Routing:** Toggle between different payment providers instantly to take advantage of lower fees or better uptime.
* **Centralized Security:** Manage API keys and secrets in one secure location rather than scattering them across multiple codebase files.

The goal is to automate the routing of payments and standardize the reporting process, saving time and reducing errors associated with manual payment integration.

---

### 2. Technology Overview
This section outlines the specific technologies chosen to implement the modular architecture and ensure the system is scalable and maintainable.

#### Languages
* **Backend:** Java 21 (LTS) – Selected for its strong typing and enterprise-level security features.
* **Frontend:** JavaScript (ES6+) – Used within the React framework.

#### Libraries & Frameworks
* **Spring Boot:** The primary backend framework used for dependency injection, REST API creation, and security management.
* **React.js:** A component-based frontend library used to build the responsive Merchant Dashboard.
* **Hibernate / JPA:** Used for Object-Relational Mapping (ORM) to interact with the database.
* **Lombok:** To reduce boilerplate code in Java models.

#### Platforms
* **Database:** PostgreSQL – A relational database chosen for its ACID compliance and robust handling of financial transaction logs.
* **Containerization:** Docker – Used to containerize the application for consistent deployment across different environments.

#### Hosting
* **Local:** Runs on a local server/VM for development and testing.
* **Cloud:** Deployable to AWS (Amazon Web Services) or Azure via Docker containers for production scalability.

---

### 4. Feature List (Prioritized)
This list represents the prioritized functional requirements that will be delivered within the allowed timeframe.

#### Priority 1: Core Payment Processing (Must Have)
* **Unified Payment API:** A single internal REST endpoint that accepts payment details and routes them to external providers.
* **Adapter Implementation:** Functional integration with **Stripe** and **PayPal** using the Adapter Design Pattern to standardize their different APIs.
* **Transaction Logging:** Automatic recording of every transaction attempt (success/fail) into the PostgreSQL database.

#### Priority 2: User Management (High Priority)
* **Secure Authentication:** User registration and login functionality using JWT (JSON Web Tokens) and Spring Security.
* **Merchant Dashboard:** A React-based UI allowing users to view their transaction history table.

#### Priority 3: Routing Configuration (Medium Priority)
* **Dynamic Switching:** A UI toggle allowing the merchant to select the "Active" gateway (e.g., switch all traffic from Stripe to PayPal).
* **Fee Calculation:** A basic Strategy implementation that calculates estimated transaction fees before processing.

#### Priority 4: Reporting (Low Priority)
* **Export Functionality:** Ability to download transaction logs as a PDF receipt using the iText library.

---

### 5. Future Feature List
This section outlines non-prioritized features that would be implemented if time constraints were lifted. These features extend the system into a commercial-grade SaaS product.

* **Cryptocurrency Support:** Integration with blockchain wallets (e.g., Coinbase API) to allow merchants to accept Bitcoin and Ethereum.
* **AI Fraud Detection:** Integration with external AI services to analyze transaction velocity and flag high-risk payments before sending them to the bank.
* **Webhooks & Notifications:** An automated notification system to alert merchants via email or SMS when a transaction fails or a refund is requested.
* **Recurring Billing Scheduler:** Automated cron jobs to handle subscription-based payments without manual triggers.
* **Cloud Storage Integration:** Automatically backing up monthly transaction reports to Google Drive or AWS S3.

---

### 6. Basic Technical Features
This section details the technical implementations that demonstrate the software engineering principles and design patterns learned in the class.

#### 1. Design Patterns (Object-Oriented Design)
* **Adapter Pattern:** Used to bridge the gap between the internal `PaymentRequest` interface and external APIs (Stripe/PayPal). This ensures that switching providers does not break the core application logic.
* **Strategy Pattern:** Used to implement different fee calculation algorithms (e.g., `FlatRateStrategy` vs. `PercentageStrategy`). This allows the system to switch logic at runtime based on the selected provider.
* **Factory Pattern:** Used to dynamically instantiate the correct payment provider object based on the merchant's configuration settings.

#### 2. Architectural Pattern (MVC)
* The application follows the **Model-View-Controller (MVC)** architecture. This strictly separates the business logic (Java Services), the data layer (PostgreSQL entities), and the presentation layer (React UI), ensuring maintainability and testability.

#### 3. RESTful API Design
* The backend exposes stateless **REST APIs** for communication between the frontend and backend. This demonstrates understanding of HTTP verbs (GET, POST), status codes, and JSON data structures.

#### 4. Security Implementation
* Implementation of **JWT (JSON Web Tokens)** for stateless session management.
* Usage of **BCrypt** hashing algorithms for password storage, adhering to security standards discussed in class.

#### 5. Database Normalization
* The database schema is designed up to **3rd Normal Form (3NF)** to reduce data redundancy and ensure integrity between Merchants, Transactions, and Gateway Configurations.

# 🏦  Banking Database System

[![SQL Server](https://img.shields.io/badge/Database-MSSQL%20Server-red?style=flat&logo=microsoftsqlserver)](https://www.microsoft.com/en-us/sql-server/)
[![PostgreSQL](https://img.shields.io/badge/Database-PostgreSQL-blue?style=flat&logo=postgresql)](https://www.postgresql.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A production-ready, highly normalized relational database architecture designed for modern retail banking systems. This project models core banking operations including **Customer Management**, **Branch Operations**, **Multi-Account Handling**, and **Financial Transaction Processing** with strict data integrity enforced.

---

## 📌 Features & Business Rules

- **Branch Operations:** Tracks physical bank branches and their geographical locations.
- **Customer Profiling:** Stores validated customer records with unique contact constraints.
- **Account Management:** Supports **Savings** and **Current** accounts with balance validation (`CHECK Balance >= 0`).
- **Transaction Logging:** Records real-time financial activities (**Deposit**, **Withdrawal**, **Transfer**) with strict audit timestamps.
- **Data Integrity:** Enforces relational logic using `PRIMARY KEY`, `FOREIGN KEY` (with `ON DELETE CASCADE` where applicable), `UNIQUE`, and `CHECK` constraints.

---

## 📐 Entity-Relationship Diagram (ERD) Schema

```text
  +------------------+         +------------------+
  |     BRANCHES     |         |    CUSTOMERS     |
  +------------------+         +------------------+
  | Branch_id (PK)   |<---+   +| Customer_id (PK) |
  | Branch_Name      |    |   | | Full_Name        |
  | Location         |    |   | | Phone_Number    |
  +------------------+    |   | +------------------+
                          |   |
                          |   |
                  +-------+---+------+
                  |     ACCOUNTS     |
                  +------------------+
                  | Account_id (PK)  |
                  | Account_Number   |
                  | Customer_id (FK) |
                  | Branch_id (FK)   |
                  | Balance          |
                  +--------+---------+
                           |
                           | 1:N
                  +--------v---------+
                  |   TRANSACTIONS   |
                  +------------------+
                  | Transaction_id   |
                  | Account_id (FK)  |
                  | Amount           |
                  | Transaction_Type |
                  +------------------+


🛠️ Tech Stack & Compatibility
Primary RDBMS: Microsoft SQL Server (T-SQL)

Cloud Database: PostgreSQL (Compatible with Supabase)

Tools Used: SQL Server Management Studio (SSMS), Git & GitHub

💻 Sample Production Queries
1. Account Summary Report (CUSTOMER JOIN)
Fetches all registered customers alongside their account details and active balances:

SQL
SELECT 
    C.Full_Name,
    A.Account_Number,
    A.Account_Type,
    A.Balance
FROM Customers C
INNER JOIN Accounts A ON C.Customer_id = A.Customer_id;
2. High-Value Account Filter
Retrieves accounts holding balances greater than $1,000 for VIP auditing:

SQL
SELECT 
    Account_id, 
    Balance 
FROM Accounts 
WHERE Balance > 1000;
🚀 Getting Started / Installation
Clone the Repository:

Bash
git clone [https://github.com/YOUR_USERNAME/core-banking-database-system.git](https://github.com/YOUR_USERNAME/core-banking-database-system.git)
Deploy Schema:

Open your favorite SQL Client (SSMS / Supabase / DBeaver).

Execute the setup script (database_setup.sql).

📜 License
This project is licensed under the MIT License - feel free to use, modify, and distribute for educational or enterprise purposes.




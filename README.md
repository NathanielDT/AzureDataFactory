# Azure Data Factory – JSONPlaceholder to ADLS Pipeline

## 📌 Overview

This project demonstrates a simple data ingestion pipeline built using Azure Data Factory (ADF). The pipeline extracts user data from a public REST API and stores it as a CSV file in Azure Data Lake Storage (ADLS).

The goal of this project is to showcase:

* API data ingestion using ADF
* Data movement using Copy Activity
* Cloud-native data storage in ADLS

---

## 🏗️ Architecture

**Source:** JSONPlaceholder API
**Ingestion Tool:** Azure Data Factory (ADF)
**Destination:** Azure Data Lake Storage Gen2 (ADLS)
**Output Format:** CSV

**Flow:**

1. ADF pipeline triggers a Copy Activity
2. Data is fetched from the JSONPlaceholder `/users` endpoint
3. JSON response is mapped and flattened (if required)
4. Data is written to ADLS as a CSV file

---

## 🔧 Components

### 1. Linked Services

* **REST Linked Service**

  * Connects to JSONPlaceholder API
* **Azure Data Lake Storage Linked Service**

  * Authenticated via Managed Identity / Key Vault

### 2. Datasets

* **Source Dataset (REST/JSON)**

  * Points to `/users` endpoint
* **Sink Dataset (ADLS CSV)**

  * Defines file format, delimiter, and storage path

### 3. Pipeline

* **Copy Data Activity**

  * Handles ingestion from API → ADLS
  * Includes schema mapping

---

## ▶️ How to Run

1. Deploy resources:

   * Azure Data Factory
   * Azure Data Lake Storage Gen2
   * Azure Key Vault

2. Configure Linked Services:

   * Update base URL for API: `https://jsonplaceholder.typicode.com`
   * Configure ADLS connection

3. Publish ADF changes

4. Trigger the pipeline:

   * Manual trigger via ADF UI
   * Schedule using a Trigger

---

## 📂 Output

The pipeline writes a CSV file to ADLS with the following structure:


| id | name | username | email | phone | website |
| -- | ---- | -------- | ----- | ----- | ------- |

---

## ⚠️ Assumptions & Limitations

* JSONPlaceholder is a mock API (no authentication required)
* Data volume is small (no pagination handling implemented)
* No incremental loading (full extract only)

---

## 🚀 Improvements & Enhancements

Schema Drift - Data flow
Output to SQL table
Mutiple input streams
Find API with security to set up key vault token
Meta driven data collection (Api -> SQl Control table -> pipeline trigger ) 
Improved Error logging 



## 👤 Author

Nathaniel Thorpe - Skills Training. 

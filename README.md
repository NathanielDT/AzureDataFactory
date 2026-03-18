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

### 🔹 1. Parameterisation

* Add pipeline parameters for:

  * API endpoint (e.g. `/users`, `/posts`)
  * Output file name/path
* Makes pipeline reusable across datasets

---

### 🔹 2. Schema Drift & Data Flow

* Introduce Mapping Data Flow to:

  * Handle nested JSON (e.g. address, company)
  * Enable schema drift for flexible ingestion

---

### 🔹 3. Incremental Loads

* Implement watermarking or pagination:

  * Use query parameters if API supports it
  * Store last load timestamp

---

### 🔹 4. Error Handling & Logging

* Add:

  * Retry policies on Copy Activity
  * Failure paths with alerts
* Integrate with:

  * Azure Monitor / Log Analytics

---

### 🔹 5. Secure Configuration

* Store secrets in Azure Key Vault
* Use Managed Identity for authentication
* Avoid hardcoding credentials

---

### 🔹 6. Data Partitioning

* Store output using a dynamic folder structure:

  ```
  /users/year=YYYY/month=MM/day=DD/
  ```
* Improves query performance and organisation

---

### 🔹 7. CI/CD Integration

* Use ARM templates or Bicep for deployment
* Integrate with GitHub Actions or Azure DevOps pipelines

---

### 🔹 8. Metadata-Driven Framework

* Store ingestion configs in a control table
* Dynamically drive pipelines based on metadata
* Scales to multiple APIs and datasets

---

### 🔹 9. Data Validation

* Add validation checks:

  * Row counts
  * Schema validation
* Use Stored Procedures or Data Flows

---

### 🔹 10. Format Optimisation

* Convert CSV → Parquet

  * Better compression
  * Faster analytics performance

---

##  Next Steps

Schema Drift

## 👤 Author

Nathaniel Thorpe - Skills Training. 

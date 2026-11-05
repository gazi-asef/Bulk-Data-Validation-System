# Bulk Loader – Bulk CSV Data Processing Application

A Power Apps-based application built to simplify bulk CSV uploads and data processing. It allows users to upload large CSV files, validate records, identify duplicates, and store the processed data in SQL Server.

I built this project to reduce manual data handling and explore how Microsoft Power Platform can be used with SQL Server to process large datasets more efficiently.

The application is designed to handle large CSV files containing **100,000+ records**, with a focus on data validation, batch tracking, and performance.

---

## Application Overview

The application uses Microsoft Power Apps as the front end, Power Automate to manage the processing workflow, and SQL Server for data storage and server-side processing.

![Bulk Loader End-to-End Process Flow](<docs/screenshots/Bulk Loader End-to-End Process Flow.png>)

---

## Application Screenshots

### 1. Upload Screen

Users can upload CSV files through a simple interface and initiate the bulk data processing workflow.

![Upload Screen](<docs/screenshots/Main Screen.png>)

### 2. Data Review Screen

After processing, users can review the uploaded records, apply filters, and manage the data.

![Data Review Screen](<docs/screenshots/All records view.png>)

### 3. Invalid Records

Invalid records are displayed separately along with their corresponding error reasons, making it easier to identify and review data issues.

![Invalid Records Screen](<docs/screenshots/Invalid Records View.png>)

### 4. Duplicate Records

Duplicate records are maintained separately so users can identify records that should not be processed as new entries.

![Duplicate Records Screen](<docs/screenshots/Duplicate Records View.png>)

### 5. Analytics Dashboard

The dashboard provides an overview of upload activity, processing results, and upload performance through KPI cards and charts.

![Analytics Dashboard](<docs/screenshots/Dashboard View.png>)

---

## Key Features

- **Bulk CSV Upload:** Upload large CSV files through a Power Apps Canvas application.
- **Data Validation:** Validate uploaded records and identify incorrect or missing data.
- **Duplicate Detection:** Identify duplicate records and keep them separate from valid records.
- **SQL Server Processing:** Use SQL Server stored procedures for data processing and database operations.
- **Batch Tracking:** Maintain upload information to track individual upload batches.
- **Error Management:** Store invalid records along with their corresponding error messages.
- **Pagination:** Retrieve records in smaller pages instead of loading large datasets into Power Apps galleries at once.
- **Data Monitoring:** View upload details, processing status, and categorized records through the application.
- **Analytics Dashboard:** Monitor upload activity and processing statistics.

---

## How It Works

The application follows a structured process from file upload to final data storage.

### 1. Upload CSV File

The user selects a CSV file and uploads it through the Power Apps Canvas application.

### 2. Create Upload Batch

The application creates an upload record to maintain batch information and track the processing activity.

### 3. Power Automate Processing

Power Automate manages the workflow, connects Power Apps with SQL Server, and executes the required processing operations.

### 4. Temporary Data Loading

The uploaded CSV records are loaded into a SQL Server staging table before further processing.

### 5. Data Validation and Duplicate Checking

SQL Server stored procedures process the staging records and categorize them into three groups:

- Valid Records
- Invalid Records
- Duplicate Records

### 6. Store Processed Records

After processing, records are stored in their respective SQL Server tables.

| Table | Purpose |
|---|---|
| `Sales_Staging` | Temporarily stores uploaded CSV records |
| `Sales_Main` | Stores valid sales records |
| `Sales_Errors` | Stores invalid records and error messages |
| `Sales_Duplicates` | Stores duplicate records |
| `Sales_Items` | Stores item-related information |
| `Sales_UploadLog` | Maintains upload activity details |
| `UploadLog` | Maintains upload and processing statistics |

### 7. View Processing Results

Users can review upload information, processing status, valid records, invalid records, and duplicate records through the Power Apps interface.

---

## Technology Stack

| Technology | Purpose |
|---|---|
| Microsoft Power Apps (Canvas) | Application interface and user interaction |
| Microsoft Power Automate | Workflow automation and processing orchestration |
| Microsoft SQL Server | Database and bulk data processing |
| SQL Stored Procedures | Validation, duplicate checking, filtering, and data retrieval |
| On-Premises Data Gateway | Connects Power Platform with the on-premises SQL Server |

---

## Database Architecture

SQL Server is used as the primary database for this application.

The application follows a staging-based approach, where uploaded records are first stored temporarily before validation and further processing.

Based on the processing results, records are moved into the appropriate tables:

- `Sales_Main` – Valid records
- `Sales_Errors` – Invalid records
- `Sales_Duplicates` – Duplicate records

The `UploadBatchId` field is used to associate records with their respective upload batches. These associations support logical batch tracking and do not necessarily represent enforced SQL foreign-key relationships.

---

## Performance and Data Handling

One of the main challenges in this project was handling large datasets without putting unnecessary load on Power Apps.

To address this, I worked with the following approaches:

- Used SQL Server stored procedures for server-side data processing.
- Implemented pagination to retrieve records in smaller batches.
- Used SQL-based filtering instead of loading entire datasets into Power Apps collections.
- Maintained separate tables for valid, invalid, and duplicate records.
- Used indexed database columns where appropriate.
- Implemented batch-based tracking to organize upload activities.

These approaches help reduce unnecessary data transfer between SQL Server and Power Apps and make the application more manageable when working with large datasets.

---

## Project Highlights

- Built an end-to-end bulk CSV upload application using Microsoft Power Platform.
- Integrated Power Apps, Power Automate, and SQL Server.
- Implemented a staging-based data processing approach.
- Separated valid, invalid, and duplicate records.
- Used SQL Server stored procedures for data processing.
- Worked on pagination and performance optimization for large datasets.
- Created an analytics dashboard to monitor upload activities and processing results.

---

## Repository Structure

```text
BulkLoader/
│
├── src/
│   ├── CanvasApps/
│   ├── Other/
│   └── Workflows/
│
├── docs/
│   └── screenshots/
│       └──Application Images
│
├── .gitignore
├── BulkLoader.cdsproj
└── README.md
```

---

## Developed By

**Asef Gazi**

Power Platform Developer

---

This project is part of my hands-on learning and development with Microsoft Power Platform and SQL Server. It gave me an opportunity to work on bulk data processing, database operations, workflow automation, and handling large datasets in a practical application.
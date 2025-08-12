# Airflow Pipeline with Random Digit Count and Conditional Branching

## 📌 Overview
This project implements an Airflow DAG that orchestrates a simple ETL-like pipeline with PostgreSQL integration. It creates tables, inserts job records, randomly generates digits to count occurrences in a string, and conditionally branches workflow tasks based on the count and error handling.


## 🚀 Features
- **Table Creation:** Creates two tables for storing job metadata and results if they don’t exist.  
- **Record Insertion:** Inserts records into both tables and tracks job IDs across tasks.  
- **Random Digit Hit Counting:** Generates random digits, counts their occurrences in a predefined string, with a simulated 30% chance to raise an error.  
- **Branching Logic:** Uses Airflow’s `BranchPythonOperator` to route execution based on hit count threshold.  
- **Error Handling:** Updates job records accordingly on task failure or success.  


## 📦 Environment Setup
1. Configure PostgreSQL connection parameters (`DB_HOST`, `DB_PORT`, `DB_USERNAME`, `DB_PASSWORD`) in the DAG code.  
2. Ensure Airflow is running with access to the PostgreSQL server specified.  
3. Place this DAG file in Airflow’s DAG folder.  
4. Install dependencies: `sqlalchemy`, `psycopg2`, `apache-airflow`.  


## 🛠 How It Works

**Create Tables**  
Checks if the tables `dummy_job` and `dummy_job_result` exist; creates them if not.

**Insert Records**  
Inserts a new job record into `dummy_job`, retrieves the generated `id`, and inserts a corresponding record into `dummy_job_result`. Shares the `job_id` with downstream tasks via XCom.

**Generate Random Digit Hits**  
Generates 1 million random digits (0-9). For each digit, checks if it is found in a fixed string. Counts how many digits are found and stores the count via XCom. Simulates a 30% chance of failure by raising an exception.

**Branching**  
Reads the hit count. If above threshold, routes to `action_on_gt_threshold`. Otherwise, routes to `action_on_lte_threshold`.

**Actions on Threshold**  
Updates the `dummy_job` record to mark it inactive, and updates `dummy_job_result` to mark success and whether the hit count was greater than the threshold.

**Error Handling**  
If the digit counting task fails, this task marks the job inactive and the result unsuccessful.


## 📚 Data & Tables
- `dummy_job`: stores job IDs and active status.  
- `dummy_job_result`: stores job results, hit count thresholds, and success flags.  


## ▶️ Usage
1. Update DB connection info in the DAG script.  
2. Deploy DAG to Airflow.  
3. Trigger DAG manually or via scheduler.  
4. Monitor tasks in Airflow UI.  

## 📚 Technologies Used
- Python — DAG logic and helpers.  
- Apache Airflow — Workflow orchestration.  
- PostgreSQL — Job metadata and results storage.  
- SQLAlchemy — Database interaction.  
- Psycopg2 — PostgreSQL adapter for Python.  

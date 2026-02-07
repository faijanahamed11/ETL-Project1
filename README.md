# ETL Data Pipeline Project (Python + PostgreSQL)

This is a simple ETL project that I built to practice how data is extracted from a file, cleaned using Python, and then stored in a PostgreSQL database.

The project follows basic ETL steps:  
Extract → Transform → Load.

---

## What this project does

1. Reads employee data from a CSV file  
2. Cleans the data (handles missing values and duplicates)  
3. Connects to a PostgreSQL database  
4. Loads the cleaned data into a database table  

---

## Tools and Technologies Used

- Python 3
- Pandas (for data cleaning and transformation)
- PostgreSQL (database)
- SQLAlchemy (database connection)
- psycopg2 (PostgreSQL driver)

---

## Dataset Details

The input data is taken from a CSV file:


The dataset contains employee information such as:
- employee_id
- department
- region
- education
- gender
- recruitment_channel
- age
- previous_year_rating
- length_of_service
- awards_won
- avg_training_score

---

## ETL Process Explanation

### Step 1: Extract
- The CSV file is loaded into a Pandas DataFrame using `read_csv()`
- First and last few rows are checked to understand the data

### Step 2: Transform
- Duplicate rows are removed
- Missing values are handled:
  - `education` column missing values are replaced with `"unknown"`
  - `previous_year_rating` missing values are replaced with `0`
- After cleaning, the data is checked again to confirm no missing values remain

### Step 3: Database Setup
- PostgreSQL database name: `etl_db`
- Table name: `employee_table`
- Connection is created using SQLAlchemy

### Step 4: Load
- The cleaned DataFrame is loaded into PostgreSQL
- If the table already exists, it is replaced

---

## Database Configuration Used

```python
username = "postgres"
password = "Root1234"
host = "localhost"
port = 5432
db_name = "etl_db"

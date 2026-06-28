# ETL Data Pipeline Project (Python + MySQL)

This is a simple ETL project that I built to practice how data is extracted from a file, cleaned using Python, and then stored in a MySQL database.

The project follows basic ETL steps:  
Extract → Transform → Load.

---

## What this project does

1. Reads employee data from a CSV file
2. Cleans the data (handles missing values and duplicates)
3. Connects to a MySQL database using secure environment variables
4. Loads the cleaned data into a database table

---

## Tools and Technologies Used

- Python 3
- Pandas (for data cleaning and transformation)
- MySQL (database)
- SQLAlchemy (database connection management)
- mysql-connector-python (MySQL driver)
- python-dotenv (for secure credential management)

---

## Project Structure

```
ETL-Project1/
├── data/
│   └── employees.csv        # Input dataset
├── .env                     # Database credentials (not uploaded to GitHub)
├── .gitignore               # Excludes .env from version control
├── ETLPipeline.ipynb        # Main ETL notebook
├── requirements.txt         # Python dependencies
└── README.md
```

--- 


## Dataset Details

The input dataset is a CSV file containing employee information:

| Column | Description |
|---|---|
| employee_id | Unique identifier for each employee |
| department | Department the employee belongs to |
| region | Geographic region |
| education | Education level |
| gender | Gender of the employee |
| recruitment_channel | How the employee was recruited |
| age | Age of the employee |
| previous_year_rating | Performance rating from previous year |
| length_of_service | Years of service |
| awards_won | Whether the employee won an award |
| avg_training_score | Average score across training sessions |

---

## ETL Process Explanation

### Step 1: Extract
- The CSV file is loaded into a Pandas DataFrame using `read_csv()`
- First and last few rows are inspected to understand the data structure

### Step 2: Transform
- Duplicate rows are identified and removed
- Missing values are handled:
  - `education` column: filled with `"unknown"`
  - `previous_year_rating` column: filled with `0`
- Data is verified to confirm no missing values remain after cleaning

### Step 3: Database Setup
- MySQL database name: `etl_db`
- Table name: `employee_table`
- Connection is managed securely using SQLAlchemy and environment variables

### Step 4: Load
- The cleaned DataFrame is loaded into MySQL using `to_sql()`
- If the table already exists, it is replaced with fresh data

---

## Environment Setup

### 1. Clone the repository

```bash
git clone https://github.com/faijanahamed11/ETL-Project1.git
cd ETL-Project1
```

### 2. Create a virtual environment and install dependencies

```bash
python -m venv venv
source venv/bin/activate        # Mac/Linux
venv\Scripts\activate           # Windows

pip install -r requirements.txt
```

### 3. Create a `.env` file in the project root

```
DB_USERNAME=your_mysql_username
DB_PASSWORD=your_mysql_password
DB_HOST=127.0.0.1
DB_PORT=3306
DB_NAME=etl_db
```

> ⚠️ Never commit your `.env` file to GitHub. It is already listed in `.gitignore`.

### 4. Create the database in MySQL

```sql
CREATE DATABASE etl_db;
```

### 5. Run the notebook

Open `ETLPipeline.ipynb` in VS Code or Jupyter and run all cells.

---

## Database Connection Approach

Credentials are loaded securely from the `.env` file and passed via `connect_args` to avoid URL parsing issues with special characters in passwords:

```python
from sqlalchemy import create_engine
from dotenv import load_dotenv
import os

load_dotenv(override=True)

engine = create_engine(
    'mysql+mysqlconnector://',
    connect_args={
        "host":     os.getenv("DB_HOST"),
        "port":     int(os.getenv("DB_PORT")),
        "user":     os.getenv("DB_USERNAME"),
        "password": os.getenv("DB_PASSWORD"),
        "database": os.getenv("DB_NAME")
    }
)
```

---

## Key Learnings

- How to build an end-to-end ETL pipeline using Python
- Data cleaning techniques with Pandas (handling nulls and duplicates)
- Secure credential management using environment variables
- Connecting Python to a MySQL database using SQLAlchemy
- Loading transformed data into a relational database table
# 🚦 Traffic Surveillance Project Dummy Data Setup Guide

This guide explains how to set up the MySQL database for the Traffic
Project. You can follow either the **Short Method (recommended)** or the
**Long Method (manual setup)**.

------------------------------------------------------------------------

## ⚡ Short Method (Recommended)

This is the quickest way to import the database schema.

### Steps:

1.  Open **Command Prompt** on your system.

2.  Copy the file:

        TrafficProjectSchema.sql

    into your **Current Working Directory (CWD)**\
    *(or navigate your terminal to that directory).*

3.  Run the following command:

    ``` bash
    mysql -u [username] -p [database_name] < [input_file.sql]
    ```

    **Example:**

    ``` bash
    mysql -u root -p TrafficProjectFinal < TrafficProjectSchema.sql
    ```

4.  ⚠️ Important:\
    Make sure the database already exists before running the above
    command.

    Run this in MySQL shell:

    ``` sql
    CREATE DATABASE TrafficProjectFinal;
    ```

------------------------------------------------------------------------

## 🛠️ Long Method (Manual Setup)

Use this method if you want more control over the setup process.

### Step 1: Create Database

Open MySQL shell and run:

``` sql
CREATE DATABASE TrafficProjectDatabase;
USE TrafficProjectDatabase;
```

------------------------------------------------------------------------

### Step 2: Create Tables

1.  Open the file:

        TrafficProjectFinalSchema_MysqlCode.txt

2.  Copy and paste the SQL code into MySQL shell.

⚠️ **Note:** - Sometimes all tables may not execute at once. - If that
happens, paste and execute the remaining tables individually.

------------------------------------------------------------------------

### Step 3: Insert Data

To populate the database:

1.  Navigate to the `CodeHelp` folder.

2.  Run the Python script:

        EntringDataFromExcelToMysqltable.py

------------------------------------------------------------------------

### Step 4: Configure Python Script

Before running the script, update:

-   `excel_file_path` → Path to your Excel file
-   MySQL credentials:
    -   Username
    -   Password
    -   Database name

------------------------------------------------------------------------

### Step 5: Run the Script

Execute the Python file.
Once completed, the data from Excel will be inserted into the MySQL
database.

------------------------------------------------------------------------

## ✅ Final Outcome

After completing either method:

-   Database is created ✔️
-   Tables are set up ✔️
-   Data is inserted ✔️

------------------------------------------------------------------------

## 📌 Notes

-   Ensure MySQL is installed and running.
-   Make sure Python dependencies (like `mysql-connector` / `pandas`)
    are installed if using the long method.
-   Double-check file paths and credentials before execution.

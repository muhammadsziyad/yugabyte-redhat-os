# YugabyteDB on RHEL OS Project

## Overview

YugabyteDB is an open-source, distributed SQL database designed for high performance and scalability. This project provides a step-by-step guide to installing and configuring YugabyteDB on Red Hat Enterprise Linux (RHEL) OS, and demonstrates basic usage with sample SQL commands.

## Objectives

1. **Install YugabyteDB**: Set up YugabyteDB on RHEL OS.
2. **Configure YugabyteDB**: Configure the database for optimal performance.
3. **Use YugabyteDB**: Execute sample SQL commands to interact with the database.

## Step-by-Step Installation

### 1. Prepare Your RHEL System

- **Step 1:** Update your system.
  ```bash
  sudo yum update -y
  ```

  
- **Step 2:** Install necessary dependencies.
    ```bash
    sudo yum install -y wget tar
    ```
    

### 2. Download and Install YugabyteDB

-   **Step 1:** Download the latest YugabyteDB release.
    
    ```bash
    wget https://downloads.yugabyte.com/releases/2.23.0.0/yugabyte-2.23.0.0-b710-linux-x86_64.tar.gz
    ``` 
    
-   **Step 2:** Extract the downloaded tarball.
    
    ```bash
    tar xvf yugabyte-2.19.1.0-linux-x86_64.tar.gz
    ``` 
    
-   **Step 3:** Move into the extracted directory.

    
    ```bash
    cd yugabyte-2.19.1.0
    ``` 
    

### 3. Start YugabyteDB

-   **Step 1:** Start YugabyteDB using the provided script.
    

    
    ```bash
    ./bin/yugabyted start
    ``` 
    

## Step-by-Step Configuration

### 1. Verify the Installation

-   **Step 1:** Check the status of YugabyteDB.
    
    ```bash
    ./bin/yugabyted status
    ``` 
    
-   **Step 2:** Access the YugabyteDB web console by navigating to `http://localhost:7000` in your web browser.
    

### 2. Configure YugabyteDB

-   **Step 1:** Modify the `yugabyted` configuration file located at `./conf/yugabyted.conf` to adjust settings such as memory limits and ports if needed.

### 3. Configure Firewall

-   **Step 1:** Allow necessary ports through the firewall.

    
    ```bash
    sudo firewall-cmd --zone=public --add-port=7000/tcp --permanent
    sudo firewall-cmd --zone=public --add-port=5433/tcp --permanent
    sudo firewall-cmd --reload
    ``` 
    

## Step-by-Step Usage with Sample SQL Commands

### 1. Access the YugabyteDB Shell

-   **Step 1:** Use `ysqlsh` to connect to the YugabyteDB cluster.
    
    
    ```bash
    ./bin/ysqlsh -h <your-host> -p <host-port>
    ``` 
    

### 2. Create a Database and Table

-   **Step 1:** Create a new database.

    
    ```sql
    CREATE DATABASE sample_db;
    ``` 
    
-   **Step 2:** Switch to the new database.

    
    ```sql
    \c sample_db
    ``` 
    
-   **Step 3:** Create a new table.

    ```sql
    CREATE TABLE users (
        id SERIAL PRIMARY KEY,
        name TEXT NOT NULL,
        email TEXT UNIQUE NOT NULL
    );
    ```
    

### 3. Insert Data

-   **Step 1:** Insert sample data into the table.

    
    ```sql
    INSERT INTO users (name, email) VALUES ('Alice', 'alice@example.com');
    INSERT INTO users (name, email) VALUES ('Bob', 'bob@example.com');
    ``` 
    

### 4. Query Data

-   **Step 1:** Retrieve data from the table.
    

    
    ```sql
    SELECT * FROM users;
    ``` 
    

### 5. Update and Delete Data

-   **Step 1:** Update data in the table.
    

    
    ```sql
    UPDATE users SET email = 'alice_new@example.com' WHERE name = 'Alice';
    ``` 
    
-   **Step 2:** Delete data from the table.

    
    ```sql
    DELETE FROM users WHERE name = 'Bob';
    ```
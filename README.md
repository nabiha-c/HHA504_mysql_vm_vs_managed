# HHA504: MySQL VM vs Managed Service (GCP)

This project compares two ways of running MySQL in the cloud:  
1. A **self-managed MySQL server on a GCP VM**, and  
2. A **managed MySQL database using Cloud SQL for MySQL**.

The goal was to connect to both using Python (SQLAlchemy + pandas), create a database and table, insert data, and read it back.

I used **Google Cloud Platform (GCP)** for everything.  
Region: <us-central1>

---

## Project Structure

HHA504_mysql_vm_vs_managed/
├─ README.md
├─ .gitignore
├─ .env.example
├─ scripts/
│   ├─ vm_demo.py
│   └─ managed_demo.py
├─ screenshots/
└─ docs/
    ├─ setup_notes_vm.md
    ├─ setup_notes_managed.md
    └─ comparison.md

---

## How to Reproduce 

### 1. VM MySQL Setup
- Create a VM on GCP (Ubuntu 22.04)
- Open firewall port 3306
- Install MySQL using apt
- Edit mysqld.cnf to allow remote connections (bind-address = 0.0.0.0)
- Restart MySQL
- Create a MySQL user and database
- Run vm_demo.py from VS Code to test connection

### 2. Managed Cloud SQL Setup
- Create a Cloud SQL (MySQL) instance
- Add your laptop’s public IP to "Authorized Networks"
- Connect using Cloud Shell:
  gcloud sql connect <instance_name> --user=root
- Create database (and optional user)
- Run managed_demo.py from VS Code

---

## Connection String Patterns (No Secrets)

Both scripts use the SQLAlchemy PyMySQL format:

mysql+pymysql://USER:PASS@HOST:PORT/DBNAME

I stored my real secrets in a local .env file (not committed), and used:

- VM_DB_HOST, VM_DB_USER, VM_DB_PASS, VM_DB_NAME
- MAN_DB_HOST, MAN_DB_USER, MAN_DB_PASS, MAN_DB_NAME

---

## Screenshots

All screenshots are under /screenshots.

### VM screenshots:
- VM creation
- Firewall rules
- MySQL install + status
- Config changes
- MySQL prompt
- Python script output

### Managed screenshots:
- Cloud SQL creation
- Authorized networks
- MySQL prompt via Cloud Shell
- Python script output

---

## Demo Video (2–4 minutes)
Link to recording:  
<insert your Loom or Zoom link here>

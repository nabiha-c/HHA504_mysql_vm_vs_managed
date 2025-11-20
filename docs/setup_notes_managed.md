# Setup Notes: Managed MySQL (Cloud SQL for MySQL)

## Cloud SQL Instance Provisioning (GCP)
- Cloud provider: **GCP**
- Service: **Cloud SQL – MySQL**
- Edition: MySQL 8.x

### Cloud SQL Creation Summary
![managed creation](/screenshots/managed_creation_summary.png)

---

## Networking Settings
Authorized networks:
- Added my laptop’s public IP
- Public IP access enabled

### Authorized Networks 
![network](/screenshots/managed_network.png)

---

## MySQL Database Setup via Cloud Shell

Connected using:

```bash
gcloud sql connect hha504-managed-mysql --user=root --quiet
```

Entered root password at prompt.

Created database:

```sql
CREATE DATABASE IF NOT EXISTS class_db_netid;
```

(Optional) Created class_user:

```sql
CREATE USER IF NOT EXISTS 'class_user'@'%' IDENTIFIED BY 'Hha504Managed123!';
GRANT ALL PRIVILEGES ON class_db_netid.* TO 'class_user'@'%';
FLUSH PRIVILEGES;
```

Verified:

```sql
SHOW DATABASES;
USE class_db_netid;
SHOW TABLES;
```

### Cloud SQL MySQL Prompt 
![managed prompt](/screenshots/managed_mysql_prompt.png)

---

## Python Test — managed_demo.py

Ran from VS Code:

```bash
python scripts/managed_demo.py
```

The script successfully:

- Connected to the Cloud SQL instance  
- Ensured the database existed  
- Created the `visits` table  
- Inserted 5 rows via pandas  
- Read back the row count  

### managed_demo.py Output 
![managed demo output](/screenshots/managed_demo_output.png)



# Setup Notes: MySQL on VM (Self-Managed)


## VM Provisioning (GCP)
- Cloud provider: **GCP**
- Service: **Compute Engine**
- OS: Ubuntu 22.04 LTS

### VM Creation Summary  

![vm creation](/screenshots/vm_creation_summary.png)

---

## Firewall Rule
Opened **TCP port 3306** to my laptop's public IP.

- Rule name: `allow-mysql-from-my-ip`
- Direction: **Ingress**
- Allowed: TCP 3306 
 
![firewall rule](/screenshots/firewall_3306.png)

---

## MySQL Installation on the VM

Commands executed:

```bash
sudo apt update
sudo apt install mysql-server -y
sudo systemctl status mysql
mysql --version
```

**MySQL Status:**  
![install](/screenshots/sql_install.png)
![restart](/screenshots/sql_restart.png)

---

## MySQL Configuration Changes

Edited the MySQL config file:

```
/etc/mysql/mysql.conf.d/mysqld.cnf
```

Changed:

```
bind-address = 127.0.0.1
```

to:

```
bind-address = 0.0.0.0
```

Restarted MySQL:

```bash
sudo systemctl restart mysql
sudo systemctl status mysql
```

---

## MySQL User + Database Setup

Accessed MySQL:

```bash
sudo mysql
```

Created user + database:

Tested login:

```bash
mysql -u class_user -p -h 127.0.0.1 -P 3306
```

Verified:

```sql
SHOW DATABASES;
USE class_db_netid;
SHOW TABLES;
```

**MySQL Prompt Screenshot:**  
![mysql prompt](/screenshots/mysql_prompt_showdbs.png)

---

## Python Test — vm_demo.py

Ran from VS Code:

```bash
python scripts/vm_demo.py
```

The script:

- Connected successfully to the VM MySQL  
- Ensured the database existed  
- Created the `visits` table  
- Inserted 5 rows using pandas  
- Read back the row count  

**vm_demo.py Output Screenshot:**  
![vm demo output](/screenshots/vm_demo_output.png)


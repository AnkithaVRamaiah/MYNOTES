# **Cron Jobs in Shell Scripting**  

## **1. Introduction to Cron Jobs**  
A **cron job** is a scheduled task that runs automatically at specified intervals on a Linux system. It is managed by the **cron daemon (`crond`)** and is useful for automating repetitive tasks such as backups, log rotation, and system monitoring.  

✅ **Why Use Cron Jobs?**  
- Automates repetitive tasks  
- Saves time and reduces manual effort  
- Ensures tasks run at the correct time  

---

## **2. Understanding the Crontab File**  
The `crontab` file stores scheduled jobs for each user. Each line in the file represents a job.  

To edit the crontab, use:  
```bash
crontab -e
```
To view existing cron jobs:  
```bash
crontab -l
```
To remove all cron jobs:  
```bash
crontab -r
```

---

## **3. Cron Job Syntax**  
A cron job follows this format:  
```
* * * * * command_to_run
- - - - -
| | | | |  
| | | | +---- Day of the week (0 - Sunday, 6 - Saturday)  
| | | +------ Month (1 - 12)  
| | +-------- Day of the month (1 - 31)  
| +---------- Hour (0 - 23)  
+------------ Minute (0 - 59)  
```

---

## **4. Examples of Cron Jobs**  

### **1️⃣ Run a Script Every Minute**  
```bash
* * * * * /home/user/myscript.sh
```

---

### **2️⃣ Run a Script Every Day at 3 AM**  
```bash
0 3 * * * /home/user/backup.sh
```

---

### **3️⃣ Run a Script Every Monday at 6 PM**  
```bash
0 18 * * 1 /home/user/monday_task.sh
```

---

### **4️⃣ Run a Script on the First Day of Every Month**  
```bash
0 0 1 * * /home/user/monthly_report.sh
```

---

### **5️⃣ Run a Script Every 15 Minutes**  
```bash
*/15 * * * * /home/user/task.sh
```

---

### **6️⃣ Run a Script at Startup**  
```bash
@reboot /home/user/startup_script.sh
```

---

## **5. Redirecting Output in Cron Jobs**  
By default, cron jobs do not display output. Redirect output to a file for logging:  
```bash
* * * * * /home/user/script.sh >> /home/user/logs.txt 2>&1
```
➡ `2>&1` captures errors and standard output.  

---

## **6. Automating Cron Job Management in a Shell Script**  
**Example: Creating a Cron Job via Script**  
```bash
#!/bin/bash
echo "0 3 * * * /home/user/backup.sh" | crontab -
echo "Cron job added successfully!"
```

---

## **7. Troubleshooting Cron Jobs**  
| **Issue** | **Solution** |
|-----------|------------|
| Script is not running | Check with `crontab -l` if it’s scheduled correctly |
| Permissions issue | Ensure the script has execute permissions (`chmod +x script.sh`) |
| Path issues | Use absolute paths in the script |
| No output | Redirect output to a log file (`>> logfile 2>&1`) |
| Cron daemon not running | Restart cron service (`sudo systemctl restart cron`) |

---

# **Interview Questions & Answers**  

### **Beginner Level**  

**Q1: What is a cron job?**  
✅ **A:** A cron job is a scheduled task that runs automatically at predefined intervals on a Linux system.  

---

**Q2: How do you list all cron jobs for the current user?**  
✅ **A:**  
```bash
crontab -l
```

---

**Q3: How do you add a new cron job?**  
✅ **A:**  
```bash
crontab -e
```
➡ This opens the crontab file for editing.  

---

### **Intermediate Level**  

**Q4: How do you schedule a script to run every Sunday at 4 AM?**  
✅ **A:**  
```bash
0 4 * * 0 /path/to/script.sh
```
➡ `0` represents Sunday in cron jobs.  

---

**Q5: What does this cron job do?**  
```bash
*/10 * * * * /home/user/script.sh
```
✅ **A:** It runs the script every 10 minutes.  

---

### **Advanced Level**  

**Q6: What is the difference between `@reboot` and `@daily` in cron?**  
✅ **A:**  
- `@reboot` runs the job once at system startup.  
- `@daily` runs the job once a day at midnight.  

---

**Q7: How do you debug a cron job that isn’t running?**  
✅ **A:**  
1. Check if cron is running:  
   ```bash
   systemctl status cron
   ```
2. Verify the cron job:  
   ```bash
   crontab -l
   ```
3. Add logging to capture errors:  
   ```bash
   * * * * * /home/user/script.sh >> /home/user/log.txt 2>&1
   ```

---

# **8. Summary**  
✔ **Cron jobs** automate scheduled tasks in Linux.  
✔ Use `crontab -e` to add jobs and `crontab -l` to list them.  
✔ Always use **absolute paths** in cron scripts.  
✔ Redirect output to logs for debugging (`>> log.txt 2>&1`).  

Would you like a **real-world automation script** using cron?
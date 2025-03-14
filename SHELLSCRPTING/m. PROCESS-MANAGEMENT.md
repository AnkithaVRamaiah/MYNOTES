# **Process Management in Shell Scripting**  

## **1. Introduction to Processes**  
A **process** is a running instance of a program. Every command executed in a shell creates a process.  

✅ **Why is process management important?**  
- Monitors and controls system resources  
- Helps manage background and foreground tasks  
- Prevents performance issues caused by unnecessary processes  

---

## **2. Types of Processes in Linux**  

| **Process Type** | **Description** |
|----------------|---------------|
| **Foreground Process** | Runs in the terminal and waits for user input |
| **Background Process** | Runs in the background without blocking the terminal |
| **Daemon Process** | Runs in the background continuously (e.g., web servers) |
| **Zombie Process** | A terminated process that still has an entry in the process table |
| **Orphan Process** | A process whose parent has exited but still runs under `init` |

---

## **3. Managing Processes in Shell Scripting**  

### **1️⃣ Checking Running Processes (`ps` Command)**  
```bash
ps aux   # Shows all running processes
ps -ef   # Detailed process list
```

✅ **Example Output:**  
```
USER       PID %CPU %MEM    COMMAND
root       1234  0.1  1.2    apache2
ankita     5678  0.0  0.5    bash
```
➡ `PID` (Process ID) helps identify a process.

---

### **2️⃣ Running a Process in the Background (`&` Operator)**  
```bash
long_running_task.sh &  # Runs in background
```
✅ **Output:**  
```
[1] 4567  # Process started with PID 4567
```

---

### **3️⃣ Bringing a Background Process to Foreground (`fg`)**  
```bash
fg %1  # Brings the first background job to foreground
```

---

### **4️⃣ Suspending and Resuming a Process**  
- **Suspend:** Press `Ctrl + Z`  
- **Resume in Background:** `bg`  
- **Resume in Foreground:** `fg`  

---

### **5️⃣ Killing a Process (`kill` Command)**  
```bash
kill 4567  # Gracefully stops process 4567
kill -9 4567  # Forcefully kills process 4567 (SIGKILL)
```

✅ **Alternative:**  
```bash
pkill -9 process_name  # Kills process by name
```

---

### **6️⃣ Automating Process Monitoring in Shell Scripts**  

```bash
#!/bin/bash
process_name="apache2"

if pgrep "$process_name" > /dev/null
then
    echo "$process_name is running."
else
    echo "$process_name is not running. Starting it..."
    sudo systemctl start apache2
fi
```
✅ **This script checks if `apache2` is running and starts it if not.**  

---

## **4. Process Priorities (`nice` and `renice`)**  

| **Command** | **Function** |
|------------|------------|
| `nice -n 10 command` | Runs a command with lower priority |
| `renice -n 5 -p 4567` | Changes priority of an existing process |

✅ **Example:**  
```bash
nice -n 10 ./heavy_task.sh
```
➡ Runs the script with lower priority to avoid slowing down the system.  

---

## **5. Finding and Stopping Zombie Processes**  
### **Find Zombies:**  
```bash
ps aux | awk '$8=="Z" {print $2}'
```
### **Kill Parent Process to Remove Zombie:**  
```bash
kill -9 parent_PID
```

---

# **Interview Questions & Answers**  

### **Beginner Level**  

**Q1: What is a process in Linux?**  
✅ **A:** A process is an executing instance of a program.  

---

**Q2: How do you list all running processes?**  
✅ **A:**  
```bash
ps aux
```

---

**Q3: What is the difference between a foreground and background process?**  
✅ **A:**  
| **Foreground Process** | **Background Process** |
|----------------|----------------|
| Runs in terminal | Runs in the background |
| Blocks user input | Doesn’t block input |
| Example: `vi filename` | Example: `long_task.sh &` |

---

### **Intermediate Level**  

**Q4: How do you kill a process by its name?**  
✅ **A:**  
```bash
pkill process_name
```

---

**Q5: How do you bring a background process back to the foreground?**  
✅ **A:**  
```bash
fg %1
```
➡ `%1` is the job ID.  

---

### **Advanced Level**  

**Q6: What is a zombie process, and how do you remove it?**  
✅ **A:**  
A **zombie process** is a terminated process that remains in the process table.  
➡ **To remove it:** Kill its parent process.  

---

**Q7: How do you change the priority of a process?**  
✅ **A:**  
```bash
renice -n 5 -p PID
```

---

# **6. Summary**  
✔ Processes can be foreground, background, daemon, zombie, or orphan.  
✔ Use `ps aux` or `top` to monitor processes.  
✔ Use `kill` or `pkill` to terminate a process.  
✔ Use `nice` and `renice` to adjust process priorities.  
✔ Use shell scripts to automate process monitoring.  

Would you like **real-world automation scripts** for process management?
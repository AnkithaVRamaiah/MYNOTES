# **Signals and Traps in Shell Scripting**  

## **1. Introduction to Signals**  
A **signal** is a notification sent to a process to notify it of an event, like termination, pause, or user interrupts. Signals help manage and control processes in Linux.  

✅ **Why are signals important?**  
- Control running processes  
- Handle unexpected interruptions  
- Prevent data loss during script execution  

---

## **2. Common Signals in Shell Scripting**  

| **Signal Name** | **Number** | **Description** |
|---------------|----------|----------------|
| `SIGINT` | `2` | Interrupt signal (Ctrl + C) |
| `SIGTERM` | `15` | Termination request |
| `SIGKILL` | `9` | Forcefully kill a process |
| `SIGHUP` | `1` | Hang-up signal (logout) |
| `SIGSTOP` | `19` | Pause a process |
| `SIGCONT` | `18` | Continue a paused process |
| `SIGQUIT` | `3` | Quit signal (Ctrl + \) |

---

## **3. Sending Signals to Processes**  

### **Terminate a Process (`kill` Command)**  
```bash
kill -15 1234  # Sends SIGTERM to process ID 1234
kill -9 1234   # Forcefully kills process ID 1234
```

### **Interrupt a Running Process (Ctrl + C)**
When you press `Ctrl + C` while a script is running, it sends a `SIGINT` signal to stop the script.

### **Pause and Resume a Process**
```bash
kill -STOP 1234  # Pause the process
kill -CONT 1234  # Resume the process
```

---

## **4. Traps in Shell Scripting**  

A **trap** is used to catch a signal and execute a command instead of terminating the script.  

✅ **Why use traps?**  
- Prevent accidental termination  
- Clean up resources before exiting  
- Handle user interruptions gracefully  

### **Syntax**  
```bash
trap 'command' SIGNAL
```

### **Example: Prevent Script from Terminating on `Ctrl + C`**  
```bash
trap 'echo "You pressed Ctrl+C, but I won’t stop!"' SIGINT

while true; do
    echo "Running..."
    sleep 2
done
```
✅ **Output:**  
```
Running...
Running...
You pressed Ctrl+C, but I won’t stop!
Running...
```
➡ **Even after pressing `Ctrl + C`, the script continues.**  

---

## **5. Cleaning Up Before Exiting**  
Use `trap` to clean temporary files before the script exits.  

```bash
trap 'echo "Cleaning up..."; rm -f temp.txt; exit' SIGINT SIGTERM

echo "Creating temp file..."
touch temp.txt

while true; do
    echo "Working..."
    sleep 3
done
```
✅ **If you press `Ctrl + C`, the script will delete `temp.txt` before exiting.**  

---

## **6. Removing a Trap**  
```bash
trap - SIGINT
```
➡ Removes the `SIGINT` trap, allowing `Ctrl + C` to stop the script again.  

---

# **Interview Questions & Answers**  

### **Beginner Level**  

**Q1: What is a signal in shell scripting?**  
✅ **A:** A signal is a way to notify a process about an event, like termination or pause. Examples include `SIGINT` (interrupt) and `SIGTERM` (terminate).  

---

**Q2: What happens when you press `Ctrl + C` in a running script?**  
✅ **A:** It sends a `SIGINT` signal (signal number `2`) to terminate the script.  

---

**Q3: How do you kill a process using the `kill` command?**  
✅ **A:**  
```bash
kill -15 1234  # Sends SIGTERM (graceful stop)
kill -9 1234   # Sends SIGKILL (force stop)
```

---

### **Intermediate Level**  

**Q4: What is a `trap` in shell scripting?**  
✅ **A:** A trap catches a signal and executes a command instead of allowing the signal to terminate the script.  

---

**Q5: How do you prevent a script from stopping when `Ctrl + C` is pressed?**  
✅ **A:**  
```bash
trap 'echo "You cannot stop me!"' SIGINT
```

---

### **Advanced Level**  

**Q6: How do you handle multiple signals in a single trap?**  
✅ **A:**  
```bash
trap 'echo "Caught SIGINT or SIGTERM"; exit' SIGINT SIGTERM
```
➡ This handles both `SIGINT` (Ctrl + C) and `SIGTERM`.  

---

**Q7: How do you remove a trap?**  
✅ **A:**  
```bash
trap - SIGINT
```
➡ This removes the trap for `SIGINT`, allowing normal termination.  

---

# **7. Summary**  
✔ Signals control processes (e.g., `SIGINT`, `SIGTERM`).  
✔ `kill -9 PID` forcefully kills a process.  
✔ `trap` catches signals to prevent unwanted termination.  
✔ Traps help in cleanup before exiting.  
✔ Use `trap - SIGNAL` to remove a trap.  

Would you like to see **real-world use cases** for traps and signals?
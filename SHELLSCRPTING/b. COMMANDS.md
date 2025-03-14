### **Everything About Shell Commands**  

Shell commands are the basic building blocks of **Linux shell scripting**. They allow users to **interact with the system**, manage files, processes, users, and automate tasks.

---

## **1. Types of Shell Commands**  
There are two main types of shell commands:  

### **1️⃣ Built-in Commands**  
- Commands that are **part of the shell itself** (e.g., `echo`, `cd`, `pwd`, `export`).  
- Faster because they do not need an external program to run.  

**Example:**  
```bash
echo "Hello, World!"
cd /home
pwd
```

💡 **How to check if a command is built-in?**  
Use the `type` command:  
```bash
type echo
```
✅ **Output:**  
```
echo is a shell builtin
```

---

### **2️⃣ External Commands (Executable Programs)**
- Located in `/bin/`, `/usr/bin/`, etc.  
- Require separate execution (e.g., `ls`, `grep`, `find`, `awk`).  

**Example:**  
```bash
ls -l
grep "word" file.txt
find /home -name "*.sh"
```

💡 **How to check if a command is external?**  
```bash
type ls
```
✅ **Output:**  
```
ls is /bin/ls
```

---

## **2. Essential Shell Commands**
### **📁 File and Directory Commands**
| Command  | Description | Example |
|----------|------------|---------|
| `ls` | List files | `ls -l` |
| `pwd` | Print current directory | `pwd` |
| `cd` | Change directory | `cd /home` |
| `mkdir` | Create directory | `mkdir new_folder` |
| `rmdir` | Remove empty directory | `rmdir old_folder` |
| `rm` | Remove files | `rm file.txt` |
| `cp` | Copy files | `cp file1.txt file2.txt` |
| `mv` | Move/Rename files | `mv old.txt new.txt` |

🔹 **Example:**
```bash
mkdir mydir
cd mydir
touch file1.txt file2.txt
ls
```

---

### **📄 File Content Commands**
| Command  | Description | Example |
|----------|------------|---------|
| `cat` | View file contents | `cat file.txt` |
| `tac` | View file in reverse | `tac file.txt` |
| `head` | Show first N lines | `head -5 file.txt` |
| `tail` | Show last N lines | `tail -5 file.txt` |
| `less` | View large files page by page | `less bigfile.txt` |
| `more` | Similar to `less` but less powerful | `more bigfile.txt` |

🔹 **Example:**
```bash
cat file.txt
head -10 file.txt
tail -5 file.txt
less file.txt
```

---

### **🔍 Searching Commands**
| Command  | Description | Example |
|----------|------------|---------|
| `grep` | Search for a pattern in a file | `grep "error" logfile.txt` |
| `find` | Search for files/directories | `find /home -name "*.sh"` |
| `locate` | Find files quickly | `locate file.txt` |

🔹 **Example:**
```bash
grep "hello" file.txt
find /home -type f -name "*.log"
locate document.pdf
```

---

### **📊 Disk Usage Commands**
| Command  | Description | Example |
|----------|------------|---------|
| `df` | Show disk space usage | `df -h` |
| `du` | Show directory size | `du -sh /home` |

🔹 **Example:**
```bash
df -h
du -sh /var/log
```

---

### **🛠 Process Management Commands**
| Command  | Description | Example |
|----------|------------|---------|
| `ps` | Show running processes | `ps aux` |
| `top` | Show system usage in real time | `top` |
| `kill` | Kill a process | `kill 1234` |
| `pkill` | Kill by name | `pkill firefox` |

🔹 **Example:**
```bash
ps aux
kill 1234
pkill firefox
```

---

### **⚙️ User Management Commands**
| Command  | Description | Example |
|----------|------------|---------|
| `whoami` | Show current user | `whoami` |
| `who` | Show logged-in users | `who` |
| `id` | Show user/group ID | `id` |
| `passwd` | Change password | `passwd` |

🔹 **Example:**
```bash
whoami
who
id
passwd
```

---

### **🕒 Scheduling and Automation**
| Command  | Description | Example |
|----------|------------|---------|
| `crontab` | Schedule tasks | `crontab -e` |
| `at` | Schedule a one-time task | `at 5pm` |
| `nohup` | Run a command even after logout | `nohup script.sh &` |

🔹 **Example:**
```bash
crontab -e
at now + 5 minutes
nohup ./myscript.sh &
```

---

## **3. Interview Questions & Answers on Shell Commands**
### **Beginner Level**
**Q1: What is the difference between `rm` and `rmdir`?**  
✅ **A:**  
- `rm` is used to remove **files and directories** (`rm -r directory`).  
- `rmdir` can only remove **empty directories**.  

**Q2: How do you find all `.txt` files in a directory and its subdirectories?**  
✅ **A:**  
```bash
find /path/to/directory -type f -name "*.txt"
```

**Q3: How do you display the first 10 lines of a file?**  
✅ **A:**  
```bash
head -10 filename.txt
```

---

### **Intermediate Level**
**Q4: How do you search for a word inside all files in a directory?**  
✅ **A:**  
```bash
grep -r "word" /path/to/directory
```

**Q5: What is the difference between `df -h` and `du -sh`?**  
✅ **A:**  
- `df -h` shows **disk space usage** (how much space is available).  
- `du -sh` shows **directory size** (how much space a folder is using).  

**Q6: How do you find which process is using the most CPU?**  
✅ **A:**  
```bash
top
```
or  
```bash
ps aux --sort=-%cpu | head
```

---

### **Advanced Level**
**Q7: How do you schedule a shell script to run every day at midnight?**  
✅ **A:**  
```bash
crontab -e
```
Add this line:  
```bash
0 0 * * * /path/to/script.sh
```

**Q8: What command can you use to kill all processes running a specific program?**  
✅ **A:**  
```bash
pkill process_name
```

**Q9: What is the difference between `nohup` and `&`?**  
✅ **A:**  
- `&` runs a process in the **background** but stops when the terminal closes.  
- `nohup` allows the process to **keep running even after logout**.  

---

## **4. Summary**
✔ **Built-in vs. External commands**  
✔ **Essential commands for file, process, and user management**  
✔ **Searching, disk usage, and automation commands**  
✔ **Common interview questions & answers**  

Would you like me to explain any specific command in more detail?
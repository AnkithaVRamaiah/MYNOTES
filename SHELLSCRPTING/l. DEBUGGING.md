# **Debugging in Shell Scripting**  

## **1. Introduction to Debugging in Shell Scripts**  
Debugging is the process of identifying and fixing errors (bugs) in a script. Shell scripts can sometimes behave unexpectedly, so debugging helps us understand what's happening step by step.  

✅ **Why is debugging important?**  
- Identifies syntax errors and logical mistakes  
- Helps understand script execution flow  
- Saves time in troubleshooting complex scripts  

---

## **2. Methods of Debugging Shell Scripts**  

### **1️⃣ Using `set -x` (Execution Trace Mode)**  
The `set -x` command prints each command **before execution**, helping us see the flow.  

```bash
#!/bin/bash
set -x  # Enable debugging

name="Ankita"
echo "Hello, $name"

set +x  # Disable debugging
echo "Script execution completed"
```
✅ **Output:**  
```bash
+ name='Ankita'
+ echo 'Hello, Ankita'
Hello, Ankita
+ set +x
Script execution completed
```
➡ **Each command is displayed before execution**  

---

### **2️⃣ Using `bash -x script.sh` (Debugging While Running a Script)**  
Instead of modifying the script, you can run it with debugging enabled:  
```bash
bash -x myscript.sh
```
✅ **This shows command execution in real-time**  

---

### **3️⃣ Using `set -e` (Exit on Error)**  
If any command fails, the script **immediately exits**.  
```bash
#!/bin/bash
set -e  

echo "This will run"
wrong_command  # This command does not exist, script exits
echo "This will not run"
```
✅ **If `wrong_command` fails, the script stops execution.**  

---

### **4️⃣ Using `set -v` (Verbose Mode)**  
Displays each command **before execution** (including comments).  
```bash
#!/bin/bash
set -v
echo "Hello, Debugging!"
```

---

### **5️⃣ Redirecting Errors to a Log File**  
```bash
./myscript.sh 2> error.log
```
✅ **This saves all error messages to `error.log` for later analysis.**  

---

## **3. Common Debugging Issues & Fixes**  

| **Issue** | **Possible Fix** |
|-----------|----------------|
| `command not found` | Check for typos in command names |
| `Permission denied` | Use `chmod +x script.sh` to make the script executable |
| `unexpected token` | Check if brackets and quotes are properly closed |
| `file not found` | Verify if the file exists and the path is correct |
| `syntax error: unexpected end of file` | Ensure all `if`, `for`, or `while` blocks are properly closed |

---

## **4. Debugging Example**  
### **Script with a Bug**  
```bash
#!/bin/bash
echo "Enter your name: "
read name
echo "Hello, $nmae"  # Typo in variable name
```
✅ **Fix:** Change `$nmae` to `$name`  

### **Debugging with `bash -x`**
```bash
bash -x script.sh
```
✅ **Output:**  
```
+ read name
Ankita
+ echo 'Hello,'
Hello,
```
➡ **It shows that `$nmae` was not found, so the variable was empty.**  

---

# **Interview Questions & Answers**  

### **Beginner Level**  

**Q1: How do you enable debugging in a script?**  
✅ **A:** Use `set -x` inside the script or run it with `bash -x script.sh`.  

---

**Q2: What is the difference between `set -x` and `set -v`?**  
✅ **A:**  
| **Option** | **Function** |
|-----------|------------|
| `set -x` | Shows command execution after expansion |
| `set -v` | Shows raw command before execution |

---

### **Intermediate Level**  

**Q3: How can you stop script execution when an error occurs?**  
✅ **A:** Use `set -e` to exit on the first error.  

---

**Q4: How do you redirect script errors to a file?**  
✅ **A:**  
```bash
./script.sh 2> error.log
```
➡ This saves error messages to `error.log`.  

---

### **Advanced Level**  

**Q5: How do you debug a script without modifying it?**  
✅ **A:** Run the script with:  
```bash
bash -x script.sh
```

---

**Q6: What would cause a `command not found` error?**  
✅ **A:** Possible reasons:  
- Typo in command name  
- Missing executable permission (`chmod +x script.sh`)  
- Script not in the `$PATH`  

---

# **5. Summary**  
✔ Use `set -x` or `bash -x script.sh` for debugging.  
✔ Use `set -e` to stop on errors.  
✔ Redirect errors to a file using `2> error.log`.  
✔ Fix common issues like typos, permissions, and syntax errors.  

Would you like **real-world debugging scenarios** to practice?
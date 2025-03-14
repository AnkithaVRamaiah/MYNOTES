# **User Input and Output in Shell Scripting**  

## **1. Introduction**
User input and output (I/O) are essential in shell scripting to **interact with users**.  
- **User Input** → Takes data from the user using `read`.  
- **Output** → Displays data using `echo` or `printf`.

---

# **2. User Input in Shell Scripting**
### **🔹 Basic Input using `read`**
The `read` command is used to take input from the user.

**Syntax:**
```bash
read variable_name
```
**Example:**
```bash
echo "Enter your name:"
read name
echo "Hello, $name!"
```
✅ **Output:**
```
Enter your name:
Ankita
Hello, Ankita!
```

---

### **🔹 Prompting Input in the Same Line**
Instead of displaying a message on one line and taking input on another, use `-p`.

**Example:**
```bash
read -p "Enter your age: " age
echo "You are $age years old."
```
✅ **Output:**
```
Enter your age: 24
You are 24 years old.
```

---

### **🔹 Hiding Input (For Passwords)**
Use `-s` to hide input (useful for passwords).

**Example:**
```bash
read -s -p "Enter password: " password
echo
echo "Password saved!"
```
✅ **Output:**
```
Enter password: ****
Password saved!
```

---

### **🔹 Taking Multiple Inputs**
You can read multiple values at once.

**Example:**
```bash
read -p "Enter first name and last name: " first last
echo "First Name: $first"
echo "Last Name: $last"
```
✅ **Output:**
```
Enter first name and last name: Ankita V
First Name: Ankita
Last Name: V
```

---

### **🔹 Setting a Timeout for Input**
Use `-t` to set a timeout.

**Example:**
```bash
read -t 5 -p "Enter your city: " city
echo "You entered: $city"
```
✅ **Output (if no input in 5 seconds):**
```
Enter your city: 
```
(Timeout occurs, and it moves to the next command.)

---

### **🔹 Using Default Values**
If the user doesn’t enter input, set a default value.

**Example:**
```bash
read -p "Enter your country (default: India): " country
country=${country:-India}
echo "Country: $country"
```
✅ **Output (if no input):**
```
Enter your country (default: India): 
Country: India
```

---

### **🔹 Reading Input from a File**
You can use `<` to read input from a file.

**Example:**
```bash
read username < username.txt
echo "Welcome, $username!"
```

---

# **3. Output in Shell Scripting**
### **🔹 Displaying Output using `echo`**
The `echo` command prints text to the terminal.

**Example:**
```bash
echo "Hello, World!"
```
✅ **Output:**
```
Hello, World!
```

---

### **🔹 Using Escape Sequences**
Use `-e` to enable escape sequences.

| Escape Sequence | Description |
|----------------|-------------|
| `\n` | New line |
| `\t` | Tab space |
| `\\` | Backslash |

**Example:**
```bash
echo -e "Line1\nLine2"
echo -e "Name:\tAnkita"
```
✅ **Output:**
```
Line1
Line2
Name:    Ankita
```

---

### **🔹 Using `printf` for Formatted Output**
Unlike `echo`, `printf` gives better formatting.

**Syntax:**
```bash
printf "format-string" values
```

**Example:**
```bash
printf "Name: %s\nAge: %d\n" "Ankita" 24
```
✅ **Output:**
```
Name: Ankita
Age: 24
```

---

### **🔹 Redirecting Output to a File**
Use `>` to **overwrite** a file and `>>` to **append**.

**Example (overwrite):**
```bash
echo "This is a log entry" > logfile.txt
```
**Example (append):**
```bash
echo "New log entry" >> logfile.txt
```

---

### **🔹 Using `tee` to Display and Save Output**
**Example:**
```bash
echo "Logging this message" | tee logfile.txt
```
✅ **Output:**
```
Logging this message
```
(Also saves it in `logfile.txt`.)

---

# **4. Interview Questions & Answers**
### **Beginner Level**
**Q1: How do you take user input in a shell script?**  
✅ **A:** Use `read`:
```bash
read -p "Enter your name: " name
echo "Hello, $name!"
```

**Q2: How do you print a variable’s value?**  
✅ **A:** Use `echo`:
```bash
echo $name
```

**Q3: How do you print a new line using `echo`?**  
✅ **A:** Use `-e` and `\n`:
```bash
echo -e "Hello\nWorld"
```

**Q4: How do you hide input when taking user input?**  
✅ **A:** Use `read -s`:
```bash
read -s -p "Enter password: " pass
```

---

### **Intermediate Level**
**Q5: How do you set a default value if the user doesn’t enter anything?**  
✅ **A:** Use `${variable:-default}`:
```bash
read -p "Enter country: " country
country=${country:-India}
echo "Country: $country"
```

**Q6: How do you redirect output to a file?**  
✅ **A:** Use `>` for overwrite, `>>` for append:
```bash
echo "Hello" > file.txt   # Overwrites
echo "World" >> file.txt  # Appends
```

**Q7: How do you format output using `printf`?**  
✅ **A:**  
```bash
printf "Name: %s\nAge: %d\n" "Ankita" 24
```

---

### **Advanced Level**
**Q8: How do you set a timeout for user input?**  
✅ **A:** Use `-t`:
```bash
read -t 5 -p "Enter your name: " name
```

**Q9: What is the difference between `echo` and `printf`?**  
✅ **A:**  
| Feature  | `echo` | `printf` |
|----------|--------|----------|
| Simplicity | Simple | More control |
| Formatting | Limited | Advanced formatting |
| Escape sequences | Requires `-e` | Supports all |

**Q10: How do you take multiple inputs in one `read` command?**  
✅ **A:**  
```bash
read -p "Enter name and age: " name age
echo "Name: $name, Age: $age"
```

---

# **5. Summary**
✔ **`read`** for user input  
✔ **`echo` & `printf`** for output  
✔ **Taking multiple inputs**  
✔ **Setting default values**  
✔ **Hiding input for passwords**  
✔ **Redirecting output to files**  
✔ **Using `tee` to save and display output**  

Would you like code examples for any specific topic?
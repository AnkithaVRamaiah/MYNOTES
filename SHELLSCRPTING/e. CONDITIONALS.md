# **Conditional Statements in Shell Scripting**  

## **1. Introduction**  
Conditional statements in shell scripting help **make decisions** based on conditions.  
- **If condition is true** → Execute a set of commands.  
- **If condition is false** → Execute another set of commands.  

---

## **2. Types of Conditional Statements**  
1. `if` statement  
2. `if-else` statement  
3. `if-elif-else` statement  
4. `case` statement  

---

# **3. `if` Statement**  
The simplest conditional statement.  

**Syntax:**  
```bash
if [ condition ]; then
    commands
fi
```

**Example:**  
```bash
num=10
if [ $num -gt 5 ]; then
    echo "Number is greater than 5"
fi
```
✅ **Output:**  
```
Number is greater than 5
```

---

# **4. `if-else` Statement**  
Executes different commands based on the condition.

**Syntax:**  
```bash
if [ condition ]; then
    commands_if_true
else
    commands_if_false
fi
```

**Example:**  
```bash
age=18
if [ $age -ge 18 ]; then
    echo "You are an adult."
else
    echo "You are a minor."
fi
```
✅ **Output:**  
```
You are an adult.
```

---

# **5. `if-elif-else` Statement**  
Checks multiple conditions.

**Syntax:**  
```bash
if [ condition1 ]; then
    commands_if_condition1_is_true
elif [ condition2 ]; then
    commands_if_condition2_is_true
else
    commands_if_all_are_false
fi
```

**Example:**  
```bash
marks=75
if [ $marks -ge 90 ]; then
    echo "Grade: A"
elif [ $marks -ge 75 ]; then
    echo "Grade: B"
else
    echo "Grade: C"
fi
```
✅ **Output:**  
```
Grade: B
```

---

# **6. `case` Statement**  
Used when checking multiple values for a variable.

**Syntax:**  
```bash
case variable in
    value1) commands ;;
    value2) commands ;;
    *) default_commands ;;
esac
```

**Example:**  
```bash
echo "Enter a day:"
read day

case $day in
    Monday) echo "Start of the week!" ;;
    Friday) echo "Weekend is coming!" ;;
    Sunday) echo "It's a holiday!" ;;
    *) echo "It's a normal day." ;;
esac
```
✅ **Output:**  
```
Enter a day:
Friday
Weekend is coming!
```

---

# **7. Operators Used in Conditions**  

### **🔹 Comparison Operators (for Numbers)**  
| Operator | Meaning |
|----------|---------|
| `-eq` | Equal to |
| `-ne` | Not equal to |
| `-gt` | Greater than |
| `-ge` | Greater than or equal to |
| `-lt` | Less than |
| `-le` | Less than or equal to |

**Example:**  
```bash
if [ $num -gt 10 ]; then
    echo "Number is greater than 10"
fi
```

---

### **🔹 String Operators**  
| Operator | Meaning |
|----------|---------|
| `=` | Equal |
| `!=` | Not equal |
| `-z` | String is empty |
| `-n` | String is not empty |

**Example:**  
```bash
name="Ankita"
if [ "$name" = "Ankita" ]; then
    echo "Hello, Ankita!"
fi
```

---

### **🔹 Logical Operators**  
| Operator | Meaning |
|----------|---------|
| `&&` | AND (Both conditions must be true) |
| `||` | OR (At least one condition must be true) |
| `!` | NOT (Reverses condition) |

**Example:**  
```bash
age=20
if [ $age -ge 18 ] && [ $age -le 25 ]; then
    echo "You are a young adult."
fi
```

✅ **Output:**  
```
You are a young adult.
```

---

# **8. Interview Questions & Answers**  

### **Beginner Level**  
**Q1: What is an `if` statement in shell scripting?**  
✅ **A:** An `if` statement checks if a condition is true and executes commands accordingly.  

**Example:**  
```bash
if [ $num -gt 5 ]; then
    echo "Greater than 5"
fi
```

---

**Q2: What is the difference between `=` and `-eq`?**  
✅ **A:**  
- `=` is used for **string comparison**.  
- `-eq` is used for **numeric comparison**.  

**Example:**  
```bash
if [ "$name" = "Ankita" ]; then  # String comparison
if [ $num -eq 10 ]; then         # Numeric comparison
```

---

### **Intermediate Level**  
**Q3: How do you check if a file exists?**  
✅ **A:** Use `-e` flag.  
```bash
if [ -e file.txt ]; then
    echo "File exists"
fi
```

**Q4: How do you use `&&` (AND) in `if` condition?**  
✅ **A:**  
```bash
if [ $age -gt 18 ] && [ $age -lt 30 ]; then
    echo "Young adult"
fi
```

---

### **Advanced Level**  
**Q5: What is the difference between `if-elif-else` and `case`?**  
✅ **A:**  
- `if-elif-else` is used for **range-based conditions** (e.g., marks, age).  
- `case` is used for **matching exact values** (e.g., days of the week).  

**Example:**  
```bash
case $color in
    red) echo "Stop!" ;;
    green) echo "Go!" ;;
esac
```

---

# **9. Summary**  
✔ **`if`, `if-else`, `if-elif-else`, and `case` statements**  
✔ **Comparison, string, and logical operators**  
✔ **Checking files and directories**  
✔ **Common interview questions and examples**  

Would you like more examples on any topic?
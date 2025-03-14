# **Loops in Shell Scripting**  

## **1. Introduction**  
Loops in shell scripting **repeat a set of commands multiple times** until a condition is met. This helps automate repetitive tasks.  

---

## **2. Types of Loops in Shell Scripting**  
1. `for` loop  
2. `while` loop  
3. `until` loop  
4. `break` and `continue` (used to control loops)  

---

# **3. `for` Loop**  
Used to iterate over a range or a list of values.  

### **Syntax:**  
```bash
for variable in list; do
    commands
done
```

### **Example 1: Loop through a list**  
```bash
for name in Alice Bob Charlie; do
    echo "Hello, $name"
done
```
✅ **Output:**  
```
Hello, Alice
Hello, Bob
Hello, Charlie
```

---

### **Example 2: Loop with a range of numbers**  
```bash
for i in {1..5}; do
    echo "Number: $i"
done
```
✅ **Output:**  
```
Number: 1
Number: 2
Number: 3
Number: 4
Number: 5
```

---

# **4. `while` Loop**  
Repeats a set of commands **as long as the condition is true**.  

### **Syntax:**  
```bash
while [ condition ]; do
    commands
done
```

### **Example: Print numbers from 1 to 5**  
```bash
i=1
while [ $i -le 5 ]; do
    echo "Count: $i"
    ((i++))
done
```
✅ **Output:**  
```
Count: 1
Count: 2
Count: 3
Count: 4
Count: 5
```

---

# **5. `until` Loop**  
Repeats commands **until** a condition becomes true.  

### **Syntax:**  
```bash
until [ condition ]; do
    commands
done
```

### **Example: Print numbers from 1 to 5**  
```bash
i=1
until [ $i -gt 5 ]; do
    echo "Count: $i"
    ((i++))
done
```
✅ **Output:**  
```
Count: 1
Count: 2
Count: 3
Count: 4
Count: 5
```
➡ **Difference between `while` and `until`?**  
- **`while` runs while the condition is true.**  
- **`until` runs until the condition becomes true.**

---

# **6. `break` and `continue` in Loops**  
Used to control loop execution.  

## **🔹 `break` – Stop the loop immediately**  
```bash
for i in {1..5}; do
    if [ $i -eq 3 ]; then
        break
    fi
    echo "Number: $i"
done
```
✅ **Output:**  
```
Number: 1
Number: 2
```
➡ Loop **stops** when `i` is 3.  

---

## **🔹 `continue` – Skip the current iteration**  
```bash
for i in {1..5}; do
    if [ $i -eq 3 ]; then
        continue
    fi
    echo "Number: $i"
done
```
✅ **Output:**  
```
Number: 1
Number: 2
Number: 4
Number: 5
```
➡ **3 is skipped, but the loop continues.**  

---

# **7. Interview Questions & Answers**  

### **Beginner Level**  
**Q1: What is a loop in shell scripting?**  
✅ **A:** A loop is used to **repeat** a set of commands multiple times until a condition is met.  

---

**Q2: What is the difference between `while` and `until` loops?**  
✅ **A:**  
- `while` runs **while** the condition is true.  
- `until` runs **until** the condition becomes true.  

**Example:**  
```bash
# while loop
i=1
while [ $i -le 5 ]; do
    echo "While Count: $i"
    ((i++))
done
```
```bash
# until loop
i=1
until [ $i -gt 5 ]; do
    echo "Until Count: $i"
    ((i++))
done
```

---

### **Intermediate Level**  
**Q3: How do you loop through files in a directory?**  
✅ **A:** Use a `for` loop.  
```bash
for file in *.txt; do
    echo "File: $file"
done
```

---

**Q4: How do you read a file line by line using a loop?**  
✅ **A:** Use `while` loop with `read`.  
```bash
while read line; do
    echo "$line"
done < myfile.txt
```

---

### **Advanced Level**  
**Q5: What happens if a loop runs indefinitely?**  
✅ **A:** It creates an **infinite loop**, which can crash the system if not stopped.  

**Example of an infinite loop:**  
```bash
while true; do
    echo "Running..."
done
```
➡ **To stop the loop, press `Ctrl + C`**  

---

**Q6: What is the use of `break` and `continue` in loops?**  
✅ **A:**  
- `break` **stops** the loop immediately.  
- `continue` **skips** the current iteration and moves to the next.  

**Example:**  
```bash
for i in {1..5}; do
    if [ $i -eq 3 ]; then
        break  # Stops loop when i is 3
    fi
    echo "Number: $i"
done
```

---

# **8. Summary**  
✔ **`for`, `while`, `until` loops**  
✔ **`break` to stop the loop, `continue` to skip an iteration**  
✔ **Loops for file processing and reading input**  
✔ **Common interview questions and answers**  

Would you like more examples?
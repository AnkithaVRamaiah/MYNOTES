# **Everything About Variables in Shell Scripting**  

## **1. Introduction to Variables in Shell Scripting**
Variables in shell scripting store values that can be reused. They make scripts **dynamic and flexible** by allowing data to be assigned and used multiple times.

---

## **2. Declaring and Using Variables**
### **🔹 Syntax:**
```bash
variable_name=value
```
- No spaces around `=`
- Variable names are case-sensitive (`NAME` ≠ `name`)
- By default, variables are **local to the script**

### **🔹 Example:**
```bash
name="Ankita"
echo "My name is $name"
```
✅ **Output:**
```
My name is Ankita
```

💡 **Using `{}` to avoid confusion:**
```bash
num=10
echo "The number is ${num}0"  # Correct
```

---

## **3. Types of Variables**
### **1️⃣ User-Defined Variables**
- Created and used within the script.
- Lost when the script ends.

**Example:**
```bash
greeting="Hello, World!"
echo $greeting
```

---

### **2️⃣ Environment Variables**
- System-wide variables available to all processes.
- Examples: `PATH`, `HOME`, `USER`, `SHELL`

**Example:**
```bash
echo $HOME  # Shows home directory
echo $USER  # Shows current username
```

💡 **How to list all environment variables?**
```bash
printenv
```

💡 **How to create a permanent environment variable?**
```bash
export MY_VAR="Persistent Value"
```
(Temporary; lost when the session ends.)

To make it **permanent**, add `export MY_VAR="Persistent Value"` to `~/.bashrc` or `~/.bash_profile`.

---

### **3️⃣ Special Variables (Shell Script Arguments)**
Used to **pass arguments** to a script.

| Variable  | Description |
|-----------|------------|
| `$0` | Script name |
| `$1, $2, $3...` | Positional parameters (arguments) |
| `$#` | Number of arguments |
| `$@` | All arguments as a list |
| `$$` | Current process ID (PID) |
| `$?` | Exit status of the last command (0 = success, non-zero = failure) |

**Example:**
```bash
#!/bin/bash
echo "Script Name: $0"
echo "First Argument: $1"
echo "Second Argument: $2"
echo "Total Arguments: $#"
```
Run the script:
```bash
bash script.sh Hello World
```
✅ **Output:**
```
Script Name: script.sh
First Argument: Hello
Second Argument: World
Total Arguments: 2
```

---

## **4. Reading User Input**
We use the `read` command to take input from users.

**Example:**
```bash
#!/bin/bash
echo "Enter your name:"
read user_name
echo "Hello, $user_name!"
```

✅ **Output:**
```
Enter your name:
Ankita
Hello, Ankita!
```

💡 **Using `-p` to prompt in the same line:**
```bash
read -p "Enter your age: " age
echo "Your age is $age"
```

💡 **Hiding input (e.g., passwords):**
```bash
read -s -p "Enter password: " password
echo "Password saved!"
```

---

## **5. Constants (Readonly Variables)**
To make a variable **unchangeable**, use `readonly`.

**Example:**
```bash
name="Ankita"
readonly name
name="NewName"  # This will cause an error
```

✅ **Output:**
```
bash: name: readonly variable
```

---

## **6. Variable Operations**
### **🔹 Arithmetic Operations**
Use `let`, `expr`, `(( ))`, or `$(( ))` for calculations.

```bash
num1=10
num2=5

# Method 1: Using expr
sum=`expr $num1 + $num2`
echo "Sum: $sum"

# Method 2: Using (( ))
diff=$(( num1 - num2 ))
echo "Difference: $diff"

# Method 3: Using let
let mul=num1*num2
echo "Multiplication: $mul"
```

✅ **Output:**
```
Sum: 15
Difference: 5
Multiplication: 50
```

---

## **7. String Operations**
### **🔹 Concatenation**
```bash
str1="Hello"
str2="World"
str3="$str1 $str2"
echo $str3  # Output: Hello World
```

### **🔹 Length of a String**
```bash
text="ShellScripting"
echo "Length: ${#text}"
```
✅ **Output:** `Length: 14`

### **🔹 Extract Substring**
```bash
echo ${text:0:5}  # Output: Shell (First 5 characters)
```

---

## **8. Interview Questions & Answers**
### **Beginner Level**
**Q1: What is a variable in shell scripting?**  
✅ **A:** A variable is a name that stores a value, which can be used later in the script.

**Q2: How do you assign and access a variable in a shell script?**  
✅ **A:**  
```bash
name="Ankita"  # Assign
echo $name      # Access
```

**Q3: What is the difference between `$@` and `$*`?**  
✅ **A:**  
- `$@` treats arguments **individually**.  
- `$*` treats all arguments as **one single string**.  

Example:
```bash
#!/bin/bash
echo "Using \"\$@\":"
for arg in "$@"; do echo "$arg"; done

echo "Using \"\$*\":"
for arg in "$*"; do echo "$arg"; done
```

**Q4: How do you read user input in a shell script?**  
✅ **A:**  
```bash
read -p "Enter your name: " name
echo "Hello, $name!"
```

---

### **Intermediate Level**
**Q5: How do you declare a constant in shell scripting?**  
✅ **A:**  
```bash
readonly PI=3.14
```

**Q6: What command prints all environment variables?**  
✅ **A:** `printenv`

**Q7: How do you perform arithmetic operations in shell scripts?**  
✅ **A:**  
```bash
num1=10
num2=5
sum=$(( num1 + num2 ))
echo "Sum: $sum"
```

---

### **Advanced Level**
**Q8: How do you extract a substring in a shell script?**  
✅ **A:**  
```bash
text="ShellScripting"
echo ${text:0:5}  # Output: Shell
```

**Q9: How do you make a variable available to other scripts?**  
✅ **A:** Use `export`:  
```bash
export MY_VAR="Hello"
```
Other scripts can now use `$MY_VAR`.

**Q10: What is the difference between local and global variables?**  
✅ **A:**  
- **Local variables** exist only inside a script/function.  
- **Global variables** are available system-wide (`export` makes them global).  

Example:
```bash
function test() {
  local my_var="Inside Function"
  echo $my_var
}
test
echo $my_var  # Won't print anything
```

---

## **9. Summary**
✔ **Declaring and using variables**  
✔ **Types: User-defined, environment, special variables**  
✔ **Reading user input**  
✔ **Making variables constant (`readonly`)**  
✔ **String and arithmetic operations**  
✔ **Common interview questions**  

Would you like examples for any specific topic?
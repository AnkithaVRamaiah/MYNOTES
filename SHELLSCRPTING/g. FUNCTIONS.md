# **Functions in Shell Scripting**  

## **1. Introduction**  
A function in shell scripting is **a block of reusable code** that performs a specific task. Instead of writing the same code multiple times, we define a function and call it whenever needed.  

### **Why use functions?**  
✅ Makes scripts modular and readable  
✅ Avoids code repetition  
✅ Easy to debug and maintain  

---

## **2. How to Define and Call a Function**  

### **Syntax:**  
```bash
function function_name() {
    commands
}
```
or  
```bash
function_name() {
    commands
}
```

---

## **3. Basic Function Example**  

```bash
greet() {
    echo "Hello, Welcome to Shell Scripting!"
}

# Calling the function
greet
```
✅ **Output:**  
```
Hello, Welcome to Shell Scripting!
```

---

## **4. Function with Arguments**  
We can pass arguments to a function using **$1, $2, $3, ...**  

```bash
greet_user() {
    echo "Hello, $1!"
}

# Calling the function with an argument
greet_user Ankita
```
✅ **Output:**  
```
Hello, Ankita!
```

➡ `$1` refers to the first argument (`Ankita`).  

---

## **5. Function with Multiple Arguments**  

```bash
add_numbers() {
    sum=$(( $1 + $2 ))
    echo "Sum: $sum"
}

# Calling the function with two arguments
add_numbers 5 10
```
✅ **Output:**  
```
Sum: 15
```

➡ `$1` refers to `5`, `$2` refers to `10`.  

---

## **6. Returning Values from a Function**  
A function can return an exit status (0 for success, non-zero for failure).  

```bash
is_even() {
    if (( $1 % 2 == 0 )); then
        return 0  # Success (Even)
    else
        return 1  # Failure (Odd)
    fi
}

# Calling the function
is_even 4
if [ $? -eq 0 ]; then
    echo "Number is even."
else
    echo "Number is odd."
fi
```
✅ **Output:**  
```
Number is even.
```

➡ `$?` stores the exit status of the last command.  

---

## **7. Function with Local Variables**  
Use `local` to define variables **inside** a function so they don’t affect the rest of the script.  

```bash
calculate_square() {
    local num=$1
    local square=$(( num * num ))
    echo "Square of $num is $square"
}

calculate_square 6
```
✅ **Output:**  
```
Square of 6 is 36
```
➡ `local` ensures `num` and `square` exist only inside the function.  

---

## **8. Calling a Function in a Loop**  
We can call a function inside a loop for repeated execution.  

```bash
print_numbers() {
    echo "Number: $1"
}

for i in {1..5}; do
    print_numbers $i
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

## **9. Recursive Functions (Calling a Function Inside Itself)**  
A function can call itself to perform **recursion**.  

```bash
factorial() {
    if [ $1 -eq 1 ]; then
        echo 1
    else
        prev=$(factorial $(( $1 - 1 )))
        echo $(( $1 * prev ))
    fi
}

# Calling the function
factorial 5
```
✅ **Output:**  
```
120
```

➡ **Explanation:**  
- `factorial(5) = 5 * factorial(4)`  
- `factorial(4) = 4 * factorial(3)` ... and so on.  

---

# **10. Interview Questions & Answers**  

### **Beginner Level**  

**Q1: What is a function in shell scripting?**  
✅ **A:** A function is a **block of reusable code** that performs a specific task. It helps avoid repetition and improves script structure.  

---

**Q2: How do you define and call a function in shell scripting?**  
✅ **A:**  

```bash
my_function() {
    echo "This is a function"
}

my_function  # Calling the function
```

---

**Q3: How do you pass arguments to a function?**  
✅ **A:**  

```bash
greet() {
    echo "Hello, $1!"
}

greet Ankita
```
➡ `$1` refers to the first argument (`Ankita`).  

---

### **Intermediate Level**  

**Q4: What is the difference between global and local variables in functions?**  
✅ **A:**  
- **Global variables** can be accessed **anywhere** in the script.  
- **Local variables** (declared with `local`) exist **only inside the function**.  

Example:  
```bash
my_function() {
    local name="Ankita"
    echo "Inside function: $name"
}

my_function
echo "Outside function: $name"  # This will be empty
```

---

**Q5: How do you return a value from a function?**  
✅ **A:** Use `return` for exit status and `echo` for actual values.  

```bash
get_square() {
    echo $(( $1 * $1 ))
}

square=$(get_square 4)
echo "Square: $square"
```
✅ **Output:**  
```
Square: 16
```

---

### **Advanced Level**  

**Q6: Can you create a recursive function in shell scripting?**  
✅ **A:** Yes, a function can call itself.  

Example:  
```bash
countdown() {
    if [ $1 -eq 0 ]; then
        echo "Done!"
    else
        echo "$1"
        countdown $(( $1 - 1 ))
    fi
}

countdown 5
```

✅ **Output:**  
```
5
4
3
2
1
Done!
```

---

**Q7: How do you use a function inside a loop?**  
✅ **A:**  

```bash
print_num() {
    echo "Number: $1"
}

for i in {1..3}; do
    print_num $i
done
```
✅ **Output:**  
```
Number: 1
Number: 2
Number: 3
```

---

# **11. Summary**  
✔ **Functions make scripts modular and reusable**  
✔ **Arguments are passed using `$1, $2, ...`**  
✔ **`local` defines function-specific variables**  
✔ **Use `return` for exit status and `echo` for output**  
✔ **Functions can be used in loops and recursion**  

Would you like additional real-world examples?
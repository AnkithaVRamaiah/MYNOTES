# **Arrays in Shell Scripting**  

## **1. Introduction to Arrays**  
An **array** is a collection of values stored under a **single variable name**, where each value is accessed using an index.  

✅ **Why use arrays in shell scripting?**  
- Store multiple values in a single variable  
- Access and manipulate data efficiently  
- Simplify handling of lists (e.g., filenames, numbers, strings)  

---

## **2. Declaring and Initializing Arrays**  

### **Syntax:**  
```bash
array_name=(value1 value2 value3 ...)
```

### **Example:**  
```bash
fruits=("Apple" "Banana" "Mango" "Orange")
```

➡ Stores 4 fruit names in a single variable called `fruits`.

---

## **3. Accessing Array Elements**  

Use **index numbers** starting from `0`.  

```bash
echo "${fruits[0]}"   # Apple
echo "${fruits[2]}"   # Mango
```

➡ `"${array_name[index]}"` is used to get the value at a specific index.

---

## **4. Display All Elements of an Array**  

```bash
echo "${fruits[@]}"  
```
✅ **Output:**  
```
Apple Banana Mango Orange
```
➡ `"${array_name[@]}"` retrieves all elements.  

---

## **5. Finding the Length of an Array**  

```bash
echo "${#fruits[@]}"
```
✅ **Output:**  
```
4
```
➡ `"${#array_name[@]}"` gives the number of elements in the array.

---

## **6. Adding Elements to an Array**  

```bash
fruits+=("Grapes")
echo "${fruits[@]}"
```
✅ **Output:**  
```
Apple Banana Mango Orange Grapes
```
➡ `+=` adds a new element to the array.

---

## **7. Updating an Array Element**  

```bash
fruits[1]="Blueberry"
echo "${fruits[@]}"
```
✅ **Output:**  
```
Apple Blueberry Mango Orange Grapes
```
➡ The second element (`index 1`) is updated from `Banana` to `Blueberry`.

---

## **8. Removing an Element from an Array**  

```bash
unset fruits[2]
echo "${fruits[@]}"
```
✅ **Output:**  
```
Apple Blueberry Orange Grapes
```
➡ `"unset array_name[index]"` removes an element but does not shift indexes.

---

## **9. Looping Through an Array**  

### **Using a `for` loop**  
```bash
for fruit in "${fruits[@]}"; do
    echo "$fruit"
done
```
✅ **Output:**  
```
Apple
Blueberry
Orange
Grapes
```

➡ Iterates over each element in the array.

---

## **10. Indexed vs. Associative Arrays**  

### **Indexed Array (Default Type)**  
```bash
numbers=(10 20 30 40)
echo "${numbers[1]}"  # 20
```

### **Associative Array (Key-Value Pairs) - Bash 4+ Only**  
```bash
declare -A user
user[name]="Ankita"
user[role]="DevOps Engineer"

echo "${user[name]}"  # Ankita
echo "${user[role]}"  # DevOps Engineer
```
➡ Associative arrays require `declare -A`.

---

# **Interview Questions & Answers**  

### **Beginner Level**  

**Q1: What is an array in shell scripting?**  
✅ **A:** An array is a collection of values stored in a **single variable**, accessed using an index.  

---

**Q2: How do you declare and initialize an array?**  
✅ **A:**  
```bash
fruits=("Apple" "Banana" "Mango")
```

---

**Q3: How do you access a specific element in an array?**  
✅ **A:**  
```bash
echo "${fruits[1]}"  # Accesses the second element (Banana)
```

---

**Q4: How do you find the length of an array?**  
✅ **A:**  
```bash
echo "${#fruits[@]}"  # Returns the number of elements
```

---

### **Intermediate Level**  

**Q5: How do you add an element to an array?**  
✅ **A:**  
```bash
fruits+=("Grapes")
```

---

**Q6: How do you remove an element from an array?**  
✅ **A:**  
```bash
unset fruits[2]  # Removes the third element
```

---

**Q7: How do you loop through an array?**  
✅ **A:**  
```bash
for fruit in "${fruits[@]}"; do
    echo "$fruit"
done
```

---

### **Advanced Level**  

**Q8: What is the difference between an indexed and an associative array?**  
✅ **A:**  
| Indexed Arrays  | Associative Arrays  |
|----------------|----------------|
| Uses numeric index (0, 1, 2...)  | Uses key-value pairs (`user[name]`)  |
| Default in Bash  | Requires `declare -A` (Bash 4+)  |

---

**Q9: Can you pass an array to a function?**  
✅ **A:** Yes, but it must be passed as arguments.  
```bash
print_array() {
    for value in "$@"; do
        echo "$value"
    done
}

print_array "${fruits[@]}"
```

---

# **11. Summary**  
✔ Arrays store multiple values in a single variable.  
✔ Access elements using `${array[index]}`.  
✔ Use `"${array[@]}"` to get all elements.  
✔ Use `unset` to delete elements.  
✔ Loop through arrays using `for` loops.  
✔ Indexed arrays use numbers, while associative arrays use key-value pairs.  

Would you like some **real-world use cases** of arrays in shell scripting?
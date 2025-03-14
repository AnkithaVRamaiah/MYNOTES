# **String Manipulations in Shell Scripting**  

## **1. Introduction to Strings in Shell Scripting**  
A **string** is a sequence of characters. In shell scripting, strings are used to store and manipulate text data.  

✅ **Why is string manipulation important?**  
- Extract information from text  
- Modify content dynamically  
- Automate text processing tasks  

---

## **2. Declaring and Assigning Strings**  

```bash
name="Ankita"
message="Welcome to DevOps"
```
➡ Strings are assigned using `=` **without spaces** on either side.

---

## **3. Finding the Length of a String**  

```bash
echo ${#name}
```
✅ **Output:**  
```
6
```
➡ `"${#variable}"` gives the length of the string.

---

## **4. Extracting a Substring**  

```bash
message="Hello DevOps Engineers"
echo ${message:6:6}
```
✅ **Output:**  
```
DevOps
```
➡ `${variable:start_position:length}` extracts part of a string.

---

## **5. Replacing a Substring**  

```bash
str="I love Python"
echo ${str/Python/Bash}
```
✅ **Output:**  
```
I love Bash
```
➡ `${variable/old_value/new_value}` replaces **first occurrence**.  
➡ Use `${variable//old_value/new_value}` to replace **all occurrences**.

---

## **6. Extracting a String Before or After a Character**  

### **Extracting Before a Character (`%` operator)**
```bash
file="document.txt"
echo ${file%.txt}
```
✅ **Output:**  
```
document
```
➡ Removes `.txt` from the end.

### **Extracting After a Character (`#` operator)**
```bash
url="https://example.com"
echo ${url#https://}
```
✅ **Output:**  
```
example.com
```
➡ Removes `https://` from the beginning.

---

## **7. Changing String Case (Upper/Lowercase) – Requires Bash 4+**  

### **Convert to Uppercase**  
```bash
name="ankita"
echo "${name^^}"
```
✅ **Output:**  
```
ANKITA
```

### **Convert to Lowercase**  
```bash
name="ANKITA"
echo "${name,,}"
```
✅ **Output:**  
```
ankita
```
➡ Use `^^` for uppercase, `,,` for lowercase.

---

## **8. Concatenating (Joining) Strings**  

```bash
greeting="Hello"
name="Ankita"
full_message="$greeting, $name!"
echo "$full_message"
```
✅ **Output:**  
```
Hello, Ankita!
```
➡ Strings are joined using `"variable1 variable2"`.

---

## **9. Checking if a String Contains a Substring**  

```bash
str="DevOps is amazing"
if [[ "$str" == *"DevOps"* ]]; then
    echo "Substring found!"
else
    echo "Substring not found!"
fi
```
✅ **Output:**  
```
Substring found!
```
➡ `*substring*` checks if a string contains another string.

---

## **10. Removing Leading and Trailing Spaces**  

```bash
input="  Hello  "
trimmed=$(echo "$input" | xargs)
echo "$trimmed"
```
✅ **Output:**  
```
Hello
```
➡ `xargs` removes **leading and trailing** spaces.

---

# **Interview Questions & Answers**  

### **Beginner Level**  

**Q1: How do you find the length of a string in shell scripting?**  
✅ **A:**  
```bash
str="DevOps"
echo ${#str}  # Output: 6
```

---

**Q2: How do you extract a substring from a string?**  
✅ **A:**  
```bash
text="Hello DevOps"
echo ${text:6:6}  # Output: DevOps
```

---

**Q3: How do you replace a word in a string?**  
✅ **A:**  
```bash
str="I love Python"
echo ${str/Python/Bash}  # Output: I love Bash
```

---

### **Intermediate Level**  

**Q4: How do you check if a string contains a specific word?**  
✅ **A:**  
```bash
str="Shell scripting is powerful"
if [[ "$str" == *"scripting"* ]]; then
    echo "Word found!"
fi
```

---

**Q5: How do you convert a string to uppercase?**  
✅ **A:**  
```bash
text="devops"
echo "${text^^}"  # Output: DEVOPS
```

---

### **Advanced Level**  

**Q6: What is the difference between `#` and `%` in string manipulation?**  
✅ **A:**  
| Operator | Description | Example | Output |
|----------|------------|---------|--------|
| `#` | Removes from the beginning | `"${url#https://}"` | `example.com` |
| `%` | Removes from the end | `"${file%.txt}"` | `document` |

---

**Q7: How do you remove all occurrences of a word in a string?**  
✅ **A:**  
```bash
text="I love love DevOps"
echo ${text//love/}  # Output: I  DevOps
```

---

# **11. Summary**  
✔ Strings are declared using `variable="text"`.  
✔ `"${#variable}"` gets the string length.  
✔ `"${variable:start:length}"` extracts a substring.  
✔ `"${variable/old/new}"` replaces text.  
✔ `"${variable^^}"` converts to uppercase.  
✔ `"${variable,,}"` converts to lowercase.  
✔ `"${variable#prefix}"` removes from the beginning.  
✔ `"${variable%suffix}"` removes from the end.  

Would you like **practical exercises** to practice string manipulation?
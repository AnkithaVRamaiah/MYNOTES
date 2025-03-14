# **File Handling and Transcripting in Shell Scripting**  

## **1. Introduction to File Handling**  
File handling in shell scripting allows you to **create, read, write, append, and delete** files. This is useful for automating tasks like logging, data processing, and configuration management.  

✅ **Why is file handling important?**  
- Automates file operations  
- Helps in log management  
- Simplifies data extraction and processing  

---

## **2. Creating a File**  

### **Using `touch` Command**  
```bash
touch myfile.txt
```
✅ **Creates an empty file named `myfile.txt`**  

### **Using `echo` Command**  
```bash
echo "Hello, DevOps!" > file.txt
```
✅ **Creates `file.txt` and writes "Hello, DevOps!"**  

### **Using `cat` Command**  
```bash
cat > myfile.txt
```
Type some content and press `Ctrl + D` to save.  

---

## **3. Reading a File**  

### **Using `cat` Command**  
```bash
cat myfile.txt
```
✅ **Displays the file content**  

### **Using `less` and `more` Commands**  
```bash
less myfile.txt
more myfile.txt
```
✅ **Used for reading large files page by page**  

### **Using `while` Loop**  
```bash
while read line; do
    echo "$line"
done < myfile.txt
```
✅ **Reads file line by line**  

---

## **4. Writing to a File**  

### **Overwriting a File (`>` operator)**  
```bash
echo "New content" > file.txt
```
✅ **Replaces existing content with "New content"**  

### **Appending to a File (`>>` operator)**  
```bash
echo "Appended line" >> file.txt
```
✅ **Adds "Appended line" at the end of `file.txt`**  

---

## **5. Deleting a File**  
```bash
rm myfile.txt
```
✅ **Deletes `myfile.txt`**  

---

## **6. Checking if a File Exists**  
```bash
if [ -f myfile.txt ]; then
    echo "File exists"
else
    echo "File does not exist"
fi
```
✅ **Checks if `myfile.txt` exists**  

---

## **7. Counting Lines, Words, and Characters**  
```bash
wc -l myfile.txt   # Count lines  
wc -w myfile.txt   # Count words  
wc -c myfile.txt   # Count characters  
```

---

## **8. Searching for a Word in a File**  

```bash
grep "DevOps" myfile.txt
```
✅ **Searches for "DevOps" in `myfile.txt`**  

---

## **9. Transcripting in Shell Scripting**  
Transcripting means **recording everything that happens in a shell session** into a file.  

### **Starting a Transcript (`script` command)**  
```bash
script mylog.txt
```
➡ Everything typed in the terminal is recorded in `mylog.txt`.  

### **Stopping a Transcript**  
```bash
exit
```
✅ **Stops recording and saves `mylog.txt`**  

---

# **Interview Questions & Answers**  

### **Beginner Level**  

**Q1: How do you create a file using a shell script?**  
✅ **A:**  
```bash
touch myfile.txt  # Creates an empty file
echo "Hello" > myfile.txt  # Creates a file and writes to it
```

---

**Q2: How do you read a file line by line in a shell script?**  
✅ **A:**  
```bash
while read line; do
    echo "$line"
done < myfile.txt
```

---

**Q3: What is the difference between `>` and `>>`?**  
✅ **A:**  
| Operator | Function | Example |
|----------|----------|---------|
| `>` | Overwrites file | `echo "New" > file.txt` |
| `>>` | Appends to file | `echo "More" >> file.txt` |

---

### **Intermediate Level**  

**Q4: How do you check if a file exists in a script?**  
✅ **A:**  
```bash
if [ -f file.txt ]; then
    echo "File exists"
else
    echo "File not found"
fi
```

---

**Q5: How do you search for a specific word in a file?**  
✅ **A:**  
```bash
grep "word" myfile.txt
```

---

### **Advanced Level**  

**Q6: How do you count the number of words in a file?**  
✅ **A:**  
```bash
wc -w myfile.txt
```

---

**Q7: What is a transcript in shell scripting?**  
✅ **A:** Transcripting records the entire terminal session into a file using the `script` command.

---

# **10. Summary**  
✔ Use `touch` or `echo` to create files.  
✔ Use `cat`, `less`, or `more` to read files.  
✔ Use `>` to overwrite and `>>` to append data.  
✔ Use `rm` to delete files.  
✔ Use `if [ -f file ]` to check if a file exists.  
✔ Use `grep` for searching text in a file.  
✔ Use `script` to record terminal sessions.  

Would you like **practical exercises** to test file handling?
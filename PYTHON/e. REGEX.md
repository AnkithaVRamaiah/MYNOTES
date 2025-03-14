# **Regular Expressions and String Manipulation in Python**  

Regular expressions (**regex**) and string manipulation are essential for handling text data in Python. They help in searching, extracting, modifying, and validating strings efficiently.  

---

# **1. String Manipulation in Python**  

Python provides several built-in methods to manipulate strings.  

## **1.1 String Basics**  
```python
# Creating a string
text = "Hello, Python!"
print(text)  # Output: Hello, Python!

# Accessing characters
print(text[0])   # Output: H
print(text[-1])  # Output: !

# Slicing
print(text[0:5])  # Output: Hello
print(text[:5])   # Output: Hello
print(text[7:])   # Output: Python!

# String length
print(len(text))  # Output: 14
```

---

## **1.2 String Methods**  
Python provides various built-in methods for string manipulation.

### **1.2.1 Changing Case**  
```python
text = "Hello, Python!"

print(text.upper())  # Output: HELLO, PYTHON!
print(text.lower())  # Output: hello, python!
print(text.title())  # Output: Hello, Python!
print(text.capitalize())  # Output: Hello, python!
```

### **1.2.2 Removing Whitespace**  
```python
text = "  Hello, Python!  "
print(text.strip())  # Output: "Hello, Python!" (Removes spaces from both sides)
print(text.lstrip()) # Output: "Hello, Python!  " (Left strip)
print(text.rstrip()) # Output: "  Hello, Python!" (Right strip)
```

### **1.2.3 Finding and Replacing**  
```python
text = "Hello, Python! Python is fun."

print(text.find("Python"))  # Output: 7 (Index of first occurrence)
print(text.replace("Python", "Java"))  # Output: Hello, Java! Java is fun.
```

### **1.2.4 Splitting and Joining**  
```python
text = "apple,banana,grape"
words = text.split(",")  # Splitting a string into a list
print(words)  # Output: ['apple', 'banana', 'grape']

joined_text = "-".join(words)  # Joining list elements into a string
print(joined_text)  # Output: apple-banana-grape
```

### **1.2.5 Checking Substrings**  
```python
text = "Hello, Python!"

print("Python" in text)   # Output: True
print("Java" not in text) # Output: True
```

---

# **2. Regular Expressions (Regex) in Python**  

Regular expressions (**regex**) are used for searching and manipulating text patterns. Python provides the **`re`** module for regex operations.  

```python
import re
```

---

## **2.1 Basic Regex Functions**  

### **2.1.1 `re.search()` – Find First Match**
Finds the first occurrence of a pattern in a string.  
```python
import re

text = "Hello, my number is 9876543210."
match = re.search(r"\d+", text)  # Finds the first number in the text

if match:
    print("Found:", match.group())  # Output: 9876543210
```

### **2.1.2 `re.findall()` – Find All Matches**
Returns a list of all occurrences of a pattern.  
```python
text = "Contact: 9876543210, 9123456789"
numbers = re.findall(r"\d+", text)  # Find all numbers

print(numbers)  # Output: ['9876543210', '9123456789']
```

### **2.1.3 `re.sub()` – Replace Matches**
Replaces occurrences of a pattern with another string.  
```python
text = "I like Python and Python is great!"
new_text = re.sub(r"Python", "Java", text)

print(new_text)  # Output: I like Java and Java is great!
```

### **2.1.4 `re.split()` – Split by Pattern**
Splits a string wherever the pattern matches.  
```python
text = "apple, banana; grape|mango"
words = re.split(r"[,;|]", text)

print(words)  # Output: ['apple', ' banana', ' grape', 'mango']
```

---

## **2.2 Regex Metacharacters and Special Sequences**  

| Symbol | Meaning | Example | Matches |
|--------|---------|---------|---------|
| `.`    | Any character except newline | `h.t` | `hat, hit, hot` |
| `^`    | Start of string | `^Hello` | `Hello world!` |
| `$`    | End of string | `Python$` | `I love Python` |
| `*`    | 0 or more occurrences | `ab*c` | `ac, abc, abbc` |
| `+`    | 1 or more occurrences | `ab+c` | `abc, abbc` |
| `?`    | 0 or 1 occurrence | `colou?r` | `color, colour` |
| `{n}`  | Exactly n occurrences | `\d{3}` | `123` (Matches 3-digit numbers) |
| `{n,}` | n or more occurrences | `\d{2,}` | `12, 123, 1234` |
| `{n,m}`| Between n and m occurrences | `\d{2,4}` | `12, 123, 1234` |
| `\d`   | Digit (0-9) | `\d+` | `123, 4567` |
| `\D`   | Non-digit | `\D+` | `abc, Hello!` |
| `\w`   | Word character (A-Z, a-z, 0-9, _) | `\w+` | `Python, hello_123` |
| `\W`   | Non-word character | `\W+` | `!@#%` |
| `\s`   | Whitespace | `\s+` | Matches spaces, tabs |
| `\S`   | Non-whitespace | `\S+` | Matches words |

---

## **2.3 Practical Examples**  

### **2.3.1 Validating an Email Address**  
```python
import re

email = "test.email@example.com"
pattern = r"^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$"

if re.match(pattern, email):
    print("Valid Email")
else:
    print("Invalid Email")
```

### **2.3.2 Extracting Phone Numbers**  
```python
text = "My phone numbers are 9876543210 and 9123456789."
phone_numbers = re.findall(r"\b\d{10}\b", text)

print(phone_numbers)  # Output: ['9876543210', '9123456789']
```

### **2.3.3 Extracting URLs from Text**  
```python
text = "Visit https://google.com or http://example.com for more info."
urls = re.findall(r"https?://[a-zA-Z0-9./]+", text)

print(urls)  # Output: ['https://google.com', 'http://example.com']
```

---

# **3. Summary**  
✅ **String Manipulation**  
- **String slicing, case conversion, find, replace, split, join, strip**  
- **Checking substrings (`in`, `not in`)**  

✅ **Regular Expressions (Regex)**  
- `re.search()`, `re.findall()`, `re.sub()`, `re.split()`  
- **Metacharacters** (`.`, `*`, `+`, `?`, `{}`, `\d`, `\w`, `\s`)  
- **Practical uses**: Email validation, phone number extraction, URL detection  

---

# **4. Practice Exercises**  
1. Write a regex to extract all **dates** in the format `DD-MM-YYYY` from a text.  
2. Validate a **strong password** (At least 8 characters, 1 uppercase, 1 lowercase, 1 number).  
3. Extract all **hashtags** (`#Python`, `#Coding`) from a tweet.  

---

Would you like detailed **hands-on coding examples** for any part?
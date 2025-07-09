---
title: Strings
weight: 1
# prev: /docs/getting-started
# next: /docs/guide/organize-files
sidebar:
  open: true
---
------------------------------------

In all programming languages, including Python, the **string** data type represents a fundamental data type. In Python, a string is defined as a **sequence of characters** enclosed within single ('...'), double ("..."), or triple quotes ('''...''' or """..."""). This sequence can include alphabets, digits, symbols, or Unicode characters.

### **Memory Allocation Basics**

Traditionally, each character was considered to occupy **1 byte** of memory, with the total string size computed as the number of characters multiplied by one byte. For example, the string "hello" corresponds to the ASCII values \[104, 101, 108, 108, 111\] and is stored in five contiguous memory locations—i.e., five sequential bytes in memory.

### **Contiguous Memory in String Buffers**

Python strings allocate **contiguous memory** for their character buffers. This arrangement, managed via the PyUnicodeObject structure, contains metadata (length, encoding kind, hash) alongside a pointer to the underlying contiguous byte array, enabling efficient random access and slicing operations. 
> [!NOTE]
> However, in the newer versions of python (after 3.3), PEP 393 is introduced which does a smart way to handle the encoding to save memory. A detailed article will be made on this and linked here. Stay tuned for the updates. For now, we assume we are not dealing with the more special characters and hence consider ASCII encoding as the standard for this tutorial. 

### **Immutability**
The behaviour that once an object is created, cannot be changed or modified is called immutability. Strings are immutable in nature and hence once created can't be modified. 


### **How can we access the characters in a string?**

Accessing a string can be done in two ways:
1. Indexing
2. Slicing

#### *Indexing*

We can access characters of a string by using the indexes. There are two types of indexes - Positive and Negative.
```python
## synatax ##
# char = s[i]
s = "hello world"
print(s[0])  # Output: 'h'
print(s[-1])  # Output: 'd'
```

* **Time Complexity - O(1)**: Since the string will be stored in contingious memoty locatuions, the time complexity of indexing is O(1)
* **Space Complexity - O(1)**: No extra strings are created when accessing using the indexing and hence the space complexity is also O(1)


#### *Slicing*

Slicing is the operation of extracting a portion of a string using a range of indices. In Python, this is done using the syntax:
```python
## syntax ##
#substring = original_string[start:end]
s = "hello world"
print(s[0:5])  # Output: 'hello'
```
This creates a new string that includes characters from index start up to, but not including, end.

* **Time Complexity - O(k)**: Because python has to copy each of the k characters from the original string to create a new string (k is the length of the resulting substring end - start) and takes linear time, the complexity is O(k).

* **Space Complexity - O(k)**: Because strings are immutable, a new string is always created during slicing. This new string takes up space proportional to k characters.


### **Additon**
Adding or concatenation of the strings creates a brand-new string that contains all characters from s1 followed by all characters from s2. Python must allocate new memory and copy over both strings.

```python
s1 = "hello"
s2 = "world"
s3 = s1 + s2
print(s3)  # Output: 'helloworld'
print(s1.concat(s2))  # Output: 'helloworld'
```
* **Time Complexity - O(n + m)**: Because python has to copy the both the original strings to create a new string and takes linear time, the complexity is O(n + m) time.

* **Space Complexity - O(n + m)**: Because strings are immutable, a new string is always created with the combined content. This new string takes up space proportional to n + m characters.


### **Multiplication**
This repeats the original string n times, resulting in a string of length n * len(s). Python performs the repetition by allocating enough memory and copying the string n times, leading to O(n * len(s)) time and space complexity.

```python
s = "hello"
n = 3
s1 = s * n
print(s1)  # Output: 'hellohellohello'
```
* **Time Complexity - O(n * len(s))**: Python performs the repetition by allocating enough memory and copying the string n times, leading to O(n * len(s)) time complexity.

* **Space Complexity -O(n * len(s))**: O(n + m) space complexity

### **Membership Operators: In and not in**
The in and not in operators in Python are used to check for the existence of a substring within another string. These are membership operators and return boolean value as per the existence

```python
"ell" in "hello"   # True
"x" in "hello"     # False
```
```python
"ell" not in "hello"   # False
"x" not in "hello"     # True
```

* **Time Complexity - O(n x m)**: The time complexitiy of the membership operators would be O(n x m), where n is the length of the string **s** and m is be the legnth of the substring **sub**. Python loops through every possible starting position in s where sub could fit. At each position, it checks character-by-character if sub matches the corresponding slice of s.
    1. Each time a comparision of length m is made which adds O(m) time complexity
    2. It is made for whole length of n of the string which adds O(n) time complexity
    3. Hence the overall time complexity is O(n x m)


* **Space Complexity - O(1)**: The space complexity is O(1), because a new string is not created in these operations

> [!NOTE]
> CPython uses fast substring search algorithms (e.g., Boyer-Moore or variations), so the average case is faster, often close to O(n + m), but the worst-case theoretical time is O(n × m).

### **strip(), lstrip(), rstrip() Operations**
These are whitespace-trimming operations that return a new string with characters removed from either or both ends.
| Method       | Action                                              |
| ------------ | --------------------------------------------------- |
| `s.strip()`  | Removes leading and trailing whitespace (both ends) |
| `s.lstrip()` | Removes whitespace only from the left (start)       |
| `s.rstrip()` | Removes whitespace only from the right (end)        |

```python
s = "  hello  "
print(s.strip())      # 'hello'
print(s.lstrip())     # 'hello  '
print(s.rstrip())     # '  hello'

s2 = "**hello**"
print(s2.strip("*"))  # 'hello'
```

Python will start from the beginning (or end) and skips over all removable characters. Then copies the remaining characters into a new string (due to immutability).

* **Time Complexity - O(n)**: he maximum number of characters it may need to look at is the full length of the string. Hence the time complexity is O(n).

* **Space Complexity -O(n)**: O(n) space complexity because a new string will be created.

### **find() Operationn**
The find() method is used to locate the first occurrence of a substring within another string. It returns the index of the first matching element or -1 if not found.


```python
### syntax ###
#   s.find(sub[, start[, end]]) #
#
s = "machine learning"
print(s.find("learn"))     # Output: 8
print(s.find("deep"))      # Output: -1
print(s.find("a", 2, 10))  # Output: 6
```

* **Time Complexity - O(n x m)**: It works similarly to the in operator sliding a window of size len(sub) over the string. At each position, checks if the substring matches. Stops when the first match is found. Hence the time complexity is O(n x m) 
* **Space Complexity - O(1)**: the space complexity is O(1). 

index() is similar to find() except that it throws an exception in case the sub string is not found

> [!NOTE]
> CPython uses fast substring search algorithms (e.g., Boyer-Moore or variations), so the average case is faster, often close to O(n + m), but the worst-case theoretical time is O(n × m).

### **replace() Operation**
The replace() method returns a new string where all (or a limited number of) occurrences of a specified substring are replaced with another substring. In case of zero occurences of the specified string, it returns the original string without creating a new one

```python
### syntax ###
#   s.replace(old, new[, count])
# s = "data science is a science"
print(s.replace("science", "engineering"))
# Output: "data engineering is a engineering"

print(s.replace("science", "engineering", 1))
# Output: "data engineering is a science"
```

1. Python scans the string from left to right.

2. Each time it finds old, it replaces it with new.

3. Stops after count replacements if provided.

4. Constructs a new string (because strings are immutable).

* **Time Complexity - O(n)**: The time complexity is O(n).

* **Space Complexity - O(1)**: the space complexity is O(1).


### **split() Operation**
The split() method divides a string into a list of substrings, using a delimiter (separator). It’s commonly used to tokenize a string.

```python
### syntax ###
#   s.split(sep=None, maxsplit=-1)
s = "Python is fun"
print(s.split())  
# Output: ['Python', 'is', 'fun']

s = "2025-07-09"
print(s.split("-"))  
# Output: ['2025', '07', '09']

s = "one,two,three,four"
print(s.split(",", 2))  
# Output: ['one', 'two', 'three,four']
```

1. Python iterates over the string from left to right.

2. At each match of the delimiter, it extracts the current token and starts collecting the next one.

3. Once all matches are found or maxsplit is reached, the remaining part is returned as the final substring.

* **Time Complexity - O(n)**: Each character is read once.

* **Space Complexity - O(1)**: A new list with up to k substrings is created (depending on number of splits).

### **join() Operation**
The join() method is used to concatenate (combine) elements of an iterable (like a list or tuple of strings) into a single string, with a separator (the string calling join()) inserted between each element.

```python
### syntax ###
#   separator.join(iterable)

words = ["Python", "is", "awesome"]
result = " ".join(words)
print(result)
# Output: "Python is awesome"

fields = ["2025", "07", "09"]
result = ",".join(fields)
print(result)
# Output: "2025,07,09"

chars = ["a", "b", "c"]
print("".join(chars))
# Output: "abc"

```

1. Python first calculates the total length of the final string in memory to optimize allocation.

2. Then it iteratively copies each string from the iterable and inserts the separator between them.

3. Strings are immutable, so a new string is created (efficiently, in one pass—not through repeated concatenation).


* **Time Complexity - O(n)**: Python loops once over the iterable to compute the result.

* **Space Complexity - O(1)**:  A new string is created with the combined content.


### **Time and Space Complexity of Common String Operations**


| Operation | Time Complexity | Space Complexity | Description |
| --- | --- | --- | --- |
| `s[i]` | O(1) | O(1) | Retrieve character at index `i` |
| `s[start:end]` | O(k) | O(k) | Extract substring of length `k`; a new string is created |
| `s1 + s2` | O(n + m) | O(n + m) | Concatenate strings of length `n` and `m`; new memory is allocated |
| `s * n` | O(n * len(s)) | O(n * len(s)) | Repeat string `n` times; creates a new string with repeated content |
| `len(s)` | O(1) | O(1) | Return number of characters |
| `'sub' in s` | O(n * m) worst-case | O(1) | Substring search using pattern matching algorithms |
| `s1 == s2` | O(k) | O(1) | Character-wise equality comparison |
| `s.strip()` | O(n) | O(n) | Trim leading/trailing whitespace |
| `s.replace(a, b)` | O(n) | O(n) | Replace all instances of `a` with `b` |
| `s.split(delim)` | O(n) | O(k) | Divide string into substrings at delimiter |
| `delim.join(list)` | O(n) | O(n) | Join list of strings with delimiter |
| `s.lower()` | O(n) | O(n) | Convert string to lowercase |
| `s.upper()` | O(n) | O(n) | Convert string to uppercase |
| `s.find(sub)` | O(n * m) worst-case | O(1) | Return index of first occurrence or -1 |
| `s.index(sub)` | O(n * m) worst-case | O(1) | Like `find`, but raises error if not found |
| `s.count(sub)` | O(n * m) worst-case | O(1) | Count occurrences of substring |
| `s.startswith(sub)` | O(k) | O(1) | Test if string begins with substring |
| `s.endswith(sub)` | O(k) | O(1) | Test if string ends with substring |


--------------------------------------------------------
**Strings as a Primitive Data Type**
------------------------------------

In all programming languages, including Python, the **string** data type represents a fundamental data type. In Python, a string is defined as a **sequence of characters** enclosed within single ('...'), double ("..."), or triple quotes ('''...''' or """..."""). This sequence can include alphabets, digits, symbols, or Unicode characters.

### **Memory Allocation Basics**

Traditionally, each character was considered to occupy **1 byte** of memory, with the total string size computed as the number of characters multiplied by one byte. For example, the string "hello" corresponds to the ASCII values \[104, 101, 108, 108, 111\] and is stored in five contiguous memory locations—i.e., five sequential bytes in memory.

**Contiguous Memory in String Buffers**

Python strings allocate **contiguous memory** for their character buffers. This arrangement, managed via the PyUnicodeObject structure, contains metadata (length, encoding kind, hash) alongside a pointer to the underlying contiguous byte array, enabling efficient random access and slicing operations.**Time and Space Complexity of Common String Operations**

**Operation**

**Time Complexity**

**Space Complexity**

**Remarks**

s\[i\]

O(1)

O(1)

Direct indexing

s\[start:end\]

O(k)

O(k)

Creates a new substring

s1 + s2

O(n + m)

O(n + m)

Concatenation creates a new string

s \* n

O(n \* len(s))

O(n \* len(s))

String repetition

len(s)

O(1)

O(1)

Cached length

'abc' in s

O(n \* m) worst-case

O(1)

Substring search

s1 == s2

O(k)

O(1)

Early termination on mismatch

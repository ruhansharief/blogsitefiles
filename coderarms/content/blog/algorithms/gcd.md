---
weight: 1
title: "Greatest Common Divisor Alogrithm"
date: 2020-03-06T21:29:01+08:00
lastmod: 2020-03-06T21:29:01+08:00
draft: false
author: "sharuh"
description: "Go through the GCD alogirthm from brute force to the best optimized solution"
images: ["py.png"]
resources:
- name: "featured-image"
  src: "featured-image.png"

tags: ["python", "alogorithm"]
categories: ["Algorithms"]

lightgallery: true

toc:
  auto: false
---
Go through the **GCD alogirthm** from brute force to the best optimized solution

<!--more-->

## Naive method

Algorithm:

- First check for the factors of each number by looping the intergers from 1 to that number.
- Add the factors to a list
- Repeat the above two steps for both the numbers
- Then loop in thorugh the one of the list and sort out the common numbers in both.
- Since the common list will be in ascending order, return the last number which would be the gcd.
- The algorithm can be improved in many places.

```python
def factors(x):
  f = []
  for i in range(1,x+1):
    if x%i == 0:
      f.append(i)
  return f

def gcd(m,n):
  fm = factors(m)
  fn = factors(n)
  comm = []
  for i in fm:
    if i in fn:
      comm.append(i)
  return comm[-1]

print(gcd(14,63))
```


## 1 Improvisation - Single Scan


- We are scanning 1 to m and 1 to n to find the common factors. Instead we can just scan from 1 to max(m,n) so that one scan (loop) would be sufficient.
- For each i in 1 to max(m,n) add i to fm if it divides m and add i to fn it divides n.
- We are computing two lists and then checking for the common numbers among them.
- Instead, we can create only one list which contains the numbers which divide both m and n.
- For each i in 1 to max(m,n) add the i to comm if it divides both m and n.
- Actually the common factor would be smaller or equal to the smaller number among m and n.
Hence scannig the numbers from 1 to min(m,n) would suffice.

```python
def gcd(m,n):
  #Improvisation 1
  comm = []
  for i in range(1,min(m,n)+1):
    if m % i == 0 and n % i == 0:
      comm.append(i)
  return comm[-1]
```

## Improvisation 2  - No lists

- Its not required to store all the common factors in a list.
- Instead we can just store the common factor in a variable (rather than list).
- While scanning for the common factor, if we get one then the variable should be replaced with earlier factor.

```python
def gcd2(m,n):
  #Improvisation 2
  for i in range(1,min(m,n)+1):
    if m % i == 0 and n % i == 0:
      mrcomm = i # We will not get the name error as there would be atleast one common factor that is 1.
  return mrcomm
```
## Improvisation 3: Scan Backwards

- In the above steps we are scanning from 1 and checking all the common factors.
- Since we want the greatest common factor, scanning from backwards would give us the result much faster in many cases.

```python
def gcd3_1(m,n):
  #Improvisation 3
  for i in range(min(m,n),0,-1):
    if m % i == 0 and n % i == 0:
      return i

def gcd3_2(m,n):
  #Improvisation 3 - while loop - using while loop is recommended
  #because in for loop the range gets all the values, in while that time can be reduced.
  i = min(m,n)
  while i>0:
    if m % i == 0 and n % i == 0:
      return i
    else:
      i = i - 1
```

# 📝 Worksheet: 01 - Working with Data

Use this worksheet to review and reinforce your understanding of Python's core data containers. Each section ends with an **🤖 Explain It** prompt — write your explanation in your own words, then (optionally) paste it into an AI tutor and ask it to point out anything you got wrong or left out.

---

## 🧠 Section 1: Lists

1. What method adds an item to the end of a list?  
   `Answer:` append()

2. How can you remove an item from a list by value? By position?  
   `Answer:` To remove an item from a list by value, use 'remove()' and 'pop()' for position

3. What's the result of this code?

```python
nums = [2, 4, 6]
nums.append(8)
print(nums)
```

   `Answer:` [2, 4, 6, 8]

4. What does `my_list[1:4]` return, given `my_list = [10, 20, 30, 40, 50]`?  
   `Answer:` [20, 30, 40]

4a. Given `a = [1, 2]` and `b = [3, 4]`, what is the result of `a + b`? Of `a.append(b)`? Of `a.extend(b)`?  
   `Answer:` 'a + b' = a new list [1, 2, 3, 4], 'a.append(b)' = [1, 2, [3, 4]], and 'a.extend(b)' = a modified 'a' [1, 2, 3, 4]

4b. Given `grid = [[1, 2], [3, 4]]`, how do you access the value `3`?  
   `Answer:` grid[1][0]

4c. List three different ways to remove an item from a list.  
   `Answer:` 1. 'remove(value)' | 2. 'pop(index)' | 3. del list[index]

---

### ✏️ Task: List Practice

```python
# Create a list of your top 3 favorite foods.
# Add another food to the list.
# Remove one item and print the list.
```

Answer:
foods = ["pizza", "hamburger", "empanada"]
foods.append("beef tips")
foods.remove("hamburger")
print(foods)

### ✏️ Task: Slicing and Sorting

```python
# Given: numbers = [42, 17, 8, 99, 23, 4]
# 1. Print the first three numbers using slicing.
# 2. Print the numbers sorted from smallest to largest.
# 3. Print the numbers sorted from largest to smallest.
```

Answer: 
#1
numbers_slice = numbers_list[0:3]
print(numbers_slice)

#2
numbers.sort()
print(numbers)

#3
numbers.sort()
numbers.reverse()
print(numbers)


### ✏️ Task: Filtering

```python
# Given: temps = [55, 72, 90, 43, 88, 67, 101]
# Build a new list called "hot" containing only temps over 85.
# Print "hot".
```
Answer:
hot = []
for temp in temps:
    if temp > 85:
        hot.append(temp)
print(hot)

### ✏️ Task: Combine Lists Three Ways

```python
# Given: morning = ['eggs', 'toast']
#        extras  = ['jam', 'coffee']
# 1. Use + to make a new list "breakfast" without changing "morning".
# 2. On a fresh copy of "morning", use .append(extras) and print the result.
#    Notice how many items the list has now, and why.
# 3. On another fresh copy, use .extend(extras) and print the result.
```
Answer:
#1
breakfast = morning + extras
print(breakfast)

#2
morning2 = ['eggs', 'toast']
extras   = ['jam', 'coffee']

morning2.append(extras)
print(morning2)

#3
morning3 = ['eggs', 'toast']
extras   = ['jam', 'coffee']

morning3.extend(extras)
print(morning3)


### ✏️ Task: 2D List (grid)

```python
# board = [
#     [1, 2, 3],
#     [4, 5, 6],
#     [7, 8, 9],
# ]
# 1. Print the value in row 2, column 0.
# 2. Change the center value to 0.
# 3. Loop over the board and print each row on its own line.
```
Answer:
print(board[2][0])
board[1][1] = 0
for row in board:
    print(row)

### ✏️ Task: Deleting Items

```python
# Given: queue = ['Ana', 'Ben', 'Cy', 'Dana', 'Eve']
# 1. Remove 'Cy' by value.
# 2. Use .pop() to remove and capture the last person into a variable "served".
# 3. Use del to remove the first person.
# 4. Print the remaining queue and "served".
```
Answer:
queue.remove('Cy')
served = queue.pop()
del queue[0]
print(queue)
print("served:", served)

### ✏️ Task: Iterate by Index

```python
# Given: prices = [10, 20, 30, 40]
# 1. Use "for i in range(len(prices)):" to print each item as "0: 10", "1: 20", ...
# 2. Using the index, add 5 to every price in place, then print the list.
# 3. Rewrite step 1 using enumerate() instead.
```
Answer:
for i in range(len(prices)):
    print(i, ":", prices[i])

for i in range(len(prices)):
    prices[i] += 5
print(prices)

for i, price in enumerate(prices):
    print(i, ":", price)

### 🤖 Explain It

In your own words: what's the difference between a list and a slice of a list? Is slicing a list the same as modifying it? And when you write `a.append(b)` versus `a.extend(b)`, what ends up in `a` each way?

Answer: A 'list' is the original container, while a 'slice' is a copied piece of a list. Slicing is not the same as modifying a list, as slicing does not change the original list. 'a.append(b)' adds 'b' as one item, while 'a.extend(b)' adds each item from 'b' individually.

---

## 🔒 Section 2: Tuples

5. What is a key difference between a list and a tuple?  
   `Answer:` A list can be modified, while a tuple is immutable.

6. Can you change the contents of a tuple once it is created? Why or why not?  
   `Answer:` No, you can not change the contents of a tuple because they are immutable.

7. What does `first, *rest = (10, 20, 30, 40)` assign to `first` and `rest`?  
   `Answer:` 'first' is assigned to 10, while '*rest' is assigned to 20, 30, and 40.

---

### ✏️ Task: Tuple Practice

```python
# Create a tuple with your favorite 3 numbers.
# Unpack it into three variables and print each.
```
Answer:
nums = (67, 41, 7)
a, b, c = nums
print(a)
print(b)
print(c)

### ✏️ Task: Unpacking with *rest

```python
# Given: race_times = (9.58, 9.63, 9.69, 9.71, 9.74)
# Unpack this into "winner" (the first time) and "others" (everything else).
# Print both.
```
Answer:
winner, *others = race_times

print("winner:", winner)
print("others:", others)

### ✏️ Task: Tuples as Dictionary Keys

```python
# Build a dictionary called "distances" where the keys are (city1, city2)
# tuples and the values are the distance in miles between them.
# Add at least two entries, then look up and print one of them.
```
Answer:
distances = {
    ("Wichita Falls", "Amarillo"): 224,
    ("Dallas", "San Antonio"): 274,
}

print(distances[("Dallas", "San Antonio")])

### 🤖 Explain It

In your own words: why does Python allow a tuple to be a dictionary key, but not a list? What property makes that possible?

Answer: In Python, a tuple is allowed to be a dictionary key because tuples are immutable, while a list can't be a dictionary key because it is mutable. 

---

## 🔑 Section 3: Dictionaries

8. What does the `.get()` method do differently from accessing a key directly with `[]`?  
   `Answer:` '.get()' will return 'None' if the key doesn't exist, while '[]' would raise an error

9. How do you loop through both keys and values in a dictionary?  
   `Answer:` for key, value in dict.items():

10. How would you remove a key from a dictionary and also capture the value it held?  
    `Answer:` value = dict.pop(key)

11. In a list of dictionaries like `people = [{'name': 'Ana'}, {'name': 'Ben'}]`, how do you get Ben's name?  
    `Answer:` people[1]['name']

12. If the same dictionary object is stored in both a list and another dictionary, and you change it through one, does the other see the change? Why?  
    `Answer:` Yes, because dictionaries and lists store 'references' to objects, not copies.

---

### ✏️ Task: Dictionary Practice

```python
# Create a dictionary with keys: 'name', 'age', and 'hobby'.
# Print each key and value in the format "key: value".
```
Answer:
person = {
    'name': 'Eli',
    'age': 21,
    'hobby': 'gaming'
}
for key, value in person.items():
    print(key + ":", value)

### ✏️ Task: Build from Two Lists

```python
# Given: products = ['pen', 'notebook', 'eraser']
#        prices = [1.50, 3.25, 0.75]
# Build a dictionary mapping each product to its price.
# Print the total cost of all products (hint: sum the .values()).
```
Answer:
product_prices = dict(zip(products, prices))
total = sum(product_prices.values())
print("Total cost:", total)

### ✏️ Task: Nested Dictionaries

```python
# Given:
# inventory = {
#     'apples': {'count': 50, 'price': 0.50},
#     'bananas': {'count': 30, 'price': 0.25},
# }
# Loop through inventory and print a line for each fruit like:
# "apples: 50 units at $0.50"
```
Answer:
for fruit, info in inventory.items():
    print(f"{fruit}: {info['count']} units at ${info['price']:.2f}")

### ✏️ Task: List of Dictionaries (table rows)

```python
# roster = [
#     {'name': 'Alex', 'major': 'CS'},
#     {'name': 'Ana',  'major': 'Math'},
#     {'name': 'Ben',  'major': 'History'},
# ]
# 1. Loop over roster and print "name - major" for each student.
# 2. Add a new student record to the list.
# 3. Build and print a list of just the names of everyone majoring in 'CS'.
```
Answer:
for student in roster:
    print(student['name'], "-", student['major'])
roster.append({'name': 'Zeke', 'major': 'CS'})
cs_students = [s['name'] for s in roster if s['major'] == 'CS']
print(cs_students)

### ✏️ Task: Update a Record by Row Number

```python
# Using the roster above:
# 1. Build a dict "by_row" mapping each row number to its record
#    (hint: {i: row for i, row in enumerate(roster)}).
# 2. Change the major of the student in row 2 to 'CS'.
# 3. Print roster[2] and explain why it changed too.
```
Answer:
by_row = {i: row for i, row in enumerate(roster)}
by_row[2]['major'] = 'CS'
print(roster[2]) #Changed because roster[2] and by_row[2] refer to the same dictionary object

### 🤖 Explain It

In your own words: what's the difference between `student['gpa']` and `student.get('gpa')` when `'gpa'` isn't in the dictionary? Which would you use, and when? Also: why does changing `by_row[2]` also change `roster[2]`?

Answer: The difference is that `student['gpa']` will raise an error if the key doesn't exist, while `student.get('gpa')` will return 'None'. You use `student['gpa']` if the 'gpa' key is required and `student.get('gpa')` when the key is not required. Also, changing `by_row[2]` also changes `roster[2]` because both refer to the same dictionary objects in memory.

---

## 🚀 Section 4: Going Further (Optional)

These pair with the "🔥 Challenge" sections in the notebooks — skip if you haven't gotten there yet.

### ✏️ Task: List Comprehension

```python
# Rewrite this loop as a one-line list comprehension:
# cubes = []
# for n in range(6):
#     cubes.append(n ** 3)
```

### ✏️ Task: namedtuple

```python
# Create a namedtuple called "Book" with fields "title" and "author".
# Make one instance and print both fields by name.
```

### ✏️ Task: Word Counter

```python
# text = "to be or not to be that is the question"
# Build a dictionary counting how many times each word appears.
# (Try it by hand first, then check yourself with collections.Counter.)
```

### ✏️ Task: Parse Some JSON

```python
import json
raw = '''
{
  "course": "Programming for Data Science",
  "online": true,
  "instructor": null,
  "students": [
    {"name": "Alex", "grade": 91},
    {"name": "Ana",  "grade": 88}
  ]
}
'''
# 1. Use json.loads(raw) to turn this into Python objects.
# 2. Print the course name and the second student's grade.
# 3. Print the Python type of the value that came from "online" and from "instructor".
```

### ✏️ Task: Walk a GeoJSON FeatureCollection

```python
geo = {
    "type": "FeatureCollection",
    "features": [
        {"type": "Feature",
         "geometry": {"type": "Point", "coordinates": [-98.529, 33.878]},
         "properties": {"name": "Bolin Hall"}},
        {"type": "Feature",
         "geometry": {"type": "Point", "coordinates": [-98.531, 33.876]},
         "properties": {"name": "Moffett Library"}},
    ],
}
# Loop over geo["features"] and print each building's name with its
# latitude and longitude. Remember: coordinates are [longitude, latitude].
```

---

## 🧾 Submit Checklist

- [X] I practiced creating, slicing, sorting, and filtering lists.
- [X] I can explain the difference between `+`, `append()`, and `extend()`.
- [X] I built and traversed a nested (2D) list.
- [X] I removed list items with `remove()`, `pop()`, and `del`.
- [X] I looped by index with `range(len(...))` and with `enumerate()`.
- [X] I understand how tuples are different from lists, and why that makes them hashable.
- [X] I accessed, looped through, updated, and removed items from a dictionary.
- [X] I built a dictionary from two separate lists.
- [X] I worked with at least one nested dictionary.
- [X] I processed a list of dictionaries as table rows and updated a record by row number.
- [X] I parsed JSON with `json.loads()` and walked a GeoJSON FeatureCollection.
- [X] I completed the "Explain It" prompts in my own words.

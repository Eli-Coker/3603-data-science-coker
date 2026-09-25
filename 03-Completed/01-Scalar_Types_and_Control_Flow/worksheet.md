# 📝 Worksheet: 02 - Scalar Types and Control Flow

Use this worksheet to reinforce your understanding of variables, arithmetic, comparisons, and decision logic. Each section ends with an **🤖 Explain It** prompt — write your explanation in your own words, then (optionally) paste it into an AI tutor and ask it to point out anything you got wrong or left out.

---

## 🧠 Section 1: Scalar Types and Casting

1. What is the output of the following code?

```python
x = 10
print(type(x))
```

   `Answer:` <class 'int'>

2. What scalar type would best represent:
   - A person's name: string
   - Their age: int
   - Whether they passed a test: bool

3. Why does `int('21')` work, but `int('twenty-one')` raise an error?  
   `Answer:` Because '21' is valid numeric syntax, whereas 'twenty-one' is not valid numeric syntax.

---

### ✏️ Task: Type Practice

```python
# Create a variable for each type and print its value and type.
# Example: an int, float, str, and bool.
```
Answer:
my_int = 33
my_float = 20.1
my_str = Eli
my_bool = True

print(my_int, type(my_int))
print(my_float, type(my_float))
print(my_str, type(my_str))
print(my_bool, type(my_bool))

### ✏️ Task: Arithmetic

```python
# Given: hours_worked = 37, hourly_rate = 15.50
# Print the total pay.
# Print the total pay rounded to 2 decimal places (hint: round()).
```
Answer:
total_pay = hours_worked * hourly_rate
print("Total pay:", total_pay)
print("Total pay (rounded):", round(total_pay, 2))


### ✏️ Task: Casting Round Trip

```python
# Given: user_input = "3.14159"
# Convert it to a float, then print it rounded to 2 decimal places.
```
Answer:
float_value = float(user_input)
print(round(float_value, 2))

### 🤖 Explain It

In your own words: why does `input()` always return a string, and why does that matter when you want to do math with what the user typed?

Answer: 'input()' always returns a string because the information the user enters will always be a string. To perform mathematical calculation with user-typed input, you must parse the input.
---

## 🔁 Section 2: Comparison Operators

4. What does the `!=` operator mean?

   `Answer:` Not equal to

5. What will the following code print?

```python
a = 5
b = 3
print(a < b or b < 10)
```

   `Answer:` True

6. What does `0 <= score <= 100` check, and how would you write the same thing *without* chaining?  
   `Answer:` It checks if a score is within the bounds of 0-100. 
   To write without chaining, you can use 'and':
   score >= 0 and score <= 100

---

### ✏️ Task: Comparison Practice

```python
# Given: temperature = 98.6
# Print True if it's within normal human body temperature range (97.0 to 99.0), else False.
# Try it both as a chained comparison and as two separate comparisons joined with "and".
```
Answer:
print(97.0 <= temperature <= 99.0)
print(temperature >= 97.0 and temperature <= 99.0)

### 🤖 Explain It

In your own words: what's the difference between `=` and `==` in Python? Why does mixing them up cause errors (or worse, silently wrong code)?

Answer: '=' Assigns a value to a variable, while '==' compares the values of two variables. Mixing these up causes errors as '=' and '==' perform different functions.

**If you've written C++:** explain why `0 <= score <= 100` is safe to write in Python but dangerous to write in C++. What does the C++ version actually evaluate to, and how would you fix it?

Answer:
This is safe to write in Python because it supports chained comparisons, but it's dangerous in C++ because it does not process chained comparisons. The C++ version would evaluate (0 <= score) <= 100, meaning the answer will always be true.
To fix this in C++, use &&: score >= 0 && score <= 100

---

## 🔀 Section 3: Control Flow

7. Write a conditional that prints "Pass" if a grade is >= 70, and "Fail" otherwise.

```python
# Your code: 

if grade >= 70:
    print("Pass")
else:
    print("Fail")
```

8. What does `elif` allow you to do that separate `if` statements don't?  
   `Answer:` 'elif' allows you to create mutually exclusive chains of decisions.

9. What will this print?

```python
age = 16
has_ticket = False
print(age >= 13 and has_ticket)
```

   `Answer:` False

---

### ✏️ Task: Multi-Branch Logic

```python
# Given: bmi = 22.5
# Print the BMI category:
# "Underweight" (< 18.5), "Normal" (18.5-24.9), "Overweight" (25-29.9), "Obese" (30+)
```
Answer:

if bmi < 18.5:
    print("Underweight")
elif bmi < 25:
    print("Normal")
elif bmi < 30:
    print("Overweight")
else:
    print("Obese")

### ✏️ Task: Multi-Line Branches

```python
# Given: cart_items = 3, member_since_days = 400
# In the if-branch (member_since_days >= 365): compute a "loyalty discount" of 15%,
#   print the discount amount, and print the final price.
# In the else-branch: print that there's no discount yet, and print the full price.
# Use item_price = 20.00 per item as the starting subtotal.
# Each branch should have at least 3 lines — this is the same shape as the
# "One Branch, Many Lines" example in the notebook.
```
Answer:
subtotal = cart_items * item_price

if member_since_days >= 365:
    loyalty_discount = subtotal * 0.15
    final_price = subtotal - loyalty_discount
    print("Loyalty discount applied!")
    print("Discount amount:", loyalty_discount)
    print("Final price:", final_price)
else:
    print("No discount applied")
    print("Subtotal:", subtotal)
    print("Final price:", subtotal)

### ✏️ Task: Your Turn

Write a program that asks for the weather and prints:
- "Bring sunscreen" if it's sunny
- "Take an umbrella" if it's raining
- "Check the forecast" otherwise

Answer:
weather = input('What is the weather like? ')

if weather.lower() == 'sunny':
    print('Bring sunscreen')
elif weather.lower() == 'rainy':
    print('Take an umbrella')
else:
    print('Check the forecast')

### 🤖 Explain It

In your own words: what's the difference between using `and` versus writing nested `if` statements to check two conditions? Do they always produce the same result?

Answer: 'and' evaluates both conditions at once, while 'if' statements evaluate conditions separatley. They do not always produce the same result.
---

## 🚀 Section 4: Going Further (Optional)

These pair with the "🔥 Challenge" sections in the notebooks — skip if you haven't gotten there yet.

### ✏️ Task: Conditional Expression

```python
# Rewrite this as a one-line conditional expression:
# if temperature > 90:
#     comfort = "too hot"
# else:
#     comfort = "fine"
```

### ✏️ Task: Float Precision

```python
# Predict, then check: does 0.1 + 0.1 + 0.1 == 0.3 evaluate to True or False in Python?
# Write a "close enough" check instead of using == directly.
```

### ✏️ Task: Match Statement

```python
# Given: grade_letter = 'B'
# Use match/case to print:
#   "Excellent" for 'A'
#   "Good" for 'B' or 'C'
#   "Needs improvement" for anything else (use the "_" wildcard case)
```

### 🤖 Explain It

**If you've written C++:** how is Python's `match`/`case` similar to a C++ `switch`? What can `match` do (strings, multiple values per case with `|`) that a plain C++ `switch` can't?

---

## 🧾 Submit Checklist

- [X] I practiced creating and casting each scalar type.
- [X] I used arithmetic operators, including `//` and `%`.
- [X] I wrote conditionals using comparison and logical operators.
- [X] I used a chained comparison at least once.
- [X] I wrote at least one branch with multiple lines inside it.
- [X] I completed the "Explain It" prompts in my own words.

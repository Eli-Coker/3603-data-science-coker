# 📝 Worksheet: 04 - More Functions & Loops

Do this worksheet **on paper, without a computer**. Each section ends with an **🤖 Explain It** prompt: write your explanation in your own words, then (optionally) paste it into an AI tutor and ask it to point out anything you got wrong or left out.

---

## 🧠 Section 1: Defaults and Keywords

```python
def price(amount, tax=0.0825, discount=0):
    return round(amount * (1 + tax) - discount, 2)
```

What does each call return?

1. `price(100)` → 108.25
2. `price(100, discount=10)` → 98.25
3. `price(100, 0)` → 100.00
4. `price(discount=5, amount=20)` → 16.65

> 🤖 **Explain It:** Why are keyword arguments easier to read than positional ones in a call like `price(100, 0, 10)`?

Answer: Keyword arguments are easier to read because they show specifically what parameter a value is related to

---

## 🧠 Section 2: Scope

What prints? Explain why.

```python
count = 0

def add_one(count):
    count = count + 1
    return count

result = add_one(count)
print(count, result)
```

`Answer:` 0, then 1 - Count is set to the value 0 and changes to 1 locally in the add_one function, with the functin result being stores in 'result', not 'count'.

> 🤖 **Explain It:** Describe the "room with two doors" model of a function in your own words.

Answer: The "room with two doors" function model explains how parameters, local variables, and returns work in a function call. Essentially, parameters are the "door" that allows data into a function "room", local variables and their values remain in the function "room" and do not leave, and a "return" statement is the exit door that data leaves out of.

---

## 🧠 Section 3: Trace a While Loop

```python
balance = 100
years = 0
while balance < 150:
    balance = balance + 20
    years += 1
```

| pass | `balance` at the start | `balance < 150`? | `balance` after | `years` after |
|------|------------------------|------------------|-----------------|---------------|
| 1 | 100 | True | 120 | 1 |
| 2 | 120 | True | 140 | 2 |
| 3 | 140 | True | 160 | 3 |
| 4 | 160 | False | | |

Final `years`: 3  Final `balance`: 160

What single change would make this an **infinite** loop?  
`Answer:` Removing the balance update within the while loop

---

## 🧠 Section 4: `for` or `while`?

| Task | `for` or `while`? | Why? |
|------|-------------------|------|
| Print each line of a file | For | Files have a known, finite amount of lines |
| Keep asking for a password until it's correct | While | You do not know how many times someone may guess a wrong password |
| Find the average of a list of prices | For | You need to iterate over each price |
| Double a number until it's over one million | While | There is a threshold with an unknown number of iterations to reach it |

---

## 🧠 Section 5: Files

Given the file `pets.txt`:

```text
name,species
Rex,dog

# rescued in May
Tom,cat
```

1. How many times does `for line in f:` run? '5'
2. Which lines should your code skip, and how would you detect each one?  
   `Answer:` The code should skip... 
   
   'name,species' - detect using 'line == "name,species"',

   the blank line - detect using 'line.strip() == ""'

   '# rescued in May' - detect using 'line.startswith("#")'

3. Write the list of dictionaries a `read_pets` function should return:  
   `Answer:` {"name": "Rex", "species": "dog"}, {"name": "Tom", "species": "cat"}

> 🤖 **Explain It:** When is `try` / `except` a good idea, and when does it just hide bugs?

Answer: Using `try` / `except` is a good idea when checking for user input errors or missing files, but only serves to hide errors when used to catch *everything* as a means of ignoring code problems instead of catching specific errors.
# 📝 Worksheet: 03b - Containers → Functions

Do this worksheet **on paper, without a computer**. The point is to practice being the computer. Each section ends with an **🤖 Explain It** prompt: write your explanation in your own words, then (optionally) paste it into an AI tutor and ask it to point out anything you got wrong or left out.

---

## 🧠 Section 1: Trace a Loop

Fill in the table for this code:

```python
temps = [31, 45, 28, 52]
total = 0
count = 0
for t in temps:
    total += t
    if t <= 32:
        count += 1
```

| pass | `t` | `total` | `count` |
|------|-----|---------|---------|
| start | — | 0 | 0 |
| 1 | 31 | 31 | 1 |
| 2 | 45 | 76 | 1 |
| 3 | 28 | 104 | 2 |
| 4 | 52 | 156 | 2 |

Which **two** patterns are mixed together in this loop?  
`Answer:` Accumulate and Count

> 🤖 **Explain It:** Explain the difference between Accumulate, Count, and Filter as if you were talking to someone who has never programmed.

Answer: Accumulate adds item values to a total, Count adds 1 for each item that meets a certain criteria, and Filter adds items that pass some test to a list.

---

## 🧠 Section 2: Pick Your Weapon

| Scenario | Container | Why? |
|----------|-----------|------|
| Daily step counts for a month | list | Because there are many counts ordered by day |
| A playing card (rank, suit) | Tuple | A card is one thing with fixed parts being rank and suit |
| Username → password hash | Dictionary | For fast lookups, you need to map usernames to password hashes |
| Every distinct IP address in a log file | Set | Duplicates and order are not counted, only unique instances of IP addresses|
| Your class schedule, in order | list | The order of many classes needs to be preserved |

> 🤖 **Explain It:** Pick the scenario you were *least* sure about and argue for a different container than the one you chose.

Answer: The scenario I was least sure about was the 'daily step counts for a month'. A different container that could be used for 'daily step counts for a month' is a dictionary, as you could assign date keys to the step counts for search purposes if needed.
---

## 🧠 Section 3: Take It Apart

```python
course = {
    "title": "CMPS 3603",
    "students": [
        {"name": "Ana", "scores": [88, 92]},
        {"name": "Ben", "scores": [75, 81]}
    ]
}
```

Write the value after **each** step:

1. `course["students"]` → [{"name": "Ana", "scores": [88, 92]}, {"name": "Ben", "scores": [75, 81]}]
2. `course["students"][1]` → [{"name": "Ben", "scores": [75, 81]}]
3. `course["students"][1]["scores"]` → [75, 81]
4. `course["students"][1]["scores"][0]` → 75

Write the expression that gets Ana's second score:  
`Answer:` `course["students"][0]["scores"][1]`

---

## 🧠 Section 4: Functions

1. What prints?

```python
def f(x):
    return x + 1

print(f(f(f(0))))
```

   `Answer:` 3

2. What prints? Explain why.

```python
def shout(word):
    print(word.upper())

x = shout("hi")
print(x)
```

   `Answer:` 'HI', 'None' - The shout(word) function prints something, but doesn't return a value. Thus, x = shout("hi") will result in 'HI' being printed, but that result is not stored in x, so print(x) returns 'None'.

3. Circle the **parameters** and underline the **arguments**:

```python
def greet(name, greeting):
    return greeting + ", " + name

greet("Ada", "Hello")
```

Answer: Circled - '(name, greeting)', underlined '("Ada", "Hello")'

> 🤖 **Explain It:** In your own words, explain `print()` vs. `return`. Then explain why getting it wrong breaks a pipeline.

Answer: 'print()' displays a result to the user, but does not store the value of that result for later use, while 'return' stores a value that can be assigned or used later. Using 'print()' instead of 'return()' in the wrong scenario, such as in a function that needs to return a value to be used later, will break a pipeline as values that need to be assigned or used can get lost.
---

## 🧠 Section 5: Contracts and Tests

Write a contract for a function `longest_word(words)`:

```text
IN: A list of strings
OUT: A string
DOES: Loops through all words in the list and returns the longest
```

Write one test of each kind:

- Normal: longest_word(["pizza", "elephant", "zoo"])
- Boundary: longest_word(["hi"])
- Weird: longest_word([])

---

## 🧠 Section 6: Draw the Pipeline

> "Given a list of prices, drop any that are `0` or less, add 8.25% tax to each, then find the total."

1. Name each function you'd need.

Answer: 'filter_prices(prices)', 'add_tax(prices)', 'total(prices)'

2. For each one, write what goes **in** and what comes **out** (shape, not just "data").

Answer:
'filter_prices(prices)'
IN - A list of numbers
OUT - A new list of numbers

'add_tax(prices)'
IN - A list of numbers
OUT - A list of updated numbers

'total(prices)'
IN - A list of numbers
OUT - A number

3. Draw the pipeline with arrows, labeling each arrow with the data's shape.

Answer:
    list of numbers
           │
           ▼
 ┌──────────────────┐
 │  filter_prices   │
 └──────────────────┘
           │
           ▼
  list of numbers [clean] 
           │             
           ▼                  
     ┌───────────┐              
     │  add_tax  │              
     └───────────┘              
           │                    
           ▼                    
list of numbers [updated]                   
           │                    
           ▼
     ┌───────────┐
     │   total   │
     └───────────┘
           │
           ▼
     number result

> 🤖 **Explain It:** Why is a pipeline of small functions easier to fix than one big block of code?

Answer: Each function of a pipeline has a single job, making it easier to find which part of your code is messing up. In one big block of code, every job is jumbled together, making it much more difficult to determine where a problem may be occuring.
# 📝 Worksheet: 06 - Foundations

Use this worksheet to reinforce the Jupyter/IPython tooling skills from this module. There's one section per notebook, in order. Each section ends with an **🤖 Explain It** prompt. Write your explanation in your own words, then (optionally) paste it into an AI tutor and ask it to point out anything you got wrong or left out.

---

## 🧙 Section 1: Magic Commands (01)

1. What magic command lists every variable currently in memory, along with its type?  
   `Answer:` %whos

2. What's the difference between a line magic (`%pwd`), a cell magic (`%%writefile`), and a shell command (`!ls`)?  
   `Answer:` Line magic applies to a single line, cell magic applies to the entire cell, and a shell command sends the line to the OS's shell

3. Why does `%cd ..  # go up` fail, and how do you fix it?  
   `Answer:` `%cd ..  # go up` fails because the %cd magic interprets '# go up' as an argument instead of a comment
    - To fix this, move `%cd ..` to it's own line.

---

### ✏️ Task: Write, Run, and Reload

```python
# Use %%writefile to create tools.py containing a function shout(text)
# that returns text in uppercase with "!" on the end.
%%writefile tools.py
def shout(text):
    return text.upper() + "!"

# Turn on %load_ext autoreload and %autoreload 2, then import tools and call shout().
%load_ext autoreload
%autoreload 2

import tools
tools.shout("hello")

# Rewrite tools.py so shout() adds "!!!" instead, and call it again WITHOUT restarting.
%%writefile tools.py
def shout(text):
    return text.upper() + "!!!"
```

### 🤖 Explain It

In your own words: why can `!pip install` "succeed" while `import` still fails with `ModuleNotFoundError`? Why does `%pip` avoid the problem?

`Answer:` `!pip install` uses whichever pip the shell finds first, which may belong to a different python, while `%pip` installs the same notebook enviroment the notebook kernel is on.

---

## ⚡ Section 2: Jupyter Workflow (02)

4. What are the two Jupyter cell modes, and what key switches to each?  
   `Answer:` There's `Edit Mode (Enter)` and `Command Mode (Esc)`

5. What do the numbers in `[3]`, `[4]`, `[12]` next to code cells tell you, and what *don't* they tell you?  
   `Answer:` The numbers `[3]`, `[4]`, `[12]` tell you what order the cells were **executed** in, but not the order of the cells in the notebook

6. A cell's code ends with three expressions on three lines. How many of their values are displayed?  
   `Answer:` Only one, the last expression's value, is shown.

---

### ✏️ Task: Shortcut Drill

```
Using only the keyboard (no mouse):
- Insert 2 new cells below this one.
- Turn one into a Markdown cell and the other into a Code cell.
- Move the Code cell above the Markdown cell.
- Delete the Markdown cell, then undo the deletion.
- Run the Code cell.
```

**Answer:** To perform this task...
- Select the cell above and press 'B' to create two new cells below
- Select the first new cell and press 'M' to change to markdown
- Select the second new celland press 'Y' to change into code
- While on the code cell, hold 'Alt' + ↑ to move it above the Markdown cell
- Move to the Markdown cell and press 'D, D' to delete it, then Ctrl+Z to undo
- Move to the code cell and press 'Ctrl' + 'Enter' to run it.

### ✏️ Task: Break It, Then Fix It

```python
# In three separate cells, IN THIS ORDER, type:
#   print(area)
#   width, height = 4, 5
#   area = width * height
# Get it to work by running cells out of order. Then Restart & Run All,
# watch it fail, and fix the ORDER so it runs top to bottom.
```
**Answer:** In a notebook, the correct order would be...
- width, height = 4, 5
- area = width * height
- print(area)

### 🤖 Explain It

In your own words, using the "recipe and kitchen" idea: why can a notebook look correct on your screen and still fail for your grader?

**Answer:** Your own "kitchen" (kernel) may have left over ingredients (data in memory) to complete a recipe (notebook), but the "recipe" (notebook) may fail for your grader since they are working in a clean, empty "kitchen" (kernel) without your left-overs (data in memory).
---

## 📚 Section 3: Getting Help (03)

7. What's the difference between `help(len)` and `len?`? Which one also works in a plain `.py` script?  
   `Answer:` 'help(len)' is a built-in Python function, while 'len?' is for use in IPython shells and Jupyter notebooks. 'help(len)' also works in a plain '.py' script. 

8. In the signature `round(number, ndigits=None)`, which argument is required and which is optional? What's the optional one's default?  
   `Answer:` 'number' is requirted and 'ndigits' is optional. The default value of 'ndigits' is 'None'.

9. Name the error type for each: `'5' + 5`, `int('hello')`, `[1, 2][5]`, `{'a': 1}['b']`.  
   `Answer:` `'5' + 5` = TypeError | `int('hello')` = ValueError | `[1, 2][5]` = IndexError | `{'a': 1}['b']` = KeyError

---

### ✏️ Task: Investigate Without Searching

```python
# Using only ?, Tab/IntelliSense, dir(), and help() (no web searching):
# 1. Find a string method that checks whether a string contains only digits.
# 2. Use a wildcard search (np.*sum*?) to list NumPy functions with "sum" in the name.
# 3. Find out whether np.random.randint's upper limit is included. Prove it with code.

# Answer
#1
"1359".isdigit();

#2
np.*sum*?

#3
import numpy as np
np.random.seed(0)
values = np.random.randint(0, 10, size=1000)

print("Maximum value:", values.max())
print("Contains 10?", 10 in values)

```

### 🤖 Explain It

In your own words: when would you reach for `?` versus `??` versus `help()` versus `dir()` versus the official docs? Is there a natural order you'd try them in?

**Answer**: 
- '?' is used when you want to briefly know what a function does and what arguments it accepts.
- '??' is used if you want to see the source code (inner workings) of a function.
- 'help()' is used if you need to see full documentation, parameter descriptions, and return values (or if you are outside of a notebook).
- 'dir()' is used for listing every method an object has.
- The official docs are used for in depth explanations, tutorials, and examples of a library.
- The natural order I would try is 'dir()' --> '?' --> '??' --> 'help()' --> official docs.
---

## 📝 Section 4: Markdown (04)

10. What's the difference between `*italic*` and `**bold**` in Markdown?  
    `Answer:` `*italic*` emphasizes text by making it italicized, where as `**bold**` strongly emphasizes text in bold font.

11. Write the Markdown for a 2-item bulleted list where the second item has its own sub-bullet.  
    `Answer:` 
    - Item 1
    - Item 2
      - Subitem

12. How do you show a literal price like `$5` in Markdown without it turning into math?  
    `Answer:` Use a backslash '\' in front of the '$'.

---

### ✏️ Task: Mini Report

```markdown
# Write a Markdown cell with:
# - a level-2 heading
# - a short paragraph with a line break in the middle
# - a 3-item list
# - one inline LaTeX expression (try the mean, \bar{x})
# - a small table with a right-aligned number column
```

**Answer:**
```markdown
## My Heading
This is a short paragraph. The following line break <br> will split this sentence into two lines. Next I will creat a bulleted list.
- Item 1
- Item 2
- Item 3

$$
\bar{x} = \frac{1}{n} \sum_{i=1}^{n} x_i
$$

| Name | Age | Major |
|:--------|-----:|:-------|
|Eli |21 |Computer Science |
|Zeke |21 |Computer Science |
|Trinity |19 |Business |
```

### 🤖 Explain It

In your own words: what's lost if you write an entire notebook as code + comments only, with no Markdown cells at all? When would *generating* Markdown from code (`display(Markdown(...))`) be better than typing it?

**Answer:** 
- If you write an entire notebook with just code and comments, you lose the professional-look and clear explanations that Markdown cells provide.
- Generating Markdown from code is better tha typing it when the content of the Markdown cell is dependent on data or calculations. 

---

## 📂 Section 5: Files and Paths (05)

13. What does the `with` keyword do when you open a file, and why is it preferred over a plain `open()`/`.close()` pair?  
    `Answer:` The 'with' keyword automatically handles opening and closing a file, making preferrable over manually using `open()`/`.close()`.

14. What's the difference between modes `'w'`, `'a'`, and `'x'`?  
    `Answer:` 
    - `'w'` creates a file and writes to it, and if the file already exists, it erases it and then writes to it.
    - `'a'` appends to the end of an existing file, and creates the file if it doesn't already exist.
    - `'x'` creates and writes to a file ONLY if it doesn't already exist. 

15. For `Path('reports') / 'final.pdf'`, what are the `.name`, `.stem`, `.suffix`, and `.parent`?  
    `Answer:`
    - `.name` = 'final.pdf'
    - `.stem` = 'final'
    - `.suffix` = '.pdf'
    - `.parent` = 'Path('reports')'

---

### ✏️ Task: Build, Save, Reload

```python
# Create a dictionary describing yourself (name, major, hobbies as a list).
from pathlib import Path
import json
OUT = Path("output")
OUT.mkdir(exist_ok=True)

myself = {
    "name": "Elijah",
    "major": "Computer Science",
    "hobbies": ["gaming", "songwriting", "drawing"]
}

# Save it to a JSON file with indent=2 (use pathlib to build the path).
json_file = OUT / "myself.json"

with open(json_file, "w", encoding="utf-8") as f:
    json.dump(myself, f, indent=2)

# Read it back into a NEW variable and confirm it matches the original with ==.
with open(json_file, "r", encoding="utf-8") as f:
    myself_loaded = json.load(f)

print("Original matches loaded:",
      myself == myself_loaded)

# Then add a tuple to the dictionary and repeat. Does it still match? Why not?
myself["coordinates"] = (2, 5)

with open(json_file, "w", encoding="utf-8") as f:
    json.dump(myself, f, indent=2)

with open(json_file, "r", encoding="utf-8") as f:
    myself_loaded = json.load(f)

print("After adding tuple:",
      myself == myself_loaded) 
      # It no longer matches because JSON doesn't have a tuple type.
      # JSON onverts the tuple to a list in the loaded version, making it differ from the original.
```

### ✏️ Task: Find Files

```python
# Write three small .txt files into a folder using a loop.
from pathlib import Path

folder = Path("text_files")
folder.mkdir(exist_ok=True)

for i in range(1, 4):
    file_path = folder / f"file{i}.txt"

    with open(file_path, "w", encoding="utf-8") as f:
        f.write(f"File number {i}.\n")

# Use glob('*.txt') to find them WITHOUT typing their names, and print each
# file's name and size in bytes.
for file_path in folder.glob("*.txt"):
    print(
        f"Name: {file_path.name}, "
        f"Size: {file_path.stat().st_size} bytes"
    )
```

### 🤖 Explain It

In your own words: why does `csv.reader` give you `'90'` instead of `90`, and why does splitting a CSV line on `','` break on a value like `"Smith, John"`?

**Answer:** 
- Because CSV files are just text, any digit `csv.reader` returns will be a string. 
- Splitting a CSV line on `','` will break on values like `"Smith, John"` because the data contains commas that aren't intended to split values.

---

## 📊 Section 6: Data Input and Output (06)

16. Name three things `.info()` tells you about a DataFrame that `.head()` doesn't.  
    `Answer:` `.info()` also shows you data types, the number of non-null values per column, and memory usage.

17. What does `index=False` do in `df.to_csv(...)`, and what happens if you forget it?  
    `Answer:` `index=False` tells pandas not to write the dataframe's index to the CSV file. If you forget it, pandas will writhe the index as an unnamed column, producing a junk 'Unnamed: 0' column upon reading the file back.

18. When would you use `pd.json_normalize()` instead of `pd.read_json()`?  
    `Answer:` You would use `pd.json_normalize()` when the JSON contains nested data that you want to flatten into regular columns.

---

### ✏️ Task: CSV Round Trip

```python
# Create a small DataFrame from a dictionary of lists (use pd.DataFrame(your_dict)).
my_dict = {
    'Name': ['Eli', 'Zeke', 'Emma'],
    'Grade': ['A', 'B', 'D']
}

# Save it to a CSV, then read that CSV back into a new DataFrame.
df = pd.DataFrame(my_dict)
df.to_csv('data.csv', index=False)
df_reloaded = pd.read_csv('data.csv')

# Use .equals() to confirm the reloaded DataFrame matches the original.
print(df.equals(df_reloaded))
```

### ✏️ Task: Convert Between Formats

```python
# Take the same DataFrame and save it as JSON (orient='records') and as Excel.
df.to_json("data.json", orient="records", indent=2)
df.to_excel("data.xlsx", index=False)

# Read the Excel file back and convert it to a CSV.
df_from_excel = pd.read_excel("data.xlsx")
df_from_excel.to_csv("from_excel.csv", index=False)

# Print the raw text of the JSON and CSV files and compare them.
print("\nJSON file:")
with open("data.json", "r", encoding="utf-8") as f:
    print(f.read())

print("\nCSV file:")
with open("from_excel.csv", "r", encoding="utf-8") as f:
    print(f.read())
```

### 🤖 Explain It

In your own words: what information can get lost or changed when converting Excel → CSV, or CSV → DataFrame? Give two examples.

**Answer:** When converting from Excel→ CSV, or CSV → DataFrame, leading zeros can dissapear, formatting may be lost, and nesting may not fit.
- Example 1: In Excel → CSV, the ZIP code "09846" is changed to "9846" in since CSV has no types.
- Example 2: Color is dropped from an Excel file when converted to CSV.
---

## 📈 Section 7: Plotting with NumPy (07)

19. What's the difference between `[1, 2, 3] * 2` and `np.array([1, 2, 3]) * 2`?  
    `Answer:` `[1, 2, 3] * 2` repeats the list, resulting in '[1, 2, 3, 1, 2, 3]', while `np.array([1, 2, 3]) * 2` multiplies each element by 2, resulting in [2, 4, 6]

20. What does `plt.legend()` require in order to show meaningful labels (hint: think about the `plot()` calls before it)?  
    `Answer:` `plt.legend()` requires defined label arguments (e.g. plt.xlabel('value'), plt.ylabel('value'))

21. Which chart would you use for: comparing categories, change over time, a relationship between two numbers, and the distribution of one number?  
    `Answer:` 
    - Comparing categories = **Bar Chart**
    - Change over time = **Line Chart**
    - Relationship between two numbers = **Scatter plot**
    - distribution of one number = **Histogram**

---

### ✏️ Task: Compare Three Categories

```python
# Given: subjects = ["Math", "Science", "History"]
#        hours_studied = [5, 8, 3]
# Build a bar plot with a title and axis labels (with units).
OUT = Path("output")
OUT.mkdir(exist_ok=True)

plt.bar(subjects, hours_studied, color='red')
plt.title("Hours Studied by Subject")
plt.xlabel("Subject")
plt.ylabel("Hours Studied")

# Save it to a PNG file, then display it.
plt.savefig(OUT / "study_hours.png")
plt.show()
```

### ✏️ Task: Distribution

```python
# Generate 200 test scores with np.random.normal(75, 10, size=200).
scores = np.random.normal(75, 10, size=200)

# Plot a histogram and mark the mean with a vertical dashed line and a legend.
mean_score = scores.mean()

plt.hist(test_scores, bins=12, color='steelblue', edgecolor='white')
plt.axvline(mean_score, color='red', linestyle='--', label=f'Mean = {mean_score:.1f}')
plt.title('Distribution of Test Scores')
plt.xlabel('Score')
plt.ylabel('Number of Students')
plt.legend()
plt.show()

# Then show the same data as a box plot side by side, using subplots.
fig, axes = plt.subplots(1, 2, figsize=(10, 4))
axes[0].hist(test_scores, bins=12, color='steelblue', edgecolor='white')
axes[0].axvline(mean_score, color='red', linestyle='--', label=f'Mean = {mean_score:.1f}')
axes[0].set_title('Score')
axes[0].set_ylabel('Number of Students')
axes[0].legend()

axes[1].boxplot(test_scores)
axes[1].set_title('Box Plot')
axes[1].set_ylabel('Score')

plt.tight_layout()
plt.show()
```

### 🤖 Explain It

In your own words: why does a line plot make sense for `sin(x)` or monthly revenue but not for the categories `"Math"`, `"Science"`, `"History"`? What's different about the two kinds of data?

**Answer:** A line plot makes sense for showing change over time (monthly revenue) or another ordered value (`sin(x)`), but doesn't work for categories since the data isn't a continuous scale.
---

## ⏱️ Section 8: Timing and Performance (08)

22. What's the difference between `%time`, `%timeit`, `%%time`, and `%%timeit`?  
    `Answer:` 
    - `%time` runs an expression for **one line** once and reports how long that single execution took. 
    - `%timeit` runs an expression for **one line** many times and reports the average execution time.
    - `%%time` runs **the whole cell** once and reports how long that single execution took.
    - `%%timeit` runs **the whole cell** many times and reports the average execution time.

23. Name two things that make a timing comparison **unfair**.  
    `Answer:` Timing **list coversions** for one expression but not the other.

24. What does `%prun` tell you that `%timeit` doesn't?  
    `Answer:` `%prun`also tells you the time spent in each function called.

---

### ✏️ Task: Timing Comparison

```python
# Build a list of the first 500,000 integers, and a NumPy array of the same.
numbers_list = list(range(500_000))
numbers_array = np.array(numbers_list)

# Use %timeit -o to compare squaring the list with a comprehension
# vs. squaring the array (numbers ** 2).
list_time = %timeit -o [x**2 for x in numbers_list]
array_time = %timeit -o numbers_array**2

# Confirm both give the same values, then print how many times faster NumPy is.
list_squared = [x**2 for x in numbers_list]
array_squared = numbers_array**2
print(np.array_equal(np.array(list_squared), array_squared))
print(f'NumPy is about {list_time.average / array_time.average:.0f}x faster')

```

### ✏️ Task: Find the Repeated Work

```python
# This function is slow. Time it, find the repeated work, fix it, and time it again:
def above_average(values):
    return [v for v in values if v > sum(values) / len(values)]

slow_time = %timeit -o above_average(values)

# The repeated work is sum(values) / len(values)
# Fixed function:
def above_average_fixed(values):
    average = sum(values) / len(values)
    return [v for v in values if v > average]

fast_time = %timeit -o above_average_fixed(values)
```

### 🤖 Explain It

In your own words: why does `%timeit` run your code many times instead of just once like `%time`? And why should you "measure first" instead of rewriting code that just *looks* slow?

**Answer:** 
- `%timeit` runs code many times to ensure a more accurate result, as only running code once like `%time` often gives unreliable results.
- You should "measure first" to find and understand where bottlenecks are occuring, as rewriting code that just *looks* slow may not solve the real workload issue at all.

---

## 🧾 Submit Checklist

- [x] I used at least 3 different magic commands, including one cell magic and one `!` shell command.
- [x] I fixed a notebook that only worked when run out of order, and I can explain why it failed.
- [x] I ran **Restart & Run All** on my notebooks before submitting.
- [x] I used `?`, `help()`, or `dir()` to look something up instead of guessing.
- [x] I wrote a Markdown cell with a heading, a list, a table, and LaTeX math.
- [x] I wrote and read back a text file, a JSON file, and a CSV file using `pathlib` paths.
- [x] I loaded data with Pandas and converted it between at least two formats.
- [x] I built at least one plot with a title, axis labels, and (if applicable) a legend, and saved it to a file.
- [x] I timed two approaches fairly with `%timeit`.
- [x] I uploaded each notebook's `NN-OutputFiles` folder along with the notebook.
- [x] I completed the "Explain It" prompts in my own words.
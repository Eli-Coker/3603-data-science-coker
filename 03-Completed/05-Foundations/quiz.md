# 📝 Quiz: 05 - Foundations

45 questions covering all 8 Foundations notebooks, in order: magic commands, Jupyter workflow, getting help, Markdown, files and paths, data I/O, plotting with NumPy, and timing. Mix of multiple choice, true/false, code-tracing, and short answer.

This is a conceptual self-check. For hands-on practice writing and running real code, see `Foundations_Quiz.ipynb` in this folder.

Try every question on your own first. The Answer Key is at the bottom, no peeking. If you're using an AI tutor, paste in *your answer* and ask it to check your reasoning rather than asking it to solve the question first.

---

## Section A — Magic Commands (01)

**1.** (Multiple Choice) Which magic command shows your current working directory?
A) `%pwd`  B) `%cd`  C) `%ls`  D) `%dir`

**Answer:** A (`%pwd`)

**2.** (Short Answer) What's the difference between a line magic (`%pwd`), a cell magic (`%%writefile`), and a shell command (`!ls`)?

**Answer:** A line magic (`%pwd`) applies to one line, a cell magic (`%%writefile`) applies to the entire code cell, and a shell command (`!ls`) sends the line to the OS's shell.

**3.** (Code Tracing) A folder contains only `a.csv` and `b.txt`. What kind of value is stored in `files`, and what does it contain?
```python
files = !ls
```

**Answer:** A list of lines

**4.** (True/False) `%cd ..  # go up one folder` moves you to the parent folder.

**Answer:** False, the '# go up one folder' comment will cause an error

**5.** (Short Answer) Inside a notebook, why should you install packages with `%pip install` instead of `!pip install`?

**Answer:** Because `%pip install` installs the same notebook enviroment the notebook kernel is on, while `!pip install` uses whichever pip the shell finds first, which may belong to a different python.

**6.** (True/False) `%who` only shows variable *names*, while `%whos` also shows their types and a value summary.

**Answer:** True

---

## Section B — Jupyter Workflow (02)

**7.** (Multiple Choice) In Command mode, which keyboard shortcut inserts a new cell *below* the current one?
A) `A`  B) `B`  C) `D D`  D) `M`

**Answer:** B

**8.** (Short Answer) What's the practical difference between Command mode and Edit mode? You press `B` and the letter "b" appears in your code. What happened, and what should you press?

**Answer:** 'Command mode' acts on the whole cell, while 'Edit mode' types inside the cell. If you press `B` and the letter "b" appears in the cell, that means you are in 'Edit mode' and should switch to 'Command mode' by pressing 'Esc'.

**9.** (Code Tracing) What does this cell display when it runs?
```python
x = 5
x * 2
x * 3
```

**Answer:** This cell will display 15 when it runs (only the last line's value).

**10.** (Short Answer) A cell near the bottom of a notebook shows `[7]`, and the cell above it shows `[9]`. What does that tell you?

**Answer:** The cell near the bottom was executed before the above cell.

**11.** (True/False) If you delete the cell that created the variable `message`, `message` is removed from memory immediately.

**Answer:** False

**12.** (Short Answer) Why should you **Restart & Run All** before submitting a notebook?

**Answer:** You should **Restart & Run All** before submitting a notebook to ensure that every code cell executes properly in order without relying on leftover data in memory.

---

## Section C — Getting Help (03)

**13.** (Short Answer) `?` shows a docstring. What does `??` sometimes show that `?` doesn't, and why doesn't it always work?

**Answer:** Unlike `?`, `??` tries to show the source code for a docstring, but it doesn't work if used on something written in 'C'.

**14.** (Multiple Choice) The signature is `sorted(iterable, /, *, key=None, reverse=False)`. Which call is valid?
A) `sorted(iterable=nums)`  B) `sorted(nums, None, True)`  C) `sorted(nums, reverse=True)`  D) `sorted()`

**Answer:** C (`sorted(nums, reverse=True)`)

**15.** (Code Tracing) What error does this raise, and what does it mean?
```python
numbers = [1, 2, 3]
numbers.mean()
```

**Answer:** This code raises an 'AttributeError' - 'numbers' is a list object, which doesn't have the attribute 'mean'.

**16.** (Short Answer) A long traceback fills the screen. Which line should you read first, and why?

**Answer:** You should read the **last line** first because it will name the error type and say what went wrong.

**17.** (Short Answer) What does `dir(obj)` give you that Tab completion doesn't?

**Answer:** `dir(obj)` gives you a complete list of attributes and methods for an object. 

---

## Section D — Markdown (04)

**18.** (Short Answer) What's the Markdown syntax for a level-2 heading (like `## Section 2`)?

**Answer:** `## ____`

**19.** (Short Answer) How do you write **inline** LaTeX math in a Markdown cell, versus a **block** equation on its own line(s)?

**Answer:** 'Inline' LaTex math uses single '$' signs, while 'block' equations use '$$'.

**20.** (Short Answer) The Markdown text `The item costs $5 and the tax is $2.` renders strangely. Why, and how do you fix it?

**Answer:** The text renders strangely because '$' indicates LaTeX math. To fix this, use backslashes('\') to escape:  
- (e.g.) The item costs \$5 and the tax is \$2.

**21.** (Short Answer) You typed two lines directly under each other in a Markdown cell, but they render as **one** line. Name two ways to fix it.

**Answer:** You can use a <br> tag to force a line break or end a line with two spaces.

**22.** (Short Answer) Why might you add narrative Markdown cells between code cells instead of just writing code comments?

**Answer:** While code comments tend to be used to explain specific lines of code, narrative 'markdown cells' help to explain the larger goal of the code and present more thoughful conclusions.

---

## Section E — Files and Paths (05)

**23.** (Code Tracing) What does this print?
```python
with open('x.txt', 'w', encoding='utf-8') as f:
    f.write('hi')

with open('x.txt', 'r', encoding='utf-8') as f:
    print(f.read())
```

**Answer:** hi

**24.** (Multiple Choice) Which file mode adds to the end of an existing file **without** erasing it?
A) `'r'`  B) `'w'`  C) `'a'`  D) `'x'`

**Answer:** C (`'a'`)

**25.** (Code Tracing) What does this print?
```python
from pathlib import Path
p = Path('data') / 'sales_2026.csv'
print(p.name, p.stem, p.suffix)
```

**Answer:** sales_2026.csv sales_2026 .csv

**26.** (Short Answer) Why is it good practice to use a relative path (like `'data/file.csv'`) instead of an absolute path (like `'C:/Users/yourname/...'`) in a notebook you'll share or submit?

**Answer:** A relative path starts from the current working directory, allowing for portability across systems, while an absolute path will only work on your own system.

**27.** (Code Tracing) `scores.csv` contains the two lines `Name,Score` and `Alice,90`. What does this print, and why might that cause a problem?
```python
import csv
with open('scores.csv', newline='', encoding='utf-8') as f:
    rows = list(csv.reader(f))
print(rows[1])
```

**Answer:** This will print '['Alice', '90']', which might cause a problem if you want to do math with these values because csv.reader reads everything as *strings*.

**28.** (True/False) After saving `{'point': (3, 4)}` with `json.dump` and reading it back with `json.load`, you get back exactly the same dictionary.

**Answer:** False, JSON does not have a tuple type, so the tuple will come back as a *list* through `json.load`.

---

## Section F — Data Input and Output (06)

**29.** (Short Answer) What does `pd.read_csv('file.csv')` return?

**Answer:** `pd.read_csv('file.csv')` returns a DataFrame

**30.** (Multiple Choice) Which DataFrame method shows summary statistics (mean, standard deviation, min/max, etc.)?
A) `.head()`  B) `.info()`  C) `.describe()`  D) `.columns()`

**Answer:** C (`.describe()`)

**31.** (Short Answer) You save a DataFrame with `df.to_csv('out.csv')`, read it back, and find an extra `Unnamed: 0` column. What caused it, and how do you prevent it?

**Answer:** The DataFrame saved an extra index column. To prevent this, use index=False `df.to_csv('out.csv', index=False)`

**32.** (Short Answer) What does JSON written with `orient='records'` look like, and why is it usually the layout you want?

**Answer:** `orient='records'` looks like a list with one dictionary per row, which is usually the layout you want as most APIs are formatted in this way.

**33.** (Short Answer) After `pd.read_csv`, the ZIP code `02108` shows up as `2108`. Why, and how do you fix it?

**Answer:** `pd.read_csv` interprets `02108` as a number, so leading zeros vanish. Use `dtype={'Zip': str}` to fix it.

**34.** (Short Answer) What does `pd.read_excel('file.xlsx', sheet_name=None)` return?

**Answer:** `pd.read_excel('file.xlsx', sheet_name=None)` returns a dictionary of DataFrames.

---

## Section G — Plotting with NumPy and Matplotlib (07)

**35.** (Code Tracing) What do these two lines print?
```python
print([1, 2] * 2)
print(np.array([1, 2]) * 2)
```

**36.** (Matching) Choose the best chart (line, bar, scatter, or histogram) for each question:
a) Which department sold the most? 

**Answer:** Bar Chart

b) How did daily website visits change over a month?

**Answer:** Line Plot

c) Is there a relationship between price and units sold?

**Answer:** Scatter Plot

d) What is the distribution of customer order values?

**Answer:** Histogram

**37.** (Short Answer) A histogram and a bar chart both draw rectangles. What's the difference in what they show?

**Answer:** Bar Charts compare categories, while histograms show the distribution of numeric data.

**38.** (Short Answer) You call `plt.show()` and then `plt.savefig('chart.png')`, and the saved image is blank. Why?

**Answer:** Calling `plt.show()` finishes the figure and clears it, resulting in a blank image if you save afterwards.

**39.** (Short Answer) On a box plot, what does the line **inside** the box represent, and what do the dots **beyond** the whiskers represent?

**Answer:** The line inside the box represents the **median**, and the dots beyond the whiskers represent **possible outliers**.

---

## Section H — Timing and Performance (08)

**40.** (Short Answer) What's the difference between `%time` and `%timeit`, and why is `%timeit` more trustworthy for comparisons?

**Answer:** `%time` runs an expression once and reports how long that single execution took. `%timeit` runs an expression many times and reports the average execution time, resulting in more reliable comparisons.

**41.** (Short Answer) Why is a NumPy vectorized operation like `arr ** 2` usually much faster than a Python `for` loop doing the same calculation element by element?

**Answer:** NumPy runs the whole loop in efficient compiled code, while a Python 'for' loop handles one value at a time.

**42.** (True/False) A variable created inside a `%%timeit` cell is available in the cells after it.

**Answer:** False

**43.** (Short Answer) What's unfair about comparing `%timeit np.array(my_list) ** 2` against `%timeit arr ** 2` to decide whether squaring is fast?

**Answer:** `%timeit np.array(my_list) ** 2` has to convert the list to an array every time, while `%timeit arr ** 2` doesn't.

**44.** (Short Answer) Why is `[s / max(scores) for s in scores]` slow for large lists? How would you fix it, and roughly what happens to its runtime when the list doubles in size?

**Answer:** `[s / max(scores) for s in scores]` is slow for large lists because each loop scans the entire list. If the list doubles in size, the runtime becomes 4x slower. To fix this, compute the max outside of the loop. 

**45.** (Multiple Choice) What does `%prun` show you?
A) Only the total time of the cell  B) How much time was spent in each function called  C) How much memory each variable uses  D) The source code of a function

**Answer:** B (How much time was spent in each function called)
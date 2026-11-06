# 📝 Worksheet: 06 - Working with Data (Advanced)

Use this worksheet to reinforce Pandas Series/DataFrames and the core data-wrangling workflow: load, explore, select, clean, transform, sort/filter/search, group, and combine. Each section ends with an **🤖 Explain It** prompt — write your explanation in your own words, then (optionally) paste it into an AI tutor and ask it to point out anything you got wrong or left out.

---

## 🐼 Section 1: Series and DataFrames

1. What's the difference between a Pandas `Series` and a `DataFrame`? How does a list of dictionaries (from Module 03) turn into one?  
   `Answer:` A `Series` is one labeled column of values, while a `DataFrame` is a labeled table. A list of dictionaries turns into a Series giving each value a label, and becomes a DataFrame by turning the dictionary keys to indexes.

2. If you add two `Series` together and a label appears in only one of them, what value do you get at that label, and why?  
   `Answer:` The value you would get at that label is `NaN`, as pandas did not find a mathing value in the other Series.

---

### ✏️ Task: Series Basics

```python
# Create a Series from a dictionary mapping 4 of your classes to your grade in each.
grades = {
    'Data Science': 100,
    'Database Management': 95,
    'Government I': 98,
    'Spanish': 92
}
grades_series = pd.Series(grades)

# Print the Series, then print the average of all grades (hint: .mean()).
print("Grades:")
print(grades_series)

print("\nAverage grade:")
print(grades_series.mean())
```

### 🤖 Explain It

In your own words: how is a Pandas `Series` similar to a Python dictionary, and how is it similar to a list? What does it borrow from each?

**Answer:** A Pandas `Series` is similar to a Python dictionary in that they both have labels associated with the values they hold. On the other hand, a `Series` is similar to a list as both act as ordered sequences of values.
---

## 📂 Section 2: Loading and Exploring

3. What does `df.info()` tell you that `df.describe()` doesn't?  
   `Answer:` `df.info()` additionally tells you about the data types for columns, non-null counts, and memory usage.

4. If `df.isnull().sum()` shows `Age: 177`, what does that number mean?  
   `Answer:` The result of `177` would mean that there are that many missing values under Age.

5. In `titanic.csv`, what does **one row** represent, and which column identifies each row?  
   `Answer:` In `titanic.csv`, one row represents a passenger, and the PassengerId column identifies each row.

---

### ✏️ Task: First Look at a Dataset

```python
# Load pokemon.csv.
poke = pd.read_csv('pokemon.csv')

# Print its shape, its columns, and .describe() for just the numeric columns.
print(poke.shape)
print(poke.columns)
print(poke[['#', 'Total', 'HP', 'Attack', 'Defense']].describe())

# Which column has the most missing values, if any?
# ANSWER: The `Type 2` column has the most missing values.
```

### 🤖 Explain It

In your own words: why is it worth running `.info()` and `.isnull().sum()` on a dataset *before* you start analyzing it, rather than jumping straight to the questions you actually care about?

**Answer:** It is worth running `.info()` and `.isnull().sum()` beforehand as it helps you to understand the quality and structure of the data before jumping to conclusions.
---

## 🎯 Section 3: Indexing and Selection

6. Rewrite this using `.loc[]` instead of bracket + `.iloc[]` mixed together — or explain why you can't mix them the way it's written:
```python
df.iloc[df['Age'] < 10]  # this is actually broken — why?
```
   `Answer:` df.loc[df['Age'] < 10] - .iloc[] breaks in this case because it expects numeric indexes whereas the inner expression creates labels.

7. What's wrong with `df[df['Age'] < 10 and df['Fare'] > 100]`, and how would you fix it?  
   `Answer:` The issue is the use of `and`; to fix it, use `&`: `df[(df['Age'] < 10) & (df['Fare'] > 100)]`

8. Rewrite `df[(df['Pclass'] == 1) | (df['Pclass'] == 2)]` with `.isin()`. Why is `.isin()` easier to read when there are five values to match instead of two?  
   `Answer:` df[df['Pclass'].isin([1, 2])] - `.isin()` is easier to read when there are more values as it is more concise.

---

### ✏️ Task: Titanic Slicing

```python
# Using titanic.csv:
# 1. Select passengers in 3rd class (Pclass == 3) who survived (Survived == 1).
# 2. Of those, show only the Name, Age, and Fare columns.
# 3. Sort the result by Fare, descending.

(df.loc[(df['Pclass'] == 3) & (df['Survived'] == 1), ['Name', 'Age', 'Fare']]
   .sort_values('Fare', ascending=False))
```

### 🤖 Explain It

In your own words: why does `df.iloc[df['Age'] < 10]` not work, when `df.loc[df['Age'] < 10]` and `df[df['Age'] < 10]` both do?

**Answer:** `df.loc[df['Age'] < 10]` and `df[df['Age'] < 10]` work in this case as `.loc` and boolean masks are designed for labels and conditions. `df.iloc[df['Age'] < 10]` does not work as `.iloc` is designed for numeric positions, which the inner expression does not provide in this case.

---

## 🧼 Section 4: Cleaning

9. If a column has the values `['25', 'thirty', '35']`, what happens when you run `pd.to_numeric(col, errors='coerce')` on it?  
   `Answer:` 'thirty' will not be converted, and `errors='coerce'` will turn it into `NaN`.

10. When would you choose `.dropna()` over `.fillna()`, and vice versa?  
   `Answer:` You would choose `.dropna()` over `.fillna()` when missing values are not useful, and vice versa when you want to keep the data and replace the missing values.

11. A survey stores missing ages as `-1`. Why is that *worse* for analysis than a blank (`NaN`), and what one-line fix turns them into real missing values?  
   `Answer:` Storing the missing ages as `-1` is worse because Pandas will treat is as a normal value, hiding it from `.isnull()`. A one-line fix for this is `df['Age'] = df['Age'].replace(-1, np.nan)`

12. Two rows share an `order_id` but have different amounts. Will `df.drop_duplicates()` remove one? What argument makes it compare only `order_id`?  
   `Answer:` `df.drop_duplicates()` will not remove a row - it will only drop a row that is an **exact** duplicate. Use a subset argument to compare only `order_id`: `df.drop_duplicates(subset=['order_id'])`

---

### ✏️ Task: Clean a Column

```python
# Using ufo.csv:
# 1. Check .isnull().sum() for the whole dataset.
ufo = pd.read_csv('ufo.csv')
print(ufo.isnull().sum())

# 2. Pick the column with the most missing values.
missing_counts = ufo.isnull().sum()
most_missing = missing_counts.nlargest(1).index[0]

# 3. Decide (and justify in a comment) whether dropping or filling makes more
#    sense for that specific column, then do it.
ufo[most_missing] = ufo[most_missing].fillna('Unknown')

# In this case, 'Shape' is the column with the most missing values, 
# thus filling makes more sense for this column as the rest of the data is still valuable.
```

### 🤖 Explain It

In your own words: why might dropping rows with missing data be a bad idea if a large fraction of your dataset has at least one missing value somewhere?

**Answer:** In this case, it would be a bad idea to drop rows with missing data as you lose a ton of valuable data and be left with a much smaller dataset.

---

## 🧱 Section 5: Column Operations, Sorting, and Filtering

13. What's the difference between `df.rename(columns={'a': 'b'})` and `df.columns = ['b', 'c', 'd']`?  
   `Answer:` `df.rename(columns={'a': 'b'})` only renames column 'a', whereas `df.columns = ['b', 'c', 'd']` replaces the whole column list.

14. Rewrite this bracket-filter as a `.query()` call:
```python
df[(df['math_score'] >= 80) & (df['science_score'] >= 80)]
```
   `Answer:` df.query('math_score >= 80 and science_score >= 80')

15. If `status` is a brand-new column, what do the rows with `score >= 70` contain after `df.loc[df['score'] < 70, 'status'] = 'review'`? How do you give every row a default first?  
   `Answer:` In this case, `review` will only be assigned to rows where `score >= 70`, leaving every other row's status column with `NaN`. To give every row a default first, initialize the `status` column beforehand.

---

### ✏️ Task: Build a Feature

```python
# Using students.csv:
# 1. Create a "total_score" column (math + science).
students["total_score"] = (students["math_score"] + students["science_score"])

# 2. Sort by total_score, descending.
top_students = students.sort_values("total_score", ascending=False)

# 3. Print just the top 3 students' first_name and total_score.
print(top_students[["first_name", "total_score"]].head(3))
```

### ✏️ Task: Loop vs. Vectorized

```python
# Using students.csv:
# 1. Build a list of each student's total score with an .itertuples() loop.
total_score = []

for row in students.itertuples():
    total_score.append(row.math_score + row.science_score)

students["total_score_loop"] = total_score

# 2. Compute the same totals with one whole-column expression.
students["total_score_vector"] = (students["math_score"] + students["science_score"])

# 3. Confirm they match, then use %timeit to compare the two.
print("Results match:", (students["total_score_loop"] == students["total_score_vector"]).all())

%timeit [row.math_score + row.science_score for row in students.itertuples()]

%timeit students["math_score"] + students["science_score"]
```

### 🤖 Explain It

In your own words: what does "feature engineering" mean in the context of `total_score` or `average_score` — why create a new column instead of just computing the value fresh every time you need it?

**Answer:** "Feature engineering" in this context means to create new variables derived from existing data, which has the advantage of reuse and avoiding redundancy.

---

## 🧩 Section 6: Grouping and Combining

16. Describe the three steps of `df.groupby('Pclass')['Survived'].mean()` (split, apply, combine) in plain words. What does the result tell you?  
   `Answer:` Step 1. Split the rows into groups by `Pclass` | 2. Apply the `.mean(0)` function to the `Survived` column | 
   <br>3. Combine the results into a new series. | The result tells you the survival rate for each passenger class.

17. What's the difference between `pd.concat()` and `.merge()`, and between a `'left'` and an `'inner'` merge?  
   `Answer:` `pd.concat()` stacks rows of the same data, whereas `.merge()` adds related columns through a shared key. `'left'` keeps every row of the "left" table in a merge, whereas `'inner'` only keeps rows whose key is in both tables.

---

### ✏️ Task: Survival by Group

```python
# Using titanic.csv:
# 1. Find the survival rate by Pclass, then by Pclass AND Sex together.
survival_by_class = df.groupby('Pclass')['Survived'].mean()
print("Survival rate by Pclass:")
print(survival_by_class)

survival_by_class_sex = (df.groupby(['Pclass', 'Sex'])['Survived'].mean())

# 2. Use .agg() to show, per Embarked port: passengers, average Fare, survival rate.
embarked_summary = (df.groupby('Embarked')
                    .agg(
                     passengers=('PassengerId', 'count'),
                     average_fare=('Fare', 'mean'),
                     survival_rate=('Survived', 'mean')))

# 3. .reset_index() the result and sort it by survival rate, highest first.
embarked_summary = (embarked_summary.reset_index().sort_values('survival_rate', ascending=False))
```

### ✏️ Task: Join Two Tables

```python
# Build a table of 5 students (student_id, name) and a table of 4 grades
students = pd.DataFrame({'student_id': [1, 2, 3, 4, 5], 'name': ['Joe', 'Chris', 'Sally', 'Gina', 'Jay']})

# (student_id, grade), where one student has no grade.
grades = pd.DataFrame({'student_id': [1, 2, 3, 4], 'grade': [77, 98, 82, 90]})

# Merge them with how='left' and with how='inner'. How many rows does each give, and why?
left_merge = students.merge(grades, on='student_id', how='left')
print("Left merge:")
print(left_merge)
print("Rows:", len(left_merge))

inner_merge = students.merge(grades, on='student_id', how='inner')
print("\nInner merge:")
print(inner_merge)
print("Rows:", len(inner_merge))

# Left merge gives 5 rows because all data is preserved, whereas Inner merge gives only 4 rows because student 5 is dropped.
```

### 🤖 Explain It

In your own words: when you merge UFO sightings (state codes like `'tx'`) with populations (codes like `'TX'`), every state fails to match at first. Why, and what does that teach you about checking keys *before* you join?

**Answer:* Merges require keys to be the exact same, thus `'tx'` and `'TX'` will fail to match because pandas sees them as different strings. This shows the importance of checking keys *before* joining in order to avoid errors such as these.
---

## 🧾 Submit Checklist

- [X] I created a `Series` and a `DataFrame` from Python containers (a dictionary or a list of dictionaries).
- [X] I loaded a local CSV into a DataFrame and inspected it with `.info()` and `.describe()`.
- [X] I used both `.loc[]` and `.iloc[]` at least once each.
- [X] I filtered a DataFrame using a compound condition (`&` or `|`).
- [X] I cleaned at least one column with `.fillna()`, `.dropna()`, or `pd.to_numeric()`.
- [X] I created a new column and sorted by it.
- [X] I removed duplicate rows or replaced a placeholder value with `NaN`.
- [X] I filtered with `.isin()`, `.between()`, or `.str.contains()`.
- [X] I used a whole-column (vectorized) calculation instead of a row-by-row loop.
- [X] I summarized groups with `groupby()` (and `.agg()`), and combined tables with `pd.concat()` or `.merge()`.
- [X] I completed the "Explain It" prompts in my own words.
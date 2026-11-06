# 📝 Quiz: 06 - Working with Data (Advanced)

47 questions covering Pandas Series/DataFrames, loading/exploring data, indexing/selection, cleaning, column operations, sorting/filtering/searching, grouping and combining tables, and a "going further" bonus. Mix of multiple choice, true/false, code-tracing, and short answer.

Try every question on your own first — the Answer Key is at the bottom, no peeking. If you're using an AI tutor, paste in *your answer* and ask it to check your reasoning rather than asking it to solve the question first.

---

## Section A — Series and DataFrames

**1.** (Short Answer) What's the difference between a Pandas `Series` and a `DataFrame`?

`Answer:` A `Series` is one labeled column of values, while a `DataFrame` is a labeled table.

**2.** (Code Tracing) What prints?
```python
s = pd.Series({'a': 1, 'b': 2})
print(s['a'])
```
`Answer:` 1

**3.** (Short Answer) What does `df.shape` return?

`Answer:` `df.shape` returns the dimensions of a dataframe as a tuple.

**4.** (Short Answer) If you add two `Series` together and one has a label the other doesn't, what happens at that label?

`Answer:` You would get the value `NaN` at that label, as pandas did not find a mathing value in the other Series.

**5.** (Short Answer) You have a list of dictionaries, one per student (the way you stored records in Module 03b). What does `pd.DataFrame(that_list)` turn each dictionary into?

`Answer:` `pd.DataFrame(that_list)` turns each dictionary turns into a row.

**6.** (Code Tracing) What prints?
```python
scores = pd.Series([70, 95, 88])
print(scores[scores > 80].tolist())
```
`Answer:` [95, 88]

---

## Section B — Loading and Exploring Data

**7.** (Multiple Choice) Which method shows summary statistics (mean, std, min/max) for numeric columns?
A) `.head()`  B) `.columns`  C) `.describe()`  D) `.shape`

`Answer:` C) `.describe()`

**8.** (Short Answer) What's the difference between what `.head()` and `.info()` each tell you about a DataFrame?

`Answer:` `.head()` shows the first 5 rows of data values, while `.info()` shows structural information like the number of rows and columns, non-null counts per column, dtypes, and memory use.

**9.** (Short Answer) How do you count how many missing values are in *each column* of a DataFrame?

`Answer:` Use `df.isnull().sum()` to show the total missing values per DataFrame column.

**10.** (Short Answer) What do `df.duplicated().sum()` and `df['col'].value_counts(dropna=False)` each tell you?

`Answer:` `df.duplicated().sum()` tells you how many rows are exact duplicates, while `df['col'].value_counts(dropna=False)` tells you how often each value appears in a column, including missing values.

**11.** (Short Answer) Titanic's `Age` column holds whole numbers, but its dtype is `float64`. Why?

`Answer:` `Age` has missing values, and `NaN` only exists as a float.

---

## Section C — Indexing and Selection

**12.** (Short Answer) What's the difference between `.loc[]` and `.iloc[]`?

`Answer:` `.loc[]` is used for label-based selection, whereas `.iloc[]` is used for numeric position-based selection.

**13.** (Short Answer) Is `df.loc[0:4]` inclusive or exclusive of row `4`? What about `df.iloc[0:4]` and position `4`?

`Answer:` `df.loc[0:4]` is inclusive of row `r`, whereas `df.iloc[0:4]` excludes position `4`.

**14.** (Short Answer) What symbols does Pandas require for combining conditions when filtering a DataFrame (instead of the `and`/`or` keywords)?

`Answer:` For filtering a DataFrame, Pandas uses `&` for `and`, `|` for `or`, and `~` for `not`.

**15.** (Short Answer) What does `df[df['Age'] < 10]` return?

`Answer:` `df[df['Age'] < 10]` returns a filtered DataFrame containing only rows where `Age` is less than 10. 

**16.** (Short Answer) Rewrite `df[(df['Embarked'] == 'C') | (df['Embarked'] == 'Q')]` using `.isin()`. Does `df['Age'].between(13, 19)` include ages 13 and 19?

`Answer:` `df[df['Embarked'].isin(['C', 'Q'])]` | `df['Age'].between(13, 19)` does include ages 13 and 19.

**17.** (Multiple Choice) Which one returns a `DataFrame` rather than a `Series`?
A) `df['Age']`  B) `df[['Age']]`  C) `df.Age`  D) `df.loc[0]`

`Answer:` B) `df[['Age']]`

**18.** (Short Answer) After `by_id = df.set_index('PassengerId')`, what does `by_id.loc[2]` select, and how is that different from `df.loc[2]`?

`Answer:` `by_id.loc[2]` selects the row whose `PassengerId` is `2`. This is different from `df.loc[2]`, as that would select the row with an *index label* of 2.

**19.** (Code Tracing) After `by_id = titanic.set_index('PassengerId')`, do `by_id.loc[3]` and `by_id.iloc[3]` select the same passenger? Why or why not?

`Answer:` No, `by_id.loc[3]` and `by_id.iloc[3]` will not select the same passenger because `.loc[]` uses index labels, while `.iloc[]` uses numeric positions.

**20.** (Short Answer) Write a filter for passengers who did **not** board at Southampton (`'S'`), using `~` and `.isin()`.

`Answer:` `df[~df['Embarked'].isin(['S'])]`

**21.** (Short Answer) What's wrong with `df[df['Age'] < 10]['child'] = True`, and what should you write instead?

`Answer:` `df[df['Age'] < 10]['child'] = True` has a *chained assignment* problem: The first step makes a *copy* that is then thrown away without changing the original. Instead, use `.loc[]`: `df.loc[df['Age'] < 10, 'child'] = True`

---

## Section D — Cleaning

**22.** (Short Answer) What's the difference between `.dropna()` and `.fillna()`?

`Answer:` `.dropna()` removes all rows or columns containing missing values, whereas `.fillna()` replaces missing values with a chosen value.

**23.** (Short Answer) What does `pd.to_numeric(col, errors='coerce')` do to a value like `'ninety'` in that column?

`Answer:` 'ninety' will not be converted, and `errors='coerce'` will turn it into `NaN`.

**24.** (True/False) `NaN` and an empty string `""` are always treated identically by `.isnull()`.

`Answer:` False

**25.** (Short Answer) Two rows have the same `order_id` but different `amount`s. Does `df.drop_duplicates()` remove one of them? What would you write to keep only the last row for each `order_id`?

`Answer:` `df.drop_duplicates()` will not remove a row - it will only drop a row that is an **exact** duplicate. To keep only the last row for each `order_id`, use `keep='last'`: `df.drop_duplicates(subset=['order_id'], keep='last')`

**26.** (Short Answer) A survey stores missing ages as `-1`. Why is that a problem for `df['age'].mean()`, and how do you fix it?

`Answer:` Storing the missing ages as `-1` is a problem because Pandas will treat is as a normal value, making `df['age'].mean()` inaccurate. To fix this, use `df['Age'] = df['Age'].replace(-1, np.nan)`

**27.** (Short Answer) A date column holds `'2022-01-01'`, `'2022/03/01'`, and `'April 5, 2022'`. Why can `pd.to_datetime(col, errors='coerce')` turn two perfectly valid dates into `NaT`, and how do you fix it?

`Answer:` Because `pd.to_datetime` guesses the format from the first value (in this case `'2022-01-01'`), everything that doesn't match it is silently turned into `NaT`. To fix this, use `format='mixed'`: `pd.to_datetime(col, errors='coerce', format='mixed')`

**28.** (Short Answer) Why does `.astype('int64')` fail on a column with missing values, while `.astype('Int64')` works?

`Answer:`

**29.** (Short Answer) Before deleting rows with a repeated `order_id`, why would you look at `df[df.duplicated(subset=['order_id'], keep=False)]` first?

`Answer:` You should look at `df[df.duplicated(subset=['order_id'], keep=False)]` before deleting rows with a repeated `order_id` in order to examine which rows should be kept to avoid losing valuable data.

---

## Section E — Column Operations, Sorting, Filtering, and Searching

**30.** (Short Answer) How do you create a new column that's the sum of two existing numeric columns?

`Answer:` When creating the new column, you can use the `+` with two exisiting numeric columns and assign the reslt to the new column. 
- For example: `df['total_score'] = df['math_score'] + df['science_score']`

**31.** (Short Answer) What does `.apply()` do that you could also do with a `for` loop over rows — and why is `.apply()` usually preferred?

`Answer:` `.apply()` lets you run a function on every value in a column and is usually preferred for it's shorter/cleaner code.

**32.** (Short Answer) What does `ascending=False` do inside `df.sort_values(by='score', ascending=False)`?

`Answer:` `ascending=False` sorts the score values in *descending* order.

**33.** (Short Answer) What's the main advantage of `.query()` over bracket-based boolean filtering (`df[df['col'] > 5]`)?

`Answer:` The main advantage of `.query()` is readability, as it makes writing complex filters much more concise.

**34.** (Code Tracing) `bonus` is a brand-new column. What value do the rows with `score >= 80` get in it?
```python
df.loc[df['score'] < 80, 'bonus'] = 5
```
`Answer:` Rows with `score >= 80` receive `NaN`.

**35.** (Short Answer) To compute `price * qty` for every row, why should you write `df['price'] * df['qty']` instead of looping with `.iterrows()`? When *is* a loop (preferably `.itertuples()`) the right tool?

`Answer:` To compute `price * qty` for every row, you should write `df['price'] * df['qty']` instead as it is shorter, more readable, and more efficient. A loop like `.itertuples()` is the right tool when the task requires row by row processing.

**36.** (Short Answer) What do `case=False` and `na=False` each do in `df['name'].str.contains('an', case=False, na=False)`?

`Answer:` `case=False` makes the search *case-insensitve*, while `na=False` treats missing values like `NaN` as an invalid match.

**37.** (Code Tracing) A student has `math = 95` and `average = 91`. What is their `award` after these three lines, and what would it be if the last two lines were swapped?
```python
df['award'] = 'None'
df.loc[df['average'] >= 85, 'award'] = 'Honor Roll'
df.loc[df['math'] >= 90, 'award'] = 'Math Star'
```
`Answer:` After these three lines, the student's award is `Math Star`. If the last two lines were swaped, the award would be `Honor Roll`.

**38.** (Short Answer) What does `pd.cut(df['score'], bins=[0, 70, 90, 101], labels=['Low', 'Mid', 'High'], right=False)` do, and why is it usually better than `.apply()` with an `if`/`elif` function for the same job?

`Answer:` In this case, `pd.cut()` creates labeled score bands, with `0-70` being `Low`, `70-90` being `Mid`, and `90-100` as `High`, with `right=False` excluding `101`. This is usually better than using `.apply()` with an `if`/`elif` function as it is more concise and readable.

**39.** (Short Answer) What's the difference between `df.query('math_score >= minimum')` and `df.query('math_score >= @minimum')`?

`Answer:` `df.query('math_score >= minimum')` looks for an existing column called `minimum`, whereas `df.query('math_score >= @minimum')` uses the Python variable `minimum`.

**40.** (Code Tracing) What does each line return, and why are they different?
```python
books = pd.Series(['C++ Primer', 'C Programming'])
books.str.contains('C++').tolist()
books.str.contains('C++', regex=False).tolist()
```
`Answer:` The first line creates a series, the second line returns [True, True], and the third line returns [True, False]. The second and third lines differ because the use of `regex=False` determines how `C++` is interpreted.

---

## Section F — Grouping and Combining

**41.** (Code Tracing) What does this return?
```python
df = pd.DataFrame({'team': ['A', 'B', 'A', 'B'], 'points': [10, 4, 20, 6]})
df.groupby('team')['points'].mean()
```
`Answer:`
<br>team
<br>A    15.0
<br>B     5.0
<br>Name: points, dtype: float64

**42.** (Short Answer) Write a `groupby` with `.agg()` that gives, for each `team`, the number of rows and the total `points`, as columns named `games` and `total`.

`Answer:` df.groupby('team').agg(games=('points', 'count'), total=('points', 'sum'))

**43.** (Short Answer) When would you use `pd.concat()` instead of `.merge()`? What does `ignore_index=True` do?

`Answer:` You would use `pd.concat()` to stack rows of the same data together, and `.merge()` to add related columns through a shared key. `ignore_index=True` resets the index numbers in the result.

**44.** (Short Answer) In `orders.merge(prices, on='product_id', how='left')`, what happens to an order whose `product_id` isn't in `prices`? What would `how='inner'` do instead? And why does a merge on state codes fail when one table uses `'tx'` and the other uses `'TX'`?

`Answer:` `how='left'` keeps all rows from orders, even if there is no matching `product_id` in `prices`. `how='inner'` would only keep the rows that have matches in *both* tables. A merge on tables with state codes `'tx'` and `'TX'` respectively will fail to match because pandas sees them as different strings.

**45.** (Short Answer) In Titanic, `groupby('Pclass').size()` gives 216 for 1st class, but `groupby('Pclass')['Age'].count()` gives 186. Why are they different?

`Answer:` They are different `.size()` counts rows, whereas `.count()` counts non-missing values in a column.

**46.** (Short Answer) `purchases` has 6 rows. After `purchases.merge(buyers, on='buyer_id', how='left')`, it has 8. What probably happened, and how can `validate=` protect you?

`Answer:` It's likely that `buyers` contained duplicate `buyer_id` values. `validate=` will help as it tells Pandas what relationship you're expecting and will stop with an error.

---

## Section G — Going Further (Bonus)

**47.** (Short Answer) What do the `usecols` and `nrows` arguments to `pd.read_csv()` do, and when would you reach for them?

`Answer:` `usecols` would be used when you only need a few columns, as it loads only specified columns. `nrows` would be used when you want a quick sample of a large dataset, as it loads only the first `N` rows.
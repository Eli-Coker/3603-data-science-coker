# 📝 Worksheet: 07 - Describing Data

Use this worksheet to reinforce the descriptive workflow: what each column means, what's typical, how much it varies, what's unusual, how groups differ, and which columns move together. Each section ends with an **🤖 Explain It** prompt. Write your explanation in your own words, then (optionally) paste it into an AI tutor and ask it to point out anything you got wrong or left out.

---

## 🏷️ Section 1: Types of Data

1. Classify each as nominal, ordinal, interval, or ratio: `zip code`, `t-shirt size (S/M/L/XL)`, `year of birth`, `monthly rent`.  
   `Answer:` `zip code` - **nominal** | `t-shirt size (S/M/L/XL)` - **ordinal** | `year of birth` - **interval** | `monthly rent` - **ratio**

2. A column has dtype `int64` and only 4 distinct values. Name two things it might really be, and how you'd decide.  
   `Answer:` This instance of `int64` might really be a **category** or an **ordered category**. I'd decide based on the meaning of the distinct values and whether or not they have a meaningful order.

---

### ✏️ Task: Record the Meaning

```python
# Using titanic.csv:
# 1. Convert Embarked to 'category' and map C/Q/S to 'Cherbourg'/'Queenstown'/'Southampton'.
titanic['Embarked'] = titanic['Embarked'].astype('category')
embarked_map = {'C': 'Cherbourg', 'Q': 'Queenstown', 'S': 'Southampton'}

# 2. Create an ordered 'class' column (3rd < 2nd < 1st).
class_labels = {1: '1st', 2: '2nd', 3: '3rd'}
class_order = pd.CategoricalDtype(['3rd', '2nd', '1st'], ordered=True)

titanic['class'] = titanic['Pclass'].map(class_labels).astype(class_order)

# 3. Print the share of passengers above 3rd class, using a comparison on 'class'.
above_3rd = (titanic["class"] > "3rd").mean()
print(f"Share of passengers above 3rd class: {above_3rd:.3f}")
```

### 🤖 Explain It

In your own words: why does it matter whether a variable is nominal or ordinal before you compute anything with it? What could go wrong if you averaged an ordinal column's codes?

**Answer:** It's necessary to determine whether a variale is nominal or ordianl before computing because their measurement scale determines which mathematical operations can be used on them. For instance, you can't take the average of an ordinal column's codes because the gaps between numbers aren't guaranteed to be equal.

---

## 🎯 Section 2: Center and Spread

3. Why is the median usually reported for house prices instead of the mean?  
   `Answer:` House prices can have extreme/lopsided values, which the median is suited for.

4. You compute a standard deviation with pandas and get 14.53, and a classmate uses NumPy and gets 14.52. Who's wrong?  
   `Answer:` Neither is "wrong" per say. Pandas and NumPy use different defaults when calculating std, which can result in slightly different results. 

---

### ✏️ Task: Compare Center and Spread

```python
# Using pokemon.csv:
# For Attack, print the mean, median, std, and IQR.
attack = poke['Attack']
attack_iqr = attack.quantile(0.75) - attack.quantile(0.25)

print("All Pokémon")
print("Mean:", attack.mean())
print("Median:", attack.median())
print("Std:", attack.std())
print("IQR:", attack_iqr)

# Then do the same for Legendary Pokémon only.
legendary_attack = poke.loc[poke['Legendary'], 'Attack']
legendary_iqr = (legendary_attack.quantile(0.75) - legendary_attack.quantile(0.25))

print("\nLegendary Pokémon")
print("Mean:", legendary_attack.mean())
print("Median:", legendary_attack.median())
print("Std:", legendary_attack.std())
print("IQR:", legendary_iqr)

# Which group is more spread out, by std and by IQR? Do the two measures agree?
```
**Answer:** 'All Pokemon' are more spread compared to Legendaries, and both the std and IQR measures agree.

### 🤖 Explain It

In your own words: two classes have the same average exam score, but very different standard deviations. Describe what being a student in each class might be like.

**Answer:** For a student in the *lower standard deviation* class, their grades would generally be very similar to their classmates' grades. For a student in the *higher standard deviation* class, some classmates' may have very high grades while others may have very low grades.

---

## 📐 Section 3: Shape and Outliers

5. A column has mean 50, median 38, and `.skew()` of 2.1. Describe its shape.  
   `Answer:` This column is *strongly right-skewed*.

6. Name one situation where you **should** remove an outlier, and one where you shouldn't.  
   `Answer:` You should remove an outlier that represents an impossible value / error (e.g. age 1000). You shouldn't remove an outlier with an unusual but real/meaningful value (e.g. age 90).

---

### ✏️ Task: Outlier Report

```python
# Using penguins.csv (drop the 2 rows with no measurements first):
clean = penguins.dropna(subset=MEASUREMENTS).copy()

# 1. Write or copy iqr_fences(series, k=1.5).
def iqr_fences(series, k=1.5):
    """Return the (lower, upper) outlier fences for a numeric Series."""
    q1 = series.quantile(0.25)
    q3 = series.quantile(0.75)
    iqr = q3 - q1
    return q1 - k * iqr, q3 + k * iqr

# 2. Count outliers in body_mass_g overall, then within each species.
# 3. Print the flagged rows. Are any of them impossible values?
low, high = iqr_fences(clean['body_mass_g'])

overall_outliers = clean[
    (clean['body_mass_g'] < low) |
    (clean['body_mass_g'] > high)
]

print("Overall outliers:", len(overall_outliers))
print(overall_outliers[['species', 'island', 'sex', 'body_mass_g']])

for species, group in clean.groupby('species', observed=True):
    lower, upper = iqr_fences(group['body_mass_g'])

    outliers = group[
        (group['body_mass_g'] < lower) |
        (group['body_mass_g'] > upper)
    ]

    print(f"\n{species}: {len(outliers)} outliers")
    print(outliers[['species', 'island', 'sex', 'body_mass_g']])

```
**Answer:** Chinstrap had 2 flagged rows, but they do not have impossible values.

### 🤖 Explain It

In your own words: explain to a classmate why "outlier" and "error" aren't the same thing, using an example from the Titanic fares.

**Answer:** An "outlier" is an unusually high or low value, while an "error" is an incorrect value. For example, a fare of **512.33** would be flagged as an outlier as it is larger than most fares, but it is not an incorrect value. However, a fare of **-1.00** would be an error as there can not be a negative fare.

---

## 👥 Section 4: Comparing Groups

7. When should you compare groups with counts, and when with rates?  
   `Answer:` You should compare with *counts* when the groups are the same size, and compare with *rates* when the groups are different sizes.

8. What's the difference between `normalize='index'` and `normalize='columns'` in `pd.crosstab()`? Write a question each one answers.  
   `Answer:` 
   - In `normalize='index'`, each *row* adds up to 100%. ("Within each class, what share is male?")
   - In `normalize='columns'` each *column* adds up to 100%. ("Of all the men, what share was in each class?")
   - In `pd.crosstab()`, the *whole table* adds up to 100%. ("What share of everyone is a 2nd-class male?")

---

### ✏️ Task: Survival Table

```python
# Using titanic.csv:
# 1. Bin Age into child (0-12), teen (13-18), adult (19-60), senior (61+) with pd.cut().
titanic['age_group'] = pd.cut(
    titanic['Age'],
    bins=[0, 12, 18, 60, 100],
    labels=['child', 'teen', 'adult', 'senior'],
)

# 2. Build a pivot_table of survival rate with age group as rows and Sex as columns.
survival_rate = pd.pivot_table(
    titanic,
    values='Survived',
    index='age_group',
    columns='Sex',
    aggfunc='mean',
    observed=False
)

print("Survival rate")
print(survival_rate)

# 3. Add the group sizes (a second pivot_table with aggfunc='size').
group_sizes = pd.pivot_table(
    titanic,
    index='age_group',
    columns='Sex',
    aggfunc='size',
    observed=False
)

print("\nGroup sizes")
print(group_sizes)

# Which cell has the highest rate? Is its group big enough to trust?
```
**Answer:** Senior females have the highest rate. However, the group size is only 3, thus not large enough to trust.

### 🤖 Explain It

In your own words: what's a confounder? Describe one in the Titanic data, and how you'd check for it with a table.

**Answer:** A confounder is a second variable that makes it appear as though a relationship is stronger or weaker than it really is. In the Titanic data, `Pclass` could be a confounder when comparing `Embarked` and survival. To check for this with a table, you could compare survival rates *within each passenger class* instead.

---

## 🔗 Section 5: Relationships and Correlation

9. When would you use Spearman instead of Pearson?  
   `Answer:` You would use **Spearman** instead of Pearson when the data is *ordinal*, the relationship is *curved but always rising (or always falling)*, or there are *outliers*.

10. A news story says "cities with more ice-cream sales have more drownings." Give a likely confounder.  
    `Answer:` A likely confounder would be *weather*, as hotter weather would contribute to more ice-cream sales and be associated with more water-based activities.

---

### ✏️ Task: Correlation Report

```python
# Using pokemon.csv:
# 1. Compute the Pearson and Spearman correlation matrices of the six stats.
pearson = poke[stats].corr(method='pearson')
spearman = poke[stats].corr(method='spearman')

# 2. List the three strongest pairs (use the upper triangle).
upper = np.triu(np.ones(pearson.shape, dtype=bool), k=1)

pearson_top3 = (pearson.where(upper).stack().rename('r').sort_values(key=abs, ascending=False).head(3))
spearman_top3 = (spearman.where(upper).stack().rename('r').sort_values(key=abs, ascending=False).head(3))

print("Top 3 Pearson pairs")
print(pearson_top3.round(3))

print("\nTop 3 Spearman pairs")
print(spearman_top3.round(3))

# 3. Recompute r(Attack, Defense) for Legendary and non-Legendary separately.
rows = []
for legendary, group in poke.groupby('Legendary'):
    rows.append({
        'group': f'Legendary={legendary}',
        'size': len(group),
        'r_attack_defense': group['Attack'].corr(group['Defense'])
    })

# Generation
for generation, group in poke.groupby('Generation'):
    rows.append({
        'group': f'Generation {generation}',
        'size': len(group),
        'r_attack_defense': group['Attack'].corr(group['Defense'])
    })

corr_attack_defense = pd.DataFrame(rows).round(3)

print(corr_attack_defense)
```

### 🤖 Explain It

In your own words: Anscombe's four datasets all have r = 0.82. What does that teach you about reporting a correlation without a plot? What's the danger of a single summary number?

**Answer:** Anscombe's Quartet shows that datasets can have the same correlation coefficient and still have very different patterns. Thus, relying on a single number (in this case r = 0.82) without a plot is dangerous as important details, like unusual patterns, can be hidden.

---

## 🧾 Submit Checklist

- [X] I built a data dictionary that separates dtype from measurement scale.
- [X] I used an ordered category and computed a proportion from a boolean column.
- [X] I reported center and spread that fit a column's shape, and explained `ddof`.
- [X] I flagged outliers with the IQR rule, inspected them, and decided what to do with them.
- [X] I compared groups with sizes and rates, using a crosstab and a pivot table.
- [X] I computed Pearson and Spearman correlations and explained a possible confounder.
- [X] I completed the "Explain It" prompts in my own words.
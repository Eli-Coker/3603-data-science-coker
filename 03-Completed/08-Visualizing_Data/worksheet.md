# 📝 Worksheet: 08 - Visualizing Data

Use this worksheet to reinforce object-oriented Matplotlib, pandas plotting, Seaborn, and chart design. Each section ends with an **🤖 Explain It** prompt. Write your explanation in your own words, then (optionally) paste it into an AI tutor and ask it to point out anything you got wrong or left out.

---

## 🖼️ Section 1: Matplotlib, Object-Oriented

1. What's the difference between `plt.title('X')` and `ax.set_title('X')`? When does the difference matter?  
   `Answer:` `plt.title('X')` is *pyplot style* and sets the title on a hidden "current axes". `ax.set_title('X')` is *object-oriented style* and sets the title on an *explicit axes object*. The difference matters when you're working with several charts, in which case `ax.set_title('X')` is preferable.

2. You're comparing three histograms in a 1 × 3 figure. Name two settings that make the panels fair to compare.  
   `Answer:` Using the *same axis scale* (`sharex=True`/`sharey=True`) or the *same bins* in every panel makes them fair to compare.

---

### ✏️ Task: A Reusable Chart Function

```python
# Write plot_distribution(ax, series, title, unit) that draws a histogram on ax,
# marks the mean and median with vertical lines, and labels everything.
def plot_distribution(ax, series, title, unit=''):
    """Histogram of a numeric Series on ax, with its mean and median marked."""
    values = series.dropna()
    ax.hist(values, bins=25, color='lightgray', edgecolor='white')
    ax.axvline(values.mean(), color='tab:red', linestyle='--', label=f'mean {values.mean():.1f}')
    ax.axvline(values.median(), color='tab:blue', label=f'median {values.median():.1f}')
    ax.set(title=title, xlabel=unit)
    ax.spines[['top', 'right']].set_visible(False)
    ax.legend(frameon=False)

# Use it to build a 2 x 2 figure of Titanic Age, Fare (log scale!), SibSp, and Parch.
fig, axes = plt.subplots(2, 2, figsize=(10, 8), layout='constrained')

plot_distribution(axes[0, 0], titanic['Age'], 'Age Distribution', 'Age (years)')
plot_distribution(axes[0, 1], titanic['Fare'], 'Fare Distribution', 'Fare ($)')
plot_distribution(axes[1, 0], titanic['SibSp'], 'SibSp Distribution', 'SibSp')
plot_distribution(axes[1, 1], titanic['Parch'], 'Parch Distribution', 'Parch')

axes[0, 1].set_xscale('log')

# Save the figure with fig.savefig().
plt.show()
```

### 🤖 Explain It

In your own words: why is a function that takes an `ax` argument more useful than a function that calls `plt.` directly?

**Answer:** A function that takes an `ax` argument is more useful because it can draw on any subplot you give it and allows you to reuse it in any figure/panel.

---

## 🐼 Section 2: Plotting with Pandas

3. When you call `.plot.bar()` on a DataFrame, what does the index become, and what do the columns become?  
   `Answer:` The index becomes the x-axis, and each column becomes one series.

4. Give one example of wide data and the same data in long form.  
   `Answer:` One example of wide data is `survival = titanic.pivot_table(values='Survived', index='class', columns='Sex', aggfunc='mean')`. It has one column per series, with the x-values in the index.
   <br>`long = survival.reset_index().melt(id_vars='class', var_name='Sex', value_name='survival_rate')` would be the long form.

---

### ✏️ Task: Summary Table to Chart

```python
# Using pokemon.csv:
# 1. Build a crosstab of Generation vs. Legendary, normalized by row.
shares = pd.crosstab(poke['Generation'], poke['Legendary'], normalize='index')

# 2. Plot it as a 100% stacked bar chart with a percent-formatted axis.
ax = shares.plot.bar(stacked=True, figsize=(8, 3.5), colormap='viridis', rot=0)
ax.yaxis.set_major_formatter(PercentFormatter(xmax=1))
ax.set(title='Legendaries by Generation', xlabel='Generation', ylabel='Share of Pokémon')
ax.legend(title='Legendary', bbox_to_anchor=(1.01, 1), loc='upper left')
ax.spines[['top', 'right']].set_visible(False)

# 3. Melt the (un-normalized) crosstab into long form with columns Generation, Legendary, count.
counts = pd.crosstab(poke['Generation'], poke['Legendary'])
counts_long = (counts.reset_index().melt(id_vars='Generation', var_name='Legendary', value_name='count'))

```

### 🤖 Explain It

In your own words: when would you plot with pandas `.plot`, and when would you switch to Seaborn?

**Answer:** You would use pandas `.plot` for *wide data* and quick charts from an already built summary table. You would switch to Seaborn for *long data* and statistical charts from raw data rows.

---

## 🌊 Section 3: Seaborn Distributions

5. Why can a histogram with `hue` and raw counts be misleading when the groups are very different sizes? What's the fix?  
   `Answer:` It can be misleading because when one group is much larger than the other, it will naturally have taller bars even if both groups have similar distributions. The *fix* would be to compare groups by proportion/density rather than raw counts.

6. Explain how a box plot's whiskers and dots connect to the 1.5 × IQR rule from Module 07.  
   `Answer:` A box plot's *upper whisker* and *lower whisker* represent the *highest value* and *lowest whisker* respectively within the IQR fences, while it's dots represent the *outliers* beyond either fence.

---

### ✏️ Task: Compare Distributions Four Ways

```python
# Using penguins.csv, for flipper_length_mm by species, make a 2 x 2 figure:
fig, axes = plt.subplots(2, 2, figsize=(12, 8), layout='constrained')

# a step histogram with hue, a KDE with hue, a box plot, and a violin plot.
# Use the same species order and the same colors in every panel.

# Step histogram with hue
sns.histplot(data=penguins, x='flipper_length_mm', hue='species', palette=palette,
             element='step', stat='density', common_norm=False, ax=axes[0, 0])
axes[0, 0].set_title('Step Histogram')

# KDE with hue
sns.kdeplot(data=penguins, x='flipper_length_mm', hue='species', palette=palette,
            ax=axes[0, 1])
axes[0, 1].set_title('KDE')

# Box plot
sns.boxplot(data=penguins, x='species', y='flipper_length_mm', order=order,
            palette=palette, ax=axes[1, 0])
axes[1, 0].set_title('Box Plot')

# Violin plot
sns.violinplot(data=penguins, x='species', y='flipper_length_mm', order=order,
               palette=palette, ax=axes[1, 1])
axes[1, 1].set_title('Violin Plot')

for ax in axes.flat:
    ax.spines[['top', 'right']].set_visible(False)
fig.suptitle('Flipper Length by Penguin Species', fontsize=12)
```

### 🤖 Explain It

In your own words: the overall penguin body-mass histogram looked like one lumpy pile, and its skew was only 0.47. What did coloring by species reveal, and why couldn't the skew statistic reveal it?

**Answer:** Coloring by species revealed that Gentoos make up of the right hand side and that Adelies and Chinstraps almost completely overlap. The skew statistic couldn't reveal that because it lacked visual context.
---

## 🔍 Section 4: Seaborn Relationships and Categories

7. What do the error bars on a default `sns.barplot()` mean? How would `errorbar='sd'` change them?  
   `Answer:` By default, the error bars on a `sns.barplot()` represent a *95% confidence interval* for the mean of the data. `errorbar='sd'` would change them by making them to show how spread out the individual values are with *± one standard deviation*.

8. Why should you color a scatter plot by group before adding a trend line?  
   `Answer:` You should color a scatter plot by group because it makes it clear to see the different patterns that different groups may have.

---

### ✏️ Task: Reveal the Paradox

```python
# Using penguins.csv:
# 1. Draw one regplot of bill_length_mm vs. bill_depth_mm for all penguins.
sns.regplot(data=penguins, x='bill_length_mm', y='bill_depth_mm', ax=axes[0],
            scatter_kws={'alpha': 0.4, 'color': 'gray'}, line_kws={'color': 'black'})
r_all = penguins['bill_length_mm'].corr(penguins['bill_depth_mm'])

# 2. Draw one regplot per species on a second panel, with r in each label.
palette = dict(zip(SPECIES_ORDER, sns.color_palette(n_colors=3)))
for species, group in penguins.groupby('species'):
    r = group['bill_length_mm'].corr(group['bill_depth_mm'])
    sns.regplot(data=group, x='bill_length_mm', y='bill_depth_mm', ax=axes[1],
                color=palette[species], scatter_kws={'alpha': 0.5}, label=f'{species} (r = {r:.2f})')

# 3. Give each panel a title that states what it shows.
axes[0].set(title=f'All penguins together: r = {r_all:.2f}')
axes[1].set(title='Relationships within each species')
axes[1].legend()
for ax in axes:
    ax.set(xlabel='Bill length (mm)', ylabel='Bill depth (mm)')
```

### 🤖 Explain It

In your own words: explain Simpson's paradox to someone who has never heard of it, using your chart from the task above.

**Answer:** If you look only at the left panel, it would appear that penguins with longer bills tend to have shallower bills due to the downward slope. However, if you look at the right panel, you'll see that the trend slopes upward when the penguins are separated by species. Longer bills are associated with deeper bills inside each species, but combining the species data leads to misleading results, thus the paradox.

---

## 🗣️ Section 5: Choosing and Telling

9. Name three things a bar chart's y-axis can do to mislead a reader.  
   `Answer:` It's start can be above zero, differing scales between y-axes can be used, or it can have a range that's too large/small.

10. What's the difference between a descriptive title and a finding title? Write one of each for the same chart.  
    `Answer:` A *descriptive title* (e.g. "Survival Rate by Class") tells the reader what the chart is about, while a *finding title* (e.g. "Women in 1st and 2nd Class Almost All Survived") explains the chart's overall conclusions.

---

### ✏️ Task: Makeover

```python
# Start with: titanic.groupby('Embarked')['Fare'].mean().plot.bar()
titanic.groupby('Embarked')['Fare'].mean().plot.bar()
plt.savefig(OUT / 'my_makeover_before.png', dpi=150, bbox_inches='tight')
plt.close()

# Redesign it with the notebook 05 checklist: the right statistic for skewed data,
# readable port names, sorted bars, a highlight color, bar labels, and a finding title.
# Save the before and after versions.
ports = {'C': 'Cherbourg', 'Q': 'Queenstown', 'S': 'Southampton'}
median_fares = (titanic.groupby('Embarked')['Fare'].median().rename(index=ports).sort_values())

top_port = median_fares.idxmax()
colors = ['tab:orange' if port == top_port else 'lightgray' for port in median_fares.index]

fig, ax = plt.subplots(figsize=(7, 4))
median_fares.plot.bar(ax=ax, color=colors)

ax.bar_label(ax.containers[0], fmt='$%.2f')

ax.set(title='Passengers Embarking at Cherbourg Generally Paid the Highest Fare',
       xlabel='Port', ylabel='Median Fare ($)')
ax.spines[['top', 'right']].set_visible(False)

fig.savefig(OUT / 'my_makeover_after.png', dpi=150, bbox_inches='tight')
```

### 🤖 Explain It

In your own words: what's the difference between a chart made for exploration and a chart made for communication? Why do they need different amounts of polish?

**Answer:** An *exploration chart* is generally intended for personal use and is used for finding out what's in the data. A *communication chart* is intended for showing someone else and is used to clearly show one particular finding. They need different amounts of polish, as *exploration* is used for many quick charts, while *communication* is used for one or two refined charts.

---

## 🧾 Submit Checklist

- [X] I built a multi-panel Matplotlib figure with `fig, ax`, shared axes, and `fig.savefig()`.
- [X] I used a log scale, a reference line, and a tick formatter where they helped.
- [X] I turned a pandas summary table into a chart, and reshaped data between wide and long.
- [X] I compared distributions across groups fairly (`common_norm=False`, shared axes, sample sizes).
- [X] I showed a relationship with a scatter plot colored by group, and explained my error bars.
- [X] I redesigned a default chart using the checklist, with a finding title.
- [X] I completed the "Explain It" prompts in my own words.
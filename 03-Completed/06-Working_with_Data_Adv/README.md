# 🧰 Module 06: Working with Data (Advanced)

## Completed Module Commentary
This module explained...
- The Pandas data structures `Series` and `DataFrames`
- Reading CSVs and utilizing various DataFrame functions
- Indexing and Selecting rows/columns
- Detecting missing values and cleaning datasets
- Various Column Operations
- Sorting and Filtering data
- Grouping, summarizing, and combining data

- What clicked for me in this module was the many uses of Pandas sorting and querying functions. One thing that may be worth revisiting is building cleaning pipelines, as there are various important steps to keep in mind. The content in this module was clear and well-organized, with no glaring issues that I would change.

---

## 🔗 Completed Assignments

| Notebook | Description |
|----------|-------------|
| [01-Pandas_Series_and_DataFrames.ipynb](01-Pandas_Series_and_DataFrames.ipynb) | This notebook explained `Series` and `DataFrame` structures, building from a dictionary of columns or a list of dictionaries, etc. |
| [02-Loading_and_Exploring_Data.ipynb](02-Loading_and_Exploring_Data.ipynb) | This notebook showed how to read CSVs and explained dtypes, `.head()`/`.info()`/`.describe()`, duplicates and distinct values, etc. |
| [03-Indexing_and_Selection.ipynb](03-Indexing_and_Selection.ipynb) | This notebook covered `.loc[]` vs. `.iloc[]`, using `.set_index()`, boolean masks, combining rows **and** columns in one `.loc[]`, and more. |
| [04-Basic_Cleaning.ipynb](04-Basic_Cleaning.ipynb) | This notebook explained what counts as a missing value, the data cleaning process, using fill vs. drop (`subset=`, `thresh=`, `ffill`), dealing with duplicates, etc. |
| [05-Column_Operations.ipynb](05-Column_Operations.ipynb) | This notebook showed how to create columns, explained conditional updates and the use of `.loc[]`, renaming/tidying names, dropping data safely, and more |
| [06-Sorting_and_Filtering.ipynb](06-Sorting_and_Filtering.ipynb) | This notebook covered the use of `.sort_values()`, named masks for long filters, `.query()`, searching for text with `.str.contains()`, etc. |
| [07-Grouping_and_Combining.ipynb](07-Grouping_and_Combining.ipynb) | This notebook explained the use of `value_counts()`, `groupby()` (`.size()` vs. `.count()`, `as_index=False`), using named `.agg()`, filtering groups, `pd.concat()` vs. `.merge()`, and more. |
| [08-Pandas_Wrangle_Lab.ipynb](08-Pandas_Wrangle_Lab.ipynb) | This notebook acted as a lab that walked through the entire pipeline of utilizing Pandas while saving results to `08-OutputFiles`. |
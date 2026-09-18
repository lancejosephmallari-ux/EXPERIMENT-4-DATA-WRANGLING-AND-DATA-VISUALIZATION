---
# EXPERIMENT 4: DATA WRANGLING AND DATA VISUALIZATION
---
#### Name: Mallari, Lance Joseph N.
#### Date Submitted: 09/18/2026
#### Section: 2ECE-A
---
### I. Intended Learning Outcomes
At the end of this laboratory activity, the student should be able to:
1. filter tabular data using several categorical and numerical conditions;
2. construct focused DataFrames by selecting relevant features;
3. summarize the relationship between categorical features and a numerical variable; and
4. communicate a data comparison using clear and correctly labeled plots.
---
### II. Instructions
Use the same ***ECE Board Exam 2*** dataset supplied for Experiment 4. Work in a Jupyter Notebook using Pandas and a Python plotting library used in class. Use the dataset’s existing column labels, including ***Name, Gender, Track, Hometown, Math, GEAS, Electronics, and Average.***
- Derive all tables and plot values from the dataset. Do not manually type rows, category means, or
plotted values.
- When applying more than one condition, make every condition explicit in the filtering expression.
- Keep the original DataFrame unchanged.
- Every graph must have a title, axis labels, readable category labels, and a consistent scale appro-
priate to the data.
---
### III. Programming Problems
---
#### A. VISAYAS COMMUNICATION DATAFRAME
Create a DataFrame named ***VisComm*** containing students whose ***Hometown is Visayas*** and whose ***Track
is Communication***. Retain only these columns, in the stated order:
```
Name, Gender, Math, Electronics, Average
```
---
#### CODE FOR PART A:
**Create the code needed for importing panda as pd for managing, and analyzing the datasets. Along with matplotlib.pyplot as plt to cr
```
import matplotlib.pyplot as plt
import pandas as pd

# Load dataset and clean column headers
df = pd.read_csv("board2.csv")
df.columns = df.columns.str.strip()

# Calculate "Average" column if missing from the CSV
if "Average" not in df.columns:
    df["Average"] = df[["Math", "GEAS", "Electronics", "Communication"]].mean(
        axis=1
    )
```
#### OUTPUT FOR PART A:
```
Name	Gender	Math	Electronics	Average
10	S11	Female	48	    56	        54.75
11	S12	Male	89	    67	        76.00
17	S18	Male	81	    40	        63.50
21	S22	Female	64   	39	        62.50
27	S28	Male	85	    53	        67.75
Number of rows in VisComm: 5
```
Display the resulting DataFrame and its number of rows. Both filtering conditions must be applied to
the source dataset before the columns are selected.
#### B. VISAYAS FEMALE DATAFRAME
```
Name, Track, GEAS, Electronics, Average
```
Display ***VisFemale.*** Then display only the rows of ***VisFemale whose Average is at least 60***. ***DO NOT
overwrite VisFemale*** when performing this second filter.
#### C. CATEGORY-AVERAGE VISUALIZATION
Examine how the recorded Average differs across the three categorical features Track, Gender, and
Hometown.
- a. For each feature, compute the mean of Average for every category using Pandas.
- b. Display the three summary tables.
- c. Create one figure containing three bar charts: mean Average by Track, by Gender, and by
Hometown.
- d. Below the figure, write three concise statements identifying the category with the highest sample
mean for each feature.
**Interpretation rule:** Describe the observed dataset only. A difference in group means does not, by
itself, establish that a feature causes a higher board-exam score.
### IV. Submission Requirements
Submit one Jupyter Notebook file (.ipynb) containing your name and section, the two required DataFrames, the three category-mean summaries, the completed figure, and the three interpretation statements. All cells must be executed and the notebook must run from beginning to end without errors.

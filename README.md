---
# EXPERIMENT 4: DATA WRANGLING AND DATA VISUALIZATION
---
### Name: Mallari, Lance Joseph N.
### Date Submitted: 09/18/2026
### Section: 2ECE-A
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

### A. VISAYAS COMMUNICATION DATAFRAME
Create a DataFrame named ***VisComm*** containing students whose ***Hometown is Visayas*** and whose ***Track
is Communication***. Retain only these columns, in the stated order:
```
Name, Gender, Math, Electronics, Average
```
Display the resulting DataFrame and its number of rows. Both filtering conditions must be applied to
the source dataset before the columns are selected.

---
## CODING:
Create the code needed for importing panda as pd for managing, and analyzing the datasets. Along with matplotlib.pyplot as plt to cr for the graph later in Problem C. In addition we also need to get the average and set up a column for it.
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
### CODE FOR PART A:
```
# Filter Hometown == 'Visayas' and Track == 'Communication' before column selection
VisComm = df[(df["Hometown"] == "Visayas") & (df["Track"] == "Communication")][
    ["Name", "Gender", "Math", "Electronics", "Average"]
]

# Display DataFrame and row count
display(VisComm)
print(f"Number of rows in VisComm: {len(VisComm)}")
```
### OUTPUT FOR PART A:
```
    Name	Gender	Math	Electronics	Average
10	S11	    Female	48	    56	        54.75
11	S12	    Male	89	    67	        76.00
17	S18	    Male	81	    40	        63.50
21	S22	    Female	64   	39	        62.50
27	S28	    Male	85	    53	        67.75

Number of rows in VisComm: 5
```
### METHODS USED FOR PART A:
- `VisComm = df[(df["Hometown"] == "Visayas") & (df["Track"] == "Communication")][["Name", "Gender", "Math", "Electronics", "Average"]]`: Uses element-wise logical AND (&) to filter rows matching both conditions before selecting the 5 required columns in order.
- `display(VisComm)`: Renders VisComm as a formatted Jupyter table.
- `print(f"Number of rows in VisComm: {len(VisComm)}")`: Measures and prints total row count using `len()`

---
### B. VISAYAS FEMALE DATAFRAME
```
Name, Track, GEAS, Electronics, Average
```
Display ***VisFemale.*** Then display only the rows of ***VisFemale whose Average is at least 60***. ***DO NOT
overwrite VisFemale*** when performing this second filter.

### CODE FOR PART B:
```
# Filter Hometown == 'Visayas' and Gender == 'Female' before column selection
VisFemale = df[(df["Hometown"] == "Visayas") & (df["Gender"] == "Female")][
    ["Name", "Track", "GEAS", "Electronics", "Average"]
]

# Display VisFemale
print(" VisFemale DataFrame ")
display(VisFemale)

# Display rows where Average is at least 60 without overwriting VisFemale
print("\n VisFemale Students with Average >= 60 ")
vis_female_passed = VisFemale[VisFemale["Average"] >= 60]
display(vis_female_passed)
```
### OUTPUT FOR PART B:
```
 VisFemale DataFrame 
Name	  Track	            GEAS   Electronics	Average
5	S6	  Microelectronics	86	   45	        75.50
10	S11	  Communication	    48	   56       	54.75
20	S21	  Microelectronics	68     51	        68.50
21	S22	  Communication  	89	   39        	62.50
23	S24	  Microelectronics	60	   45	        57.75
25	S26   Instrumentation	83	   47       	65.75

 VisFemale Students with Average >= 60 
Name	Track	           GEAS	 Electronics	Average
5	S6	Microelectronics	86	 45         	75.50
20	S21	Microelectronics	68	 51	            68.50
21	S22	Communication    	89	 39         	62.50
25	S26	Instrumentation	    83	 47         	65.75
```
### METHODS USED FOR PART B:
- `VisFemale = df[(df["Hometown"] == "Visayas") & (df["Gender"] == "Female")][["Name", "Track", "GEAS", "Electronics", "Average"]]`: Filters students where Hometown is Visayas and Gender is Female, retaining specified columns.
- `display(VisFemale)`: Displays the full VisFemale table.
- `vis_female_passed = VisFemale[VisFemale["Average"] >= 60]`: Applies a numerical filter (Average >= 60) assigned to a new variable so VisFemale remains unmodified.
- `display(vis_female_passed)`: Displays the subset of passing female students from Visayas.

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

### CODE FOR PART C:
```
# a & b. Compute and display category means
track_avg = df.groupby("Track", as_index=False)["Average"].mean()
gender_avg = df.groupby("Gender", as_index=False)["Average"].mean()
hometown_avg = df.groupby("Hometown", as_index=False)["Average"].mean()

print(" [Summary Table: Mean Average by Track] ")
display(track_avg)

print("\n [Summary Table: Mean Average by Gender] ")
display(gender_avg)

print("\n [Summary Table: Mean Average by Hometown] ")
display(hometown_avg)

# c. Create one figure containing three bar charts
fig, axes = plt.subplots(1, 3, figsize=(16, 5), sharey=True)

# Bar plot 1: Track
axes[0].bar(
    track_avg["Track"],
    track_avg["Average"],
    color="#4C72B0",
    edgecolor="black",
)
axes[0].set_title("Mean Average by Track", fontweight="bold")
axes[0].set_xlabel("Track")
axes[0].set_ylabel("Mean Average Score")
axes[0].grid(axis="y", linestyle="--", alpha=0.7)

# Bar plot 2: Gender
axes[1].bar(
    gender_avg["Gender"],
    gender_avg["Average"],
    color="#DD8452",
    edgecolor="black",
)
axes[1].set_title("Mean Average by Gender", fontweight="bold")
axes[1].set_xlabel("Gender")
axes[1].grid(axis="y", linestyle="--", alpha=0.7)

# Bar plot 3: Hometown
axes[2].bar(
    hometown_avg["Hometown"],
    hometown_avg["Average"],
    color="#55A868",
    edgecolor="black",
)
axes[2].set_title("Mean Average by Hometown", fontweight="bold")
axes[2].set_xlabel("Hometown")
axes[2].grid(axis="y", linestyle="--", alpha=0.7)

plt.suptitle(
    "ECE Board Exam: Category-Average Comparison",
    fontsize=14,
    fontweight="bold",
)
plt.tight_layout()
plt.show()
```
### OUTPUT FOR PART C:
```
 [Summary Table: Mean Average by Track] 
Track	Average
0	Communication	67.975
1	Instrumentation	65.225
2	Microelectronics	67.500

 [Summary Table: Mean Average by Gender] 
Gender	Average
0	Female	66.616667
1	Male	67.183333

 [Summary Table: Mean Average by Hometown] 
Hometown	Average
0	Luzon	68.083333
1	Mindanao	66.678571
2	Visayas	65.750000
```
<img width="1716" height="554" alt="image" src="https://github.com/user-attachments/assets/ef2b0b88-405e-46a5-bc1a-5977f3541fcc" />

### METHODS USED FOR PART B:
***Data Aggregation (Group Means)***
- `track_avg = df.groupby("Track", as_index=False)["Average"].mean()`: Groups rows by Track category and computes the mean Average score for each track. Setting as_index=False ensures Track remains a standard column rather than becoming the row index.
- gender_avg = df.groupby("Gender", as_index=False)["Average"].mean(): Groups data by Gender to calculate mean scores for female and male categories.
-hometown_avg = df.groupby("Hometown", as_index=False)["Average"].mean(): Groups data by regional Hometown (Luzon, Visayas, Mindanao) to compute regional mean averages.

***Displaying Summary Output***
- print("--- Summary: ... ---"): Outputs styled headers in the console to separate each category's results.
- display(track_avg), display(gender_avg), display(hometown_avg): Formats and displays each aggregated pandas DataFrame as a clean table inside the Jupyter environment.
  
***Figure Setup & Subplot Layout***
- fig, axes = plt.subplots(1, 3, figsize=(16, 5), sharey=True): Initializes a 1x3 grid of subplots within a single figure container sized 16 by 5 inches. Setting sharey=True forces all three charts to use identical vertical axis limits for accurate visual comparison.
- 
***Plotting Bar Charts***
- axes[0].bar(track_avg["Track"], track_avg["Average"], color="#4C72B0", edgecolor="black"): Draws vertical bars on the first subplot (axes[0]) showing mean scores per academic track with custom color fill and black borders.
- axes[1].bar(...) & axes[2].bar(...): Plots corresponding bar charts on the second (axes[1]) and third (axes[2]) subplots for Gender and Hometown data using distinct colors.

***Axis Labeling & Grid Alignment***
- axes[0].set_title("...", fontweight="bold"): Applies bold sub-titles to individual plot panels.
- axes[0].set_xlabel(...) & axes[0].set_ylabel(...): Configures horizontal and vertical axis labels for clear category identification.
- axes[0].grid(axis="y", linestyle="--", alpha=0.7): Adds horizontal dashed gridlines at 70% opacity to help read bar height values accurately.

***Final Figure Rendering***
- plt.suptitle("ECE Board Exam: Category-Average Comparison", fontsize=14, fontweight="bold"): Places a centered main super-title across the top of the combined figure.
- plt.tight_layout(): Automatically adjusts padding between subplots to eliminate overlapping text and clipped labels.
- plt.show(): Renders and embeds the completed graphic directly within the notebook output cell.

---

### IV. Submission Requirements
Submit one Jupyter Notebook file (.ipynb) containing your name and section, the two required DataFrames, the three category-mean summaries, the completed figure, and the three interpretation statements. All cells must be executed and the notebook must run from beginning to end without errors.

# ECE-2112-Programming Assignment 4

**Made by** Ma. Ysabelle T. Laxamana **|** 2ECE-C

This repository contains the Programming Assignment 4: Data Wrangling and Data Visualization for the course ECE2112: Advanced Computer Programming and Algorithms for the school year 2026-2027. This project covers three Python problems pertaining to Module 4: Data Wrangling and Data Visualization.

## Objective
The objective of this laboratory activity is to demonstrate proficiency in filtering tabular data using multiple categorical and numerical conditions to construct focused Data Frames. Furthermore, the project aims to develop practical skills in summarizing relationships between categorical features and a numerical variable, ultimately communicating these data comparisons through clear, correctly labeled visual plots.

## Programming Problems

### A. VISAYAS COMMUNICATION DATAFRAME
Load the provided Excel dataset into a Pandas DataFrame and calculate the average. Filter the data to isolate students from the Visayas region in the Communication track, then extract specific columns. Finally, display the resulting Data Frame and its total number of rows.

**The following functions and methods were used in this problem:**

* **`pd.read_excel()`** - used to load the provided '.xslx' dataset into a structured Pandas DataFrame.
* **`.mean(axis=1)`** - used to calculate the mean across multiple columns horizontally to derive the average.
* **`.loc[]`** - used to simultaneously apply row filters and extract specific required columns by their labels.
* **`.shape[0]`** - used to extract and print only the total number of rows in the resulting filtered DataFrame.
* **Multiple Boolean Conditions (`&`)** - used to chain strict conditional statements together simultaneously.

```python
import pandas as pd

df = pd.read_excel('board2.xlsx') 

df['Average'] = df[['Math', 'GEAS', 'Electronics', 'Communication']].mean(axis=1) 

VisComm = df.loc[(df['Hometown'] == 'Visayas') & (df['Track'] == 'Communication'), ['Name', 'Gender', 'Math', 'Electronics', 'Average']]

print("Number of rows:", VisComm.shape[0])
VisComm
```
### B. VISAYAS FEMALE DATAFRAME
Create a subset of female students from the Visayas region and display their specific subject metrics. Apply a secondary filter to display only the records with an average of 60 or higher without overwriting the saved variable.

**The following functions and methods were used in this problem:**

* **`.loc[]`** - used to establish the initial filtered DataFrame containing only a specific metric with its selected columns.
* **Boolean Indexing (`df[df['col'] >= value]`)** - used to apply a secondary mathematical filter directly inside the display call to prevent overwriting the saved variable.

```python
VisFemale = df.loc[(df['Hometown'] == 'Visayas') & (df['Gender'] == 'Female'), ['Name', 'Track', 'GEAS', 'Electronics', 'Average']]

VisFemale 
```
```python
VisFemale[VisFemale['Average'] >= 60]
```
### C. CATEGORY-AVERAGE VISUALIZATION
Compute the mean board exam average across three categorical features (Track, Gender, and Hometown) and display the summary tables. Create a figure containing three correctly labeled bar charts to visually compare the highest-performing groups.

**The following Pandas and Matplotlib functions and methods were used in this problem:**

* **`.pivot_table`** - used to aggregate the dataset by specific categorical columns passed to the `index` parameter and targett the numerical data using `values`.
* **`.reset_index()`** - used to flatten the resulting summarized data into a regular DataFrame so the tables align perfectly and the column names can be called easily for graphing.
* **`display()`** - used to render all the summary tables.
* **`plt.figure(figsize=(20, 5))`** - used to define the overall dimensions of the final graphic.
* **`plt.subplot()`** - used to partition the main figure into a 1x3 grid, allowing the three distinct bar charts to be displayed neatly side-by-side.
* **`plt.bar()`** - used to construct the actual bar charts by passing the categorical data as the x-axis and the mean averages as the y-axis, along with the custom colors. 
* **`plt.title()`. `plt.xlabel()`, `plt.ylabel()`** - used to assign clear, readable text labels to the axes and headers of every single graph.
* **`plt.subplots_adjust()`** - used to create an extra space at the bottom of the graphic.
* **`fig.text()`** - used to embed the interpretation statements directly into the bottom of the figure graphic.
* **Semicolon (`;`)** - appended to the final line of each subplot block to suppress the default Matplotlib text output in Jupyter Notebook.

```python
import matplotlib.pyplot as plt

track_mean = df.pivot_table(index='Track', values='Average').reset_index()
gender_mean = df.pivot_table(index='Gender', values='Average').reset_index()
hometown_mean = df.pivot_table(index='Hometown', values='Average').reset_index()

display(track_mean)
display(gender_mean)
display(hometown_mean)
```

```python
fig = plt.figure(figsize=(20, 5))

#First Chart: Track
plt.subplot(1, 3, 1) 
plt.bar(track_mean['Track'], track_mean['Average'], color='skyblue')
plt.title('Mean Average by Track')
plt.xlabel('Track')
plt.ylabel('Average Score');

#Second Chart: Gender
plt.subplot(1, 3, 2)
plt.bar(gender_mean['Gender'], gender_mean['Average'], color='red')
plt.title('Mean Average by Gender')
plt.xlabel('Gender')
plt.ylabel('Average Score');

#Third Chart: Hometown
plt.subplot(1, 3, 3)
plt.bar(hometown_mean['Hometown'], hometown_mean['Average'], color='pink')
plt.title('Mean Average by Hometown')
plt.xlabel('Hometown')
plt.ylabel('Average Score');

plt.subplots_adjust(bottom=0.35)

fig.text(0.08, 0.20, "1. Track: Among the tracks observed in this dataset, students in the Communication track have the highest sample mean average.", fontsize=10);
fig.text(0.08, 0.13, "2. Gender: Between the genders in this dataset, Male students have the highest sample mean average.", fontsize=10);
fig.text(0.08, 0.06, "3. Hometown: Across the hometowns in this dataset, students from Luzon have the highest sample mean average.", fontsize=10);

plt.show();
```
### **Interpretations**
* **Track** - Among the tracks observed in this dataset, students in the Communication track have the highest sample mean average.

* **Gender** - Between the genders in this dataset, Male students have the highest sample mean average.

* **Hometown** - Across the hometowns in this dataset, students from Luzon have the highest sample mean average.

**Thank you for reading!**

To access the full Python code for Programming Assignment 4, download the file from this link: https://github.com/MaYsabelleLaxamana/ECE-2112-PA-4/blob/main/LAXAMANA_PA4.ipynb. To execute the code, open the file in Jupyter Notebook and run all the cells.

**README file Version History:**

* **September 11, 2026** - Initial README output uploaded.
* **September 17, 2026** - Added format tweaks to the code and the README file.



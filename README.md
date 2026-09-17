# ECE-2112-PA-4
Cian Joshua Orozco | 2ECED

This repository contains Programming Assignment 4 for, ECE2112 (Advanced Computer Programming and Algorithms). This assignment covers three problems associated to module 4.

<br>

## Instructions

Use the same ECE Board Exam 2 dataset supplied for Experiment 4. Work in a Jupyter Notebook
using Pandas and a Python plotting library used in class. Use the dataset’s existing column labels,
including Name, Gender, Track, Hometown, Math, GEAS, Electronics, and Average.

* Derive all tables and plot values from the dataset. Do not manually type rows, category means, or
plotted values.

* When applying more than one condition, make every condition explicit in the filtering expression.

* Keep the original DataFrame unchanged.

* Every graph must have a title, axis labels, readable category labels, and a consistent scale appropriate to the data.

<br>
<br>

```
import pandas as pd
import matplotlib.pyplot as plt

ECE_Board_Exam_2 = pd.read_excel('board2.xlsx')
ECE_Board_Exam_2
```

```import pandas as pd``` imports the Pandas library and assigns it as ```pd``` to be used in the script.

```import matplotlib.pyplot as plt``` imports a library that will be used for plotting and making charts and graphs.

```ECE_Board_Exam_2 = pd.read_excel('board2.xlsx')``` loads an Excel file named board2 and loads it as a DataFrame named ```ECE_Board_Exam_2```. 

```ECE_Board_Exam_2``` displays the new DataFrame.

<br><br>

## Problem A. Visayas Communication DataFrame

__Objectives:__

```
Create a DataFrame named VisComm containing students whose Hometown is Visayas and whose Track
is Communication. Retain only these columns, in the stated order:

Name, Gender, Math, Electronics, Average

Display the resulting DataFrame and its number of rows. Both filtering conditions must be applied to
the source dataset before the columns are selected.
```

<br><br>

```
ECE_Board_Exam_2['Average'] = ECE_Board_Exam_2[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)
VisComm = ECE_Board_Exam_2.loc[(ECE_Board_Exam_2['Hometown'] == 'Visayas') & (ECE_Board_Exam_2['Track'] == 'Communication')]

VisComm = VisComm[['Name', 'Gender', 'Math', 'Electronics', 'Average']]


display(VisComm)
print('Number of rows: ', len(VisComm))
```
<br>

```ECE_Board_Exam_2['Average'] = ECE_Board_Exam_2[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)``` adds an average column containing the average of grades in Math, Electronics, GEAS, and Communication.

```VisComm = ECE_Board_Exam_2.loc[(ECE_Board_Exam_2['Hometown'] == 'Visayas') & (ECE_Board_Exam_2['Track'] == 'Communication')]``` extracts rows that have Visayas and Communication in the Hometown and Track column, respectively. This is stored to ```ECE_Board_Exam_2```.

```VisComm = VisComm[['Name', 'Gender', 'Math', 'Electronics', 'Average']]``` will filter ```VisComm``` to only get columns, Name, Gender, Math, Electronics, and Average.

```display(VisComm)``` displays the filtered DataFrame.

```print('Number of rows: ', len(VisComm))``` will print the number of rows in the DataFrame. This will basically count the number of students that are from Visayas who taking Communications.

<br><br>

## Problem B. Visayas Female DataFrame

__Objectives:__

```
Create a second DataFrame named VisFemale containing students whose Hometown is Visayas and
whose Gender is Female. Retain only:

Name, Track, GEAS, Electronics, Average

Display VisFemale. Then display only the rows of VisFemale whose Average is at least 60. Do not
overwrite VisFemale when performing this second filter
```

<br><br>

```
VisFemale = ECE_Board_Exam_2.loc[(ECE_Board_Exam_2['Hometown']=='Visayas') & (ECE_Board_Exam_2['Gender']=='Female')]
VisFemale = VisFemale[['Name', 'Track', 'GEAS', 'Electronics', 'Average']]

display(VisFemale)

display(VisFemale.loc[(VisFemale['Average']>=60)])
```
<br>

```VisFemale = ECE_Board_Exam_2.loc[(ECE_Board_Exam_2['Hometown']=='Visayas') & (ECE_Board_Exam_2['Gender']=='Female')]``` extracts rows containing Visayas and Female in columns Hometown and Gender, respecitvely. This is stored to DataFrame VisFemale.

```VisFemale = VisFemale[['Name', 'Track', 'GEAS', 'Electronics', 'Average']]``` will filter the DataFrame to only get columns, Name, Track, GEAS, Electronics, and Average.

```display(VisFemale)``` will display the filtered DataFrame.

```display(VisFemale.loc[(VisFemale['Average']>=60)])``` will display ```VisFemale``` with students averaging at least 60. This is done without creating a new DataFrame.

<br><br>

## Problem C. Category-Average Visualization

__Objectives:__

```
Examine how the recorded Average differs across the three categorical features Track, Gender, and Hometown.

a. For each feature, compute the mean of Average for every category using Pandas.
b. Display the three summary tables.
c. Create one figure containing three bar charts: mean Average by Track, by Gender, and by
Hometown.
d. Below the figure, write three concise statements identifying the category with the highest sample
mean for each feature.

Interpretation rule: Describe the observed dataset only. A difference in group means does not, by
itself, establish that a feature causes a higher board-exam score
```

<br><br>

### a.
```
Track_mean = ECE_Board_Exam_2.pivot_table(index = ['Track'], values = 'Average').reset_index()
Gender_mean = ECE_Board_Exam_2.pivot_table(index = ['Gender'], values= 'Average').reset_index()
Hometown_mean = ECE_Board_Exam_2.pivot_table(index = ['Hometown'], values = 'Average').reset_index()
```

These lines of code will summarize the averages across three categorical features, Track, Gender, and Hometown. Once outputted, these will present the average the three tracks in the Track category, male and female averages in the Gender category, and the three hometowns in the Hometown category

<br>

### b.
```
display(Track_mean)
display(Gender_mean)
display(Hometown_mean)
```

The summary of each category is displayed.

<br>

### c. and d.
```fig, graph = plt.subplots(1, 3, figsize=(18,5))```

This sets up a figure that can contain 3 graphs.

<br><br>

```
graph[0].bar(Track_mean['Track'], Track_mean['Average'])
graph[0].set(title = 'Mean Average by Track')
graph[0].set(xlabel = 'Track')
graph[0].set(ylabel = 'Mean Average')
graph[0].set(ylim=(0, 100))
```

Graph 0 positioned at the left of the figure shows mean average per track as a bar graph. The ```.set``` function is used to label and organize the graph to make it consistent.

<br><br>

```
graph[1].bar(Gender_mean['Gender'], Gender_mean['Average'])
graph[1].set(title = 'Mean Average by Gender')
graph[1].set(xlabel = 'Gender')
graph[1].set(ylabel = 'Mean Average')
graph[1].set(ylim=(0, 100))
```

Graph 1 positioned at the center of the figure shows mean average by gender as a bar graph. The ```.set``` function is used to label and organize the graph to make it consistent.

<br><br>

```
graph[2].bar(Hometown_mean['Hometown'], Hometown_mean['Average'])
graph[2].set(title = 'Mean Average by Hometown')
graph[2].set(xlabel = 'Hometown')
graph[2].set(ylabel = 'Mean Average')
graph[2].set(ylim=(0, 100))
```

Graph 2 positioned at the right of the figure shows mean average by hometown as a bar graph. The ```.set``` function is used to label and organize the graph to make it consistent.

<br><br>

```
fig.text(0.01, -0.05, 'Statements:')
fig.text(0.01, -0.2, '\n(1) Communication recorded the highest mean average amount tracks.\n(2) Male Students recorded the higher average mean. \n(3) Luzon has the highest recorded average mean among hometowns.')

plt.tight_layout()
plt.show()
```

The ```fig.text``` is used to enter texts within the figure. Its position in the figure and its font size can be adjusted. ```plt.tight_layout``` will ensure that the graphs are spaced properly within the figure. ```plt.show()``` will display the figure.

<br><br>

## History
* 2026, September 11: File Created.
* 2026, September 11: Instructions added.
* 2026, September 17: Objectives and explanations added.

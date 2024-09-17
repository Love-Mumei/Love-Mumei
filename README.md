# ECE2112 PA-4
* Kyle Nathaniel Dimalanta

# Libraries Used:
* Pandas - to manipulate the data
* matplotlib.pyplot - For the graphs
* seaborn - For advanced visualization
```
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

# Tasks:
* Load the given dataset
* Construct two data frames, which are Instru and Mindy
  * Contains student from Luzon with Instrumentation track and a score greater than 70 in Electronics (Instru).
  * Contains female students only from Mindanao with an average score equal to or greater than 55 (Mindy).
# Approach:
* What I did first is to load the dataset for me to manipulate:
## Code:
```
import pandas as pd
Initial_Data = pd.read_csv('board.csv')
Initial_Data #Load the Table
```
* Now that I have successfully loaded the dataset, I will now display the second task, which is to display the Name and grades in GEAS and Electronics with the condition that Electronics needs to have a grade greater than 70 and track is constant as Instrumentation and hometown Luzon.
## Code:
```
Instru = Initial_Data.loc[(Initial_Data['Track'] == 'Instrumentation') & #To filter out the Track that only outputs "Instrumentation" as a constant
    (Initial_Data['Electronics'] > 70) &  #To filter out the grades got in Electronics to only output grades greater than 70
    (Initial_Data['Hometown'] == 'Luzon'), #To make the constant only have Luzon in the output
    ['Name', 'GEAS', 'Electronics', 'Hometown', 'Track']].reset_index(drop=True) #To only display the 'Name', grades in GEAS and Electronics and 
#Hometown
Instru #print the output
```
*For the third task I was a bit more careful than the second one since I need to add another Column which is the average grade of each student without using excel.
## Code to find the Average of each student
```
Initial_Data['Average'] = Initial_Data[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1) #Make a new column that calculates the Average
Initial_Data
```
* After adding the Average to the column I started to filter out the Hometown of the students and then filter out the gender.
## Code for the Hometown Filter:
```
Step1 = Initial_Data.loc[(Initial_Data['Hometown'] == 'Mindanao')] 
Step1 #Segment of the code for confirmation
```
## Code for the Gender Filter:
```
step2 = Initial_Data.loc[(Initial_Data['Hometown'] == 'Mindanao') & (Initial_Data['Gender'] == 'Female')]
step2 #Segment of the code for confirmation
```
* After ensuring that the Average is correct in the segment code I combined all of them and added the condition of the average should be greater than or equal to 55
## Code:
```
indy = Initial_Data.loc[(Initial_Data['Hometown'] == 'Mindanao') & #Filter the Hometown to only Mondanao
        (Initial_Data['Gender'] == 'Female') & #Filter out the gender
        (Initial_Data['Average'] >= 55), #Filter out the average less than 55
        ['Name', 'Track', 'Electronics', 'Average'] #output these specific variables
        ].reset_index(drop=True) #resets the index of the table
Mindy
```
# Problem 2:
- Visualize how features such as track, gender, and hometown contribute to the average score in a plot.

# Approach:
* For this approach, I used the box plot to compare the Average of each track to the Gender of the students and the Hometown to the Average.
* to add colors to the graph, I used the code hue = 'variable'
## Code for comparing the track average to the gender:
```
#Use boxplot as the visualization to compare the average, track and gender of the data
sns.boxplot(x ='Track', y ='Average', hue ='Gender', data = Initial_Data)
plt.show()
```

## Code for comparing the average to the hometown:
```
plt.figure(figsize=(10, 6))
sns.boxplot(x ='Hometown', y ='Average', hue = 'Hometown', data = Initial_Data) #Create a graph that compares the average by Hometown
plt.show()
```
# Learnings
- I learned how to efficiently wrangle data using pandas by applying the conditions and filtering the needed data
- I also used how to visualize relationships of the given data

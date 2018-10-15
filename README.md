# DCS-Assignment-9

import pandas as pd

url="https://raw.githubusercontent.com/guipsamora/pandas_exercises/master/06_Stats/US_Baby_Names/US_Baby_Names_right.csv"
data = pd.read_csv(url)
data.shape              # dimensions
data.columns              # variable names
data.head(5)            # few observations
print(data)

# """ 1. Delete unnamed columns """
df = data.drop(data.columns[data.columns.str.contains('unnamed',case = False)],axis = 1)
df.shape
df.columns
df.head(5)

# """ 2. Show the distribution of male and female """

import seaborn as sns
import matplotlib.pyplot as plt
gender_count = data.groupby("Gender").sum()["Count"]      # count the males and females
print(gender_count)      #print

#plot
sns.set(style="darkgrid")
sns.barplot(gender_count.index, gender_count.values, alpha=0.9)
plt.title('Distribution of Genders')
plt.ylabel('Number of Occurrences', fontsize=12)
plt.xlabel('Gender', fontsize=12)
plt.show()

# """ 3. Show the top 5 most preferred names """
#Group the names , Count and arrane in descending order
preferred_names = df.groupby("Name").sum().sort_values(by = "Count",ascending=False)["Count"]  
top_preferred_names = preferred_names.head(5)   # select top five
print(top_preferred_names)         # print

#plot
plt.bar(top_preferred_names.index, top_preferred_names.values, color=['black', 'red', 'green', 'blue', 'cyan'])
plt.title('Top 5 Most Preferred Names')
plt.ylabel('Number of Occurrences', fontsize=12)
plt.xlabel('Name', fontsize=12)
plt.show()

# """ 4. What is the median name occurence in the dataset """
preferred_names.median()

median_name = preferred_names[preferred_names == preferred_names.median()]
median_name

# """ 5. Distribution of male and female born count by states """
dist_by_states = pd.pivot_table(df, index = ["State", "Gender"], values= ["Count"], aggfunc=sum)
dist_by_states

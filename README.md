# Overview
This project explores the landscape of the data job market, with a specific focus on Data Analyst positions. It was inspired by a personal goal: to better understand current job trends and identify high-value opportunities in the field.

The dataset comes from Luke Barousse's Python course and includes detailed information on job titles, salary ranges, locations, and required skills. Using Python, I analyze this data to answer key questions such as which skills are most in demand, what the current salary trends look like, and how salary and skill demand overlap in the data analytics space.

# The Questions
Below are the questions I want to answer in my project:

1. What are the skills most in demand for the top 3 most popular data roles?
2. How are in-demand skills trending for Data Analysts?
3. How well do jobs and skills pay for Data Analysts?
4. What are the optimal skills for data analysts to learn? (High Demand AND High Paying)

# Tools I Used
For my deep dive into the data analyst job market, I harnessed the power of several key tools:

- Python: The backbone of my analysis, allowing me to analyze the data and find critical insights.I also used the following Python libraries:
   - Pandas Library: This was used to analyze the data.
    - Matplotlib Library: I visualized the data.
    - Seaborn Library: Helped me create more advanced visuals.
- Jupyter Notebooks: The tool I used to run my Python scripts which let me easily include my notes and analysis.
- Visual Studio Code: My go-to for executing my Python scripts.
- Git & GitHub: Essential for version control and sharing my Python code and analysis, ensuring collaboration and project tracking.

# Data Preparation and Cleanup
This section outlines the steps taken to prepare the data for analysis, ensuring accuracy and usability.
## Import & Clean Up Data
I start by importing necessary libraries and loading the dataset, followed by initial data cleaning tasks to ensure data quality.
```
# Importing Libraries
import ast
import pandas as pd
import seaborn as sns
from datasets import load_dataset
import matplotlib.pyplot as plt  

# Loading Data
dataset = load_dataset('lukebarousse/data_jobs')
df = dataset['train'].to_pandas()

# Data Cleanup
df['job_posted_date'] = pd.to_datetime(df['job_posted_date'])
df['job_skills'] = df['job_skills'].apply(lambda x: ast.literal_eval(x) if pd.notna(x) else x)
```

## Filter US Jobs
To focus my analysis on the U.S. job market, I apply filters to the dataset, narrowing down to roles based in the United States.
```
df_US = df[df['job_country'] == 'United States']
```

# The Analysis
Each Jupyter notebook for this project aimed at investigating specific aspects of the data job market. Here’s how I approached each question:
## 1. What are the most demanded skills for the top 3 most popular data roles?
To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting.

View my notebook with detailed steps here:[Skill Demand](C:\Users\User\OneDrive\Desktop\Python_Data_Project\3_Project\2_Skills_Count.ipynb)

### Visualize Data
```
fig, ax = plt.subplots(len(job_titles), 1)


for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)[::-1]
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')

plt.show()
```
### Results
![Skills Demand](Assets\Skills_for_data_roles.png)

*Bar graph visualizing the salary for the top 3 data roles and their top 5 skills associated with each.*

### Insights:
- SQL stands out as the top-listed skill for both Data Analysts and Data Scientists, appearing in more than half of all job postings for these positions. In contrast, Python is the leading requirement for Data Engineers, showing up in 68% of listings.

- Data Engineers are expected to have advanced technical expertise in tools like AWS, Azure, and Spark, Data Analysts and Data Scientists typically work with broader, analysis-focused tools such as Excel and Tableau.

- Python remains a highly valuable and widely requested skill across all three roles, with the highest demand seen among Data Scientists (72%) and Data Engineers (65%).
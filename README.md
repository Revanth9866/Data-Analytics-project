# The Analysis 


## 1.What are the most demanding skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targetting.

view my notebook with detailed steps here: ![2_Skill_Demand.ipynb](2_Project\2_Skill_Demand.ipynb)


### Visualize Data


```python
fig,ax = plt.subplots(len(job_titles), 1)


for i,job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)
    df_plot.plot(kind = 'barh', x = 'job_skills', y='skill_percent',ax=ax[i],title  = job_title)

    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue ='skill_count', palette= 'dark:b_r')

plt.show()    
```
#### Results

![Visualization of Top Skills](2_Project\images\skill_demand_all_data_roles.png)

### Insights

- Python is a versatile skill, highly demanded across all three roles, but most prominently for Data Scientists (72%) and Data Engineers (65%).
- SQL is the most requested skill for Data Analysts and Data Scientists, with it in over half the job postings for the both roles. For Data Engineers, Python is the most sought_after skill, appearing in 68% of job postings.
- Data Engineers require more specialized technical skills (AWS, Azure, Spark) compared to data Analysts and Data Scientists who are expected to be proficient in more general data management and analysis roles (Excel, Tableau). 

## 2. How are in-demand skills trending for Data Analysts?

### Visualize Data
```python

df_plot = df_DA_US_percent.iloc[:, :5]

sns.lineplot(data=df_plot, dashes=False, palette='tab10')
sns.set_theme(style='ticks')
sns.despine()

plt.title('Trending Top Skills for Data Analysts in the US')
plt.ylabel('Likelihood in Job Posting')
plt.xlabel('2023')

from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))

for i in range(5):
    plt.text(11.2, df_plot.iloc[-1, i], df_plot.columns[i])

plt.show()    

```
### Results

![Trending Top Skills ffor Data Analyts in the US](2_Project\images\skill_trend_DA.png)
*Bar graph visualizing the trending top skills for data analysts in the US in 2023.*

### Insights:
- SQL remains the most consistently demanded skill throughout the year, although it showss a gradual decrease in demand.
- Excel experienced a significant increase in demand starting around September, surpassing both Python and Tableau by the end of the year.
- Both Python and Tableau show relatively stable demand throughout the year with some fluctuations, But remain essential skills for data analysts. Power BI, while less demanded compared to the others, shows a slight upward trend towards the year's end.


## 3. How well do jobs and skills pay for Data Analysts?


#### Salary Analysts for Data Nerds

### Visualize data

```python
sns.boxplot(data=df_UD_top6, x='salary_year_avg',y ='job_title_short',order =job_order)
sns.set_theme(style='ticks')

plt.title('Salary Distribution in the United States')
plt.xlabel("Yearly Salary (USD)")
plt.ylabel('')
plt.xlim(0,600000)
ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()
```

### Results 
![Salary Distributions of Data Jobs in the US](2_Project\images\salary_DA.png)
*Box plot visualizing the salary distributions for the top 6 data job titles.*

#### Insights
- Salary Range Variation: The salary distribution varies widely across roles. Senior positions such as Senior Data Scientist and Senior Data Engineer have higher median salaries and broader salary ranges compared to mid-level roles like Data Scientist and Data Engineer.

- Outliers and High Earners: All roles, particularly the senior ones, have several high outliers indicating that some professionals in these roles earn significantly more than the typical salary range, with salaries extending beyond $400K.

- Data Analysts' Salary: Data Analysts, both senior and junior, have the lowest median salaries among the roles shown. The distribution is more compact, with fewer outliers, indicating less variation in earnings within this role compared to other positions in the data field.

# 3. How Well do jobs and skills pay for the Data
## Highest Paid & Most Demanded Skills for Data Analysts

### Visualize Data

```python
fig,ax = plt.subplots(2,1)

sns.set_theme(style='ticks')

#top 10 hig paid jobs for data analysts
sns.barplot(data=df_DA_top_pay, x='median', y=df_DA_top_pay.index, ax=ax[0], hue='median', palette='dark:b_r' )

#top 10 in-demand skils for data analyst
sns.barplot(data=df_DA_skills,x = 'median',y = df_DA_skills.index, ax= ax[1], hue='median', palette='light:b')
```
### Results
In_demand skills for Data Analysts in the US:

![The highest paid & most in-demand skills for dataa Analysts in the US](2_Project\images\Highpaid_and_Most_in-demand_Skills_for_DA.png)
*Two separate bar graphs visualizing the highest paid skills and most in-demand skills for data analysts in the US.*

#### Insights:
- High-Paying Niche Skills: The top-paying skills for Data Analysts are specialized and less commonly associated with the traditional data analysis toolkit. Skills like dplyr, bitbucket, and solidity command the highest median salaries, reflecting their niche demand in the market.

- In-Demand Foundational Skills: The most in-demand skills for Data Analysts are foundational tools like python, sql, and excel, which are critical for day-to-day data analysis tasks. These skills are widely required across various industries, but their median salaries are relatively lower compared to more specialized skills.

- Salary Discrepancy Between Demand and Specialization: There is a noticeable salary gap between high-demand skills and high-paying skills. While foundational skills such as python and sql are essential and highly sought after, they do not offer the same salary potential as more specialized and emerging technologies like hugging face or solidity. This suggests that acquiring niche, emerging skills may offer a better return on investment for data analysts looking to maximize their earning potential.

## 4. What is the most optimal skill to learn for Data Analyts?

### Visualize Data
```python
from adjustText import adjust_text

sns.scatterplot(
    data=df_plot,
    x='skill_percent',
    y='median_salary',
    hue = 'technology'
)
sns.despine()
sns.set_theme(style='ticks')

from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y, pos:f'${int(y/1000)}K'))
ax.xaxis.set_major_formatter(PercentFormatter(decimals=0))

plt.tight_layout()
plt.show()
```

### Results

![Most Optimal Skillss for Data Analysts in the US](2_Project\images\Most_Optimal_Skills.png)
*A scatter plot visualizing the most optimal skills for data analysts in the us.*


### Insights:
- SQL and Excel are Highly Demanded Skills: SQL is required for almost 60% of data analyst jobs and offers a median salary close to $92K. Excel is also widely required (around 40% of jobs) but comes with a lower median salary of about $84K.

- Programming Skills Pay Well: Python, a key programming skill, is associated with higher median salaries, close to $96K, even though it's required in fewer jobs compared to SQL or Excel.

- Specialized Tools Can Lead to Higher Salaries: Technologies like Oracle, SQL Server, and Go are associated with higher salaries (ranging from $90K to $98K) but are required in a smaller percentage of data analyst jobs, indicating that these specialized skills can command a premium in the job market.







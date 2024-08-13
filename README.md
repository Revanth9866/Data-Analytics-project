# The Analysis 


## 1.What are the most demanding skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targetting.

view my notebook with detailed steps here: [2_Skill_Demand.ipynb](3_Project\2_Skill_Demand.ipynb)


### Visualize Data


```python
fig,ax = plt.subplots(len(job_titles), 1)


for i,job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)
    df_plot.plot(kind = 'barh', x = 'job_skills', y='skill_percent',ax=ax[i],title  = job_title)

    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue ='skill_count', palette= 'dark:b_r')

plt.show()    
```
### Results

![Visualization of Top Skills](3_Project\images\skill_demand_all_data_roles.png)

### Insights

- Python is a versatile skill, highly demanded across all three roles, but most prominently for Data Scientists (72%) and Data Engineers (65%).
- SQL is the most requested skill for Data Analysts and Data Scientists, with it in over half the job postings for the both roles. For Data Engineers, Python is the most sought_after skill, appearing in 68% of job postings.
- Data Engineers require more specialized technical skills (AWS, Azure, Spark) compared to data Analysts and Data Scientists who are expected to be proficient in more general data management and analysis roles (Excel, Tableau). 

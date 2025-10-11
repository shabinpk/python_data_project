# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting. 

View my notebook with detailed steps here:[2_Skill_Demand](Project\2_Skill_Demand.ipynb).

## Visualize Data

```python

fig,ax=plt.subplots(len(job_titles),1)
sns.set_theme(style='whitegrid')
for i,job_title in enumerate(job_titles):
    df_plot=df_skills_perc[df_skills_perc['job_title_short']==job_title].head(5)
    sns.barplot(data=df_plot,y='job_skills',x='skill_perc',ax=ax[i],hue='skill_count',palette='dark:b_r',legend=False)
    ax[i].set_xlabel('')
    ax[i].set_ylabel('')
    ax[i].set_xlim(0,80)
    ax[i].set_title(job_title)
    for n,v in enumerate(df_plot['skill_perc']):
        ax[i].text(v+1,n,f'{v:.1f}%',color='black',va='center')
    if i!=len(job_titles)-1:    
        ax[i].set_xticks([])
fig.suptitle('Likelihood of Skills Requested in US Job Postings',y=1.02,fontsize=16)
fig.tight_layout(h_pad=2)
plt.show()
```

### Results

![Visualization of Top Skills](Project\images\skill_demand_all_data_roles.png)

### Insights

- **SQL and Python** are the most in-demand skills across all roles, especially for Engineers and Scientists.  
- **Data Analysts** rely more on **Excel, Tableau**, and light Python use for reporting and dashboards.  
- **Data Engineers** need **deep technical skills** like **cloud platforms (AWS, Azure)** and **big data tools (Spark)**.  
- **Data Scientists** prioritize **Python, R, and statistical tools (SAS)** for modeling and analysis.  
- Technical complexity and programming expectations **increase from Analyst → Engineer → Scientist**.


## 2. How are in-demand skills trending for Data Analysts?

To find how skills are trending in 2023 for Data Analysts, I filtered data analyst positions and grouped the skills by the month of the job postings. This got me the top 5 skills of data analysts by month, showing how popular skills were throughout 2023.

View my notebook with detailed steps here: [3_Skills_Trend](Project\3_Skills_Trend.ipynb).

### Visualize Data

```python

from matplotlib.ticker import PercentFormatter
df_plot=df_da_us_percent.iloc[:,:5]
sns.lineplot(data=df_plot,dashes=False,palette='tab10')
ax=plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))
plt.show()
```

### Results

![Trending Top Skills for Data Analysts in the US](Project\images\skill_trend_da.png)
*Bar graph visualizing the trending top skills for data analysts in the US in 2023.*

### Insights:

- SQL remains essential: It consistently tops job postings (above 45%) throughout 2023, confirming its status as a foundational data analyst skill despite a slight downward trend.

- Shift from traditional to modern tools: Excel shows a mid-year dip, while Python and Tableau maintain stable demand, reflecting a gradual industry shift toward programming and data visualization tools.

- SAS is declining: It has the lowest and steadily dropping demand (~18–22%), indicating its reduced relevance compared to open-source and more versatile alternatives like Python.


## 3. How well do jobs and skills pay for Data Analysts?

### Salary Analysis for Dat Roles


To identify the highest-paying roles and skills, I only got jobs in the United States and looked at their median salary. But first I looked at the salary distributions of common data jobs like Data Scientist, Data Engineer, and Data Analyst, to get an idea of which jobs are paid the most. 

View my notebook with detailed steps here: [4_Salary_Analysis](Project\4_Salary_Analysis.ipynb).

#### Visualize Data 

```python
sns.boxplot(data=df_us_top6,x='salary_year_avg',y='job_title_short',color='green',order=job_order)
ticks_x=plt.FuncFormatter(lambda x,pos:f'${int(x/1000)}k')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()

```

#### Results

![Salary Distributions of Data Jobs in the US](Project\images\Salary_Distributions_of_Data_Jobs_in_the_US.png)  
*Box plot visualizing the salary distributions for the top 6 data job titles.*

#### Insights

- Senior roles (e.g., Senior Data Scientist, Senior Data Engineer) have the highest median salaries and broader salary ranges compared to non-senior positions.

- Data Analyst has the lowest median salary and the most compact distribution, indicating lower and more consistent earnings.

- High-end salary outliers are present across all roles, especially for Data Scientists and Engineers, with some exceeding $500k annually.


### Highest Paid & Most Demanded Skills for Data Analysts

#### Visualize Data

```python

# Top 10  Highest Paid Skills for Data Analytics
fig,ax=plt.subplots(2,1)
sns.barplot(data=df_da_top_pay,x='median',y=df_da_top_pay.index,ax=ax[0],hue='median',palette='dark:b_r') 

# Top 10 Most In-Demand Skills for Data Analysts'
sns.barplot(data=df_da_skills,x='median',y=df_da_skills.index,ax=ax[1],hue='median',palette='light:b')
plt.show()

```

#### Results
Here's the breakdown of the highest-paid & most in-demand skills for data analysts in the US:

![The Highest Paid & Most In-Demand Skills for Data Analysts in the US](Project\images\Highest_Paid_and_Most_In_Demand_Skills_for_Data_Analysts_in_the_US.png)
*Two separate bar graphs visualizing the highest paid skills and most in-demand skills for data analysts in the US.*

#### Insights:

- The top graph shows specialized technical skills like `dplyr`, `Bitbucket`, and `Gitlab` are associated with higher salaries, some reaching up to $200K, suggesting that advanced technical proficiency can increase earning potential.

- The bottom graph highlights that foundational skills like `Excel`, `PowerPoint`, and `SQL` are the most in-demand, even though they may not offer the highest salaries. This demonstrates the importance of these core skills for employability in data analysis roles.

- There's a clear distinction between the skills that are highest paid and those that are most in-demand. Data analysts aiming to maximize their career potential should consider developing a diverse skill set that includes both high-paying specialized skills and widely demanded foundational skills.


## 4. What are the most optimal skills to learn for Data Analysts?


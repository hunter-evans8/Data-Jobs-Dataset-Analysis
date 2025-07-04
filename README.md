# The Analysis 

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 popular data roles I filtered the top 3 roles and then got the top 5 skills for these roles. This query highlights what skills top roles in the data field are interested in, and what aspiring data people should be learning to better prepare for these roles. 

View my notebook with detailed steps here: [2_Skill_Demand.ipynb](Data_Project_Analysis/2_Skill_Demand.ipynb)


### Visualize Data 

```python
fig, ax = plt.subplots(len(job_titles), 1)

sns.set_theme(style= 'ticks')

for i , job_title in enumerate(job_titles):
    df_plot = df_job_skills_perc[df_job_skills_perc['job_title_short'] == job_title].head(5)
    sns.barplot(data = df_plot, x = 'skill_percent', y = 'job_skills', ax= ax[i], hue = 'skill_count', palette= 'dark:g_r')
    ax[i].set_title(job_title)
    ax[i].set_xlabel("")
    ax[i].set_ylabel("")
    ax[i].set_xlim(0, 79)
    ax[i].legend().set_visible(False)

    for n, v in enumerate(df_plot['skill_percent']):
        ax[i].text(v +1 , n , f'{v:.0f}%' , va = 'center')
    if i != len(job_titles) -1:
        ax[i].set_xticks([])

fig.suptitle('Likelihood of Skills Requested in US Job Posting', fontsize= 15)
fig.tight_layout(h_pad=0.5)
plt.show()

```



### Results

![Visualization of Top Skills for Data Roles](Data_Project_Analysis/images/skill_demand_all_dataRoles.png)




### Insights

- SQL is a very important tool with it being the most requested skill in both Data Analyst and Data Engineering roles, and it coming in second for Data Scientist with over half of the job posting requesting it.
- Python is highly demanded across all jobs, but more prominent for Data Scientists (72%) and Data Engineers (65%).
- From the top requested skills we can see Data Scientist heavily focuses on more statistical view using skills like Python, R, and SAS, while the Data Engineer uses more specialized tools like AWS, Azure, and Spark.


## 2. How are in-demand skills trending for Data Analysts?

In this section I want to see what are the trends of the top skills for Data Analysts to see if any of these skills are falling out of use. To do this I filtered the data to the top 5 skills for Data Analysts. I then calculated the trend among all the months in the year using percents.

The full analysis of how I manipulated the data step by step is here: [3_Skills_Trend.ipynb](Data_Project_Analysis/3_Skills_Trend.ipynb)

### Visualize Data 

```python
df_plot_DA_US_percent = df_DA_US_percent.iloc[:, :5]

sns.lineplot(data = df_plot_DA_US_percent, dashes = False, palette = 'tab10')
sns.set_theme(style = 'ticks')
sns.despine()
plt.title('Top Trending Skills for Data Analysts in the US')
plt.xlabel('2023')
plt.ylabel('Percent Liklihood in Job Posting')
plt.legend().remove()

#Add percent sign to y axis
from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals = 0))

#Add text onto the graph
for i in range(5):
    plt.text(11.2, df_plot_DA_US_percent.iloc[-4, i], df_plot_DA_US_percent.columns[i])

```


### Results 
![Trending Top Skills for Data Analysts](Data_Project_Analysis/images/per_month_skills_trend.png)

### Insights

- SQL is the highest demanded job throughout the whole year, although it does slowly decline through the year. This skill is still highly worth learning due to about half of the jobs for Data Analysts request it in a job listing.
- All of the skills besides SQL ended about where they started at the beggining of the year. This shows that these skills are not on a downward trend, and all of these skills are still worth learning.
- Python and Excel seem to be on a big upwards trend, and we could see a big increase in jobs asking for those skills in data in future years.



  
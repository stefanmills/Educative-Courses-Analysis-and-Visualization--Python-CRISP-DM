# Educative Courses Data Analysis

This project aims to analyze data from Educative, an educational technology company offering a wide range of online courses. The analysis follows the Cross Industry Standard for Data Mining (CRISP-DM) methodology.

## Background
Educative is renowned for its online platform catering to individuals seeking to enhance their skills in professional and academic domains. This analysis delves into understanding various aspects of Educative's course offerings, including subscriber trends, content attributes, pricing strategies, and revenue generation.

## Planned Steps
1. **Data Extraction and Preparation**
   - Extraction of data from provided CSV files
   - Merging CSVs into a single dataframe and saving it as an Excel sheet
   - Initial Exploratory Data Analysis (EDA) to inspect data integrity (Nulls, Duplicates, Shape, etc.)

2. **Data Cleaning**
   - Dropping irrelevant columns such as URL
   - Removing duplicate rows based on course ID
   - Standardizing subject column by removing prefix
   - Creating additional columns for Free/Paid status and Revenue
   - Parsing timestamp columns for date and time
   - Categorizing time of day (Morning/Afternoon/Evening)
   - Renaming columns and adjusting their data types
   - Conducting further EDA on the cleaned data
   - Identifying top courses based on subscribers with key attributes

3. **Excel Sheet Creation**
   - Compiling cleaned data into a final Excel sheet with multiple tabs (Original, Cleaned, Summary)

4. **Data Visualization**
   - Generating Pivot Tables and visualizations for:
     - Total subscribers per subject
     - Average subscriber count per subject
     - Average cost per subject at each level
     - Average content duration per subject
     - Average rating per subject for each level
     - Revenue generated per subject over the years
  
5. **Report Creation by Integrating Python Script into Power Bi Desktop**
This section describes the process of integrating Python scripts into Power BI Desktop for data retrieval, ETL (Extract, Transform, Load), and report creation.

## 1. Getting Data Using Python
- Python script is utilized to read data from an Excel file containing cleaned data.
```python
import pandas as pd

cleaned_data=pd.read_excel(r"C:\Users\user\Desktop\python project\Educative Data.xlsx",sheet_name='Cleaned_Data')

```

## 2. Summarize Data
- Python scripts are employed to summarize data using pivot tables and calculations.
```python
# Pivot Table for the Total Number of Subscribers Per Subject
subject_subs=pd.pivot_table(data=pivot_data,index='Subject',values='Number_of_Subscribers',aggfunc='sum').reset_index()

# Average subscriber count per subject
avg_sub_subject=round((pd.pivot_table(data=pivot_data, index='Subject',values='Number_of_Subscribers',aggfunc='mean')),2).reset_index()

# Average content duration per subject
avg_dur_subj=round((pd.pivot_table(data=pivot_data, index='Subject',values='Content_Duration',aggfunc='mean')),1).reset_index()

# Average cost per subject at each level
avg_sub_subjlvl=round((pd.pivot_table(data=pivot_data, index='Subject', columns='Level',values='Price',aggfunc='mean')),2).reset_index()

# Average rating per subject for each level
avg_rat_subjlvl=round((pd.pivot_table(data=pivot_data, index='Subject', columns='Level',values='Rating',aggfunc='mean')),2).reset_index()

# Creating Pivot Table of the data
yoy_subj_revenue=(pd.pivot_table(data=pivot_data, index='Published_Year',values='Revenue',aggfunc="sum")).reset_index()
```

## 3. Create Report Using Visuals

### Pie Chart Visual for Subscribers Per Subject
```python
import matplotlib.pyplot as plt
import seaborn as sns

# Pie Chart Visual for Subscribers Per Subject
plt.pie(subject_subs["Number_of_Subscribers"], autopct='%1.1f%%', labels=subject_subs.loc[:, 'Subject'], shadow=True, colors=custom_palette, startangle=45)
plt.show()
```

### Bar Chart for Average Number of Subscribers Per Subject
```python
import matplotlib.pyplot as plt
import seaborn as sns

# Bar Chart for Average Number of Subscribers Per Subject
ax=sns.barplot(data=avg_sub_subject, x=avg_sub_subject['Subject'], y=avg_sub_subject['Number_of_Subscribers'], palette=custom_palette, order=avg_sub_subject['Subject'])
plt.show()
```

### Bar Chart for Average Content Duration Per Subject
```python
import matplotlib.pyplot as plt
import seaborn as sns

# Bar Chart for Average Content Duration Per Subject
ax=sns.barplot(data=avg_dur_subj, x=avg_dur_subj['Subject'], y=avg_dur_subj['Content_Duration'], palette=custom_palette, order=avg_dur_subj['Subject'])
plt.show()
```

### Bar Chart for Average Price Per Subject for Each Level
```python
import matplotlib.pyplot as plt
import seaborn as sns

# Bar Chart for Average Price Per Subject for Each Level
sns.catplot(data=pivot_data, x='Subject', y='Price', hue='Level', kind='bar', aspect=2)
plt.show()
```

### Bar Chart for Average Rating Per Subject for Each Level
```python
import matplotlib.pyplot as plt
import seaborn as sns

# Bar Chart for Average Rating Per Subject for Each Level
sns.catplot(data=pivot_data, x='Subject', y='Rating', hue='Level', kind='bar', aspect=1.5)
plt.show()
```

### Line Plot for Revenue Generated Each Year
```python
import matplotlib.pyplot as plt
import seaborn as sns

# Line Plot for Revenue Generated Each Year
sns.relplot(data=yoy_subj_revenue, x=yoy_subj_revenue['Published_Year'], y=yoy_subj_revenue['Revenue'], kind="line", markers=True, legend=False, aspect=1.5)
plt.show()
``` 

These visualizations were integrated into Power BI Desktop for creating dynamic and interactive reports.
     

## Implementation Details
- Python libraries used: Pandas, Matplotlib, Seaborn
- Data preprocessing includes unzipping files, merging dataframes, and cleaning operations.
- Visualization techniques include bar charts, pie charts, and line plots to convey insights effectively.
- Visualizations are saved in PDF format for future reference.

**Note**: Detailed code snippets are provided for each step in the analysis process. For the full code implementation, please refer to the script provided.

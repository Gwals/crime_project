# Crimes Project 

## Project Overview
- This projects aims to give insight about victims cases.

## Data Source
- Crimes data: The primary dataset used for this analysis is the "crimes.csv" file, containing information about victims data regarding the crime they faced

### Tools
- Jupyter notebook - Data analysis

## Data Cleaning
- Handling datatype converion

## Exploratory analysis
This project focus on answering the following questions:
- Hours that crimes mostly take place at
- Which age group is attacked mostly compared to other age groups
- Which gender has most number of cases reported
- How many years does it took for victims to report their cases

## Data Analysis
- area that has the largest frequency of night crimes (crimes committed between 10pm and 3:59am)
```python
crimes['TIME OCC']= crimes['TIME OCC'].astype(int)
peak_night_crime=crimes[(crimes['TIME OCC']>=2200) | (crimes['TIME OCC']<=359)]
peak_night_crime_location_count= peak_night_crime['AREA NAME'].value_counts()
peak_night_crime_location=peak_night_crime_location_count.index[0]
print(peak_night_crime_location)
```
- hour that has the highest frequency of crimes
```python
crimes = pd.read_csv("crimes.csv", parse_dates=["Date Rptd", "DATE OCC"], dtype={"TIME OCC": str})
crimes['TIME OCC_hr']= crimes['TIME OCC'].str[:2].astype(int)
crime_hour_count=crimes['TIME OCC_hr'].value_counts()
peak_crime_hour=crime_hour_count.index[0]
print(peak_crime_hour)
```
- Identifying the number of crimes committed against victims of different age groups
```python
victim_ages=["0-17", "18-25", "26-34", "35-44", "45-54", "55-64", "65+"]
age_bins=[0, 17, 25, 34, 44, 54, 64, float('inf')]
crimes['victim_age_group']=pd.cut(crimes['Vict Age'], labels=victim_ages,  bins=age_bins, right=True)
victim_ages_count= crimes['victim_age_group'].value_counts().reindex(victim_ages, fill_value=0)
victim_ages = pd.Series(victim_ages_count, name='Victim Age Counts')
print(victim_ages)
```

## Results/ findings

![sex_age_countplot](https://github.com/user-attachments/assets/8c03af72-3b1b-4b41-b9d4-dcdb07a19cb4)
- Women between 34 and 0 experience more crime than men
- Men between 35 and 65+ experience more crime than women
  
![TIME_OCC_Countplot](https://github.com/user-attachments/assets/2e8cec03-465d-438e-b39b-5f492b55bc4a)
- Most victims experience crime during 12pm.
  
![numberOfYears_countplot](https://github.com/user-attachments/assets/dd835914-f1c6-4df0-9301-e6313f18077e)
- Most victims report their cases within a year crime has taken place
  
![VictDescent_countplot](https://github.com/user-attachments/assets/62980478-573b-40a5-b3ee-02fe8743976e)
- Mexicans experience crime more followed by white race.







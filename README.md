# Phase 1 Project Overview

# 1. Business Understanding

My company want to purchase a new aircraft to expand its business portfolio using aviation data from the National Transportation Safety Board, which consists of aviation accidents and selected incidents from 1963 to 2023 (Over 60 years), in the United States and international waters

## The Project Goal
To determine aircrafts with the lowet risk of accidents and fatalities, by analysing historical data, to help the company make an informed decision on aircraft purchase in order to start a business endaviour

## Key questions
What type of aircarfts have reported the least or no total fatal injuries over the last 60 years?
what type of aircrafts have reported the most total fatal injuries over the last 60 years?
what tupe of aircrafts have reported the least incidents 


# 2. Data Understanding
## Source of Data 
This is data from the National Transport and Safety Board that includes aviation accident data and selected incidents for over 60 years (1962-2023). 
This data is saved as a **Aviation_Data.csv** file in the **Data** folder

## Loading the **Aviation_Data.cvs** to pandas 

```python  
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt```
%matplotlib inline

`df_aviation_data = pd.read_csv('Data/Aviation_Data.csv', index_col=0)`

`df_aviation_data.info()`

# Data Preparation
Renaming columns to lower case
`df_aviation_data = df_aviation_data.rename(columns=str.lower)`

Replacing '.' in the column names with '_'  
`df_aviation_data = df_aviation_data.rename(columns=lambda x: x.replace('.', '_'))`

Checking for duplicates
`df_aviation_data.duplicated().sum()`

Removal of duplicates
`df_aviation_data.drop_duplicates(keep='first', inplace=True)`

Checking and handling missing values
`df_aviation_data.isnull().sum()`

Calculating the percentage of missing data
`percentage_missing = np.round(((df_aviation_data.isnull().sum() / len(df_aviation_data)) * 100), 2)`

Droping rows where there are missing values in any of this columns and name the new dataset **df_cleaned**: 'make', 'model', 'aircraft category', 'injury_sererity', 'total_fatal_injuries' and 'total_serious_injuries', 'number_of_engines', 'report_status

`df_cleaned = df_aviation_data.dropna(subset=['make', 'model', 'aircraft_category', 'injury_severity', 'total_fatal_injuries', 'total_serious_injuries', 'number_of_engines', 'aircraft_damage', 'weather_condition', 'broad_phase_of_flight'])`

Checking the unique values in the 10 columns of interest

`unique_makes = df_cleaned['make'].unique()`
`unique_models = df_cleaned['model'].unique()`
`unique_categories = df_cleaned['aircraft_category'].unique()`
`unique_injury_severity = df_cleaned['injury_severity'].unique()`
`unique_fatal_injuries = df_cleaned['total_fatal_injuries'].unique()`
`unique_serious_injuries = df_cleaned['total_serious_injuries'].unique()`
`unique_number_of_engines = df_cleaned['number_of_engines'].unique()`
`unique_aircraft_damage = df_cleaned['aircraft_damage'].unique()`
`unique_weather_condition = df_cleaned['weather_condition'].unique()`
`unique_broad_phase_of_flight = df_cleaned['broad_phase_of_flight'].unique()`

# Exploratory Data Analysis
Explored the data, calculated the mean of all the numerical values
`df_cleaned.info()`

`df_cleaned.describe()`

`df_cleaned.mean()`

`df_cleaned['total_fatal_injuries].median()`

## Aircratf with low or no fatal injuries

`df_cleaned['total_fatal_injuries'].value_counts()`

Explored the 20 aircraft models with the least number of total fatal injuries

`top_20_total_fatal_injuries = df_cleaned.groupby("model").agg(total_fatal_injuries=('total_fatal_injuries', 'sum') ).reset_index()` 
`top_20_least_fatalities = top_20_total_fatal_injuries.sort_values("total_fatal_injuries", ascending=True).head(20)` 


20 most aircraft models with the least number of total serious injuries

`top_20_total_serious_injuries = df_cleaned.groupby("model").agg(total_serious_injuries=('total_serious_injuries', 'sum') ).reset_index()`
`top_20_least_total_serious_injuries = top_20_total_serious_injuries.

sort_values('total_serious_injuries', ascending=True).head(20)`

20 most aircraft models with the MOST number of total_fatal_injuries

`top_20_total_fatal_injuries = df_cleaned.groupby("model").agg

(total_fatal_injuries=('total_fatal_injuries', 'sum') ).reset_index()`

`top_20_most_fatalities = top_20_total_fatal_injuries.sort_values("total_fatal_injuries", ascending=False).head(20)`

# Data Visualization 
## Total Fatal Injuries by Aircraft Model

![Top 20 most fatalities](/http://localhost:8888/tree/output_to_20_fatalities_model_bar.png)

## Total Fatal Injuries by Aircraft Make

![Total Fatal Injuries by Make](/output_to_20_fatalities__make_bar.png)


# Scatter plots
pd.plotting.scatter_matrix(df_cleaned_tfatal);

![scatter plot of df_cleaned_tfatal](/output-%20scattter.png)

![scatter by make](/output-most%2020%20fatalities%20vs%20model.png)



Reccomendation 

The aircraft with the most number of fatalities is the model 747-300. This could be due to its high capacity of over 500 passengers

Makes such as Adams, Aeronca Champion and weatherly have not reported any fatal injuries. 


Link to Gitbuh Repository

Link to DashBoard 
https://public.tableau.com/authoring/Phase1ProjectPG_Dashboard/Dashboard1#1


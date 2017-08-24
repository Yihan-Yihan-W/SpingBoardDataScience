# SpingBoardDataScience
Codes for data science courses

# Data Wrangling Project
## 1. JSON Data Wrangling project

  I normalize the JSON_world_bank data and extract the top 10 countries with most projects
  I Find the top 10 major project themes based on themecode I found the themecode difficult to understand, therefore,   I extract the information of themecode with its corresponding themename as a DataFrame called themename. By merging the top 10 counts with themename dataframe, the outcome shows both themecode, themename, and counts
  There are some blanks for themename, to solve the missing value problems: First, I sort the data by theme code and themename so that blank values appear top for everycode Second, I change all " " to np.nan, Third, forward fill all the NaN
  To make sure the top 10 major project themes count is correct, I count again using themename. Then, apply the same merging techniques to show both themecode and theme name on the data frame.
  
  json_normalize() 
  DataFrame.drop_duplicates(subset=None, keep='first', inplace=False) 
  DataFrame.columns = [" "] 
  pd.merge(df1, df2, how=' ', on=' ' ) 
  df.reindex(columns= ) 
  df.replace('', np.nan).bfill()
 
## 2. XML Data Wrangling Project 
XML exercise is an ipython notebook to extract useful information from xml files.
The data source is from Mondial database: http://www.dbis.informatik.uni-goettingen.de/Mondial/

1) To find the lowest infant mortality rate
  I loop through each country by root.iter()
  find the name, and the population of the country by find().text and 
  use population as subchild from root, i get the population by using .text, and change it to float type

2) 10 cities with the largest population
  use the lastest year as population year
  read dictionary as df, and sort the values

3) 10 ethnic groups with the largest overall populations
  use a for loop through population, compare each attribute year, 
  update the list of population if the year attribute is latest
  get the list of population of each ethnictity in each country
  read list as dataframe, group by ethnicity and sum within each group
  
4) Name & Country of
A) longest river
  use root.iter() to find "river" element
  use if to compare length of river
  return country name attribute by using element.get()
B) largest lake
  same methods as A)
C) highest elevation airport 
  convert string to int/float
  check if there is blank/comma in the string 
  use try except function 

Useful codes:
  root.iter()
  for child in element.findall("xxx"): int(child.text)
  element.findtext()

root.find("river")[:]

## 3. SQL_Yammer Data Wrangling Project 
Its is an exericise using Mode to write SQL queries and generate reports. 
Reports & Codes : https://modeanalytics.com/yihanyihan/reports/5d1898a86885

# Inferential Statistics 
## 4. Statistics1_body temperature
## 5. Statistics2_race employment 

# SpingBoardDataScience
Codes for data science courses


# JSON_world_bank.ipynb is the practice for JSON and Pandas library
1) I normalize the JSON_world_bank data and extract the top 10 countries with most projects
2) I Find the top 10 major project themes based on themecode
   I found the themecode difficult to understand, therefore, 
   I extract the information of themecode with its corresponding themename as a DataFrame called themename.
   By merging the top 10 counts with themename dataframe, the outcome shows both themecode, themename, and counts
3) There are some blanks for themename, to solve the missing value problems:
   First, I sort the data by theme code and themename so that blank values appear top for everycode
   Second, I change all " " to np.nan,
   Third, forward fill all the NaN 
4) To make sure the top 10 major project themes count is correct, I count again using themename.
   Then, apply the same merging techniques to show both themecode and theme name on the data frame.

# Useful functions:
json_normalize()
DataFrame.drop_duplicates(subset=None, keep='first', inplace=False)
DataFrame.columns = [" "]
pd.merge(df1, df2, how=' ', on=' ' )
df.reindex(columns= )
df.replace('', np.nan).bfill()

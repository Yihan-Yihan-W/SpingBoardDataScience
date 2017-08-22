XML exercise is an ipython notebook to extract useful information from xml files.

The data source is from Mondial database:  http://www.dbis.informatik.uni-goettingen.de/Mondial/

# 1) To find the lowest infant mortality rate
    I loop through each country by root.iter()
    find the name, and the population of the country by find().text and 
    use population as subchild from root, i get the population by using .text, and change it to float type

# 2) 10 cities with the largest population
    use the lastest year as population year
    read dictionary as df, and sort the values
# 3) 10 ethnic groups with the largest overall populations
    use a for loop through population, compare each attribute year, 
    update the list of population if the year attribute is latest
    get the list of population of each ethnictity in each country
    read list as dataframe, group by ethnicity and sum within each group
# 4) Name & Country of 
    A) longest river
    use root.iter() to find "river" element
    use if to compare length of river
    return country name attribute by using element.get()
    B) largest lake
    same methods as A)
    C) highest elevation airport 
    # ?????? I can't convert string to int/float #
   

# Useful codes:
root.iter()

for child in element.findall("xxx"):
    int(child.text)

element.findtext()

root.find("river")[:]


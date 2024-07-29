# python
from bs4 import BeautifulSoup
import requests

url = 'https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue'
page = requests.get(url)
soup = BeautifulSoup(page.text, 'html')
print(soup)

soup.find_all('table')[1]

table = soup.find_all('table')[1]

print(table)

world_title = table.find_all('th')

world_title

world_table_titles = [title.text.strip() for title in world_title]

print(world_table_titles)

import pandas as pd

pd.DataFrame(columns = world_table_titles)

table.find_all('tr')

column_data = table.find_all('tr')

for row in column_data:
    row_data = row.find_all('td')
    print(row_data)

#to remove the empty column

for row in column_data[1:]:
    row_data = row.find_all('td')
    individual_row_data = [data.text.strip() for data in row_data]
    print(individual_row_data)

    
#
df = pd.DataFrame(columns = world_table_titles)

#to pull the data into the frame
for row in column_data[1:]:
    row_data = row.find_all('td')
    individual_row_data = [data.text.strip() for data in row_data]
    
    length = len(df)
    df.loc[length] = individual_row_data


#print df
df

#to export it to excel

df.to_csv(r'C:\Data Science\Data Analyst\Company1.csv', index = False)















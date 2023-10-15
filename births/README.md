# U.S. Births

This folder contains data behind the story [Some People Are Too Superstitious To Have A Baby On Friday The 13th](http://fivethirtyeight.com/features/some-people-are-too-superstitious-to-have-a-baby-on-friday-the-13th/).

There are two files:

`US_births_1994-2003_CDC_NCHS.csv` contains U.S. births data for the years 1994 to 2003, as provided by the Centers for Disease Control and Prevention's National Center for Health Statistics.

`US_births_2000-2014_SSA.csv` contains U.S. births data for the years 2000 to 2014, as provided by the Social Security Administration.

Both files have the following structure:

Header | Definition
---|---------
`year` | Year
`month` | Month
`date_of_month` | Day number of the month
`day_of_week` | Day of week, where 1 is Monday and 7 is Sunday
`births` | Number of births

import pandas as pd

df_1994_2003 = pd.read_csv('US_births_1994-2003_CDC_NCHS.csv')
df_2000_2014 = pd.read_csv('US_births_2000-2014_SSA.csv')

combined_data = pd.concat([df_1994_2003, df_2000_2014])

friday_13_births = combined_data[(combined_data['day_of_week'] == 5) & (combined_data['date_of_month'] == 13)]

monthly_friday_13_births = friday_13_births.groupby(['year', 'month'])['births'].sum()

import matplotlib.pyplot as plt

monthly_friday_13_births.plot(legend=True, figsize=(12, 6))
plt.xlabel('Year-Month')
plt.ylabel('Number of Friday the 13th Births')
plt.title('Friday the 13th Births Over the Years')
plt.show()

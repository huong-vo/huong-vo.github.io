---
layout: post
title: Data Visualization and Analysis for AI 101 Warm-up
date: 2025-08-04
description: pandas, series, dataframe, visualization, seaborn
tags: coding AIO prob-stat
categories: AI
giscus_comments: true                         # github comment - automatically generated - not working for now
pretty_table: true                            # add table
# featured: true                                # pin a post
toc:                                          # table of contents
    sidebar: right
---

**Acknowledgement:** This post is based mainly on TA Nguyen Quoc Thai's presentation and slides and partly on on TA, STA, and peers' responses from the course AIO2025 offered by AI VIETNAM.

**Relevance:** The audience of this lecture were those who have read [Math for AI 102]({% post_url 2025-07-04-math102 %}), had some coding experience, and known a bit of AI knowledge. Absolute beginners are encouraged to read the material and repeatedly practice coding without AI assistance to strengthen their coding and code-reading skills. Note that only necessary pandas knowledge is introduced here.

In today's post, we'll explore basic pandas using examples: Pokemon Data Analysis and Time Series Dataset.

<hr>

## **pandas**
### **Introduction**
[Data analysis](https://en.wikipedia.org/wiki/Data_analysis) is a process of inspecting, cleansing, transforming, and modeling data with the goal of discovering useful information, informing conclusions, and supporting decision-making. That is, it includes visualization like charts, graphs, or maps based on which users can produce insights about a dataset.

**pandas** is a library built on NumPy written specifically for Python language. It is a data manipulation and analysis tool, providing simple and practical data structures ready for usage.

Check out [pandas documentation](https://pandas.pydata.org/docs/) for more packages. We can set up pandas and check its version as follows. 

```python
!pip install pandas

import pandas as pd

pd.__version__
>>> 
```

There are three primary data structures in pandas, but one of them is barely used these days, so we'll focus on the other two: *DataFrame* and *Series*. Since pandas is built on NumPy, its data structures have certain similarities with ndarray.

### **DataFrame** 
A **DataFrame** is a 2D labeled data structure in which data in columns can be of different types. Visually, it is like 2D tables with headers in Excel. 

Upon its creation, indices for rows are *automatically generated* by default. But we can certainly set up our own indices.

We are allowed to create a dataframe from various data structures such as arrays, dictionaries, lists, zip() functions, or even an existing DataFrame. Take a look at an example below.

```python
data = {
    'Name': ['Brucy', 'Fiona', 'Ziggy', 'Ranger'],
    'Gender': ['M', 'F', 'F', 'M']
}

df = pd.DataFrame(data)
df

'''
    Name    Gender
0   Brucy   M
1   Fiona   F
2   Ziggy   F
3   Ranger  M
'''
```

### **Series**
A **Series** is a 1D labeled array that can hold any data type. Upon its creation, indices for rows also are *automatically generated* by default. But we can explicitly name the indices. Since there is only one non-indexed column, the header row is not shown in the rendered table, but we can display it by converting the Series to a DataFrame. 

```python
data = np.array(['Brucy', 'Fiona', 'Ziggy', 'Ranger'])

s = pd.Series(data, name = 'Name')
s

'''
0     Brucy
1     Fiona
2     Ziggy
3    Ranger
Name: Name, dtype: object
'''
```

The definitions of both data structures infer that a DataFrame is *essentially* a combination of a Series sequence. Continue from the DataFrame example.

```python
name_series = df['Name']
type(name_series)
<class 'pandas.core.series.Series'>

gender_series = df['Gender']
type(gender_series)
<class 'pandas.core.series.Series'>

new_df = pd.concat([name_series, gender_series], axis=1)
type(new_df)
<class 'pandas.core.frame.DataFrame'>
```

Thus, we can also create a DataFrame from Series. 

```python
# create two Series
name_series = pd.Series(['Brucy', 'Fiona', 'Ziggy', 'Ranger'], name='Name')
gender_series = pd.Series(['M', 'F', 'F', 'M'], name='Gender')

# create DataFrame from Series
df_from_series = pd.concat([name_series, gender_series], axis=1)
df_from_series

'''
    Name    Gender
0   Brucy   M
1   Fiona   F
2   Ziggy   F
3   Ranger  M
'''
```

<hr>

In the next two sections, we'll use a couple of hands-on examples to learn pandas step by step. These datasets are written in .csv files, which are quite common for storing data. 

## **Pokemon Data Analysis**
**Read and Save a CSV File** <br>
If we print `data` out, we'll see the information table and its numbers of rows and columns.

```python
DATASET_PATH = 'Pokemon.csv'
data = pd.read_csv(DATASET_PATH)
```

We can certainly save a dataset to a file under various format. The following is for a .csv file.

```python
data.to_csv('new_Pokemon.csv')
```

**Head/Tail Method** <br>
With this method, we can check out how many first and last rows we want with some following syntax. By default, five rows at the top or at the bottom of the DataFrame will be shown when no argument is added. 

```python
data.head()
data.head(n=7)
data.head(900)
data.tail(10)
```

**Rows** <br>
Not only header/tail rows, we can read an equally-spaced sequence of rows by *slicing* a DataFrame using `[start:stop:step]`.

```python
data[2:10:3]

'''
    #   Name                        Type 1  Type 2  Total   HP  Attack  Defense Sp. Atk Sp. Def Speed   Generation  Legendary
2   3   Venusaur                    Grass   Poison  525     80  82      83      100     100     80      1           False
5   5   Charmeleon                  Fire    NaN     405     58  64      58      80      65      80      1           False
8   6   CharizardMega Charizard Y   Fire    Flying  634     78  104     78      159     115     100     1           False
'''
```

However, we cannot do indexing to read one specific row. Instead, we can use `iloc`---**index-based** selecting method. We can treat a row index as an array index or a real row in a table. Thus, the datatypes of two ways are different---one is a Series and the other is a DataFrame. 

Only a snippet of the output is provided in the following code. 

```python
# this renders a Series
data.iloc[7]

'''
#                                     6
Name          CharizardMega Charizard X
Type 1                             Fire
...                                 ...

Name: 7, dtype: object
'''
```

A Series is like a 1D array, so we can get its elements by their indices or slicing. Or you can think of it as getting an element from a 2D array where the first argument is index/slice for rows and the second for columns.

```python
data.iloc[7, 10]

'''
100
'''
```

```python
# this renders a DataFrame
data.iloc[[7]]

'''
    #   Name                        Type 1  Type 2  Total   HP  Attack  Defense Sp. Atk Sp. Def SpeeD   Generation  Legendary
7   6   CharizardMega Charizard X   Fire    Dragon  634     78  130     111     130     85      100     1           False
'''
```

Since it is a DataFrame, it can handle multiple rows and columns simultaneously. We can read more rows by adding more row indices to the list.

```python
# this renders a DataFrame
data.iloc[[7, 10]]

'''
    #   Name	                    Type 1  Type 2  Total   HP  Attack  Defense Sp. Atk Sp. Def Speed   Generation  Legendary
7   6   CharizardMega Charizard X   Fire    Dragon  634	    78  130	    111	    130	    85	    100	    1	        False
10  8   Wartortle                   Water   NaN	    405	    59  63	    80	    65	    80	    58	    1	        False
'''
```

If row indices are renamed to something esle, we can use `loc`---**label-based** selecting method to check out rows. Because of how it works, we must use a header or a list of headers rather than an index or slicing to get elements.

```python
data.loc[7, 'Legendary']

'''
False
'''
```

This is also very powerful since it can filtering rows. We'll talk more about it later when we have sufficient tools.

**Reset Index** <br>
As we see above, indices of rows are kept the same as in the original dataset when extracted. This is inconvenient to work with just that part of the dataset. We can save it to a new variable and reset index. The original indices are kept and the new indices is added.

```python
new_slice = data.loc[7:20:3]
new_slice.reset_index()

'''
    index   #   Name                        Type 1  Type 2  Total   HP  Attack  Defense Sp. Atk Sp. Def Speed   Generation  Legendary
0   7       6   CharizardMega Charizard X   Fire    Dragon  634     78  130     111     130     85      100     1           False
1   10      8   Wartortle                   Water   NaN     405     59  63      80      65      80      58      1           False
2   13      10  Caterpie                    Bug     NaN     195     45  30      35      20      20      45      1           False
3   16      13  Weedle                      Bug     Poison  195     40  35      30      20      20      50      1           False
4   19      15  BeedrillMega Beedrill       Bug     Poison  495     65  150     40      15      80      145     1           False
'''
```

**Headers** <br>
We can see all the headers of columns in a dataset. They will

```python
data.columns
>>> Index(['#', 'Name', 'Type 1', 'Type 2', 'Total', 'HP', 'Attack', 'Defense',
           'Sp. Atk', 'Sp. Def', 'Speed', 'Generation', 'Legendary'],
           dtype='object')
```

**Columns** <br>
There are two simple ways to check out data values in particular columns. We can treat a header as an index of a list or a real header of a table. Like rows above, one result is a Series and the other is a DataFrame. 

Only a snippet of the output is provided in the following code. Check out the practice exercise to read more than one columns.

```python
data['Name']

data[['Name']]
```

**Row Filtering** <br>
Like an array, we can filter rows via comparison operations. We can see whole rows or just a few columns of satisfied rows. 

First, let's apply `loc`.

```python
# only rows with data value being True in the Legendary column are selected
data.loc[data['Legendary'] == True]

# only a column and rows with data value being True in the Legendary column are selected
data.loc[data['Legendary'] == True, 'Name']

data.loc[data['Legendary'] == True, ['Name']]
```

```python
data.loc[(data['Type 1'] == 'Grass') & (data['Type 2'] == 'Poison')]
```

In addition, we can choose selective rows by **Regex** with package `import re`.

```python
import re

# rows with name containing 'Mega'
data.loc[data['Name'].str.contains('Mega')]

# rows with type 1 being either 'Fire' or 'Grass'
data.loc[data['Type 1'].str.contains('Fire|Grass')]
```

**Describe Method** <br>
pandas provides basic descriptive statistics on every numerical column of a dataset with a simple syntax `describe()`.

```python
data.describe()
```

**Arranging Order** <br>
We can sort a dataset based on columns and the result is in an increasing order by default. We can add the `ascending=False` or `ascending=0` argument to reverse it. We use a list to sort multiple columns and various orders. This method does *not* affect the original data.

```python
# sort by one column
data.sort_values('Total')

# sort by multiple columns
data.sort_values(['Total', 'Type 1'], ascending=[1, 0])
```

We can also arrange columns in a certain order. This produces a DataFrame of selected columns in the desired order. Thus, this method does *not* affect the original data.

```python
data[['Type 1', 'Name']]
```

**Update Data** <br>
We can add or remove columns for a dataset. Use `drop()` for column removal; this does *not* affect the original dataset. On the other hand, adding a column updates the original dataset. If an existing column is modified, it will be updated rather than a new column is added.

```python
# remove a column and store the new dataset to a new variable
new_data = data.drop(columns='Total')

# add a column
# add two numerical columns
new_data['Attack + Defense'] = new_data['Attack'] + new_data['Defense']
```

**groupby Function** <br>
We can group values of columns based on their types. 

```python
data.groupby(['Type 1', 'Type 2']).count()

'''
                    #   Name    Total   HP  Attack  Defense Sp. Atk Sp. Def Speed   Generation  Legendary
Type 1	Type 2											
Bug     Electric    2   2       2       2   2       2       2       2       2       2           2
        Fighting    2   2       2       2   2       2       2       2       2       2           2
...     ...         ... ...     ...     ... ...     ...     ...     ...     ...     ...         ...  

Water   Ice         3   3       3       3   3       3       3       3       3       3           3
        Poison      3   3       3       3   3       3       3       3       3       3           3
'''
```

We can further this step by using an additional function to manipulate data. You can check out more functions as needed.

```python
data.groupby(['Type 1', 'Type 2'])[['HP']].apply(
    lambda x: x.sum() / len(x)
)
```

<details class = "bordered-block">
    <summary>
        <strong>Practice Exercises</strong>
    </summary>
    <div class = "bordered-inner-block language-python">
        <strong>Exercise 1:</strong> What is the rendered output if the argument is greater than the total number of rows? An error or the entire table. 
        <br>
        <strong>Exercise 2:</strong> In the code blocks of "Columns", which one give a Series or a DataFrame? Which one can be used to read more than one column?
        <br>
        <strong>Exercise 3:</strong> In the code blocks of "Columns", which one can be used to read more than one column? Explain why. What does the other result in? Explain why?
        <br>
        <strong>Exercise 4:</strong> What is the output of <code>data.loc[7, 'Legendary', 'Total']</code> and <code>data.loc[7, ['Legendary', 'Total']]</code>?
        <br>
        <strong>Exercise 5:</strong> In the code block of "Row Filtering", what can you do to show more than one column?
    </div>
</details>
<br>

## **Time Series Dataset**
A time series dataset including a continuous time period.

```python
ts_df

'''
        Date        Daily minimum temperatures
0       1/1/1981    20.7
1       1/2/1981    17.9
2       1/3/1981    18.8
3       1/4/1981    14.6
4       1/5/1981    15.8
...	    ...	        ...

3645    12/27/1990  14
3646    12/28/1990  13.6
3647    12/29/1990  13.5
3648    12/30/1990  15.7
3649    12/31/1990  13
'''
```

**Time Format Conversion** <br>
A dataset may have a date or time column, but their values might not be in the right format. pandas allows us to convert such data to time format which makes accessing a certain date/time row convenient. We can also get each part of a date/time; for example, day, month, or year.

```python
# time format conversion
ts_df['Date'] = pd.to_datetime(ts_df['Date'])

# set 'Date' column as an index column
ts_df = ts_df.set_index('Date')
```

We can use the code below with some modification to create new meaningful columns for time.

```python
# index_cols=0 takes the first column
# parse_dates reads data as time, not string
df = pd.read_csv('timeseries_daily-minimum-temperatures.csv', index_col=0, parse_dates=True)

df.index.year
df.index.month
df.index.day_name()
```

**Time-based Indexing** <br>
As mentioned, once we convert the 'Date' column to time format, we can retrieve rows via time-based indices.

```python
# get rows from one date to another by slicing
ts_df.loc['1987-08-29':'1997-03-30']

# get ros in a specific month
ts_df.loc['1990-01']
```

### **Time Series Data Visualization**
**pandas** <br>
In order to visualize data, values should be numeric for computers to understand. If there are values that cannot be converted into a number, for example, due to wrong format, we can either remove such a row or force the value to be fixed. Otherwise, an error is produced.

```python
col_to_plot = 'Daily minimum temperatures'

# force wrong values to be fixed
ts_df[col_to_plot] = pd.to_numeric(ts_df[col_to_plot], errors='coerce')

# plot
ts_df[col_to_plot].plot(
    linewidth=0.5,
    figsize=(10,4),
    legend=True
)

# plot
ts_df[col_to_plot].plot(
    marker='.',
    alpha=0.5,
    linestyle='None',
    figsize=(10,4),
    legend=True
)
```

<figure>
    <div style='display: flex; flex-wrap:wrap; column-gap: 20px; justify-content: center'>
        {% include figure.liquid loading="eager" path="assets\aio2025\M03W01\tuesday_daily_min_temp_line_plot.png" class="img-fluid rounded z-depth-1 mx-auto d-block" zoomable=true max-width="320px" max-height="450px" alt="line plot" caption="Line plot" %} 
        {% include figure.liquid loading="eager" path="assets\aio2025\M03W01\tuesday_daily_min_temp_dot_plot.png" class="img-fluid rounded z-depth-1 mx-auto d-block" zoomable=true max-width="320px" max-height="450px" alt="dot plot" caption="Dot plot" %} 
    </div>
    <figcaption style="text-align: center; width: 100%; font-size:0.875em; margin-top:-25px;">
        <em>Figure 1:</em> Daily minimum temperatures
    </figcaption>
</figure>

**Seasonality with seaborn** <br>
When dealing with time series datasets, it's important to understand data values according to their time blocks. This is called *seasonality*. Formally, **seasonality** is a characterisitc of a time series where data experiences roughly periodic changes recurring yearly.

**seaborn** is a Python data visualization library built on top of **matplotlib**.

```python
import matplotlib.pyplot as plt
import seaborn as sns

# set figure size
sns.set(rc={'figure.figsize':(10,4)})
# plt.figure(figsize=(10,4))

# boxplot
sns.boxplot(ts_df, x='Month', y=col_to_plot)
```

{% include figure.liquid loading="eager" path="assets\aio2025\M03W01\tuesday_seasonal_min_temp_box_plot.png" class="img-fluid rounded z-depth-1 mx-auto d-block" zoomable=true max-width="500px" max-height="600px" alt="seasonal minimum temperatures with boxplot" caption="<em>Figure 2:</em> Seasonal minimum temperatures with boxplot. The box has 3 lines associated with 25%, 50%, 75% and circles on top and bottom as outliers." %} 

**Frequencies** <br>
With time format, we can get a sequence of time periods based on their frequency and/or the number of periods. Frequency is day by default, but it can be, say hour. 

```python
pd.date_range('1997-03-30', '1997-05-03')

pd.date_range('1997-03-30', '1997-05-03', freq='h')

pd.date_range('1997-03-30', periods=8, freq='h')
```

Assume that we have only 3 random time series data points. But we want to convert data to daily frequency. 

```python
# convert string to time format
times_sample = pd.to_datetime(['1981-01-01', '1981-01-04', '1981-01-08'])

# make a DataFrame to manipulate
consum_sample = ts_df.loc[times_sample, ['Daily minimum temperatures']].copy()
consum_sample

# convert data to daily frequency
# new rows has no data
consum_freq = consum_sample.asfreq('D')
consum_freq

# create a column with missings to be forward filled
# forward fill is with 'before' data
# backward fill is with 'after' data
consum_freq['Daily minimum temperatures - Forward Fill'] = consum_sample.asfreq(
    'D', method='ffill'
)
consum_freq

'''
            Daily minimum temperatures
1981-01-01  20.7
1981-01-04  14.6
1981-01-08  17.4


            Daily minimum temperatures
1981-01-01  20.7
1981-01-02  NaN
1981-01-03  NaN
1981-01-04  14.6
1981-01-05  NaN
1981-01-06  NaN
1981-01-07  NaN
1981-01-08  17.4

            Daily minimum temperatures  Daily minimum temperatures - Forward Fill
1981-01-01  20.7                        20.7
1981-01-02  NaN                         20.7
1981-01-03  NaN                         20.7
1981-01-04  14.6                        14.6
1981-01-05  NaN                         14.6
1981-01-06  NaN                         14.6
1981-01-07  NaN                         14.6
1981-01-08  17.4                        17.4
'''
```

**Resampling** <br>
Resampling is a technique used when values in each data block are close with each other. For example, temperatures at 11am, 12am, and 1pm are 99, 100, 101 degree Fahrenheit. We can somehow take only one value to represent for these data points to save resources.
- Find a common feature of values and use it to calculate a common number. Take mean or median for example.
- If there is no common feature, use one of the values. 

```python
col_to_resample = 'Daily minimum temperatures'

# take the mean of temperatures by week
ts_weekly_mean = ts_df[[col_to_resample]].resample('W').mean()
ts_weekly_mean.head(3)

'''
            Daily minimum temperatures
Date	
1981-01-04  18.000000
1981-01-11  17.542857
1981-01-18  20.371429
'''
```

{% include figure.liquid loading="eager" path="assets\aio2025\M03W01\tuesday_daily_min_weekly_mean_temp_plot.png" class="img-fluid rounded z-depth-1 mx-auto d-block" zoomable=true max-width="500px" max-height="600px" alt="comparison of Daily and Weekly Mean Minimum Temperatures in 1981." caption="<em>Figure 3:</em> Comparison of Daily and Weekly Mean Minimum Temperatures in 1981 <br> This plot shows daily minimum temperature values (blue dots and lines) alongside their weekly mean resampling (orange dots and lines) for the period January to December 1981. The weekly mean resampling smooths out short-term fluctuations to reveal broader temperature trends." %} 

```python
# plot daily and weekly resampling for a period
start, end = '1981-01', '1981-12'

# create the plot
fig, ax = plt.subplots()

ax.plot(
    ts_df.loc[start: end, col_to_resample],
    marker='.',
    linestyle='-',
    linewidth=0.5,
    label='Daily Minimum Temperatures'
)

ax.plot(
    ts_weekly_mean.loc[start: end, col_to_resample],
    marker='o',
    linestyle='-',
    label='Weekly Mean Resampling'
)

ax.set_ylabel('Temperature')
ax.legend()
```

<details class = "bordered-block">
    <summary>
        <strong>Practice Exercises</strong>
    </summary>
    <div class = "bordered-inner-block language-python">
        <strong>Exercise 1:</strong> Given the file's name is 'timeseries_daily-minimum-temperatures.csv', write code to read this dataset
        <br>
        <strong>Exercise 2:</strong> Write more code to add 'Year', 'Month', and 'Day' columns to the dataset.
    </div>
</details>

<hr>

## :speech_balloon: **FAQ**
Here are some good questions asked during class. The answers to these questions came from either some admin, TA, STA, or members of AIO2025.

| Questions | Answers |
|-----------|---------|
| If a dataset has more than one location, how can I visualize it? | You should visualization according to each location. The dataset should have locations' geographic coordinates. |


<br>

<!-- #### Check List

- [x] Exercise 1 (date)
- [ ] Exercise 2 (date)
  - [x] Put on left sock
  - [ ] Put on right sock
- [x] Go to school -->

---
layout: post
title: Data Visualization and Analysis for AI 101
date: 2025-08-05
description: pandas, series, dataframe, visualization, seaborn
tags: coding AIO prob-stat
categories: AI
giscus_comments: true                         # github comment - automatically generated - not working for now
pretty_table: true                            #  table
# featured: true                                # pin a post
toc:                                          # table of contents
    sidebar: right
---

**Acknowledgement:** This post is based mainly on Dr. Quang-Vinh Dinh's presentation and slides and partly on on TA, STA, and peers' responses from the course AIO2025 offered by AI VIETNAM.

**Relevance:** The audience of this lecture were those who have read [Math for AI 106]({% post_url 2025-07-18-math106 %}), had some coding experience, and known a bit of AI knowledge. 

In today's post, we'll explore pandas Series and DataFrame. We'll also discuss some applications in AI including processing missing values, noise reduction, and data visualization.

<hr>

pandas was built on top of NumPy, specifically for data analysis and visualization, like Excel. Since it has NumPy as an underlying structure, we can use what we know about NumPy to apply here.

## **pandas Series**
**pandas Series** is a 1D data array like a one-column table. Upone its creation, the numerical indices are *automatically generated* by default and shown in the rendered output, but they as a whole are not considered as a column. We can update the indices as desired---that is, an index can be any real number, a letter, or other data types.

### **Series Creation**
**Create a Series from a List** <br>

```python
data1 = pd.Series([2, 5, 100, 7, 3, 4], name='score')
data1

'''
0      2
1      5
2    100
3      7
4      3
5      4
Name: score, dtype: object
'''
```

```python
data2 = pd.Series(['C++', 'Java', 'Python', 'Golang', 'Swift'], 
                 index=list('CJPGS'),
                 name='Programming Language')
data2

'''
C       C++
J      Java
P    Python
G    Golang
S     Swift
Name: Programming Language, dtype: object
'''
```

**Get Elements** <br>

Use `data1`. Just like ndarray in NumPy, we can apply **indexing** and **slicing** for pandas Series to get one or more elements.

```python
# values in a Series is an ndarray
data1.values
>>> array([  2,   5, 100,   7,   3,   4], dtype=int64)

# indexing
data1[1]
>>> 5

# slicing
data1[2:4]
>>> 2   100
    3     7
    Name: score, dtype: object
```

A list of indices can be passed as an argument to obtain information from specific rows that may be unevenly-spaced.

```python
data2[['C', 'J', 'C']]
>>> C     C++
    J    Java
    C     C++
    Name: Programming Language, dtype: object
```

pandas has other methods to obtain values in a Series like `loc` which may be more non-tech-friendly.

```python
data1.loc[2:4]
>>> 2   100
    3     7
    4     3
    Name: score, dtype: object
```

Similarly, pandas also has **boolean indexing**.

```python
# boolean indexing
data1[data1 < 4]
>>> 0    2
    4    3
    Name: score, dtype: int64

# boolean indexing
data1[data1.between(5, 7)]
>>> 1    5
    3    7
    Name: score, dtype: int64
```

For `data2` with non-numeric indices, we can either use numeric or customized indices to retrieve elements. 

```python
data2['C']
>>> 'C++'

data2.loc['C':'J']
>>> C     C++
    J    Java
    Name: Programming Language, dtype: object
```

### **Operations**
**Drop a Row** <br>
We can remove an existing row by using `drop()` with indexing. This method returns a new Series *instead of* changing the original. *Note* that the returned Series keeps the original indices.

```python
data1.drop([1, 3])
>>> 0      2
    2    100
    4      3
    5      4
    Name: score, dtype: int64

data1
>>> 0      2
    1      5
    2    100
    3      7
    4      3
    5      4
    Name: score, dtype: object
```

**Insert a Row** <br>
Inserting a Row in pandas is similar to that for a Python dictionary. The new row is ed to the original Series or changes an existing row if they have the same index. 

```python
data2['K'] = 'Kotlin'
data2
>>> C       C++
    J      Java
    P    Python
    G    Golang
    S     Swift
    K    Kotlin
    Name: Programming Language, dtype: object
```

If an index is not an integer, we can certainly **reset** the Series so that it is properly indexed. This method does *not* change the original Series. 

```python
data1[2.5] = 99

# without drop=True, the old index column is ed
data1.reset_index(drop=True)
>>> 0      2
    1      5
    2      100
    3      7
    4      3
    5      4
    6      99
    Name: score, dtype: int64  
```

**Sort a Series** <br>
Sorting a Series by its index can be done with method `sort_index()`. We can decide if the original Series should be updated or not by the argument `inplace`, in particular,
- `inplace=True` returns None and update the original Series.
- `inplace=False` returns a *sorted* Series and does *not* update the original Series.

```python
# update the original Series
data2.sort_index(inplace=True)
data2
>>> C       C++
    G    Golang
    J      Java
    K    Kotlin
    P    Python
    S     Swift
    Name: Programming Language, dtype: object
```

```python
# NOT update the original Series
sorted_data2 = data2.sort_index(inplace=False)
sorted_data2 
>>> C       C++
    G    Golang
    J      Java
    K    Kotlin
    P    Python
    S     Swift
    Name: Programming Language, dtype: object

data2
>>> C       C++
    J      Java
    P    Python
    G    Golang
    S     Swift
    K    Kotlin
    Name: Programming Language, dtype: object
```

**Common Functions** <br>
pandas contains NumPy's common functions
- `series.min()`
- `series.max()`
- `series.idxmin()` or `series.argmin()`
- `series.idxmax()` or `series.argmax()`
- `series.sum()`
- `series.mean()`
- `series.var()`
- `series.std()`
- `series.str.count()`: the argument can be a character or a string and it counts the number of characters or strings in each value.
- `series.str.upper()`
- `series.replace(current_value, new_value)`: replace the current value with a new value.

** Two Series** <br>
If values from Series are of the same data type, they can be ed or concatenated. Behind the scenes, pandas looks for the matching index and  two values together. If it *cannot* find a row's matching index, it will render `NaN`.

```python
# modify data1 to have 6 rows
data1[2.5] = 99
data1.sort_index(inplace=True)

# create data3 of 5 rows
data3 = pd.Series([10, 10, 10, 10, 10])

#  data1 and data3
data1 + data3
>>> 0.0     12.0
    1.0     15.0
    2.0    110.0
    2.5      NaN
    3.0     17.0
    4.0     13.0
    5.0      NaN
dtype: float64
```

**Group Values** <br>
If some values have the same name/index and we want to group them together, we can use `groupby()`. This syntax returns another Series, so we can certainly use Series methods or function on it.

```python
data4 = pd.Series([4, 1, 0, 2, 2, 1, 8],
                  index=list(['C++', 'Golang', 'Java', 'Golang', 'Java', 'C++', 'Python']),
                  name='groupby')

# test
data4.groupby(level=0).sum()
>>> C++         5
    Golang      3
    Java        2
    Python      8
    Name: groupby, dtype: int64

data4.groupby(data4 > 3).sum()
>>> groupby
    False     6
    True     12
    Name: groupby, dtype: int64

data4['Golang'].count()
>>> 2
```

### :bulb: **Application in AI**
**1D Interpolation** <br>
1. The problem introduced here appears in scaling images and the two techniques are a part of *Super-resolution Imaging*. Since scaling an image increases the number of cells but newly ed cells need values. 
2. Another situation is when we work with *missing* data points. We can either remove or keep them depending on the type of datasets. For those that stay, we need to make sure they have values. For example, time series data can be related with each other, so we'd like to keep missing values.

In both cases, we need to fill in context-appropriate rather than random values. For some datasets, we fill in with the average. In ition, we use `interpolate()` with a method argument to resolve this issue.
- **Linear Interpolation:** `method='linear'` by default.
- **Nearest Neighbor Interpolation:** `method='nearest'`.

```python
data5 = pd.Series([2, 5, 100, np.nan, 7, 3, np.nan, 9, np.nan], name='score')

# linear
data5.interpolate(method='linear')

# nearest neighbor
data5.interpolate(method='nearest')
```

In the example above, pandas considered 100 and 7 for the first `np.nan`.

<figure>
    <div style='display: flex; flex-wrap:wrap; column-gap: 20px; justify-content: center'>
        {% include figure.liquid loading="eager" path="assets\aio2025\M03W01\wednesday_weather_1Dinterpolation.png" class="img-fluid rounded z-depth-1 mx-auto d-block" zoomable=true max-width="400px" max-height="450px" alt="original data with NaN" caption="Original data with NaN" %}
        {% include figure.liquid loading="eager" path="assets\aio2025\M03W01\wednesday_weather_linear.png" class="img-fluid rounded z-depth-1 mx-auto d-block" zoomable=true max-width="320px" max-height="450px" alt="data after applying linear interpolation" caption="Data after applying linear interpolation" %}
        {% include figure.liquid loading="eager" path="assets\aio2025\M03W01\wednesday_weather_nearest_neighbor.png" class="img-fluid rounded z-depth-1 mx-auto d-block" zoomable=true max-width="320px" max-height="450px" alt="data after applying nearest neighbor interpolation" caption="Data after applying nearest neighbor interpolation" %}
    </div>
    <figcaption style="text-align: center; width: 100%; font-size:0.875em; margin-top:-25px;">
        <em>Figure 1.</em> The first 100 data points of a weather dataset before and after interpolation techniques
    </figcaption>
</figure>

<details class = "bordered-block">
    <summary>
        <strong>Nearest Neighbor Interpolation vs. Linear Interpolation</strong>
    </summary>
    <div class = "bordered-inner-block language-python">
        <strong>Problem statement:</strong> Assume there are two data points, find another data point given one of its coordinates.  
        <br>
        <strong>Breakdown:</strong> 
        <ul>
            <li> $x$ is the index, $y$ is the value in a Series. </li>
            <li> $(x_1, y_1)$ and $(x_2, y_2)$: two given data points. </li>
            <li> $x_3$: known coordinate of the third data point. </li>
            <li> $y_3$: unknown coordinate of the third data point. </li>
        </ul> 
        <strong>Idea:</strong> There are two simple but effective techniques: <em>nearest neighbor interpolation</em> and <em>linear interpolation</em>.
        <table class = "language-python">
            <tr>
                <th></th>
                <th>Nearest Neighbor</th>
                <th>Interpolation</th>
            </tr>
            <tr>
                <th scope='row'>Solution</th>
                <td class = "centered_td">
                    <ul>
                        <li> Compute distance from $x_3$ to $x_1$ and $x_2$. </li>
                        <li> Pick the y-value of the smaller one. </li>
                    </ul>
                </td>
                <td class = "centered_td">
                    <ul>
                        <li> Find the linear equation passing $(x_1, y_1)$ and $(x_2, y_2)$. </li>
                        <li> Take the corresponding y-value on that line. </li>
                        $$\begin{align*}
                        &y_3 = \frac{x_2 - x_3}{x_2 - x_1} y_1 \\ 
                        &+ \frac{x_3 - x_1}{x_2 - x_1} y_2 
                        \end{align*}$$
                    </ul>
                </td>
            </tr>
            <tr>
                <th scope='row'>Application</th>
                <td class = "centered_td">
                    <ul>
                        <li> If objects in an image are straight up perpendicular to the edges, they should look fine when the image is scaled.  </li>
                        <li> If they are slanted, they could look like a floor function, Lego blocks, or images in Minecraft. </li>
                    </ul>
                </td>
                <td class = "centered_td">This can be better for slanted objects.</td>
            </tr>
        </table>
        <br>
        {% include figure.liquid loading="eager" path="assets\aio2025\M03W01\wednesday_1Dinterpolation_nearest_neighbor.png" class="img-fluid rounded z-depth-1 mx-auto d-block" zoomable=true max-width="320px" max-height="450px" alt="image scaling using nearest neighbor technique" caption="Image scaling using nearest neighbor technique" %}
        <figure style="margin-top: 0; ping-top: 0;">
            <iframe src="https://www.geogebra.org/classic/mhxnhwws?embed" title='Interactive GeoGebra applet showing Nearest Neighbor and Linear Interpolation.' frameborder='0' height="700px" width="100%" style="border: 1px solid #ddd; margin-top: 0; ping-top: 0;" allowfullscreen>Your browser does not support iframes. View the interactive applet <a href="https://www.geogebra.org/classic/mhxnhwws" target="_blank" rel="noopener">here</a>.</iframe>
            <figcaption style="font-size:0.875em"> <em>Figure 2.</em> $f(x)$ represents the nearest neighbor interpolation. $g(x) = ax + b$ represents linear interpolation. Move the sliders for points $A$ and $B$ to set their y-values, then drag the slider point along the x-axis to choose the input $x$. The applet updates $f(x)$ and $g(x)$ to show the estimated values using each methodView the interactive applet. Click on the symbol in the bottom right corner to open the applet in full-screen mode.
            If the applet does not load, you can open it directly <a href="https://www.geogebra.org/classic/mhxnhwws" target="_blank" rel="noopener">here</a>.</figcaption>
        </figure>
    </div>
</details>
<br>

**Noise Reduction** <br>
**Noise** refers to the random irregularity or fluctuations in real-life datasets. There are a few ways to **reduce noise** in statistics.

**Simple Moving Average (SMA):** the simplest way in which we take the mean of data windows. 

$$SMA_t = \frac{s_t + \cdots + s_{t-k+1}}{k}$$

where $k$ is the size of each window.

**Exponential Moving/Weighted Average (EMA):** widely used in optimization, considering both the previously computed values and the current value.

$$EMA_t = \rho EMA_{t-1} + (1 - \rho) s_t$$

Later on, we'll mainly use EMA, but for now let's look at the graph of the above dataset after using SMA. The *larger* the window is, the *smoother* the graph is.

```python
linear_sma_5 = linear_int.rolling(window=5).mean()
linear_sma_5.head(100).plot()
```

<figure>
    <div style='display: flex; flex-wrap:wrap; column-gap: 20px; justify-content: center'>
        {% include figure.liquid loading="eager" path="assets\aio2025\M03W01\wednesday_weather_linear_sma_window=3.png" class="img-fluid rounded z-depth-1 mx-auto d-block" zoomable=true max-width="320px" max-height="450px" alt="window=3" caption="window=3" %}
        {% include figure.liquid loading="eager" path="assets\aio2025\M03W01\wednesday_weather_linear_sma_window=5.png" class="img-fluid rounded z-depth-1 mx-auto d-block" zoomable=true max-width="320px" max-height="450px" alt="window=5" caption="window=5" %}
        {% include figure.liquid loading="eager" path="assets\aio2025\M03W01\wednesday_weather_linear_sma_window=10.png" class="img-fluid rounded z-depth-1 mx-auto d-block" zoomable=true max-width="320px" max-height="450px" alt="window=10" caption="window=10" %}
    </div>
    <figcaption style="text-align:center; width:100%; font-size:0.875em; margin-top:-25px;">
        <em>Figure 3.</em> The first 100 data points of a weather dataset before and after applying linear interpolation and SMA
    </figcaption>
</figure>

<details class = "bordered-block">
    <summary>
        <strong>Practice Exercises</strong>
    </summary>
    <div class = "bordered-inner-block language-python">
        <strong>Exercise 1:</strong> For <code>data2</code>, what is the output of <code>data2['D']</code> and <code>data2['C':'X']</code>? Explain why.
        <br>
        <strong>Exercise 2:</strong> Work out the formulae for linear interpolation technique. 
        <br>
        <strong>Exercise 3:</strong> Which values does pandas consider for second and third <code>np.nan</code> in each case of the interpolation example? 
        <br>
        <strong>Exercise 4:</strong> Write code for the two other windows of the SMA example (linear and nearest neighbor).
    </div>
</details>

<hr>

## **DataFrame**
A **DataFrame** is a 2D labeled data structure. Unlike a Series, a DateFrame can have more than one data column. Basically, it is a combination of multiple Series. Thus, we can apply methods/functions in Series to work with DataFrames.

**Get Values** <br>
We can also apply **indexing** and **slicing** for pandas Series to get one or more elements like a NumPy array---using a comma to separate axes. 

```python
df = pd.read_csv('advertising_simple.csv')
df
>>>     TV  Radio   Newspaper   Sales
    0   44     39          45      10
    1   17     45          69      12
    2   151    41          58      16
    3   180    10          58      17
    4   8      48          75      7
    5   57     32          23      11
    6   120    19          11      13
    7   8      2           1       4

# get 'Radio' column
df.loc[:, 'Radio']
>>> 0     39
    1     45
    2     41
    3     10
    4     48
    5     32
    6     19
    7      2
    Name: Radio, dtype: int64

# get a DataFrame of 'Radio' column
df.loc[:, ['Radio']]
>>>    Radio
    0     39
    1     45
    2     41
    3     10
    4     48
    5     32
    6     19
    7      2

# another way to get 'Radio' column
df.Radio
>>> 0     39
    1     45
    2     41
    3     10
    4     48
    5     32
    6     19
    7      2
    Name: Radio, dtype: int64
```

Besides `loc`, pandas has `iloc` to get values using index rather than label. Similar to NumPy, pandas has **boolean indexing**.

```python
df.loc[df.Sales > 10]
>>>     TV  Radio   Newspaper   Sales
    1   17     45          69      12
    2   151    41          58      16
    3   180    10          58      17
    5   57     32          23      11
    6   120    19          11      13
```

**Sort Values** <br>
pandas lets us sort data based on one or multiple columns sequentially. 

```python
# sort by one column
df.sort_values(['Newspaper'])

# sort by more than one column
# 'Newspaper' first, then based on that, 'Sales'
df.sort_values(['Newspaper', 'Sales'])
```

**Inser a Column** <br>
We can insert a column to a DataFrame like ing an item in Python dictionary. The original DataFrame is updated. Besides the default index 'colum', we can certainly set a column to be indices. Note that setting indices does not affect the original.

```python
#  'ID' column
df['ID'] = list(range(2, 10))

# set index
df = df.set_index('ID')
df
>>>     TV  Radio   Newspaper   Sales
    ID				
    2   44     39          45      10
    3   17     45          69      12
    4   151    41          58      16
    5   180    10          58      17
    6   8      48          75      7
    7   57     32          23      11
    8   120    19          11      13
    9   8      2           1       4
```

**Concatenate Rows** <br>
If we want to combine two DataFrames with the same columns together, we use `concat([dataFrame1, dataFrame2])`. Since the original indices from each DataFrame remain unchanged, we may need to reset index and drop the old one by `reset_index(drop=True)`.

**Datetime** <br>
When data is collected, time is often inserted as strings, which makes it harder for computers to understand and analyze. Thus, it's recommended time data be converted to real datetime format. Use `to_datetime()` method.

```python
df = pd.read_csv('WeatherHistory2D.csv')

# convert string to datetime format
time_col = 'Formatted Date'
df[time_col] = pd.to_datetime(df[time_col],
                              utc=True)

# get each feature of datetime 
#  a column for each feature
df['Year'] = df[time_col].dt.year
df['Month'] = df[time_col].dt.month
df['Day'] = df[time_col].dt.day
df['Hour'] = df[time_col].dt.hour
```

**Remove a Column** <br>
In the example above, the "Formatted Date" column is no longer needed as we  separate columns for datetime features. We can just delete it using `df.drop(label, axis)`. This syntax *returns* a new DataFrame rather than changing the original. We can certainly delete *multiple* columns.

```python
df.drop(time_col, axis=1)
>>>     Temperature (C) Year    Month   Day Hour
    0      0.577778     2005       12    31   23
    1      1.161111     2006       1     1    0
```

**Group Values** <br>
We can certain group values by columns. That is, if there are duplicate rows in a column, we can combine them together and use functions to analyze each of them as a whole.

```python
df_group = pd.read_csv('weatherHistory_simple.csv')
df_group
>>>     Precip Type Temperature (C)
    0          rain            12.2
    1          rain            13.8
    2          rain            14.7
    3          rain            13.8
    4          rain            12.7
    5          rain            0.5
    6          snow            -0.4
    7          snow            -1.1
    8          snow            -1.6
    9          snow            -2.1

# group by 'Precip Type' column and compute mean of each feature by 'Temperature (C)' column
df_group.groupby('Precip Type').mean('Temperature (C)')
>>>         Temperature (C)
Precip Type	
rain              11.283333
snow              -1.300000
```

**Convert Categories to Numbers** <br>
In the example above, the "Precip Type" column can be a *class* column as in a *classification problem*. However, computers can only work with numeric values, it's better that we convert those string categories into numbers. 

```python
# test
col_to_num = 'Precip Type'
pd.Categorical(df_group[col_to_num])
>>> [0, 0, 0, 0, 0, 0, 1, 1, 1, 1]
    Categories (2, int8): [0, 1]

pd.Categorical(df_group[col_to_num]).codes
>>> array([0, 0, 0, 0, 0, 0, 1, 1, 1, 1], dtype=int8)

# convert categories to numbers
col_to_num = 'Precip Type'
df_group[col_to_num] = pd.Categorical(df_group[col_to_num]).codes
df_group
>>>     Precip Type Temperature (C)
    0             1           12.2
    1             1           13.8
    2             1           14.7
    3             1           13.8
    4             1           12.7
    5             1           0.5
    6             0           -0.4
    7             0           -1.1
    8             0           -1.6
    9             0           -2.1
```

**Descriptive Statistics** <br>
We can check out all the basic information related to a dataset by `info()`. pandas also calculates basic descriptive statistics and lets us see them via `describe()` method.

```python
df_weather.loc[:, ['Temperature (C)']].describe()
>>>         Temperature (C)
    count      96453.000000
    mean       11.932678
    std        9.551546
    min        -21.822222
    25%        4.688889
    50%        12.000000
    75%        18.838889
    max        39.905556
```

The numbers $25\%$, $50\%$, and $75\%$ are called **k-th percentiles** where $k$ is the percentage.
- $50\%$ is the median.
- $25\%$ means one fourth of the sorted dataset from minimum.
- $75\%$ means one fourth of the sorted dataset from maximum.

Using percentiles, we can indicate if the distribution of a dataset is more left-skewed or right-skewed.

:pushpin: **Pro tip:** pandas includes many other functions and methods that allows us to analyze how training models work for a dataset. This helps us know which model we should use for our datasets in certain cases. 

<details class = "bordered-block">
    <summary>
        <strong>Practice Exercises</strong>
    </summary>
    <div class = "bordered-inner-block language-python">
        <strong>Exercise 1:</strong> What is the difference between <code>df.loc[:, 'Radio']</code> and <code>df.loc[:, ['Radio']]</code> in the indexing and slicing part above?
        <br>
        <strong>Exercise 2:</strong> Write code to get the "Radio" column without using <code>loc</code>. 
        <br>
        <strong>Exercise 3:</strong> Write code to get rows 1-4 using the output of exercises 1 and 2.
        <br>
        <strong>Exercise 4:</strong> Write code to drop "Radio" and "Sales" columns in exercise 1.
        <br>
        <strong>Exercise 5:</strong> Write code to drop rows 1, 3, 6 in exercise 1 (before and after setting index).
        <br>
        <strong>Exercise 6:</strong> For examples containing 'Temperature (C)', write code to add a 'Temperature (F)' column.
        <br>
        <strong>Exercise 7:</strong> Using data in exercise 1, what is the output of <code>df.loc[3, 'Radio']</code>, <code>df.loc[3, 4]</code>, <code>df.loc[2::2]</code>, <code>df.drop('Radio')</code>, and <code>df.iloc[1:4, 1:5]</code>?
    </div>
</details>

<hr>

## **Visualization**
We can use **seaborn**, which is built on top of **matplotlib** to visualize data.

```python
# set up seaborn
import seaborn as sns
```

We'll use a famous Iris flower classification example here. 

```python
df_iris = pd.read_csv('iris.csv')

# graph two columns in one figure
sns.jointplot(df_iris, x='PetalLength', y='PetalWidth', hue='Name')
```

This kind of plot is quite beneficial for both *classification and prediction problems* when we analyze to choose the right columns to compare. 

<figure>
    <div style='display: flex; flex-wrap:wrap; column-gap: 20px; justify-content: center'>
        {% include figure.liquid loading="eager" path="assets\aio2025\M03W01\wednesday_visualization2_jointplot.png" class="img-fluid rounded z-depth-1 mx-auto d-block" zoomable=true max-width="320px" max-height="450px" alt="sepal length vs sepal width" caption="Sepal Length vs Sepal Width" %}
        {% include figure.liquid loading="eager" path="assets\aio2025\M03W01\wednesday_visualization1_jointplot.png" class="img-fluid rounded z-depth-1 mx-auto d-block" zoomable=true max-width="320px" max-height="450px" alt="petal length vs petal width" caption="Petal Length vs Petal Width" %}
    </div>
    <figcaption style="text-align: center; width: 100%; font-size:0.875em; margin-top:-25px;">
        <em>Figure 4.</em> Graphs plot three Iris flower types' features. In the second figure, Setosa is totally isolated from Versicolor and Verginica. We may use this to distinguish them.
    </figcaption>
</figure>

We can use `pairplot()` to see all the pairs.

{% include figure.liquid loading="eager" path="assets\aio2025\M03W01\wednesday_visualization5_pairplot.png" class="img-fluid rounded z-depth-1 mx-auto d-block" zoomable=true max-width="600px" max-height="600px" alt="plots for every numerical pairs" caption="<em>Figure 5.</em>Plots for every numerical pairs" %}

We can also check out the distribution of each type as follows. **Boxplot** gives the statistical structure of a feature where min, three primary percentiles, and max are shown from top to bottom by default.

```python
# dotplot 
sns.stripplot(df_iris, y='SepalLength', x='Name', hue='Name')

# boxplot
sns.boxplot(df_iris, y='SepalLength', x='Name', hue='Name', width=0.3)
```

<figure>
    <div style='display: flex; flex-wrap:wrap; column-gap: 20px; justify-content: center'>
        {% include figure.liquid loading="eager" path="assets\aio2025\M03W01\wednesday_visualization3_stripplot.png" class="img-fluid rounded z-depth-1 mx-auto d-block" zoomable=true max-width="320px" max-height="450px" alt="sepal length dotplot" caption="Sepal Length dotplot" %}
        {% include figure.liquid loading="eager" path="assets\aio2025\M03W01\wednesday_visualization4_boxplot.png" class="img-fluid rounded z-depth-1 mx-auto d-block" zoomable=true max-width="320px" max-height="450px" alt="sepal length boxplot" caption="Sepal Length boxplot" %}
    </div>
    <figcaption style="text-align: center; width: 100%; font-size:0.875em; margin-top:-25px;">
        <em>Figure 6.</em> Graphs plot three Iris flower types' features. In the second figure, Setosa is totally isolated from Versicolor and Verginica. We may use this to distinguish them.
    </figcaption>
</figure>

<details class = "bordered-block">
    <summary>
        <strong>Practice Exercises</strong>
    </summary>
    <div class = "bordered-inner-block language-python">
        <strong>Exercise 1:</strong> Write code to plot the rest for the Iris flower example give 5 columns as above.
    </div>
</details>

<hr>

## :speech_balloon: **FAQ**
Here are some good questions asked during class. The answers to these questions came from either some admin, TA, STA, or members of AIO2025.

| Questions | Answers |
|-----------|---------|
| Is there a way to interpolate for one column using other columns? | Yes. There are many ways, for example using decision tree, random forest.  |
| How do I know which method I should use to fill missing values? | We try, particularly from the baseline method, interpolation, then improve it. |
| How do I know if a dataset has noise? | Ask experts in that field. |
| After filling in missing values, data will be distorted. Is it okay? | Yes. Actually we want to distort data properly since we care more about the data from the global and long-term point of view. |
| If a feature X has 2 missing values belonging to 2 different classes, how should we go about filling in those values? | You can fill them according to values in their own class or use other features to decide. |


<br>

<!-- #### Check List

- [x] Exercise 1 (date)
- [ ] Exercise 2 (date)
  - [x] Put on left sock
  - [ ] Put on right sock
- [x] Go to school -->

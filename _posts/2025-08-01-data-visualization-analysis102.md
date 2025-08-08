---
layout: post
title: Data Visualization and Analysis for AI 102
date: 2025-08-06
description: 
tags: coding AIO 
categories: AI
giscus_comments: true                         # github comment - automatically generated - not working for now
pretty_table: true                            # add table
mermaid:
    enabled: true
    zoomable: true
# featured: true                                # pin a post
toc:                                          # table of contents
    sidebar: right
---

**Acknowledgement:** This post is based mainly on Vinh Dinh Nguyen's presentation and slides and partly on on TA, STA, and peers' responses from the course AIO2025 offered by AI VIETNAM.

**Relevance:** The audience of this lecture were those who have read [Data Visualization and Analysis for AI 101]({% post_url 2025-07-30-data-visualization-analysis101 %}), had some coding experience, and known a bit of AI knowledge. Absolute beginners are encouraged to read the material and repeatedly practice coding without AI assistance to strengthen their coding and code-reading skills. Note that only necessary pandas knowledge is introduced here.

> ______________________quote______________________ <br>
> -quoter's name

Visualizing data *properly* plays a significant role in learning how data is distributed and related before we delve into complex data analysis. In today's post, we'll explore common types of charts used in data visualization and more importantly, how to choose the right one for our dataset in general. We'll look at real-world examples and case studies to see how different chart types work in action, giving more hands-on feel for the process. We'll also discuss some applications in AI including _____________________.

<hr>

## **Data Visualization**
**Data visualization** is the process of transforming image, number, sound, or text information into visual elements like maps or graphs. In this way, we, as human users, can approach, comprehend, and identify *insights* from the information as a whole better and more easily.

If we have thousands and thousands of lines of values, it'd be extremely challenging to look at them and draw a conclusion. A chart made out of such a dataset can be much easier on the eye, not only for data experts but also regular people. For example, we wouldn't know how president candidates are doing nationwide by just looking at numbers because of how Electoral College works.

Data visualization can be used on a wide range of data and take on various forms including 2Ds and 3Ds. Good data visualization helps lay the groundwork for further analysis like data mining, which ultimately supports smarter decision-making. There are different packages that we can use to visualize a dataset. In this post, we'll focus on using three main ones:
- **matplotlib:** it is a quite complete visualization tool, offering extensive customization but requires a lot of parameters passed to a function, so users need to understand them more clearly.
```python
import matplotlib.pyplot as plt
```
- **seaborn:** it simplifies statiscal plots with built-in themes, focusing more on data itself rather than its meaning but makes it harder to customize the output.
```python
import seaborn as sns
```
- **plotly:** it provides dynamic and interactive visualization which users can engage with charts and see details without complicating charts.
```python 
import plotly.express as px
```

It takes skill and experience to create a effective visualization. At its core, it all starts with the fundamental process. The figure below displays the full data science cycle---how visualization fits into the bigger picture.

```mermaid
flowchart LR
    A((Ask a question)) ---> B((Gather the data)) ---> C((Analyze the data)) ---> D((Convey the data)) ---> E((Communicate<br/>and Visualize<br/>the results))
    E ---> D ---> C ---> B ---> A
    E ----> A
```
<figcaption style='text-align: center; width: 100%; font-size: 0.875em; margin-top:-5px; margin-bottom:15px;'>
    <em>Figure 1.</em> Data Science Process
</figcaption>

<hr>

## **Choose the Right Chart Type**
There are *five fundamental steps* to go through when it comes to choosing the right chart type. Practically, we need to modify this process to be suitable for our datasets.

### **Determine the Type of Data** 
Data can be categorized into four following types with the first three being commonly encountered.
- **Quantitative data:** numerical values.
- **Categorical data:** non-numerical values, for example, text.
- **Temporal data:** numerical and time-series values.
- **Spatial data:** location-based values.

### **Identify the Relationship between Variables**
A dataset can have hundreds of variables/properties which are stored in columns. When working with a dataset, we need to understand its properties and know which ones are valuable to problems raised. That is, we have to learn how they are linked with each other within the dataset. As such, we can narrow down the kinds of charts we should use to magnify their relationship.

There are four primary types of charts that corresponds to connection between variables.
- **Comparison chart** 
    - used for showing differences 
        - among multiple data 
        - over time (to indicate trend)
    - a bar chart, column, or line chart.
- **Distribution chart**
    - used for showing how data is dispersed
    - a histogram or box plot.
- **Relationship chart**
    - used for showing how multiple properties are related
    - a scatter plot or bubble chart.
- **Composition chart**.

### **Determine the Purpose of Visualization**
This is where asking questions also comes into play. This step can help us indicate what we really want from a dataset and what message we want to deliver through visualization. 

Eventually, we want to answer the question how and what we want to show our data visualization.
- if we want to *compare* data points, a bar or column chart may be appropriate.
- if we want to show the *distribution* of data in specific properties a histogram or box plot might be useful.
- if we want to show a *trend* over time, we can use a line or area chart.

### **Identify the Audience**
Just like public speaking, *knowing* our audiences---who we are creating charts for---is key when it comes to data visualization. The answer should guide how complex or simple our visuals need to be.
- For experts in the field, more advanced visuals like heat maps can be an adequate choice since these charts are equipped to interpret the details.
- For clients with little to none techincal background, keeping things simple like pie or bar charts is often more effective.

### **Select the Appropriate Chart Type**
There's *no* such thing as a one-size-fits-all solution to a data-related problem. Different probelms can have different visual solutions; it sometimes takes more than one chart to tell the full story clearly. 

When we're getting our feet wet, it's imperative that we experiment various chart types. Play around, compare, and see which ones best present our data. Over time, as we become more experienced with different types of data and visuals, choosing the right chart will start to feel more intuitive and much quicker.

<hr>

## **Case Study 1: [Electricity Transformer Dataset (ETD)](https://github.com/zhouhaoyi/ETDataset)**
Some abbreviations used in this dataset are in the following table.

| Field | date | HUFL | HULL | MUFL | MULL | LUFL | LULL | OT | 
|:-----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:--:|
| Description | the recorded date | High Useful Load | High Useless Load | Middle Useful Load | Middle Useless Load | Low Useful Load | Low Useless Load | Oil Temperature (target) | 

<br>

{% include figure.liquid loading="eager" path="assets\aio2025\M03W01\friday_etth_head5.png" class="img-fluid rounded z-depth-1 mx-auto d-block" zoomable=true max-width="400px" max-height="450px" alt="the first five rows of the ETD" caption="<em>Figure 1.</em>The first five rows of the ETD" %}

First off, this dataset contains *temporal data* since it is in time series format. Let's raise some relevant questions and see what charts might resolve them.

<table class = "language-python">
    <tr>
        <th>Questions</th>
        <th>Purpose</th>
        <th>Potential Charts</th>
    </tr>
    <tr>
        <td>Which <u>time</u> has the highest OT?</td>
        <td><strong>Comparison</strong> (over time)</td>
        <td>
            <ul>
                <li> Line chart </li>
                <li> Column chart </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>What is the <u>correlation</u> among the variables?</td>
        <td><strong>Relationship</strong></td>
        <td>
            <ul>
                <li> Scatter plot </li>
                <li> Bubble chart </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>What is the <u>distribution</u> of the data over time?</td>
        <td><strong>Distribution</strong></td>
        <td>
            <ul>
                <li> Line chart </li>
                <li> Histogram </li>
                <li> Scatter plot </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>What is the <u>percentage</u> of erroneous data if any?</td>
        <td><strong>Mixed / Composition</strong></td>
        <td>
            <ul>
                <li> Pie chart </li>
                <li> Stacked bar chart </li>
                <li> Area chart </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>What is the <u>distribution</u> of average loads for each load type?</td>
        <td><strong>Distribution</strong></td>
        <td>
            <ul>
                <li>  </li>
                <li>  </li>
            </ul>
        </td>
    </tr>
</table>
<br>

### **Line Chart**
A **line chart** is used to demonstrate a single or multiple variables according to another variable. It is one of the most common charts utilized in *trend analysis* and *time series analysis*.

With a large dataset, it's commonly challenging for audiences to see a specific part if creators only show an entire line chart. We can certainly make a zoom-in period on top of the main chart to highlight such an area.

~~DEMONSTRATION~~

### **Box Plot** 
A **boxplot** or **box and whisker plot** is used to portray the data *outliers* and distribution with minimum, maximum, and *quartiles* explicitly.

~~DEMONSTRATION lke~~

**Quartiles** are $25\%$, $50\%$, and $75\%$ we talked about in the previous post. We always sort the data before determining these quartiles.
- $50%$ is the median of the entire dataset, denoted **Q2**.
- $25%$ is the median of the first half, denoted **Q1**.
- $75%$ is the median of the second half, denoted **Q3**.

An **outlier** is a data point that stands out---way out---from the rest. Outliers can have a big impact on how we interpret data. If we're not careful, they can skew our results and lead us to the wrong conclusions. Take linear regression for example, a dataset with outliers can be pulled in a direction completely different from that without ones. Sometimes they are *real valuable* but can be just *noise* other times. Thus, it's important to identify outliers and delicately handle them. 

Data points that are not outliers are contained in an **acceptable range**. The formula for it is as follows.

$$Q1 - 1.5 \cdot IQR \le \text{Acceptable Range} \le Q3 + 1.5 \cdot IQR$$

where $IQR = Q3 - Q1$ is short for **interquartile range**.

This formula comes from the idea that outliers should stay outside of the range $(\mu - 3\sigma, \mu + 3\sigma)$ given that
- $(\mu - \sigma, \mu + \sigma)$ accounts for 68.27% data points.
- $(\mu - 2\sigma, \mu + 2\sigma)$ accounts for 95.45% data points.
- $(\mu - 3\sigma, \mu + 3\sigma)$ accounts for 99.73% data points.

Using these values, we can eventually have that $(\mu - 0.675\sigma, \mu + 0.675\sigma)$ accounts for IQR. If we try some numbers in the place of 1.5, we can conclude that it is actually what we want.

~~DEMONSTRATION~~
~~outliers are small hollow circles above the max or below the min.~~




#### **__________Heading 3____________**



**Concept Name** <br>



### **__________Heading 2____________**



#### **__________Heading 3____________**



**Concept Name** <br>



### **__________Heading 2____________**



#### **__________Heading 3____________**



**Concept Name** <br>

<details class = "bordered-block">
    <summary>
        <strong>Practice Exercises</strong>
    </summary>
    <div class = "bordered-inner-block language-python">
        <strong>Exercise 1:</strong> The ages for everyone in a class are 10, 9, 10, 11, 10, 12, 36, 9. Find outliers if any.
        <br>
        <strong>Exercise 2:</strong> Use the information given about area percentage in the Box Plot section to work out the conclusion about IQR and the constant 1.5.
        <br>
        <strong>Hints:</strong> ____________________________________________________________________________ 
        <br>
        <strong>Exercise 3:</strong> ____________________________________________________________________________ 
        <ul>
            <li> ______________________________________________ </li>
            <li> ______________________________________________ </li>
        </ul>
        <strong>Exercise 4:</strong> ____________________________________________________________________________ 
        <ol>
            <li> ______________________________________________ </li>
            <li> ______________________________________________ </li>
        </ol>
    </div>
</details>
<br>


<hr>

## **__________Heading 1____________**



### **__________Heading 2____________** 



#### **__________Heading 3____________**



**Concept Name** <br>



### **__________Heading 2____________**



#### **__________Heading 3____________**



**Concept Name** <br>



### **__________Heading 2____________**



#### **__________Heading 3____________**



**Concept Name** <br>

<figure>
<div style='display: flex; flex-wrap:wrap; column-gap: 20px; justify-content: center'>
    {% include figure.liquid loading="eager" path="_____" class="img-fluid rounded z-depth-1 mx-auto d-block" zoomable=true max-width="350px" max-height="450px" alt="_____" caption="_____" %} 

    {% include figure.liquid loading="eager" path="_____" class="img-fluid rounded z-depth-1 mx-auto d-block" zoomable=true max-width="350px" max-height="450px" alt="_____" caption="_____" %} 

    {% include figure.liquid loading="eager" path="_____" class="img-fluid rounded z-depth-1 mx-auto d-block" zoomable=true max-width="350px" max-height="450px" alt="_____" caption="_____" %} 
</div>
<figcaption style="text-align:center; width:100%; font-size:0.875em; margin-top:-25px;">
    Venn diagrams demonstrating a complete system and the idea of total probability 
</figcaption>
</figure>


<figure style="margin-top: 0; padding-top: 0;">
    <iframe src="https://www.geogebra.org/classic/xhdccg7y?embed" title='Interactive GeoGebra applet showing the vector projection and dot product.' frameborder='0' height="700px" width="100%" style="border: 1px solid #ddd; margin-top: 0; padding-top: 0;" allowfullscreen>Your browser does not support iframes. View the interactive applet <a href="https://www.geogebra.org/classic/xhdccg7y" target="_blank" rel="noopener">here</a>.</iframe>
    <figcaption style="font-size:0.875em"> <em>Figure 2.</em> The shaded region under the Gaussian curve represents the probability of the variable falling within that interval. You can adjust sliders to change the bounds and see how the shaded probability region updates in real time. Click on the symbol in the bottom right corner to open the applet in full-screen mode.
    If the applet does not load, you can open it directly <a href="https://www.geogebra.org/classic/xhdccg7y" target="_blank" rel="noopener">here</a>.</figcaption>
</figure>


| Header Name 1    | Header Name 2    | Header Name 3    | 
|:----------------:|:----------------:|:----------------:|
| column content 1 | column content 2 | column content 3 |
| column content 1 | column content 2 | column content 3 |
| column content 1 | column content 2 | column content 3 |
| column content 1 | column content 2 | column content 3 |
| column content 1 | column content 2 | column content 3 |
| column content 1 | column content 2 | column content 3 |
| column content 1 | column content 2 | column content 3 |
| column content 1 | column content 2 | column content 3 |
| column content 1 | column content 2 | column content 3 |
| column content 1 | column content 2 | column content 3 |
| column content 1 | column content 2 | column content 3 |
| column content 1 | column content 2 | column content 3 |
| column content 1 | column content 2 | column content 3 |
| column content 1 | column content 2 | column content 3 |
| column content 1 | column content 2 | column content 3 |
| column content 1 | column content 2 | column content 3 |
| column content 1 | column content 2 | column content 3 |
| column content 1 | column content 2 | column content 3 |
| column content 1 | column content 2 | column content 3 |
| column content 1 | column content 2 | column content 3 |
| column content 1 | column content 2 | column content 3 |
| column content 1 | column content 2 | column content 3 |

<br>




____________________________________________________________________TABLE ONLY____________________________________________________________________
<table class = "language-python">
    <tr>
        <th>Header name 1</th>
        <th>Header name 2</th>
        <th>Header name 3</th>
    </tr>
    <tr>
        <td>
            <strong>Row content 1</strong>
            <ul>
                <li> ______________________________________________ </li>
                <li> ______________________________________________ </li>
            </ul>
        </td>
        <td>
<pre>
<code class = "language-python">
# _________________explanation_________________

_________________setup_________________

# test
_________________code_________________

'''
_________________rendered output_________________
'''
</code>
</pre>
        </td>
        <td>
<pre>
<code class = "language-python">
# _________________explanation_________________

_________________setup_________________

# test
_________________code_________________

'''
_________________rendered output_________________
'''
</code>
</pre>
        </td>
    </tr>
</table>
<br>



____________________________________________________________________COLLAPSIBLE BLOCK WITH TABLE INSIDE____________________________________________________________________
<details class = "bordered-block">
    <summary>
        <strong>Practice Exercises</strong>
    </summary>
    <div class = "inside-bordered-block language-python">
        <strong>Exercise 1:</strong> _____________________________________________________
        <br>
        <strong>Exercise 2:</strong> _____________________________________________________
        <table class = "language-python">
            <tr>
                <th>Header name 1</th>
                <th>Header name 2</th>
                <th>Header name 3</th>
            </tr>
            <tr>
                <td>
                    <strong>Row content 1</strong>
                    <ul>
                        <li> ______________________________________________ </li>
                        <li> ______________________________________________ </li>
                    </ul>
                </td>
                <td>
<pre>
<code class = "language-python">
# _________________explanation_________________

_________________setup_________________

# test
_________________code_________________

'''
_________________rendered output_________________
'''
</code>
</pre>
                </td>
                <td>
<pre>
<code class = "language-python">
# _________________explanation_________________

_________________setup_________________

# test
_________________code_________________

'''
_________________rendered output_________________
'''
</code>
</pre>
                </td>
            </tr>
        </table>
        <br>
        <strong>Exercise 3:</strong> _____________________________________________________
    </div>
</details>
<br>



____________________________________________________________________COLLAPSIBLE BLOCK WITH EXERCISES ONLY____________________________________________________________________
<details class = "bordered-block">
    <summary>
        <strong>Practice Exercises</strong>
    </summary>
    <div class = "bordered-inner-block language-python">
        <strong>Exercise 1:</strong> ____________________________________________________________________________ 
        <br>
        <strong>Exercise 2:</strong> ____________________________________________________________________________ 
        <br>
        <strong>Hints:</strong> ____________________________________________________________________________ 
        <br>
        <strong>Exercise 3:</strong> ____________________________________________________________________________ 
        <ul>
            <li> ______________________________________________ </li>
            <li> ______________________________________________ </li>
        </ul>
        <strong>Exercise 4:</strong> ____________________________________________________________________________ 
        <ol>
            <li> ______________________________________________ </li>
            <li> ______________________________________________ </li>
        </ol>
    </div>
</details>
<br>



____________________________________________________________________COLLAPSIBLE BLOCK WITH EXERCISES AND CODE____________________________________________________________________
<details class = "bordered-block">
    <summary>
        <strong>Practice Exercises</strong>
    </summary>
    <div class = "bordered-inner-block language-python">
        <strong>Exercise 1:</strong> ____________________________________________________________________________ 
<pre>
<code class = "language-python">
_________________code_________________
</code>
</pre>
        <strong>Exercise 2:</strong> ____________________________________________________________________________ 
        <br>
        <strong>Exercise 3:</strong> ____________________________________________________________________________ 
        <ol>
            <li> ______________________________________________ </li>
            <li> ______________________________________________ </li>
        </ol>
        <strong>Exercise 4:</strong> ____________________________________________________________________________ 
        <ul>
            <li> ______________________________________________ </li>
            <li> ______________________________________________ </li>
        </ul>
    </div>
</details>
<br>




1. **_______main idea_________:** ______________________content - explanation_________________________
2. **_______main idea_________:** ______________________content - explanation_________________________
3. **_______main idea_________:** ______________________content - explanation_________________________
    - **_______main idea_________:** ______________________content - explanation_________________________
    - **_______main idea_________:** ______________________content - explanation_________________________
    - **_______main idea_________:** ______________________content - explanation_________________________




- **_______main idea_________:** ______________________content - explanation_________________________
- **_______main idea_________:** ______________________content - explanation_________________________
- **_______main idea_________:** ______________________content - explanation_________________________




:bulb: **Applications in AI**




:pushpin: **Pro tip:** __________________________________________________________________




:warning: __________________________________________________________________




:heavy_exclamation mark: __________________________________________________________________




:question: **__________________________________________________________________?**




```python
__________________________________________________

>>>
```




❌
✅
⚠️




<hr>

## :speech_balloon: **FAQ**
Here are some good questions asked during class. The answers to these questions came from either some admin, TA, STA, or members of AIO2025.

| Questions | Answers |
|-----------|---------|
| Question | Answer |
| Question | Answer |
| Question | Answer |
| Question | Answer |
| Question | Answer |
| Question | Answer |
| Question | Answer |
| Question | Answer |
| Question | Answer |
| Question | Answer |
| Question | Answer |


<br>

#### Check List

- [x] Exercise 1 (date)
- [ ] Exercise 2 (date)
  - [x] Put on left sock
  - [ ] Put on right sock
- [x] Go to school

---
layout: post
title: Data Visualization and Analysis for AI 103 Warm-up
date: 2025-08-08
description: KNN
tags: coding AIO basic-math
categories: AI
giscus_comments: true                         # github comment - automatically generated - not working for now
pretty_table: true                            # add table
# featured: true                                # pin a post
toc:                                          # table of contents
    sidebar: right
---

**Acknowledgement:** This post is based mainly on TA Duong Dinh Thang's presentation and slides and partly on on TA, STA, and peers' responses from the course AIO2025 offered by AI VIETNAM.

**Relevance:** The audience of this lecture were those who have read [Data Visualization and Analysis]({% post_url 2025-08-01-data-visualization-analysis102 %}), had some coding experience, and known a bit of AI knowledge. Absolute beginners are encouraged to read the material and repeatedly practice coding without AI assistance to strengthen their coding and code-reading skills. 

> ______________________quote______________________ <br>
> -quoter's name

In today's post, we'll explore KNN, . We'll also discuss some applications in AI including scaling and text classification.

<hr>

## **Machine Learning**
### **Terminology** 
**Machine Learning** (ML) is a subfield of *Artificial Intelligent (AI)* focused on the study of algorithms that can imitate how humans learn and ultilize data to generalize or predict unseen information, and thus gradually improving their performance on specific tasks without explicit programming. 

A familiar example is the classification problems we discussed in **Math for AI series**. Specifically, given a dataset with features and a class, we need to *foresee* a value of one column based on others. If a dataset is small enough, it may be possible to use multiple conditions to figure out. Nevertheless, it's hardly impossible for a large dataset with thousands and thousands lines of data. This is where ML comes into play.

In particular, we feed an ML model the dataset whose features and class values are complete and accurate. Using the given condition, the model *takes note* and *learns* to find out which function can match the input and output together. Behind the scenes, this model repeatedly tries out every possible features-class pair. Once it's done, we need to check how well the model is doing. 

The whole process includes two primary steps: 
- **training** for learning data, requiring **training data** which is the mentioned dataset.
- **testing** for checking with non-dataset input, requiring **test data**. 

The ML model after learning the entire dataset is called a **trained ML model**. With the testing phase, we can conclude how well a trained ML model works. This is known as **machine learning generalization** which refers to a train ML model's ability to perform well on unseen data of similar types. For example, a model classifying dogs and cats should not be pedantic and distinguish African dogs and Asian dogs; they are just dogs anyway. We'll talk more about this in the future.

### **Supervised Learning (SP)**

Since this example of dataset has a **class/label**, we call it a **labeled dataset**. We call the type of machine learning where we use a labeled dataset to train a ML model a **supervised learning (SL)**. This name comes from the idea that the data is set with specific class values. 

A practical example is image classification for dogs and cats. The training data includes images of dogs and cats as a feature and a label column indicates which one is a cat and which one is a dog. The goal is for computers to answer if a test input image is a dog or a cat. Of course, if an input is a picture of a human being, the model will still result in a dog or a cat. 

SL can solve various problems which can be categorized into two types: *classification problems* and *regression problems*.

**Classification Problems** <br>
The class values in classification problems are discrete (categorical). Some examples can be dog-cat classification (0 and 1) and spam detection.

In general, for classification problems, we want to find a border line that best divide a dataset into separate regions/classes.

~~DEMONSTRATION~~

**Regression Problems** <br>
The output predicted in regression problems are continuous---any numerical value falling within a certain range. Some examples can be predicting salaries and forecasting stock prices. 

For regression problems, we generally want to find a line that best fits the data distribution.

~~DEMONSTRATION~~

<hr>

## **$k$-Nearest Neighbors (KNN)**
The *core idea* of KNN comes straight from the saying, "Show me your friends and I'll tell you who you are." That is, if you know someone's circle, you'll know what that person is like. 

Formally, **KNN** is a *non-parametric* and SL algorithm which is used to make predictions based on proximity. In particular, the predicted class depends on the majority label / average value of its k-closest neighbors in the same feature space. One of the common **metrics** used to determine k-closet neighbors is **Euclidean distance**.

This algorithm can be used for both classification problems and regression problems. 

### **Procedure**
We should always preprocess the data first. Then we can apply it to a ML model in the following steps.
1. *Initialize* the value of $k$.
2. *Compute the distance* between test data and every training data (every row of the training dataset).
3. *Sort* the calculated distances in ascending order. 
4. *Get top k* elements from the sorted array.
5. *Get the most frequent class* of these elements.
6. *Return* the predicted class.

The steps from 1 through 4 are quite straightforward while performing step 5 takes a bit more effort. This happens because of their class type differences. For classification problems, class values are discrete wheareas they are continuous for regression problems. That is, we need to approach two tasks via different strategies:
- *Classification problems:* discrete class set allows us to take the *majority* label from the top k.
- *Regression problems:* continuous class set requires us to *average* the k-neighbors' values.

#### **__________Heading 3____________**



**Concept Name** <br>



### **Calculation for Classification**



#### **__________Heading 3____________**



**Concept Name** <br>



### **Calculation for REgression**


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

<!-- #### Check List

- [x] Exercise 1 (date)
- [ ] Exercise 2 (date)
  - [x] Put on left sock
  - [ ] Put on right sock
- [x] Go to school -->

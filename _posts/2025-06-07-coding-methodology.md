---
layout: post
title: Coding Methodology in Python
date: 2025-07-03
description: pep-8, clean code
tags: coding AIO format
categories: AI
giscus_comments: true                         # github comment - automatically generated - not working for now
pretty_table: true                            # add table
# featured: true                                # pin a post
toc:                                          # table of contents
    sidebar: right
---

**Acknowledgement:** This post is based mainly on Dr. Thai Ha Nguyen's presentation and slides and partly on on TA, STA, and peers' responses from the course AIO2025 offered by AI VIETNAM.

**Relevance:** The audience of this lecture were those who have learned [Python for AI 102](/_posts/2025-06-06-python102.md), had some coding experience, and known a bit of AI knowledge. Absolute beginners are encouraged to read the material and repeatedly practice coding without AI assistance to strengthen their coding and code-reading skills. 

> Be always intentional when writing and managing code. Learn logics. Don't overuse AI assistant when starting. <br>
> -Dr. Thai Ha Nguyen

In today's post, we'll explore clean code principles for Python and standard project structures. We'll mainly mention common concepts without particular examples. Details may be updated in the future. 

<hr>

**Roadmap for learning Data Science** <br>
{% include figure.liquid loading="eager" path="assets\aio2025\M01W02\saturday_roadmap_datascience.png" class="img-fluid rounded z-depth-1" zoomable=true alt="roadmap for learning data science" caption="Figure 1. Roadmap for learning Data Science" %}

Learners should follow the core process of managing a Machine Learning projects. 
1. Planning
2. Proof of Concept (PoC)
3. Implementation
4. Deployment

Learners can work on some practical projects:
1. Sales Forecasting and Demand Prediction and Applied XAI
2. Inventory Optimization Tools
3. Customer Segmentation for Marketing Strategy using Unsupervised Learning.

<hr>

## **Introduction to Clean Code and PEP-8**
Our goal of this section is to comprehend and be able to apply clean code principles and PEP-8 so that our source code is readable, efficient, and maintainable.

Writing code is like building a house. A house can still be completed by putting things together but it's likely not to last long without a blueprint. The same goes for code: without a clear architecture, solid logic, and clean design, it's prone to errors, hard to understand, and difficult to maintain. 

> Anything that can go wrong will go wrong. <br>
> Edsel Murphey's Law

### **Clean Code** 
{% include figure.liquid loading="eager" path="assets\aio2025\M01W02\saturday_clean_code.png" class="img-fluid rounded z-depth-1" zoomable=true alt="clean code principles" caption="Figure 1. Clean code principles" %}

The core principles of clean code are:
1. **Readable:** "future" we and others should easily understand its purpose and how it works.
2. **Maintainable:** code should be easy to be modifed, extended, and reused without making errors.
3. **Testable:** code should be easy to write and automate unit tests.
4. **Extensible:** code should be easy to add new features without changing existing code.

:question: You may wonder, **How important is clean code in practice?**

When working on a project with colleagues, like in a company, we must read each other's code which can be thousands of lines. This is when clean code comes in useful. Clean code is not only favored in theory but a key factor to boost work efficiency and improve team collaboration, and lower long-term maintenance cost. To be specific:
- **Minimize bugs:** clean code helps identify and prevent potential errors and lower debug and repair time.
- **Improve team work:** clean code helps team members understand and work with each other's code easily.
- **Save time lone-term:** clean code may take time and effort to build in the first place but will save time during maintenance and development. This is to avoid **technical debt**.
- **Extend easily:** clean code makes it esy to add new features without modification.

Some examples for clean code are:
- good format: space out for code to be clear
- meaningful names: variables, functions, and classes should have names meaningful to the program.

Nevertheless, there are situations where we don't have to clean code:
- **Short-live/Emergency scripts:** when the system encounters a serious accident, we need to handle the situation first, and refactor afterwards.
- **Exploratory code:** clean code is unnecessay when learning a concept. 
- **Sample code:** we can skip clean code when checking some idea in a short time and can always refactor if implementing the idea.
- **Only-current-you code:** Only current-you need it!

### **PEP-8**
PEP-8 is short for Python Enhancement Proposal 8 introduced by Guido van Rossum---Python's inventor. It is the official format for Python code, helps preserving code unity and eligibility for projects.

**Naming Convention** <br>

| Variable/Function | Class                   | Constant   | 
|:-----------------:|:-----------------------:|:----------:|
| snake_case        | PascalCase or CamelCase | UPPER_CASE |

<br>

**Indentation and Whitespace** <br>

| Indentation       | Whitespace                                                              |
|-------------------|-------------------------------------------------------------------------|
| four white spaces | add whitespaces next to operations <br> `a = b + c`  instead of `a=b+c` |
|                   | no whitespace before a comma <br> `f(a, b)` instead of `f(a , b)`       |
|                   | no whitespaces before and after parentheses, brackets, or braces <br> `list([1, 2, 3])` instead of `list( [ 1, 2, 3 ] )`|

<br>

**Standard Code Line** <br>

| Length of a Line | Line Break for Continuation |
|------------------|-----------------------------|
| Source code: 79 characters | Explicit: backslash `\` |
| Docstring/Comment: 72 characters | Implicit: parentheses `()`, brackets `[]`, braces `{}` |
| Purpose: <br> - Easier to scroll up/down than left/right <br> - Easy to read on all screens | Before a comma or operator |

<br>

**Standard Import** <br>
We should import libraries and modules in different blocks based on their origin. Commonly, there are three blocks in the following order:
1. Python libraries: `os`, `sys`, `math`
2. Third-party packages: `requests`, `numpy`, `pandas`
3. Internal modules: `from myproject.models import User`.

**Line Break and Class/Function Structure** <br>

<table class = "language-python">
    <tr>
        <th></th>
        <th>Function</th>
        <th>Class</th>
    </tr>
    <tr>
        <td>Structure</td>
        <td>
            <ol>
                <li> docstring </li>
                <li> input validation </li>
                <li> main code </li>
                <li> return </li>
            </ol>
        </td>
        <td>
            <ol>
                <li> docstring </li>
                <li> variables </li>
                <li> __init__() </li>
                <li> other methods </li>
                <li> private methods </li>
                <li> static methods </li>
            </ol>
        </td>
    </tr>
    <tr>
        <td>Usage</td>
        <td>
            <ul>
                <li> Use two linebreaks to separate classes. </li>
                <li> Use one linebreak between functions inside a class. </li>
            </ul>
        </td>
        <td>
            <ul>
                <li> Each function should only have one purpose. </li>
                <li> Use whitespaces to separate logic blocks. </li>
                <li> Don't overuse whitespaces which can lower readability. </li>
            </ul>
        </td>
    </tr>
</table>
<br>

**Documentation: Docstring and Annotation Basics** <br>

<table class = "language-python">
    <tr>
        <th>Docstring</th>
        <th><a href="https://docs.python.org/3/library/typing.html">Annotations and Type Hints</a></th>
        <th>Documentation for Projects</th>
    </tr>
    <tr>
        <td>
            Docstring is surrounded by <code>'''</code> or <code>"""</code>. Some styles to follow:
            <ul>
                <li> Google
                    <ul> 
                        <li> Easy to read </li>
                        <li> Widely used </li>
                        <li> Clear structure with <code>Arg</code>, <code>Return</code>, and <code>Raise</code> </li>
                    </ul>
                </li>
                <li> Numpy 
                    <ul> 
                        <li> More detailed </li>
                        <li> Ideal for data science functions </li>
                    </ul>
                </li>
                <li> reStructuredText 
                    <ul> 
                        <li> Combined with <strong>Sphinx</strong> </li>
                        <li> Create web documentation </li>
                    </ul>
                </li>
            </ul>
        </td>
        <td>
            A annotation is an optional support to check data types and specify purposes. They are called type hints.
            <ul>
                <li> Basic data types: <code>def(a: int, b: float)</code> instead of <code>def(a, b)</code>. </li>
                <li> Advanced data types: need <code>from typing import List, Dict, Tuple, Optional</code> before using them. </li>
                <li> Union data types:  </li>
                <li> <code>-> return_type</code>: to specify return type. </li>
            </ul>
        </td>
        <td>
            <ul>
                <li> Module docstring: is on top of a file and describes main functions and purposes. </li>
                <li> <code>README.md</code>: contains installation instruction, sample examples, and project structure. </li>
                <li> <code>CONTRIBUTING.md</code>: contains code rules and contribution procedure. </li>
                <li> <strong>Sphinx</strong>: automatically creates <strong>API</strong> from docstring. </li>
                <!-- <li> <strong>Wiki</strong>: provides details for complicated features. </li> -->
            </ul>
        </td>
    </tr>
</table>
<br>

### **Checking Tools**
flake8: check for redundancy
black . : format all
black file_name: format file_name
pyplint: analyze more than black and grade our code
mypy: check error

### **Standard Structure for Projects**
Similar to writing Python code, it's essential to organize a Python project in order to build a healthy development cycle. There may be a few ways to construct a standard repository structure. Below is one of them. Using files described in the root directory ensures a project is efficiently managed and straightforward for contributors and readers.
1. Root directory `project_name/`
    - README.md: outlines a project's goal, setup instructions, usage examples, and contributions
    - requirements.txt: lists project dependencies
    - setup.py: defines and installs packages
    - pyproject.toml (preferred): specifies build íntructions, project dependencies, and project metadata (license, author, descriptions, etc)
    - .gitignore: contains files and folders Git should ignore/track such as temporary files, log files, or personalfiles.
2. Source code `project_name/src/`
    - Main modules
    - Main packages
3. Tests `project_name/tests/`
    - unittest
    - pytest
4. Documentation `project_name/docs`
    - API
    - Usage
5. Resources `project_name/resources/`
    - Static resources
    - Templates
    - Assets

It's adequate and fast to build our repository structure using **Command-Line Interface generator (CLIgen)** such as [Cookiecutter Data Science](https://cookiecutter-data-science.drivendata.org/).

<hr>

## **Pythonic Style**
Our goal of this section is to familiarize ourselves with standard Python programming and utilize its unique features efficiently.

There are 19 guiding principles for Python written by Tim Peters in [PEP 20](https://peps.python.org/pep-0020/). You can check them out with `import this`. 

We apply Pythonic style to utilize unique features and characteristics of Python. It not only preserves clean code and PEP-8 but adheres to Python's philosophy. Let's take a look at some Pythonic cases.

1. Use list, dict, and set comprehensions to create a sequence.
    - All on one line makes it faster to create.
    - It's very readable one you're familiar with the syntax.
```python
dict_comprehension = {i: i * i for i in range(7)}
```
2. Context manager `with` statement to open and close a file automatically.
    - `with` prevents memory leak, releases resources correctly, and is safer for exception handling. 
    - It's commonly used for file management, network database, lock thread, benchmark, transaction database, and so on.
```python
with open("file_name.txt", "r") as file:
    content = file.read()
```
3. `@contextmanager` is a decorator.
    - `@contextmanager` comes from `contextlib`.
    - It temporarily changes the system configuration and recovers once done.
    - It measures operation time.
    - It manages network database, Redis, or API.
    - It creates a temporaty environment for testing.
```python
from contextlib import contextmanager
@contextmanager
def file_reader(filename):
    f = open(filename, "r")
    try:
        # perform with statement
        yield f
    finally:
        # clean up everything and close the file
        f.close()
# use context manager
with file_reader("file_name.txt") as file:
    print(file.read())
```
4. `@property` is a decorator, making a method become an attribute.
    - No need parentheses `()` in the end if there is no argument. 
5. Comparison and condition: 
<table class = "language-python">
    <tr>
        <th>Technique</th>
        <th>Pythonic</th>
        <th>Non-Pythonic</th>
    </tr>
    <tr>
        <td><code>is None</code></td>
        <td>
        Check an object's identity: <code>w</code> is not the <code>None</code> object.
<pre>
<code class = "highlight">
class Weird:
    def __eq__(self, other):
        # it equals anything
        return True

w = weird()
print(w is None)

'''
False   
'''
</code>
</pre>
        </td>
        <td>
        Check an object's value: <code>w</code> has value of <code>None</code>.
<pre>
<code class = "language-python">
class Weird:
    def __eq__(self, other):
        # it equals anything
        return True

w = weird()
print(w == None)

'''
True
'''
</code>
</pre>
        </td>
    </tr>
    <tr>
        <td>Boolean</td>
        <td>
        Utilize truthfulness.
<pre>
<code class = "highlight">
valid = True
if valid:
    print("True")
</code>
</pre>
        </td>
        <td>
        Too lengthy.
<pre>
<code class = "language-python">
valid = True
if valid == True:
    print("True")
</code>
</pre>
        </td>
    </tr>
    <tr>
        <td>Emptiness:
        <ul>
            <li> strings </li>
            <li> lists </li>
            <li> dicts </li>
            <li> sets </li>
        </ul>
        </td>
        <td>
        Utilize truthfulness.
<pre>
<code class = "highlight">
items = []
if not items:
    print("Empty")
</code>
</pre>
        </td>
        <td>
        Too lengthy.
<pre>
<code class = "language-python">
items = []
if len(items) == 0:
    print("Empty")
</code>
</pre>
        </td>
    </tr>
    <tr>
        <td><code>in</code></td>
        <td>
        Check existence directly.
<pre>
<code class = "highlight">
a_list = [1, 2, 3]
item = 4
if item in a_list:
    print(f'{item} is in a_list')
</code>
</pre>
        </td>
        <td>
        Too complicated and time-consuming.
<pre>
<code class = "language-python">
a_list = [1, 2, 3]
item = 4
for i in a_list:
    if i == item:
        print(f'{item} is in a_list')
        break
</code>
</pre>
        </td>
    </tr>
    <tr>
        <td>Chain comparison</td>
        <td>
        Logical.
<pre>
<code class = "highlight">
value = 7
if 0 < value < 8:
    print(f'{value} is in range')
</code>
</pre>
        </td>
        <td>
        Too lengthy.
<pre>
<code class = "language-python">
value = 7
if value > 0 and value < 8:
    print(f'{value} is in range')
</code>
</pre>
        </td>
    </tr>
</table>

<hr>

## **Principles for Writing Neat Code**
Our goal of this section is to understand various rules and designs to build high-quality code.
<table class = "language-python">
    <tr>
        <th>Principle</th>
        <th>Benifits</th>
        <th>Usage</th>
    </tr>
    <tr>
        <td><strong>DRY (Don't Repeat Yourself)</strong></td>
        <td>
            <ul>
                <li> Concise, reusable, and maintainable code. </li>
                <li> Less errors when changing logic. </li>
            </ul>
        </td>
        <td>
            <ul>
                <li> Concepts should be defined in functions, classes, or modules. </li>
                <li> Each concept should appear only once. </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><strong>YAGNI (You Aren't Gonna Need It)</strong>  </td>
        <td>
            <ul>
                <li> Avoid wasting time complicate the unnecessary. </li>
                <li> Reduce technical debt. </li>
                <li> Concise and maintainable. </li>
            </ul>
        </td>
        <td>
            <ul>
                <li> Only add on a feature when truly needed. </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><strong>KISS (Keep It Simple, Stupid)</strong></td>
        <td>
            <ul>
                <li> Concise, debuggable, maintainable, and extensible code. </li>
                <li> Less bugs and higher efficiency. </li>
            </ul>
        </td>
        <td>
            <ul>
                <li> Always prioritize simple solutions. </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><strong>Defensive Programming</strong></td>
        <td>
            <ul>
                <li> Debuggable, robust, and sustainable code. </li>
            </ul>
        </td>
        <td>
            <ul>
                <li> Always anticipate unexpected inputs and potential errors. </li>
                <li> Always check them. </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><strong>Error Handling</strong></td>
        <td>
            <ul>
                <li> Catch specific bugs and deliver error messages properly. </li>
            </ul>
        </td>
        <td>
            <ul>
                <li> <code>assert</code>, <code>logging</code>, and <code>try-except</code>. </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><strong>Separation of Concerns</strong></td>
        <td>
            <ul>
                <li> Maintainable, Reusable, and Testable. </li>
            </ul>
        </td>
        <td>
            <ul>
                <li> Each function, class, and module is responsible for one specific task. </li>
            </ul>
        </td>
    </tr>
</table>
<br>

As mentioned `logging` can be used to catch bugs in the program. The purposes of using `logging` and `print` may be mistaken for each other. `logging` is a feature to journal code professionally with different levels while `print` is to catch errors quickly but have its own drawbacks.

| Print                  | Logging                                      | 
|------------------------|----------------------------------------------|
| Easy to use            | Flexible configuration                       |
| No classified levels   | Classified levels: DEBUG, INFO, WARNING, etc |
| Hard to switch off     | Configurable on/off switch                   |
| No add-ons             | Add-ons: time, file, line                    |
| Hard output management | Direct to file, email, etc                   |

<hr>

## **SOLID Rule and Design Patterns (Advanced)** - to be updated
Our goal of this section is to learn how to organize projects, divide into modules, and write highly extensible code.


**Single Responsibility** <br>


**Open/Closed** <br>
<!-- This principle means open for adding new features and closed for changing existing features.  -->


**Liskov Substitution** <br>



**Interface Segregation** <br>



**Dependency Inversion** <br>


<!-- ask about settings.json file to configure flake8 ...

ask about slide with answer key -->4



:pushpin: **Pro tip:** Use AI to create problems, with hint docstrings, and test cases. Export it to colab files and start practicing. Once you've done, ask AI to analyze your solutions and provide answer keys and learned lessons. You can use lecture slides as an attachment to your question. 

A sample prompt: "Create twenty Python programming problems from easy to diffcult. They should adhere to the lesson content in slides attached. They should have hint docstrings and test cases for each problem and learners need to complete them. After that, provide solutions separately and give lessons learned from each problem."

<https://colab.research.google.com/drive/1hwdu33Mo1wxoOcNWV80qSy2YWVodtyeL?usp=sharing>

<hr>

## :speech_balloon: **FAQ**
Here are some good questions asked during class. The answers to these questions came from either some admin, TA, STA, or members of AIO2025.

| Questions | Answers |
|-----------|---------|
| Resources | [Mathematics for Machine Learning](https://course.ccs.neu.edu/ds4420sp20/readings/mml-book.pdf), [Pattern Recognition and Machine Learning](https://www.microsoft.com/en-us/research/wp-content/uploads/2006/01/Bishop-Pattern-Recognition-and-Machine-Learning-2006.pdf), and <https://colab.research.google.com/drive/14H2oCxe06k28z30SKhdXMGxvtNneXGhs?usp=drive_link#scrollTo=QaAlW_n1Qirb> |
| What is CI/CD? | CI/CD is short for Continuous Integration and Continuous Delivery/Deployment, respectively. This is a DepOvs method to automate and speed up software development. |
| What is Cloud Computing? | Cloud Computing is the delivery of computing services including serves, storage, databases, networking over the Internet. |
| What is Explainable AI? | The process is input -> complex AI model -> explaining the model and its results -> users understand the decision -> output. Check out [XAI Overview](https://blog.vinbigdata.org/khai-quat-ve-explainable-ai/). |
| What is a data engineer, data analyst, and data scientist? | DE manages data, DA retrieves basic information using statistic models, and DS uses ML/DL to investigate larger datasets. |
| What does refactor mean? | Refactoring code is the process of changing structure of source code without changing the program's primary behavior. |
| What do I use requirement.txt for? | You can remove or update a library by just updating this file and pushing to the repository. |
| Resources for more complex Pythonic techniques like tensor/dataframe/array | You can utilize vectorized operations of libraries. Documentation can be found at[here](https://docs.pytorch.org/tensordict/main/tutorials/tensordict_slicing.html). |
| What are Redis and API? | Redis is cache database, supporting quick computations when needed but storing them is inconvenient. API (Application Programming Interface) is a network/collection of rules, methods, and data formats a software or service provides so that other programs can call and interact with. |
| How do I check all code before pushing to github? | `pre commit git hook` |



<!-- Try Except để bắt lỗi thôi bạn, Ví dụ như các lỗi ở slide M01W01 - Self-study.  thì mình sẽ try except lỗi đó, để ứng dụng ko bị crash. If-else để xử lý condition thôi nè. Sử dụng try-except khi bạn dự đoán một đoạn code có thể có lỗi do một điều kiện ngoại lệ không mong muốn, và bạn muốn bắt và xử lý điều đó. Ví dụ bạn a/b b có thể = 0 vậy thì bạn sẽ catch lỗi này và đưa ra một xử lý phù hợp đê chương trình không bị dừng đột ngột, hoặc một số ngoại lệ, lỗi mà bạn không biết trước. Sử dụng if-else khi bạn cần kiểm tra một điều kiện đã biết và quyết định luồng chương trình dựa trên kết quả kiểm tra đó. -->

<!-- nhưng ví dụ như cái hàm a/b mình cũng có thể đưa ra if b=0 thì xử lý sao phải k ạ - đúng rồi một số trường hợp có thể thay thế cho nhau, một số thì không ví dụ catch những lỗi mình chưa biết. nếu dung if thì bạn phải liệt kê ra tất cả trường hợp có thể xảy ra (mà cái này gần như bất khả thi do có nhiều lỗi mình kh lường trước được). Nên phải dung try except để bắt hết tất cả những lỗi xảy ra với đoạn code đó mà kh làm gián đoạn chương trình -->

<br>

<!-- #### Check List

- [x] Exercise 1 (date)
- [ ] Exercise 2 (date)
  - [x] Put on left sock
  - [ ] Put on right sock
- [x] Go to school -->

---
layout: post
title: Coding Methodology in Python
date: 2025-07-03
description: clean code principles
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

In today's post, we'll explore clean code principles for Python and standard project structures. We'll also discuss some applications in AI including _____________________.

<hr>

**Roadmap for learning Data Science** <br>
{% include figure.liquid loading="eager" path="assets\aio2025\M01W02\saturday_roadmap_datascience.png" class="img-fluid rounded z-depth-1" alt="roadmap for learning data science" caption="Figure 1. Roadmap for learning Data Science" %}

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

### **Clean Code** 
{% include figure.liquid loading="eager" path="assets\aio2025\M01W02\saturday_clean_code.png" class="img-fluid rounded z-depth-1" alt="clean code principles" caption="Figure 1. Clean code principles" %}

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
- **Only-current-you code:** Only current you!

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

cái này là cli gen project phải ko ad? - https://cookiecutter-data-science.drivendata.org/

#### **__________Heading 3____________**



**Concept Name** <br>




<hr>

## **Pythonic Style**
Our goal of this section is to familiarize ourselves with standard Python programming and utilize its unique features efficiently.

There are 19 guiding principles for Python written by Tim Peters in [PEP 20](https://peps.python.org/pep-0020/). You can check them out with `import this`. 

We apply Pythonic style to utilize unique features and characteristics of Python. It not only preserves clean code and PEP-8 but adheres to Python's philosophy. Let's take a look at some Pythonic cases.

1. Use List, dict, and set comprehension to create a sequence.
    - 
    - 
2. Context manager `with` helps close files once its task is done.
    - 
    - 
3. Comparison and condition: 
    - == None is not incorrect but it ghi de -> can give wrong answer
    - 
4. @ is decorator -> makes method become attribute

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

## **Principles for Writing Neat Code**
Our goal of this section is to understand various rules and designs to build high-quality code.



**DRY (Don't Repeat Yourself)** <br>
Each concept should be defined only once. 


**YAGNI (You Aren't Gonna Need It)** <br>
Only add on features when truly needed. Don't complicate the unnecessary.

overpacking when going on vacation - should check weather

**KISS (Keep It Simple, Stupid)** <br>
Always prioritize simple solutions, 


**Defensive Programming** <br>
Always be prepared for unexpected inputs and potential errors.


**Error Handling** <br>
Catch specific errors instead of general ones.


**Separation of Concerns** <br>
Each component/module is responsible for their own part in the system.

logging replaces print:
- classify levels
- configure logging

<hr>

## **SOLID Rule and Design Patterns (Advanced)**
Our goal of this section is to learn how to organize projects, divide into modules, and write highly extensible code.


### **__________Heading 2____________** 



#### **__________Heading 3____________**



**Single Responsibility** <br>


**Open/Closed** <br>
This principle means open for adding new features and closed for changing existing features. 


**Liskov Substitution** <br>



**Interface Segregation** <br>



**Dependency Inversion** <br>


ask about settings.json file to configure flake8 ...

pre commit git hook 

make file

ask about slide with answer key
### **__________Heading 2____________**



#### **__________Heading 3____________**



**Concept Name** <br>



### **__________Heading 2____________**



#### **__________Heading 3____________**



**Concept Name** <br>




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
| Resources | [Mathematics for Machine Learning](https://course.ccs.neu.edu/ds4420sp20/readings/mml-book.pdf) and [Pattern Recognition and Machine Learning](https://www.microsoft.com/en-us/research/wp-content/uploads/2006/01/Bishop-Pattern-Recognition-and-Machine-Learning-2006.pdf) |
| What is CI/CD? | CI/CD is short for Continuous Integration and Continuous Delivery/Deployment, respectively. This is a DepOvs method to automate and speed up software development. |
| What is Cloud Computing? | Cloud Computing is the delivery of computing services including serves, storage, databases, networking over the Internet. |
| What is Explainable AI? | The process is input -> complex AI model -> explaining the model and its results -> users understand the decision -> output. Check out [XAI Overview](https://blog.vinbigdata.org/khai-quat-ve-explainable-ai/). |
| What is a data engineer, data analyst, and data scientist? | DE manages data, DA retrieves basic information using statistic models, and DS uses ML/DL to investigate larger datasets. |
| What does refactor mean? | Refactoring code is the process of changing structure of source code without changing the program's primary behavior. |
| Question | Answer |
| Question | Answer |
| Question | Answer |
| Question | Answer |
| Question | Answer |


Dùng AI tạo bài tập + tạo test cases, để các TODO lại cho mình làm để học hỏi. Sau khi viết xong bảo AI phân tích lời giải của mình và trình bày đáp án, lesson học được. Các bạn có thể bảo Gemini/ChatGPT tạo bài tập từ bài học slide trên lớp rồi export ra Colab và luyện tập, ví dụ như file dưới đây: https://colab.research.google.com/drive/1hwdu33Mo1wxoOcNWV80qSy2YWVodtyeL?usp=sharing. Prompt cho Gemini (bạn nhớ đính kèm file slide bài học trên lớp):
Hãy tạo 20 bài tập lập trình Python có độ khó tăng dần từ dễ đến rất khó, có tính sư phạm cao minh hoạ sát nội dung của bài học trong tài liệu đính kèm. Bạn hãy viết chương trình Python có sẵn test case cho từng bài, và người học sẽ phải lập trình các đoạn TODO. Tách riêng phần đề bài và phần đáp án. Nêu bài học rút ra ứng với từng bài tập.


Có thấy dùng requierement khi nào ạ - thường dùng để cài đặt dependency, cho project á bạn. requirements.txt dùng để liệt kê và cố định phiên bản các thư viện Python mà dự án cần, giúp bạn và đồng đội (hay hệ thống CI/CD, server deploy) dễ dàng tái tạo môi trường đúng như đã test bằng lệnh pip install -r requirements.txt. Khi thêm, loại bỏ hoặc nâng cấp thư viện, bạn chỉ cần cập nhật file này, sau đó chia sẻ trong repo để mọi nơi cài đặt đồng nhất

models vs models trong src khác gì nhau ạ - Cái models ngoài, là để chứa các trained models. Còn cái models trong src, là chứa mã nguồn để viết các hàm train lên model

cho em hỏi những kỹ thuật pythonic trong các dạng data phức tạp hơn, như tensor/dataframe/array thì có thể đọc thêm ở đâu ạ - Thường thì theo mình thấy ở các kiể như tensor thì tránh dùng vòng lặp for của Python và tận dụng các hàm được tối ưu hóa vectorized operations của thư viện. Mỗi thư viện họ sẽ có document riêng hướng dẫn ví dụ của Pytorh: https://docs.pytorch.org/tensordict/main/tutorials/tensordict_slicing.html


redis va APIs la gi a? Redis là database dạng cache, giúp truy vấn tính toán nhanh khi cần, nhưng ko tiện để lưu trữ Còn api thì hiểu nôm na là cái kết nối mọi thứ ko cùng chung 1 nền tảng lại với nhau. Redis là một hệ quản trị cơ sở dữ liệu dạng key–value. API Application Programming Interface là giao diện lập trình ứng dụng, tập hợp các quy tắc, phương thức và định dạng dữ liệu mà một phần mềm (hoặc service) cung cấp để các chương trình khác gọi vào và tương tác

Anything that can go wrong will go wrong - https://en.wikipedia.org/wiki/Murphy%27s_law

Try Except để bắt lỗi thôi bạn, Ví dụ như các lỗi ở slide M01W01 - Self-study.  thì mình sẽ try except lỗi đó, để ứng dụng ko bị crash. If-else để xử lý condition thôi nè. Sử dụng try-except khi bạn dự đoán một đoạn code có thể có lỗi do một điều kiện ngoại lệ không mong muốn, và bạn muốn bắt và xử lý điều đó. Ví dụ bạn a/b b có thể = 0 vậy thì bạn sẽ catch lỗi này và đưa ra một xử lý phù hợp đê chương trình không bị dừng đột ngột, hoặc một số ngoại lệ, lỗi mà bạn không biết trước. Sử dụng if-else khi bạn cần kiểm tra một điều kiện đã biết và quyết định luồng chương trình dựa trên kết quả kiểm tra đó.

nhưng ví dụ như cái hàm a/b mình cũng có thể đưa ra if b=0 thì xử lý sao phải k ạ - đúng rồi một số trường hợp có thể thay thế cho nhau, một số thì không ví dụ catch những lỗi mình chưa biết. nếu dung if thì bạn phải liệt kê ra tất cả trường hợp có thể xảy ra (mà cái này gần như bất khả thi do có nhiều lỗi mình kh lường trước được). Nên phải dung try except để bắt hết tất cả những lỗi xảy ra với đoạn code đó mà kh làm gián đoạn chương trình

<br>
<!-- 
#### Check List

- [x] Exercise 1 (date)
- [ ] Exercise 2 (date)
  - [x] Put on left sock
  - [ ] Put on right sock
- [x] Go to school -->

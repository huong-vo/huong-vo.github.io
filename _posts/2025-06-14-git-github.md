---
layout: post
title: Git & GitHub for Version Control
date: 2025-07-14
description: git, github
tags: coding AIO
categories: AI
giscus_comments: true                         # github comment - automatically generated - not working for now
pretty_table: true                            # add table
# featured: true                                # pin a post
toc:                                          # table of contents
    sidebar: right
---

**Acknowledgement:** This post is based mainly on Dr. Thai-Ha Nguyen's presentation and slides and partly on on TA, STA, and peers' responses from the course AIO2025 offered by AI VIETNAM.

**Relevance:** The audience of this lecture were those who have had some coding experience. Absolute beginners are encouraged to read the material and repeatedly practice coding without AI assistance to strengthen their coding and code-reading skills. Note that only necessary Python knowledge is introduced here.

**Relevance:** The audience of this lecture were those who could have known nothing about database or have had some experience working with data. Absolute beginners are encouraged to read and practice the basics without AI assistance to familiarize themselves with the material. Note that only necessary SQL knowledge is introduced here.

> Always understand the principles first then practice. <br>
> -Dr. Thai-Ha Nguyen

In today's post, we'll explore Git and GitHub. They are essential tools any developer or engineer should be familiar with. We can use them for personal and collaborative purposes.

Let's implant some analogies of Git and GitHub in mind before delving into both. Git is like a camera capturing snapshots of a project continuously. GitHub is like Google Photos storing all photos from Git to cloud so that we can review and share with anyone at any point in time.

<hr>

## **Git Principles and Configuration**

### **Version Control System (VCS)** 
VCS is a general term for Git. VCS is a system that tracks and saves changes of files over time. It contains all information about 
- what has been changed
- who has changed it
- when it was changed
- why it was changed. 

With these properties, this system enables us to 
- revert to previous working state when bugs/errors/mistakes have been made
- compare the difference between two versions
- show related change information 
- protect data and support collaboration.

There are three types of VCS:
1. **Local VCS** is the very first VCS for one-person use. That is, everything is saved locally in a computer, so there is no way to recover if the computer quits working and it's difficult to share your work with others. 

2. **Centralized VCS (CVCS)**, for example Subversion and CVS, is another old VCS where developers use one single server to store their work. Even though it facilitates seamless collaboration, it totally depends on the centralized server. This would be catastrophic if the server corrupted. Users wouldn't be able to save versioned changes or collaborate with others.

3. **Distributed VCS (DVCS)**, for example Git and Mercurial, is the currently-used VCS where each developer has their own server. That is, every user has a local copy of complete projects and history at all times. If their server is inaccessible, they can always create a new one and share their work with others. Thus, it is complete, secure, and flexible.

### **Git**
Git is a DVCS created by Linus Torvalds in 2005, who is the father of Linux. He designed Git to manage Linux source code since Linux is developed by thousands of people from all over the place. Git is widely adopted just a short while after its creation as it is simple, lightweight, instantaneous, and easy to branch and distribute.

**SSO Principles** <br>
1. **Snapshot** instead of diff
    - Git snaps an entire project after each change (when committing) to capture all changes at once.
    - If there's no change, Git creates a link to the old version to save storage capacity.

2. **SHA-1 Data Integrity**
    - Git protects data by the SHA-1 function with unique identifiers---40-character hash codes like ID (for each commit).
    - when content alters, so does its hash code, which ensures commit integrity.

3. **Offline-first**
    - Git allows us to work and save your progress offline (commit). 
    - We only need the Internet when pull/push.

**Configuration** <br>
After installation, some basic configurations can be done for Git are
- git config --global user.name your_name: 
- git config --global user.email your_email
- git config --global core.editor "code-wait"
- git config --global color.ui auto

They are all automatically imported into a file on our computer. We can use git config --list to see them.

An alias for a command statement is very useful while we work with Git. It is to replace a long word/phrase with a short user-defined name. 

git log shows history of your work which may be prolix. We can customize the output so that it is clear, concise, and pretty.

These enables us to work faster and more efficiently.

git --init


<hr>

## **Basic Git**
A repository acts like a folder and journal.


### **Repository** 
locally
mkdir repo_name

cd repo_name

git init initiates a hidden file named .git

ls -la list all files including hidden files

clone from GitHub-the server
.gitignore contained files that we don't want to publish online

license: how to cite

click and press . to open file on github -> git dev

echo "message" >> README.md -> create readme
git branch -M main 

clone
ssh -> more secure
git clone "https://..."
git clone ssh_code


echo "message" >> sample.txt -> create a file
echo "another message" >> sample.txt -> add more message

primary process to work with git

git status
git add file_name
git add .
git commit -m "message"
git push -u origin main

git log -> too long what if there are thousands of lines
git log --oneline -> don't know who changed what
git lg (customized)


xem lich su commit: top line is main branch, bottom line is other branch


commit should have meanings - like photo should show when and where



git len extension: visualize commit

tagging -> milestone

lightweight tag -> in project, baseline or xgb 

#### **__________Heading 3____________**

branch: 
if all A B C commit to main -> unorganized and hard to managed -> not commit to main -> instead commit to a branch
for each feature developed
main should always be ready to deploy (deployable)

git branch -M main -> see all branches
git branch branch_name -> create a branch (ex, feature/login)
git checkout branch_name -> go to that branch -> all commits after go to this branch
git checkout -b branch_name -> create and go to that branch



merge all branches to main -> 2 ways
1. used less
git checkout main
git merge branch_name
2. more common
git push -u origin branch_name
on github:
compare and pull request
create pull request -> send request to all teams so reviewer can check if code is good to go
reviewer:
once good -> merge pull request -> confirm merge 

file conflict: -> in exercise
A and B change the same file but B does better -> choose B remove A -> solve conflict by ?

once a project is done, all branches are merged to main -> should erase all branches to eliminate redundancy 

rebase: more linear
merge: parallel

**Concept Name** <br>
command to link local repo to remote repo -> git remote add origin url
command to get info of all branches from remote repo to local without combining -> git fetch origin
process to create and push code to remote
git init -> git add . -> git commit -m message -> git remote add origin url -> git push origin main or
git init -> git remote add origin url -> git add . -> git commit -m message -> git push origin main
a file created in branch main, not added to staged, not committed yet -> what happens when moving to a different branch? file on new branch but not ffollowed in video exercise

### **__________Heading 2____________**



#### **__________Heading 3____________**



**Concept Name** <br>



### **__________Heading 2____________**



#### **__________Heading 3____________**



**Concept Name** <br>




<hr>

## **Intermediate Git**



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

## **Collaborate via GitHub**



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

## **Advanced Git**



### **__________Heading 2____________** 



#### **__________Heading 3____________**



**Concept Name** <br>



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

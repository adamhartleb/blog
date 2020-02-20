+++
title = "Machine Learning Intro"
description = "My notes on machine learning"
date = 2020-02-20
author = "Adam Hartleb"
+++

# Introduction

One of the earliest examples of machine learning we have took place in the 1950s when Arthur Samuel was working for IBM (he also popularized the term "Machine Learning"). He was tasked with ensuring the transistors for the large computers functioned correctly when they ran a program. To do so, he created a program that played Checkers. However, instead of programming it to just _play_ Checkers (i.e. making arbitrary moves that follow the rules), he programmed it to _learn how to play_ Checkers.

[Samuel's Checkers Player](http://www.incompleteideas.net/book/ebook/node109.html)

Machine learning can be broadly categorized into three disciplines: **supervised learning**, **unsupervised learning** and **reinforcement learning**. Supervised learning is task-driven: we feed a computer a couple of known tasks and their known outcomes. Afterward, we feed it new data and allow its algorithm to predict the outcome and provide feedback on its performance so it can adjust. Unsupervised learning is the opposite. We feed the computer unlabeled data with no known outcomes and ask it to find the underlying structure in the data using pattern recognition. Now, what if we are provided no data at all but rather just a goal to strive for? This is reinforcement learning which takes a trial and error approach by sampling actions and then observing which one leads to the desired outcome. How is this different from supervised learning though? Firstly, we might not have a known data set to compare the actions to. Secondly, such a data set might be unfeasible to use (e.g. every possible decision tree for a Chess game). Finally, we're not telling the computer what to do which may cause it to imitate a human rather than actually learning the best possible strategy.

In this series of posts, I'll be focusing on supervised learning which is learning from examples. I'll need to get some terminology out of the way first.

### Features

If we have a dataset of medical records and organize that into a table, the rows would each contain the record of a particular patient while the columns would contain the value of each attribute (e.g. height, weight, age, etc) for the patients as a whole. In machine learning parlance, we call the rows our **examples** and the columns the **features**. Feature values (a cell in a table) can either be discrete values (like male or female) or they can be continuous numerical values (like a patient's weight or height).

Now given this dataset, a doctor might use it to assess if a patient will develop heart disease in the future. In order to do that though, they would need additional information, that is, _did_ these patients develop heart disease? Remember, supervised learning requires labeled data with a known outcome in order to reach a conclusion. When picking a concrete target such as _{sick, healthy}_ as the outcome, we call the process of learning the outcome a **classification**. If the target is an interval or numerical values then the process is instead called a **regression**.

### Learning Algorithms

How does a machine figure out the relationship between a feature and its target outcome? Think of an assembly line where a conveyer belt feeds into a large metal box and on the other side, another conveyer pops _something_ out. On the metal box there are a series of dials that can be turned to adjust what the box pays particular attention to in the inputs. If there is a known goal, we can continually play with these dials to bring us closer to our goal. Learning algorithms are simply rules for how to manipulate these dials. After seeing examples of known inputs and their expected outcomes, these algorithms can begin to set the dials to good values.

### Limits of Machine Learning

Machine learing has its limits, it's not a silver bullet. If our dataset from earlier recorded the hair color of the patient's spouse, then that would not be useful in predicting heart disease. If we have no useful features, then we will only see illusory patterns. Additionally, if our dataset only contained a single patient then we'll see those false patterns again. We need an ideal number of examples in order to extract anyhting useful from our algorithm and there is a whole mathematical field dedicated to his called computational learning theory.

### Building a Learning System

In general, we can approach constructing a learning system using the following steps:

1. Data collection.

2. Data modeling.

3. Deployment.

Step #2 can be further broken down into six steps:

-   Problem definition. What problem are we trying to solve? Is this a supervised, unsupervised or reinforcement learning problem?
-   Understanding our data. What kind of data do we have? Is the data structured?
-   Evaluation. What does success mean to us? What is our goal? A classification target expects accuracy, precision and recall. For a regression target, we want our numerical value to be as close to the actual value as possible.
-   Features. What do we already know about the data?
-   Modeling. Which machine learning algorithm should we use? Some models work better on different models. Some our data can be used to train the model, other data can be used to validate the model and finally some data can be used to test the model.
-   Experimentation. How can we improve or what can we try next?

### Probability

Given a six-sided die the probability of us rolling a 1 can be given by:

```
P(1) = 1/6
```

We can simulate the rolling of a dice in a few different ways in Python such as with the NumPy library:

```
np.random.randint(1, 7)
```

This will generat a random number from 1 (inclusive) to 7 (exclusive). To run mult

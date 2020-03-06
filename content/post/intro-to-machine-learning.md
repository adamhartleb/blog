---
title: 'Intro to Machine Learning'
date: 2020-03-05
draft: false
tags: ['intro', 'machine learning']
---

Machine learning is the field of study that gives a computer the ability to learn without being explicitly programmed.

As an example, the spam filter from your email provider can learn and analyze what emails are being reported as spam and then apply that filter before the email even reaches you. If we were to program this manually, we might use regular expressions to search for certain keywords we provide in the email and feed each email that comes in through that algorithm. This would be tedious to check and update continuously. In contrast, a machine learning backed filter would be able to analyze the emails itself and adjust accordingly.

### Types of Machine Learning

Machine learning system can be broadly categorized depending on whether they are trained using human supervision (e.g. supervised, unsupervised, and reinforcement learning) or if they can learn incrementally while in progress (online vs batch learning) or whether they operate by comparing new data to old data or by building predictive models by detecting patterns in training data. These categories are not mutually exclusive and can be combined.

#### Supervised Learning

In supervised learning, the data we provide to the algorithm includes the desired outcomes (termed labels) and it infers a function from that. A typical task for supervised learning is _classification_ like the spam filter example introduced above. Another task might be to produce a numerical value (termed target) such as the price of food. This type of task is known as a _regression_. Some important supervised learning algorithms include: k-Nearest neighbors, linear and logistic regression, decision trees and random forests as well as neural networks.

In unsupervised learning, the data we provide does not include the outcome so the system attempts to learn by pattern recognition. Important algorithms include: clustering, anomaly detection and visualizaiton reduction.

Semisupervised learning takes the middle road. Often times you'll have labeled and unlabled data mixed together. For example, if you upload a bunch of photos with the same people; if you label one of the photos, the algorithm can label the same person in each of the rest.

Reinforcement learning takes an agent (the learning system) and observes its environment to select and action to perform. If the action is good, it is rewarded or if it's bad then it is penalized. It then tries to maximize its rewards over time by learning the best strategy.

#### Batch and Online Learning

In batch learning, the system cannot learn incrementally so it must be provided all the data at once. Additionally, in order to add new data, you have to retrain the entire system from scratch with the old plus new data and then deploy that.

On the other hand, with online learning, the system is trained incrementally with small batches at a time. This system is great if the flow of information is continuous or if your computing power is limited. An important property of online learning is the _learning rate_ which can be adjusted so that the system can adapt to new data quickly, but as a result, it will also forget old data quicker too.

#### Instance vs Model based learning

Most machine learning tasks are about predicting things and given enough training sets, a system needs to be able to generalize to be able to make predictions for data it has never seen before.

For instance based learning, a system learns a few examples and then generalizes what it has learned to new examples by using a similarity measure. Using the spam filter example, a similarity measure might be the number of keywords detected in the email.

Model based learning builds a model from the examples it is provided and then uses that to make its predictions. Say a new study finds happiness is correlated with how old you are (the older you are, the more grumpy you are); you would then be able to graph a linear function of happiness for a given age. This is termed a model selection as we have chosen a linear model with a single attribute: happiness at a given age. We can adjust the fit of the line and if we encounter a data point (say age 56) that has no known corresponding happiness level, we can see what interesets our linear model.

### Challenges

Machine learning isn't as cut and dry as it sounds. You'll often encounter poor algorithms or bad data. One of the most common problems is the quantity of data. Almost all agorithms perform the same given a sufficient amount of data, but results can vary wildly if there is an insufficient amount. Additionally, if the data isn't representative of the cases you want to generalize to. If our linear model mentioned previously were to add data that showed happiness actually increased with age, then it would be apparent that a simple downward sloped line wouldn't be able to accurately capture any meaningful predictions.

Irrelevant features are another challenge. Your data sets only need to contain data relevant to the goal. The fact that a patient long or short hair isn't going to be useful in predicting if they will develop heart disease.

Overfitting data can cause wildly inaccurate predictions. Imagine if the downward slope of our linear model suddenly swooped up to intersect a data point that suggests people were happier at age 55. Would you trust the prediction for the next year?

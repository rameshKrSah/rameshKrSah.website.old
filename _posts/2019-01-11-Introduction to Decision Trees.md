---
title: 	"Introduction to Decision Trees"
date: 	2019-01-11
mathjax: True
tags: 	[machine_learning]
---

# Decision Trees
A decision tree is a decision support tool that uses a tree-like model of decision and their possibile consequense to form a solution for a given problem. In a decision tree each node represents a feature (attribute), ach link (branch) represents a decision (rule) and each leaf represents an outcome (categorical or continous). Decision trees can be used for both classification and regression problems. Trees models where the target variable can take a discrete set of values are called classification trees; in these tree structures, leaves represent class labels and branches represent conjunctions of features that lead to those class labels. Decision trees where the target variable can take continous values are called regression trees. The goal is to create a model that predicts the value of a target variable by learning simple decision rules inferred form the data.  

The tree is obtained or learned by spiliting the training set into subsets based on an attribute value set. This process is repeated on each derived subset in a recursive top-down greedy manner and is known as recursive binary splitting. The approach is top-down because it begins at the top of the tree and then successively splits the predictor space; each split is indicated via two new branches further down on the tree. It is greedy because at each step of the tree-building process, the best split is made at that particular step, rather than looking ahead and picking a split that will lead to a better tree in some future step. The process is completed when the subset at a node has all the same target variables, or when spiliting no longer adds value to the predictions.

During the tree building process, we divide the predictor space -- that is, the set of possible values for X1, X2,...,Xp -- into J distinct and non-overlapping regions, R1, R2,...,Rj. For every observation that falls into the region Rj, we make the same prediction, which is simply the mean of the response values for the training observations in Rj for regression trees. In contras, for a classification tree, we predict that each observation belongs to the most commonly occurring class of training observations in the region to which it belongs.  

For instance, suppose that we obtain two regions, R1 and R2, and that the response mean of the training observations in the first region is 10, while the response mean of the training observations in the second region is 20. Then for a given observation X = x, if x belongs to R1 we will predict a value of 10, and if x belongs to R2 we will predict a value of 20.

## Tree building algorithms
1. [ID3](https://en.wikipedia.org/wiki/ID3_algorithm) (iterative Dichotomiser 3) was developed in 1986 by Ross Quinlan. The algorithm creates a multiway treel finding for each node (i.e., in a greedy manner) the categorical feature the will yeild the largest information gain for categorical targets.
2. [CART](https://machinelearningmastery.com/classification-and-regression-trees-for-machine-learning/) (Classification and Regression Trees) was introduced by Leo Bremein for classification or regression redictive modeling problem. It supports numerical target variables (regression) and does not compte rule sets. CART constructs binary trees using the feature and threshold that yield the larget gain at each node measured using Gini Index.

There are several other tree building algorithms but these two are the most used ones.

## Chossing the best split
When building a classification tree, either the Gini index or the entroy are typically used to evaluate the quality of a particular split.  
The Gini index defined as
\begin{equation*}
G = \sum_{k = 1}^KPmk(1 - Pmk)
\end{equation*}
is a measure of total variance across the K classes. It is not hard to see that the Gini index takes on a small value if all the $Pmk$'s are close to zero or one. For this reason the Gini index is referred to as a measure of node purity -- a small value indicates that a node contains predominantly observations from a single class.

An alternative to the Gini index is **entropy**, given by
\begin{equation*}
E = -\sum_{k = 1}^KPmk \log(Pmk)
\end{equation*}
We can show that the entropy will take on a value near to zero if the $Pmk$'s are all near zero or one. Therefore, like the Gini index, the entropy will take on a small value if the $mth$ node is pure.

Entropy is used to calculate the information gain which tells us the which attribute will result in highest information gain. Based on this, constructing a decision tree is all about finding attribute that returns the highest information gain. Information gain is simply given by  
\begin{equation*}
Gain(T, X) = Entropy(T) - Entropy(T, X)
\end{equation*}

### Calculating Information Gain 
Lets say that we have reached the attribute "City_Size" with total 14 instances.
            
            City_Size
            [9A, 5B]
            /     \
           /       \
          /         \
     ---------    -------
     [3A, 4B]      [6A, 1B]
     
As we can see before the split we had 9 instances in class A, and 5 instances in class B i.e., $P(A) = 9/14$ and $P(b) = 5/14$. Then the entropy before the split will be 

$$E1 = -P(A)*log(P(A)) - P(B)*log(P(B)) = -(9/14)*log(9/14) - (5/14)*log(5/14) = 0.9403$$  

If we consider the split with the attribute City_Size then we can calculate the corresponding entropy of the left and right branch like this

$$El = -(3/7)*log(3/7) - (4/7)*log(4/7) = 0.9852$$ 

$$Er = -(6/7)*log(6/7) - (1/7)*log(1/7) = 0.5917$$

Now we can combine the left/right entropies using the number of instances down each branch as weight factor, and get the final after the split

$$E2 = (7/14) * El + (7/14) * Er = 0.7885$$

Finally the information gain if we choose to split the nodes with attribute City_Size will be 

$$Gain = E1 - E2 = 0.9403 - 0.7885 = 0.1515$$

We can interpret this as: By doing the split with the attribute "City_Size", we are able to reduce the uncertainty in the sub-tree prediction outcome by 0.1518, measured in bits. At each node of the classification tree, this calculation is performed for every feature, and the feature with the largest gain is chosen for the split in the greedy manner. This process is applied recursively from the root-node down, and stops when a leaf node contains instances all having the same class or some other stopping criteria is met.

## Advantages of decision trees
- Simple to understand and to interpret. Trees can be visualized.
- Requires little data preparation and is able to handle both numerical and categorical data.
- The cost of using the tree (i.e., making predictions) is logarithmic in the number of data points used to train the tree.
- Possible to validate a model using statistical tests. That makes it possible to account for the reliability of the model.
- Performs well even if its assumptions are somewhat violated by the true model from which the data were generated.

## Disadvantages of decision trees
- Decision-trees learners can create over-complex trees that do not generalse the data well. This is called overfitting. Mechanisms such as pruning, setting the minimum number of samples required at a lead node or setting the maximum depth of the tree are necessary to avoid this problem.
- Decision trees can be unstable because small variations in the data might result in a completely different tree being generated. This problem is mitigated by using decision trees within an ensemble.
- The problem of learning an optimal decision tree is known to be NP-complete under several aspects of optimality and even for simple concepts. Consequently, practical decision-tree learning algorithms are based on heuristic algorithms such as the greedy algorithm where locally optimal decisions are made at each node. Such algorithms cannot guarantee to return the globally optimal decision tree. This can be mitigated by training multiple trees in an ensemble learner, where the features and samples are randomly sampled with replacement.
- Decision tree learners create biased trees if some classes dominate. It is therefore recommended to balance the dataset prior to fitting with the decision tree.

## Refrences
1. [Scikit learn article on Decision Trees](https://scikit-learn.org/stable/modules/tree.html)
2. [Wikipedia article on Decision Tree](https://en.wikipedia.org/wiki/Decision_tree)
3. [Wikipedia article on Decision tree learning](https://en.wikipedia.org/wiki/Decision_tree_learning)
4. [Introduction to Statistical learning](http://auapps.american.edu/alberto/www/analytics/islrlectures.html)
5. [A good article on decision trees](https://www.saedsayad.com/decision_tree.htm)

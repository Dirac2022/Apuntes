
If one had to choose a classification technique that performs well across a wide range of situations without requiring much effort from the analyst while being readily understandable by the consumer of the analysis, a strong contender would be the tree methodology developed by Breiman et al. (1984).

![Snip_TEMP0001.png (1568×1340)](https://media.cheggcdn.com/media/937/937a3f11-27ed-4393-bf83-b4c05cbced0b/Snip_TEMP0001.png)

We have two types of nodes in a tree: decision (=splitting) nodes and terminal nodes. Nodes that have successors are called **decision nodes**. Nodes that have no successors are called **terminal nodes** (or leaves of the tree), and represent the partitioning of the data by predictors.

> [!note]
> When using `export_graphviz()` function from **scikit-learn**, nodes are represented as boxes. All nodes contain 
> - information about the number of records in that node (samples)
> - the distribution of the classes
> - the majority class of that node
> 
> The nodes are colored by the average value of the node for regression or purity of node for classification.

For decision nodes, the name of the predictor variable chosen for splitting and its splitting value appear at the top. Of the two child nodes connected below, a decision node, the left box is for records that meet the splitting condition `True`, while the right box is for records that do not meet it `False`.

<h5>Classifying a new record</h5>
To classify a new record, it is “dropped” down the tree. When it has dropped all the way down to a terminal node, we can assign its class simply by taking a “vote” (or average, if the outcome is numerical) of all the training data that belonged to the terminal node when the tree was grown. The class with the highest vote is assigned to the new record.



## Classification trees

### Recursive Partitioning

Let us denote the outcome variable by Y and the input (predictor) variables by $X_1, X_2, X_3, \dots, X_p$. In classification, the outcome variable will be a categorical variable. Recursive partitioning divides up the p-dimensional space of the $X$ predictor variables into non overlapping multidimensional rectangles. The predictor variables here are considered to be continuous, binary, or ordinal. This division is accomplished recursively (i.e., operating on the results of prior divisions). First, one of the predictor variables is selected, say $X_i$, and a value of $X_i$, say $s_i$, is chosen to split the $p$-dimensional space into two parts: one part that contains all the points with $X_i < s_i$ and the other with all the points with $X_i ⩾ s_i$. Then, one of these two parts is divided in a similar manner by again choosing a predictor variable (it could be $X_i$ or another variable) and a split value for that variable. This results in three (multidimensional) rectangular regions. This process is continued so that we get smaller and smaller rectangular regions. The idea is to divide the entire $X$-space up into rectangles such that each rectangle is as homogeneous or “pure” as possible. By pure, we mean containing records that belong to just one class. (Of course, this is not always possible, as there may be records that belong to different classes but have exactly the same values for every one of the predictor variables.)


Decision tree construction follows a greedy recursive partitioning approach. The algorithm begins by evaluating all possible splits across all features and selects the single split that maximizes the reduction in impurity (measured by Gini or Entropy). This creates two child nodes. The process then continues recursively, where at each step the algorithm identifies the most impure node among all current leaf nodes and finds the optimal split for that specific node, without reconsidering previous splits. This node selection prioritizes divisions that will yield the greatest purity gain. The recursion stops when a stopping criterion is met, such as maximum tree depth, minimum samples per node, or when no significant impurity reduction is possible, resulting in pure nodes or nodes that cannot be split further.


<h5>Example: Riding Mowers</h5>
A riding-mower manufacturer would like to find a way of classifying families in a city into those likely to purchase a riding mower and those not likely to buy one. A pilot random sample of 12 owners and 12 nonowners in the city is undertaken.

| Household number | Income ($000s) | Lot size (000s ft²) | Ownership of riding mower |
|------------------|----------------|---------------------|---------------------------|
| 1                | 60.0           | 18.4                | Owner                     |
| 2                | 85.5           | 16.8                | Owner                     |
| 3                | 64.8           | 21.6                | Owner                     |
| 4                | 61.5           | 20.8                | Owner                     |
| 5                | 87.0           | 23.6                | Owner                     |
| 6                | 110.1          | 19.2                | Owner                     |
| 7                | 108.0          | 17.6                | Owner                     |
| 8                | 82.8           | 22.4                | Owner                     |
| 9                | 69.0           | 20.0                | Owner                     |
| 10               | 93.0           | 20.8                | Owner                     |
| 11               | 51.0           | 22.0                | Owner                     |
| 12               | 81.0           | 20.0                | Owner                     |
| 13               | 75.0           | 19.6                | Nonowner                  |
| 14               | 52.8           | 20.8                | Nonowner                  |
| 15               | 64.8           | 17.2                | Nonowner                  |
| 16               | 43.2           | 20.4                | Nonowner                  |
| 17               | 84.0           | 17.6                | Nonowner                  |
| 18               | 49.2           | 17.6                | Nonowner                  |
| 19               | 59.4           | 16.0                | Nonowner                  |
| 20               | 66.0           | 18.4                | Nonowner                  |
| 21               | 47.4           | 16.4                | Nonowner                  |
| 22               | 33.0           | 18.8                | Nonowner                  |
| 23               | 51.0           | 14.0                | Nonowner                  |
| 24               | 63.0           | 14.8                | Nonowner                  |

If we apply the classification tree procedure to these data, the procedure will choose Income for the first split with a splitting value of 60. The $(X_1, X_2)$ space is now divided into two rectangles, one with Income ≤ 59.7 and the other with Income > 59.7.

![[Pasted image 20251105183617.png]]
Figure: Scatter plot of Lot Size Vs. Income for 24 owners and nonowners of riding mowers

![[Pasted image 20251105183700.png]]
Figure: Splitting the 24 records by Income value of 59.7

> [!important] How has this particular split selected?
> The algorithm examined each predictor variable (in this case, Income and Lot Size) and all possible split values for each variable to find the best split. What are the possible split values for a variable? They are simply the midpoints between pairs of consecutive values for the predictor. The possible split points for Income are $\{38.1, 45.3, 50.1, …, 109.5\}$ and those for Lot Size are $\{14.4, 15.4, 16.2, …, 23\}$. These split points are ranked according to how much they reduce impurity (heterogeneity) in the resulting rectangle

The reduction in impurity is defined as ==overall impurity before the split minus the sum of the impurities for the two rectangles that result from a split==.


#### Categorical Predictors

The previous description used numerical predictors; however, categorical 
predictors can also be used in the recursive partitioning context. To handle categorical predictors, the split choices for a categorical predictor are all ways in which the set of categories can be divided into two subsets.

For example, a categorical variable with four categories, say {a, b, c, d}, 
can be split in seven ways into two subsets:

- {a} and {b, c, d}
- {b} and {a, c, d}
- {c} and {a, b, d}
- {d} and {a, b, c}
- {a, b} and {c, d}
- {a, c} and {b, d}
- {a, d} and {b, c}

When the number of categories is large, the number of splits becomes very 
large. As with k-nearest-neighbors, a predictor with m categories (m > 2) 
should be factored into m dummies (not m−1).

> [!note] Normalization
> Whether predictors are numerical or categorical, it does not make any difference if they are standardized (normalized) or not


## Measures of Impurity

There are a number of ways to measure impurity. The two most popular measures are the *Gini index* and an *entropy measure*. Denote the $m$ classes of the response variable by $k = 1, 2, \dots , m$.

The **Gini impurity** index for a rectangle $A$ is defined by

$$
I(A) = 1 - \sum_{k=1}^m p_k^2
$$
where $p_k$ is the proportion of records in rectangle $A$ that belong to class $k$. ==This measure takes values between 0 (when all the records belong to the same class) and (m − 1)/m (when all m classes are equally represented)==

![[Pasted image 20251105173209.png]]
Figure: Values of the Gini index for a two-class case as a function of $pk$. It can be seen that the impurity measure is at its peak when $p_k = 0.5$ (i.e., when the rectangle contains 50% of each of the two classes).

A second impurity measure is the **entropy measure**. The entropy for a rectangle A is defined by

$$
\text{entropy}(A) = - \sum_{k=1}^m p_k \, log_2 \, (p_k)
$$

This measure ranges between 0 (most pure, all records belong to the same class) and $log_2(m)$ (when all $m$ classes are represented equally). In the two-class case, the entropy measure is maximized (like the Gini index) at $p_k = 0.5$

Let us compute the impurity in the riding mower example before and after the first split (using Income with the value of 59.7). The unsplit dataset contains 12 owners and 12 nonowners. This is a two-class case with an equal number of records from each class. Both impurity measures are therefore at their maximum value: $Gini = 0.5$ and $entropy = log 2(2) = 1$. After the split, the left rectangle contains seven non owners and one owner. The impurity measures for this rectangle are:

$$
\begin{align*}
\text{gini\_left} &= 1 -(7/8)^2 - (1/8)^2 = 0.219 \\ \\
\text{entropy\_left} &= -(7/8) \, log_2 \, (7/8) - (1/8) \, log_2 \, (1/8) = 0.544
\end{align*}
$$

The right node contains 11 owners and 5 non owners. The impurity measures of the right node are therefore

$$
\begin{align*}
\text{gini\_left} &= 1 -(11/16)^2 - (5/16)^2 = 0.430 \\ \\
\text{entropy\_left} &= -(11/16) \, log_2 \, (11/16) - (5/16) \, log_2 \, (5/16) = 0.896
\end{align*}
$$

The combined impurity of the two nodes created by the split is a weighted average of the two impurity measures, weighted by the number of records in each:

$$
\begin{align*}
gini &= (8/24) \, (0.219) + (16/24) \, (0.430) = 0.359 \\ \\
entropy &= (8/24) \, (0.544) + (16/24) \, (0.896) = 0.779
\end{align*}
$$

Thus, the Gini impurity and the entropy measure decreased.

By comparing the reduction in impurity across all possible splits in all possible predictors, the next split is chosen. If we continue splitting the mower data, the next split is on the `Lot Size` variable at the value 21.4.

## Evaluating the Performance of a Classification Tree

- Tree structure can be quite unstable, shifting substantially depending on the sample chosen
- A fully-fit tree will invariably lead to overfitting














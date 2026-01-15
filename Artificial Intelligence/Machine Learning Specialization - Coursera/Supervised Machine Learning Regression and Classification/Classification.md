	

# Classification

## Logistic function

$$
g(z) = \dfrac{1}{1+e^{-z}} \ , \quad 0 \leq g(z) \leq 1
$$

## Logistic Regression

$$
f_{\vec{x}, b} \ (\vec{x}) = g(\vec{w} \cdot \vec{x} + b) = \dfrac{1}{1+e^{-(\vec{w} \cdot \vec{x} + b)}}
$$

**Interpretation of logistic regression output**

$$
f_{\vec{x}, b} \ (\vec{x}) = P(y=1|\vec{x}; \vec{w}, b)
$$
Probability that $y$ is $1$, given input $\vec{x}$, parameters $\vec{w}$, $b$
Where
$$
P(y=0) + P(y=1) = 1
$$


## Decision Boundary

![[Pasted image 20250304171947.png]]


If we want to predict if the value of $y$ is going to be $0$ or $1$, one thing we might do is set a  **threshold**. 

- Is $\ f_{\vec{w}, b} \ (\vec{x}) \geq 0.5$ ?
$$
\begin{matrix}
\text{Yes : } \vec{y} = 1 &  \text{No : } \vec{y} = 0
\end{matrix}
$$
- When is $f_{\vec{w}, b} \geq 0.5$ ?
$$
\begin{matrix}
g(z) \geq 0.5 & \\ \\
z \geq 0 & \\ \\
\vec{w} \cdot \vec{x} + b \geq 0  &  & \vec{w} \cdot \vec{x} + b  < 0 \\ \\
\vec{y} = 1 & & \vec{y} = 0

\end{matrix}
$$

### Examples

![[Pasted image 20250304172150.png]]
![[Pasted image 20250304172211.png]]
![[Pasted image 20250304172235.png]]

# Cost Function

## Cost Function for Logistic Regression

![[Pasted image 20250304183710.png]]

If we used the same cost function for Logistic Regression, this will be a **non-convex** cost function.
So, the **squared error cost** function is not a good choice.

We need another form of **Loss function**
### Logistic loss function

$$
L\left( f_{\vec{w}, b} (\vec{x}^{(i)}) , y^{(i)}\right) = 
\begin{cases}
-log \ \left(f_{\vec{w}, b} (\vec{x}^{(i)})\right) \quad \quad \quad \text{if } y^{(i)} = 1 \\ \\
-log \ \left(1-f_{\vec{w}, b} (\vec{x}^{(i)})\right) \quad \  \text{if } y^{(i)} = 0 \\ 
\end{cases}
$$


![[Pasted image 20250304214153.png]]



For $-log \ \left(f_{\vec{w}, b} (\vec{x}^{(i)})\right)$
- As $f_{\vec{w}, b} (\vec{x}^{(i)}) \to 1$ then **loss** $\to 0$
- As $f_{\vec{w}, b} (\vec{x}^{(i)}) \to 0$ then **loss** $\to \infty$

>[!note] Loss is lowest when $f_{\vec{w}, b} (\vec{x}^{(i)})$ predicts close to true label $y^{(i)}$


For $-log \ \left(1-f_{\vec{w}, b} (\vec{x}^{(i)})\right)$
- As $f_{\vec{w}, b} (\vec{x}^{(i)}) \to 0$ then **loss** $\to 0$
- As $f_{\vec{w}, b} (\vec{x}^{(i)}) \to 1$ then **loss** $\to \infty$

>[!note] Loss is lowest when $f_{\vec{w}, b} (\vec{x}^{(i)})$ predicts close to true label $y^{(i)}$

Therefore, the cost function is

$$
J(\vec{w}, b) = \dfrac{1}{m} \sum_{i=1}^m L(f_{\vec{w}, b} (\vec{x}^{(i)}), y^{(i)})
$$
This cost function is convex and can reach a global minimum


>[!important]
>-  **Loss** is a measure of the difference of a single example to its target value while the  
 >- **Cost** is a measure of the losses over the training set
 
### Simplified loss function

$$
L\left( f_{\vec{w}, b} (\vec{x}^{(i)}) , y^{(i)}\right) = -y^{(i)} \ log \left(f_{\vec{w}, b} (\vec{x}^{(i)})\right) - (1-y^{(i)}) \ log \left(1-f_{\vec{w}, b} (\vec{x}^{(i)})\right)
$$
and the cost function

$$
\begin{align*}
J(\vec{w}, b) &= \dfrac{1}{m} \sum_{i=1}^m L(f_{\vec{w}, b} (\vec{x}^{(i)}), y^{(i)}) \\ \\
&= - \dfrac{1}{m} \sum_{i=1}^m \left[y^{(i)} \ log \left(f_{\vec{w}, b} (\vec{x}^{(i)})\right) + (1-y^{(i)}) \ log \left(1-f_{\vec{w}, b} (\vec{x}^{(i)})\right)\right]
\end{align*}
$$

>[!tip] This loss function is convex


# Gradient Descent

## Gradient Descent Implementation

Repeat until converge {
$$
w_j = w_j - \alpha \, \dfrac{\partial}{\partial \,  w_j} J(\vec{w}, b)
$$

$$
b = b - \alpha \, \dfrac{\partial}{\partial \, b} J(\vec{w}, b)
$$
}  Simultaneous updates

>[!info] Where
>$$
>\begin{align*}
>\dfrac{\partial}{\partial \,  w_j} J(\vec{w}, b) &= \frac{1}{m} \sum_{i=1}^{m} \left(f_{\vec{w},b} \, (\vec{x}^{(i)}) - y^{(i)}\right) x_j^{(i)} \\ \\
>\dfrac{\partial}{\partial \,  b} J(\vec{w}, b) &= \frac{1}{m} \sum_{i=1}^{m} \left(f_{\vec{w},b} \, (\vec{x}^{(i)}) - y^{(i)}\right)
> \end{align*}
$$

>[!important] Although these equations look exactly like the ones we had before for linear regression, the definition of the function $f$ has changed.

- Linear Regression
$$
f_{\vec{w}, b} \ (\vec{x}) = \vec{w} \cdot \vec{x} + b
$$
- Logistic Regression
$$
f_{\vec{w}, b} \ (\vec{x}) = \dfrac{1}{1 + e^{- (\vec{w} \cdot \vec{x} + b})}
$$

**Same concepts**
- Monitor gradient descent (learning curve)
- Vectorized implementation
- Feature scaling



# Regularization to Reduce Overfitting

## The problem of Overfitting

### Underfitting
- The algorithm does not fit the training set well. 
- The algorithms has **high bias** 

> [!tip] High bias
> If the algorithm has underfit the data meaning that it's just not even able to fit the training set that well that is a clear pattern in the training data that the algorithm is just unable to capture

![[Pasted image 20250307111730.png]]

### Overfitting
- Fits the training set extremely well.
- The model cannot generalize to new, unseen examples.
- The algorithm has **high variance**.

>[!tip] High variance
>If two different machine learning engineers were to fit this fourth order polynomial model so just slightly different data sets they could end up with totally different predictions or **highly variable** predictions and that's why we say the algorithm has **high variance**

![[Pasted image 20250307113027.png]]

### Generalization

- Fits the training set pretty well.
- The model performs well on new, unseen examples.
- The algorithm has a balance between bias and variance.

![[Pasted image 20250307112954.png]]


### Examples in Classification

![[Pasted image 20250307114523.png]]


## Addressing Overfitting

### 1. Collect more training examples

If you can obtain more training examples, a larger training set will help the learning algorithm fit a function that is less wiggly. This allows you to continue using a high-order polynomial or a function with many features while maintaining good performance, as long as you have enough training data.

![[Pasted image 20250307115058.png]]


### 2. Select features to include/exclude
**See if you can use fewer features**.
If you have many features but not enough training data, your learning algorithm may overfit. Instead of using all the features, select a subset of the most relevant ones. Using this smaller subset may help reduce overfitting and improve generalization.

>[!tip] Choosing the most appropiate set of features to use is sometimes also called feature selection

**Disadvantage**
Useful features could be lost

![[Pasted image 20250307120651.png]]


### 3. Regularization

Overfitting often occurs in models with polynomial features, where parameters tend to be large. One way to address this is by eliminating certain features (e.g., setting $x_4$ to 0). However, regularization provides a more refined approach by reducing the impact of features without completely removing them.

Regularization encourages the learning algorithm to shrink parameter values, preventing them from becoming excessively large. Even when using a high-order polynomial, keeping smaller parameter values results in a smoother function that fits the training data better. This technique allows the model to retain all features while controlling their influence, ultimately improving generalization and reducing overfitting.

>[!info]  By convention we just reduce the size of the $w_j$ parameters, doesn´t make a huge impact whether you regularize the parameter $b$

![[Pasted image 20250307121801.png]]


## Cost Function with Regularization

The way that regularization tends to be implemented is if you have a lot of features, you may not know which are the most important features and which ones to penalize so the way regularization is typically implemented is to penalize all of the features or more precisely you penalize all the $w_j$ parameters .

$$
J(\vec{w}, b) = \dfrac{1}{2m} \sum_{i=1}^m \ \left( f_{\vec{w}, b} \, (\vec{x}^{(i)}) - y^{(i)}\right)^2 + \dfrac{\lambda}{2m} \sum_{j=1}^n w_j^2
$$
where $\lambda$ is the **regularization parameter**, $\lambda > 0$
>[!tip] We also divide $\lambda$ by $2m$ so both terms are scaled by $1/2m$. So: 
>- By scaling both terms the same way it becomes a little bit easier to choose a good value for $\lambda$
>- If the training set size grows ($m$ increases). The same value of $\lambda$ picked previously is also more likely to continue to work

![[Pasted image 20250307193707.png]]


## Regularized Linear Regression

Repeat until converge {
$$
w_j = w_j - \alpha \, \dfrac{\partial}{\partial \,  w_j} J(\vec{w}, b)
$$

$$
b = b - \alpha \, \dfrac{\partial}{\partial \, b} J(\vec{w}, b)
$$
}  Simultaneous updates

>[!info] Where
>$$
>\begin{align*}
>\dfrac{\partial}{\partial \,  w_j} J(\vec{w}, b) &= \frac{1}{m} \sum_{i=1}^{m} \left(f_{\vec{w},b} \, (\vec{x}^{(i)}) - y^{(i)}\right) x_j^{(i)} + \dfrac{\lambda}{m} w_j\\ \\
>\dfrac{\partial}{\partial \,  b} J(\vec{w}, b) &= \frac{1}{m} \sum_{i=1}^{m} \left(f_{\vec{w},b} \, (\vec{x}^{(i)}) - y^{(i)}\right)
> \end{align*}
$$

We don´t have to regularize $b$.

The update of $w_j$ with regularization can be seen as
$$
w_j = w_j \left(1-\alpha \dfrac{\lambda}{m} \right) - \alpha \, \frac{1}{m} \sum_{i=1}^{m} \left(f_{\vec{w},b} \, (\vec{x}^{(i)}) - y^{(i)}\right) x_j^{(i)}
$$
where $j=1, \dots , n$ is the number of features


## Regularized Logistic Regression

**Cost function**
$$
J(\vec{w}, b) = - \dfrac{1}{m} \sum_{i=1}^m \left[y^{(i)} \ log \left(f_{\vec{w}, b} (\vec{x}^{(i)})\right) + (1-y^{(i)}) \ log \left(1-f_{\vec{w}, b} (\vec{x}^{(i)})\right)\right] + \dfrac{\lambda}{2m} \sum_{j=1}^n w_j^2
$$


**Gradient descent implementation**
Repeat until converge {
$$
w_j = w_j - \alpha \, \dfrac{\partial}{\partial \,  w_j} J(\vec{w}, b)
$$

$$
b = b - \alpha \, \dfrac{\partial}{\partial \, b} J(\vec{w}, b)
$$
}  Simultaneous updates

>[!info] Where
>$$
>\begin{align*}
>\dfrac{\partial}{\partial \,  w_j} J(\vec{w}, b) &= \frac{1}{m} \sum_{i=1}^{m} \left(f_{\vec{w},b} \, (\vec{x}^{(i)}) - y^{(i)}\right) x_j^{(i)} + \dfrac{\lambda}{m} w_j\\ \\
>\dfrac{\partial}{\partial \,  b} J(\vec{w}, b) &= \frac{1}{m} \sum_{i=1}^{m} \left(f_{\vec{w},b} \, (\vec{x}^{(i)}) - y^{(i)}\right)
> \end{align*}
$$

>[!important] Although these equations look exactly like the ones we had before for linear regression, the definition of the function $f$ has changed.


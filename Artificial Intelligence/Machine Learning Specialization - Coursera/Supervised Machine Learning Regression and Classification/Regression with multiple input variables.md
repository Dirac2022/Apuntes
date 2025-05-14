# Linear Regression with Multiple Variables

## Multiple features (variables)


| Size in feet$^2$ ($x_1$) | Number of bedrooms ($x_2$) | Number of floors ($x_3$) | Age of home in years ($x_4$) | Price ($) in $1000's |
| ------------------------ | -------------------------- | ------------------------ | ---------------------------- | -------------------- |
| 2104                     | 5                          | 1                        | 45                           | 460                  |
| 1416                     | 3                          | 2                        | 40                           | 232                  |
| 1534                     | 3                          | 2                        | 30                           | 315                  |
| 825                      | 2                          | 1                        | 36                           | 178                  |
| $\dots$                  | $\dots$                    | $\dots$                  | $\dots$                      | $\dots$              |

- $x_j = j^{th}$ feature $j=1,\dots, 4$
- $n =$ number of feature
- $\vec{x}^{(i)} =$ features of $i^{th}$ training example
- $x_j^{(i)} =$ value of feature $j$ in $i^{th}$ training example

Por ejemplo
- $\vec{x}^{(2)} = \begin{bmatrix} 1416 & 3 & 2 & 40 \end{bmatrix}$
- $x_3^{(2)} = 2$


### Multiple linear regression
Our model is

$$
f_{w, b} \, (x) = w_1x_1 + w_2x_2 + \dots + w_nx_n + b
$$
where $\vec{w} = \begin{bmatrix} w_1 & w_2 & \dots & w_n \end{bmatrix}$ are the parameters of the model
and $b$ is a number.

$$
f_{w, b} \, (\vec{x}) = \vec{w}  \cdot  \vec{x} + b = w_1x_1 + w_2x_2 + \dots + w_nx_n + b
$$



## Gradient descent

$n$ features ($n \geq 2$)
Repeat until converge {
$$
\begin{align*}
w_1 &= w_1 - \alpha \, \frac{1}{m} \sum_{i=1}^{m} \left(f_{\vec{w},b} \, (\vec{x}^{(i)}) - y^{(i)}\right) x_1^{(i)} \\
&\vdots \\ 
w_n &= w_n - \alpha \, \frac{1}{m} \sum_{i=1}^{m} \left(f_{\vec{w},b} \, (\vec{x}^{(i)}) - y^{(i)}\right) x_n^{(i)} \\ \\
b &= b - \alpha \, \frac{1}{m} \sum_{i=1}^{m} \left(f_{\vec{w},b} \, (\vec{x}^{(i)}) - y^{(i)}\right)
\end{align*}
$$

$$
\text{simultaneous update}
$$
$$
w_j \ (\text{for } j = 1 , \dots , n) \text{ and } b
$$
}

### Normal equation
- Only for linear regression
- Solve for $w, b$ without iterations

Normal equation method may be used in machine learning libraries that implement linear regression. Gradient descent is the recommended method for finding parameters $w, b$

#### Disadvantages
- Doesn´t generalize to other learning algorithms
- Slow when number of features is large ($> 10 000$)



# Practical Tips for Linear Regression

## Feature Scaling

In the example of house prices
$$
\text{price} = w_1 \, x_1 + w_2 \, x_2 + b
$$
where
- $x_1$: size (feet$^2$) ,range: $300 - 20000$
- $x_2$: # bedrooms,  range: $0 - 5$


![[Pasted image 20250216091953.png]]


Parameter $w_1$ will take a small range because of $x_1$ and $w_2$ will take a large range because of $x_2$.

In contour plot above:
>[!warning] Because the contours are still tall and skinny  gradient descents may end up bouncing back and forth for a long time before it can finally find its way to the global minimum

![[Pasted image 20250204190435.png]]
In contour plot bellow:
>[!tip] In situation like this a useful thing to do is to scale the features, this means performing some transformation of your training data, by changing the range of the features.

When you have different features that take on very different ranges of values it can cause gradient descent to run slowly but rescaling the different so they all take on comparable range of values can speedup gradient descent significantly.

### Mean normalization

If $\text{min} \leq x_i \leq \text{max}$
$$
x_i = \frac{x_i - \mu_i}{\text{max} - \text{min}}
$$

Where $\mu_i$ is the mean of the $i$-th feature
for all $x_i \in X_i$

**Example**
$300 \leq x_1 \leq 2000$ ,   $0 \leq x_2 \leq 5$
If $\mu_1 = 600$ and $\mu_2 = 2.3$

$$
\begin{matrix}
x_1 = \dfrac{x_1 - \mu_1}{2000 - 3000}  & & x_2 = \dfrac{x_2 - \mu_2}{5 - 0} \\ \\
-0.18 \leq x_1 \leq 0.82 & & -0.46 \leq x_2 \leq 0.54
\end{matrix}
$$


### Z-score normalization
If $j$ is the column feature from the training matrix $X$ and $i$ indicates the $i$-th training.
$$
x_j^{(i)} = \frac{x_j^{(i)} - \mu_j}{\sigma_j}
$$

Where $\sigma_i$ is the standard deviation of the $i$-th feature and

$$
\mu_j = \dfrac{1}{m} \sum_{i=0}^{m-1} x_j^{(i)}
$$

$$
\sigma_j^2 = \dfrac{1}{m} \sum_{i=0}^{m-1} \left(x_j^{(i)} - \mu_j\right)^2
$$
**Example**
$300 \leq x_1 \leq 2000$ ,   $0 \leq x_2 \leq 5$
- If $\mu_1 = 600$ and $\mu_2 = 2.3$
- And $\sigma_1 = 450$ and $\sigma_2 = 1.4$

$$
\begin{matrix}
x_1 = \dfrac{x_1 - \mu_1}{\sigma_1}  & & x_2 = \dfrac{x_2 - \mu_2}{\sigma_2} \\ \\
-0.67 \leq x_1 \leq 3.1 & & -1.6 \leq x_2 \leq 1.9
\end{matrix}
$$

### Examples

| Range                       | Scaling                 |
| --------------------------- | ----------------------- |
| $0 \leq  x \leq 3$          | not needed              |
| $-2 \leq  x \leq 0.5$       | not needed              |
| $-100\leq  x \leq 1000$     | too large $\to$ rescale |
| $-0.001 \leq  x \leq 0.001$ | too small $\to$ rescale |
| $98.6 \leq  x \leq 105$     | too large $\to$ rescale |


## Checking Gradient Descent for Convergence


- If gradient descent is working properly then the cost $J$ should decrease after every single iteration
- If $J$ ever increases after one iteration that means either the learning rate $\alpha$ is chosen poorly, and it usually means $\alpha$ is too large or there could be a bug in the code

![[Pasted image 20250216100631.png]]

### Automatic convergence test
Let $\varepsilon$  be $10^-3$ 
- If $J\vec{w}, b)$ decreases by $\leq \varepsilon$ in one iteration, declare **convergence**.

>[!tip] Choosing the right threshold epsilon is pretty difficult, so look at the graphs $J$ vs iterations would be helpful


## Learning Rate

Given the learning rate $\alpha$
- If it's too small it would run very slowly
- If it's too large it may not even converge

If you plot the cost for a number of iterations and notices that the cost sometimes goes up and sometimes goes down you should take that as a clear sign that gradient descent is not working properly.
![[Pasted image 20250224115048.png]]

- There could be a bug code
- The learning rate is too large

![[Pasted image 20250224115120.png]]

Sometimes you may see that the cost consistently increases after each iteration, 
![[Pasted image 20250224115934.png]]
This means the learning rate is too large and it could be addressed by choosing a smaller learning rate. This could be a sign of  a bug in the code. If we write $w = w + \alpha \, d$ we are adding the derivative term and this  moves the cost $J$ further from the global minimum instead of closeup. 


## Feature Engineering

## Polynomial Regression

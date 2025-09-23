
# Word representation

>[!tip] Word Embeddings
>A way of representing words, that lets your algorithms automatically understand analogies like that: *main is to woman as king is to queen* etc.


$$
V = [a, aaron, . . ., zulu, <UNK>]
$$
**1-hot representation**
$$
\begin{array}{cccccc}
\text{Man} & \text{Woman} & \text{King} & \text{Queen} & \text{Apple} & \text{Orange} \\ 
(5391) & (9853) & (4914) & (7157) & (456) & (6257) \\
\begin{bmatrix}
0 \\ 0 \\ 0 \\ 0 \\ \vdots \\ 1 \\ \vdots \\ 0 \\ 0 
\end{bmatrix}
&
\begin{bmatrix}
0 \\ 0 \\ 0 \\ 0 \\ 0 \\ \vdots \\ 1 \\ \vdots \\ 0 
\end{bmatrix}
&
\begin{bmatrix}
0 \\ 0 \\ 0 \\ \vdots \\ 1 \\ \vdots \\ 0 \\ 0 \\ 0 
\end{bmatrix}
&
\begin{bmatrix}
0 \\ 0 \\ 0 \\ 0 \\ 0 \\ \vdots \\ 1 \\ \vdots \\ 0 
\end{bmatrix}
&
\begin{bmatrix}
0 \\ \vdots \\ 1 \\ \vdots \\ 0 \\ 0 \\ 0 \\ 0 \\ 0 
\end{bmatrix}
&
\begin{bmatrix}
0 \\ 0 \\ 0 \\ 0 \\ 0 \\ \vdots \\ 1 \\ \vdots \\ 0 
\end{bmatrix}
&
\end{array}
$$


One of the weaknesses of this representations is that treats each word as a thing unto itself and it doesn't allow an algorithm to easily generalize the cross words.

This is because the inner product between any two different *one-hot* vector is **zero**.

>[!warning] 'Orange' and 'Apple' are more close, as 'Man' and 'Woman' and 'King' and 'Queen' but with *one-hot* representation, each word is 'equally' distant to each other



## Word embedding
We can instead learn a featurized representation for each of these words, with a set of features and corresponding values

$$
\begin{array}{c|cccccc}
& \text{Man} & \text{Woman} & \text{King} & \text{Queen} & \text{Apple} & \text{Orange} \\
& (5391) & (9853) & (4914) & (7157) & (456) & (6257) \\
\\ \hline \\
\text{Gender} & -1 & 1 & -0.95 & 0.97 & 0.00 & 0.01 \\
\text{Royal} & 0.01 & 0.02 & 0.93 & 0.95 & -0.01 & 0.00 \\
\text{Age} & 0.03 & 0.02 & 0.7 & 0.69 & 0.03 & -0.02 \\
\text{Food} & 0.04 & 0.01 & 0.02 & 0.01 & 0.95 & 0.97 \\
\vdots & & & & & & \\
\text{size} \\
\text{cost} \\
\vdots
\end{array}
$$

Each word is represented by a 300 dimensional vector, each value is a *feature*
The distant is close between similar pair of words

![[Pasted image 20250803182026.png]]


# Using word embeddings

**Transfer learning and word embedding**

1. Learn word embeddings from large text corpus. (1-100B words)
	- (Or download pre-trained embedding online.)
2. Transfer embedding to new task with smaller set.
	- (say, 100k words)
3. Optional: Continue to finetune the word embedding with new data


# Properties of word embeddings

**Analogies**

$$
\begin{array}{c|cccccc}
& \text{Man} & \text{Woman} & \text{King} & \text{Queen} & \text{Apple} & \text{Orange} \\
& (5391) & (9853) & (4914) & (7157) & (456) & (6257) \\
\\ \hline \\
\text{Gender} & -1 & 1 & -0.95 & 0.97 & 0.00 & 0.01 \\
\text{Royal} & 0.01 & 0.02 & 0.93 & 0.95 & -0.01 & 0.00 \\
\text{Age} & 0.03 & 0.02 & 0.7 & 0.69 & 0.03 & -0.02 \\
\text{Food} & 0.04 & 0.01 & 0.02 & 0.01 & 0.95 & 0.97 \\
\end{array}
$$

$$
e_\text{Man} \to e_\text{Woman} \Rightarrow e_\text{King} \to e_\text{?}
$$
$$
\text{Find a word } w : \underset{w}{\text{argmax}} \ sim(e_w, e_{\text{king}} - e_{\text{man}} + e_{\text{woman}})
$$

Hallando $w = \text{Queen}$ se ve que el vector diferencia entre 'Man' y 'Woman' es aproximadamente igual al vector diferencia entre 'King' y 'Queen'.

The most commonly used similarity function $sim()$ is the **cosine similarity.

$$
sim(u, v) = \dfrac{u^t \, v}{\|u\|_2\|v\|_2}
$$



# Embedding Matrix

We form a matrix embedding  $E$ by stacking each vector representing words for embedding representation.

- $E$ : embedding matrix
- $O_j$ : One-hot vector representation of a word, with 1 in $j$ position
- $e_j$: $j$ column for the $E$ matrix, this vector is the embedding representation of a word.

$$
\Huge
E \, O_{6257} = e_{6257}
$$



# Learning word embeddings

Building a neural language model is a feasible way to learn a set of embeddings.

- **Context**: 'I want a glass of'
- **target**: 'juice'

![[Pasted image 20250803190957.png]]


## Other context/target pairs

Sentence:
$$
\text{I want a glass of orange juice to go along with my cereal}
$$

The target is **juice**.

**Last 4 words** 
<p style="color:lightblue">a glass of orange <span style="color:green">___</span></p> 

**4 words on left & right**
<p style="color:lightblue">a glass of orange <span style="color:green">___</span> to go along with</p> 

**Last 1 word**
<p style="color:lightblue">orange <span style="color:green">___</span></p> 

**Nearby 1 word**
<p style="color:lightblue">glass<span style="color:green">___</span> to go along with</p> 

>[!info] Note
>Researchers found that is you really want to build a language model, it's natural to use the last few words as a context. But if your main goal is really to learn a word embedding you can use the last three examples of context and they will work well.


---

# Word2Vec

## Skip-grams

"I want a glass of orange juice to go along with my cereal"

- Randomly picks a context word: **orange**
- Randomly pick another word withing some window: **juice**, **glass**, **my**

| Context | Target | window |
| ------- | ------ | ------ |
| orange  | juice  | +1     |
| orange  | glass  | -2     |
| orange  | my     | +6     |

We setup a supervised learning problem where given the context word, you're asked to predict what is a randomly chosen word within say, a +- 10 word window, or +- 5, etc., of that input context word.

The goal is learning good word embeddings

### Model
- Vocal size = 10 000


$$
\begin{aligned}
x \quad &\Rightarrow \quad y \\ \\
\text{Content} \quad c \quad \underset{6257}{(\text{orange})} \quad &\Rightarrow \quad \text{target}  \ \quad t  \quad  \underset{4834}{\text{(juice)}} \\ \\
O_c \to E \to e_c\quad &\Rightarrow \quad (sofmaxt) \to \hat{y}
\end{aligned}
$$

where

$$

\displaystyle
\text{Softmax} : p(t|c) = \frac{ \Huge e^{\theta_t^T e_c} } { \underset{j=1}{\overset{10000}{\sum} } \Huge e^{\theta_j^T e_c} }
$$

- $\theta_t$ is the parameter associated with the output $t$

and the loss

$$
L(\vec{y}, y) = \underset{j=1}{\overset{10000}{\sum}} y_i \, log \, \vec{y}_i
$$

where $y$ is a 10 000 dimensional  one-hot-vector

$$
\begin{array}{cccc}
y & = & 
\begin{bmatrix}
0 \\ \vdots \\ 1 \\ \vdots \\ 0
\end{bmatrix}
& 
\leftarrow 4834
\end{array}
$$

and $\hat{y}$ is a 10 000 dimensional vector output by the softmax unit with probabilities for all 10 000 possible targets words.


**Disadvantages**

- Problems with softmax classification
	- Computational speed for large possible targets words

**Alternatives**

- Hierarchical softmax


## CBOW
**Continuous Bag-of-Words**


"Takes the surrounding context from middle word and uses the surrounding words to try to predict the middle word"


---

# Negative sampling

Given a pair of words: "orange", and "juice", we're going to predict, is this a context target pair?

| context | word  | is a target? |
| ------- | ----- | ------------ |
| orange  | juice | 1            |
| orange  | king  | 0            |
| orange  | book  | 0            |
| orange  | the   | 0            |
| orange  | of    | 0            |

1. We are going to sample a context and a target word ('orange' and 'juice'). And we'll associate that with a label of 1
2. Having generated a positive example. Given the context word we just pick a word at random from the dictionary like ('orange' and 'king', 'orange' and 'book', 'orange' and 'the', 'orange' and 'of') and we associate with a label of 0. A $k$ size of picked words randomly

>[!important] Note
>Is ok if just by chance, one of those words we picked at random from the dictionary happens to appear in a window, like in a +- ten-word window say next to the context word 'orange'.

3. We're going to create a supervised learning problem, where the algorithm inputs the pair of words $x$ and then has to predict the target label $y$ (0 - 1). 

- **For smaller dataset** : $k = 5 - 20$
- **For larger dataset**: $k = 2-5$


## Model

- $c$ : contexto word
- $t$: possible target word
- $y$: 0, 1. Is this a context-target pair?

$$
p(y = 1 | c, t) = \Huge \sigma(\theta_t^T e_c)
$$

If we have $k$ examples, we have $k:1$ ratio for negative to positive examples.

## Selecting negative examples

- $f(\omega_i)$: empirical frequency of the word $\omega_i$
- vocal size : 10000

$$
p(w_i) = \dfrac{f(w_i)}{\sum_j^{10000} f(w_j)}
$$

Researches find this approach as the best for selecting negative examples   



# GloVe Word


$$
X_{ij} : \text{\# times } j \ \ \text{(the target word)} \quad \text{appears in context of } i \ \ \text{(the context word)} 
$$

$X_{ij}$ is a count that captures how often do words $i$ and $j$ appear with each other, or close to each other.

## Model

Using gradient descent

$$
\text{minimize} \huge \sum_i^{10000} \sum_j^{10000}  (\theta_i^T \, e_j + b_i + b'_j  - logX_{ij})^2
$$

- $f(X_{ij})$ is the weight function
	- If $X_{ij} = 0$, then $f(X_{ij}) = 0$ and we don't bother to calculate that pair avoiding $log(0)$ (negative infinity).
- There are various heuristic for choosing the weight function $f$.


# Sentiment classification

$$
\begin{array}{ccc}
x & \rightarrow & y \\
\text{The dessert is excellent.} & & \text{5 starts} \\
\text{Service was quite slow.} & & \text{2 starts} \\
\text{Good for a quick meal, but nothing special.} & & \text{3 starts} \\
\text{Completely lacking in good taste, good service, and good ambience.} & & \text{1 starts} 
\end{array}
$$


## Simple model

We just average the words of the sentence

![[Pasted image 20250806163355.png]]

**Disadvantages**
- This algorithm ignores word order. For example, the review: "Completely lacking in good taste, good service, and good ambience". The classifier probably thinks this is a good review because of the frequency of the word 'good'.

## RNN for sentiment classification

![[Pasted image 20250806163843.png]]

This model will be much better at taking word sequence into account and realize that things like "lacking in good taste" is a negative review, and "not good" is a negative review.

>[!note] Note
>Because your word embeddings can be trained from a much larger dataset, this will do a better job generalizing to maybe even new words not seen in your training set.


# Debiasing Word Embeddings

Examples of bias
- Man: Computer_Programmer as Woman:Homemaker
- Father:Doctor as Mother:Nurse

> [!warning] Bias
> Word embedding can reflect gender, ethnicity, age, sexual orientation, and other biases of the **text used to train the model**.


## Addressing bias in word embeddings

1. Identify bias direction
2. Neutralize: For every word that is not definitional, project to get rid of bias.
3. Equalize pairs

![[Pasted image 20250806174237.png]]



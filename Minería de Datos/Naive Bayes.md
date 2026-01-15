
# Introduction

To understand the naive Bayes classifier, we first look at the complete, or exact, Bayesian classifier. For each record to be classified:

1. Find all the other records with the same predictor profile (i.e., where the predictor values are the same).
2. Determine what classes the records belong to and which class is most prevalent.
3. Assign that class to the new record.


<h5>Cutoff Probability Method</h5>
1. Establish a cutoff probability for the class of interest above which we consider that a record belongs to that class.
2. Find all the training records with the same predictor profile as the new record (i.e., where the predictor values are the same).
3. Determine the probability that those records belong to the class of interest.
4. If that probability is above the cutoff probability, assign the new record to the class of interest.


==To classify a record, we compute its probability of belonging to each of the classes in this way then classify the record to the class that has the highest probability or use the cutoff probability to decide whether it should be assigned to the class of interest.==

> [!tip]
> The Bayesian classifier works only with categorical predictors. Numerical predictors must be binned and converted to categorical predictors



The Bayesian formula for the calculation of the probability that a record belongs to a class $C_i$ is as follow:

$$
P(C_i | x_1, \dots ,  x_p) = \frac{P(x_1, \dots ,  x_p|C_i)P(C_i)}{P(x_1, \dots ,  x_p|C_i)P(C_1) + \dots + P(x_1, \dots ,  x_p|C_m)P(C_m)}
$$

<h5>Difficulty</h5>
When the number of predictors gets larger ($\geq 20$) many of the records to be classified will be without exact matches.

## Naive Bayes

In the naive Bayes solution, we no longer restrict the probability calculation to those records that match the record to be classified.  Instead we use the entire dataset

The *naive Bayes modification* (for the basic classification procedure) is as follow:

1. For class $C_1$, estimate the individual conditional probabilities for each predictor $P(x_j|C1)$, these are the probabilities that the predictor value in the record to be classified occurs in class $C_1$. For example, for $X_1$  this probability is estimated by the proportion of $x_1$ values among the $C_1$ records in the training set.
	
2. Multiply these probabilities by each other, then by the proportion of records belonging to class $C_1$.
3. Repeat Steps 1 and 2 for all the classes.
4. Estimate a probability for class $C_i$ by taking the value calculated in Step 2 for class $C_i$ and dividing it by the sum of such values for all classes.
5. Assign the record to the class with the highest probability for this set of predictor values.

$$
P_{\text{nb}}(C_1 | x_1, \dots ,  x_p) = \dfrac{P(C_1)[P(x_1|C_1)P(x_2|C_1) \cdots P(x_p|C_1)]}{P(C_1)[P(x_1|C_1)P(x_2|C_1) \cdots P(x_p|C_1)] + \cdots + P(C_m)[P(x_1|C_m)P(x_2|C_m) \cdots P(x_p|C_m)]}
$$


### Using the Cutoff Probability Method

1. Establish a cutoff probability for the class of interest above which we consider that a record belongs to that class.
2. For the class of interest, compute the probability that each individual predictor value in the record to be classified occurs in the training data
3. Multiply these probabilities times each other, then times the proportion of records belonging to the class of interest.
4. Estimate the probability for the class of interest by taking the value calculated in Step 3 for the class of interest and dividing it by the sum of the similar values of all classes.
5. If this value falls above the cutoff, assign the new record to the class of interest, otherwise not.
6. Adjust the cutoff value as needed, as a parameter of the model.


### Example

<h5>Predicting fraudulent financial reports, two predictors</h5>

Consider the 10 customers of the accounting firm listed in Table 8.2. For each customer, we have information on whether it had prior legal trouble, whether it is a small or large company, and whether the financial report was found to be fraudulent or truthful. Using this information, we will calculate the conditional probability of fraud, given each of the four possible combinations {y, small}, {y, large}, {n, small}, {n, large}.


**Table 8.2 Information on 10 Companies**

| Company | Prior legal trouble | Company size | Status |
|---|---|---|---|
| 1    | Yes    | Small    | Truthful   |
| 2    | No    | Small    | Truthful   |
| 3    | No    | Large    | Truthful   |
| 4    | No    | Large    | Truthful   |
| 5    | No    | Small    | Truthful   |
| 6    | No    | Small    | Truthful   |
| 7    | Yes    | Small    | Fraudulent   |
| 8    | Yes    | Large    | Fraudulent   |
| 9    | No    | Large    | Fraudulent   |
| 10    | Yes    | Large    | Fraudulent   |

**Complete (Exact) Bayes Calculations:** The probabilities are computed as


$$
\begin{align*}
P(\text{fraudulent} \mid \text{PriorLegal} = y, \text{Size} = \text{small}) &= 0.5 \\ \\

P(\text{fraudulent} \mid \text{PriorLegal} = y, \text{Size} = \text{large}) &= 1 \\ \\

P(\text{fraudulent} \mid \text{PriorLegal} = n, \text{Size} = \text{small}) &= 0 \\ \\

P(\text{fraudulent} \mid \text{PriorLegal} = n, \text{Size} = \text{large}) &= 0.33 \\ \\
\end{align*}
$$

**Naive Bayes Calculations**

$$
\begin{align*}

P_{nb}(\text{fraudulent} \mid \text{PriorLegal} = y, \text{Size} = \text{small}) &= 0.53 \\ \\

P_{nb}(\text{fraudulent} \mid \text{PriorLegal} = y, \text{Size} = \text{large}) &= 0.87 \\ \\

P_{nb}(\text{fraudulent} \mid \text{PriorLegal} = n, \text{Size} = \text{small}) &= 0.07 \\ \\

P_{nb}(\text{fraudulent} \mid \text{PriorLegal} = n, \text{Size} = \text{large}) &= 0.31 \\ \\

\end{align*}
$$
Note how close these naive Bayes probabilities are to the exact Bayes probabilities. Although they are not equal, both would lead to exactly the same classification for a cutoff of $0.5$.


## Shortcomings

- Naive Bayes classifier requires a very large number of records to obtain good results.
- Where a predictor category is not present in the training data, naive Bayes assumes that a new record with that category of the predictor has zero probability.
- Good performance is obtained when the goal is classification or ranking of records according to their probability of belonging to a certain class. However, when the goal is to estimate the probability of class membership (propensity), this method provides very biased results.

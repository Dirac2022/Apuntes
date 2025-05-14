**Revisar**:
- [ ] Models for machine learning: https://developer.ibm.com/articles/cc-models-machine-learning/


**So what is the difference between machine learning and using statistical analysis to create an algorithm?**
An algorithm is a mathematical technique. With traditional programming, we take data and rules, and use these to develop an algorithm that will give us an answer. 

In the previous example, if we were using a traditional algorithm, we would take the data such as beats per minute and BMI, and use this data to create an algorithm that will determine whether the heart will fail or not. Essentially, it would be an if-then-else statement. When we submit inputs, we get answers based on what the algorithm we determined is, and this algorithm will not change.

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Artificial Intelligence\imgs\traditional programming.png">
    <figcaption></figcaption>
    </figure>
</div>

	
Machine Learning, on the other hand, takes data and answers and creates the algorithm. Instead of getting answers in the end, we already have the answers. What we get is a set of rules that determine what the machine learning model will be. The model determines the rules, and the if-then-else statement when it gets the inputs.

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Artificial Intelligence\imgs\ml process.png">
    <figcaption></figcaption>
    </figure>
</div>

 Essentially, what the model does is determine what the parameters are in a traditional algorithm, and instead of deciding arbitrarily that beats per minute plus BMI equals a certain result, we use the model to determine what the logic will be.

>[!info]
> Machine Learning relies on defining behavioral rules by examining and comparing large datasets to find common patterns


# Types of machine learning
A machine learning model is a algorithm used to find patterns in the data without the programmer having to explicitly program these patterns.

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Artificial Intelligence\imgs\types of ml.png">
    <figcaption></figcaption>
    </figure>
</div>
## Supervised Learning
We can provide a machine learning program with a large volume of pictures of birds and train the model to return the label "bird" whenever it has provided a picture of a bird. We can also create a label for "cat" and provide pictures of cats to train on. When the machine model is shown a picture of a cat or a bird, it will label the picture with some level of confidence. This type of Machine Learning is called Supervised Learning, where an algorithm is trained on human-labeled data. The more samples you provide a supervised learning algorithm, the more precise it becomes in classifying new data
## Unsupervised Learning
Unsupervised Learning, another type of machine language, relies on giving the algorithm unlabeled data and letting it find patterns by itself. You provide the input but not labels, and let the machine infer qualities that algorithm ingests unlabeled data, draws inferences, and finds patterns. This type of learning can be useful for clustering data, where data is grouped according to how similar it is to its neighbors and dissimilar to everything else. Once the data is clustered, different techniques can be used to explore that data and look for patterns. For instance, you provide a machine learning algorithm with a constant stream of network traffic and let it independently learn the baseline, normal network activity, as well as the outlier and possibly malicious behavior happening on the network
## Reinforcement Learning
Reinforcement Learning, relies on providing a machine learning algorithm with a set of rules and constraints, and letting it learn how to achieve its goals. You define the state, the desired goal, allowed actions, and constraints. The algorithm figures out how to achieve the goal by trying different combinations of allowed actions, and is rewarded or punished depending on whether the decision was a good one. The algorithm tries its best to maximize its rewards within the constraints provided. You could use Reinforcement Learning to teach a machine to play chess or navigate an obstacle course


# Supervised Learning

>[!info]  
>Supervised Learning refers to when we have class labels in the dataset and we use these to build the classification model. What this means is when we receive data, it has labels that say what the data represents.


## Categories
We can split supervised learning in three categories

### Regression
Regression models are built by looking at the relationships between features $x$ and the result $y$ where $y$ is a continuous variable. Essentially, Regression estimates continuous values.

### Neural Networks
Neural Networks refer to structures that imitate the structure of the human brain

### Classification
Classification focuses on discrete values it identifies. We can assign discrete class labels $y$ based on many input features $x$. In a previous example, given a set of features $x$, like beats per minute, body mass index, age and sex, the algorithm classifies the output $y$ as two categories, **True** or **False**, predicting whether the heart will fail or not. 

In other Classification models, we can classify results into more than two categories. For example, predicting whether a recipe is for an Indian, Chinese, Japanese, or Thai dish. 

Some forms of classification include 
- Decision trees, 
- Support Vector Machines, 
- Logistic Regression, 
- Random Forests. 

With Classification, we can extract features from the data. The features in this example would be beats per minute or age. **Features are distinctive properties of input patterns that help in determining the output categories or classes of output**. 

>[!tip]
>Classification is the process of predicting the class of given data points. 

Our classifier uses some training data to understand how given input variables relate to that class.


## Training
 Training refers to using a learning algorithm to determine and develop the parameters of your model. 
 While there are many algorithms to do this, in layman's terms, if you're training a model to predict whether the heart will fail or not, that is True or False values, you will be showing the algorithm some real-life data labeled True, then showing the algorithm again, some data labeled False, and you will be repeating this process with data having True or False values, that is whether the heart actually failed or not. 
 The algorithm modifies internal values until it has learned to tell from data that indicates heart failure that is True or not, that is False. 
 With Machine Learning, we typically take a dataset and split it into three sets, **Training**, **Validation** and **Test sets**. 
 - The Training subset is the data used to train the algorithm. 
 - The Validation subset is used to validate our results and fine-tune the algorithm's parameters.
 - The Testing data is the data the model has never seen before and used to evaluate how good our model is. We can then indicate how good the model is using terms like, **accuracy**, **precision** and **recall**.

# Unsupervised Learning


>[!info]
>Unsupervised Learning, we don't have class labels and we must discover class labels from unstructured data. This could involve things such as deep learning looking at pictures to train models. Things like this are typically done with something called clustering.


# Reinforcement Learning

>[!info]
>Reinforcement Learning is a different subset, and what this does is it uses a reward function to penalize bad actions or reward good actions.


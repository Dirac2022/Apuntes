


# Regular expressions and Word tokenization

## Intro to regular expressions
[[Regex]]

**What is Natural Language Processing?

- Field of study focused on making sense of language
	- Using statistics and computers
- NLP applications include:
	- Chatbots
	- Translation
	- Sentiment Analysis
	- etc.

**What are regular expresssions?**
- String with a special syntax
- Allow us to match patterns in other strings

```python
import re

re.match('abc', 'abcdef')
# <_sre.SRE_Match object; span=(0, 3), match='abc'>

word_regex = '\w+'
re.match(word_regex, 'hi there')
# <_sre.SRE_Match object; span=(0, 2), match='hi'>
```


<h4>Common regex patterns</h4>

| pattern    | matches         | example      |
| ---------- | --------------- | ------------ |
| `\w+`      | word            | 'Magic'      |
| `\d`       | digit           | 9            |
| `\s`       | space           | ' '          |
| `.*`       | wildcard        | 'username74' |
| `+` or `*` | greedy match    | 'aaaaa'      |
| `\S`       | not space       | 'no_spaces'  |
| `[a-z]`    | lowercase group | 'abcdefg'    |


<h4>Python's re module</h4>

- `re` module 
- `split` : split a string on regex 
- `findall` : Find all patterns in a string 
- `search` : search for a pattern match : 
- `match` : an entire string or substring based on a pattern 
- Pattern first, and the string second May return an iterator, string, or match object


## Introduction to tokenization

- Turning a string or document into **tokens** (smaller chunks)
- One step in preparing a text for NLP
- Many different theories and rules
- You can create your own rules using regular expressions
- Some examples
	- Breaking out words or sentences
	- Separating punctuation
	- Separating all hashtags in a tweet


<h4>nltk library</h4>
`nltk` : natural language toolkit

```python
import nltk

# Download required resources for word_tokenize (Recent versions)
nltk.download('punkt')
nltk.download('punk_tab')

from nltk.tokenize import word_tokenize
word_tokenize('Hi there!') # word_tokenize returns a list of word tokens (str)
# ['Hi', 'there', '!']
```

- `sent_tokenize` : tokenize a document into sentences
	- `sent_tokenize(text, language='english')`
	
- `regexp_tokenize` : tokenize a string or document based on a regular expression pattern
	- `regexp_tokenize(text, pattern)`
	
- `TweetTokenizer` : special class just for tweet tokenization, allowing you to separate hashtags, mentions and lots of exclamation points!!!

## Advanced tokenization with regex

<h4>Regex groups using or '|'</h4>

- OR is represented using `|`
- You can define a group using `()`
- You can define explicit character ranges using `[]`

```python
import re
match_digits_and_words('(\d+|\w+)')
re.findall(match_digits_and_words, 'He has 11 cats.')
# ['He', 'has', '11', 'cats']
```


<h4>Regex ranges and groups</h4>

| pattern        | matches                                            | example          |
| -------------- | -------------------------------------------------- | ---------------- |
| `[A-Za-z]+`    | upper and lowercase English alphabet               | 'ABCDEFghijk'    |
| `[0-9]`        | numbers from 0 to 9                                | 9                |
| `[A-Za-z\-\.]` | upper and lowercase English alphabet , `-` and `.` | 'My-website.com' |
| `(a-z)`        | a, `-` and z                                       | 'a-z'            |
| `(\s+\|,)`     | spaces or a comma                                  | ','              |

```python
import re
my_str = 'match lowercase spaces nums like 12, but no commas'
re.match('[a-z0-9 ]+', my_str)
# <_sre.SRE_Match object; span=(0, 35), match='match lowercase spaces nums like 12'>
```



---

# Simple topic identification

## Word counts with bag-of-words


**Bag-of-words**
- Basic method for finding topics in a text.
- Need to first create tokens using tokenization ... and then count up all the tokens.
- The more frequent a word, the more important it might be.
- Can be a great way to determine the significant words in a text.

**Example**

- Text: *The cat is in the box. The cat likes the box. The box is over the cat.*
- Bag of words (stripped punctuation):
	- *The*: 3, *box*: 3
	- *cat*: 3. *the*: 3
	- ...

```python
import nltk

# Download required resources for word_tokenize (Recent versions)
nltk.download('punkt')
nltk.download('punk_tab')

from nltk.tokenize import word_tokenize
from collections import Counter
Counter(word_tokenize("""The cat is in the box. The cat likes the box. The box is over the cat.""")) # Returns a Counter objects, like a dictionary 'word': frequency (int)
```

Output:

```
Counter({'.': 3, 
'The': 3, 
'box': 3, 
'cat': 3, 
'in': 1, 
... 
'the': 3}) 
```
f
```python
counter = Counter(word_tokenize("""The cat is in the box. The cat likes the box. The box is over the cat."""))

counter.most_common(2) # Return a list of tuples ('word', frequency)
# [('The', 3), ('box', 3)]
```



## Simple text preprocessing


**Why preprocess?**

- Helps make for better input data
	- When performing machine learning or other statistical methods.
- Examples:
	- Tokenization to create a bag of words
	- Lowercasing words
- Lemmatization/Stemming
	- Shorten words to their root stems.
- Removing stop words, punctuation, or unwanted tokens.
- Good to experiment with different approaches.

**Example**
- Input text: *Cats, dogs and birds are common pets. So are fish*
- Output tokens: cat, dog, bird, common, pet, fish.


```python
import nltk

nltk.download('punkt')
nltk.download('punkt_tab')
nltk.download('stopwords')

from nltk.tokenize import word_tokenize
from nltk.corpus import stopwords
from collections import Counter
text = """The cat is in the box. The cat likes the box.  
The box is over the cat."""
tokens = [w for w in word_tokenize(text.lower()) if w.isalpha()]
no_stops = [t for t in tokens if t not in stopwords.words('english')]
Counter(no_stops).most_common(2)
# Output
# [('cat', 3), ('box', 3)]
```



### WordNetLemmatizer

- `WordNetLemmatizer` is an NLTK tool that reduces words to their lemma using the **WordNet** lexical database.
- Unlike stemming, it returns valid dictionary words rather than chopped roots.
- It can take a `pos` argument to specify the part of speech for better accuracy.
	- For example, *"better"* with `pos='a'` → *"good"*.
	
- It’s widely used in NLP to normalize words and reduce morphological variations.


```python
# Import WordNetLemmatizer
from nltk.stem import WordNetLemmatizer

# Retain alphabetic words: alpha_only
alpha_only = [t for t in lower_tokens if t.isalpha()]

# Remove all stop words: no_stops
no_stops = [t for t in alpha_only if t not in english_stops]

# Instantiate the WordNetLemmatizer
wordnet_lemmatizer = WordNetLemmatizer()

# Lemmatize all tokens into a new list: lemmatized
lemmatized = [wordnet_lemmatizer.lemmatize(t) for t in no_stops]

# Create the bag-of-words: bow
bow = Counter(lemmatized)

# Print the 10 most common tokens
print(bow.most_common(10))
# [('debugging', 40), ('system', 25), ('bug', 17), ('software', 16), ...
```




## Introduction to gensim

**What is gensim?**
- Popular open-source NLP library
- Uses top academic models to perform complex tasks
	- Building document or **word vectors**
	- Performing topic identification and document comparison


<div style="text-align:center">
<img src="https://polakowo.io/datadocs/assets/1*jpnKO5X0Ii8PVdQYFO2z1Q.png" width=500/>
</div>



Gensim allows you to build corpora and dictionaries using simple classes and functions

```python
from gensim.corpora.dictionary import Dictionary
from nltk.tokenize import word_tokenize
my_documents = ['The movie was about a spaceship and aliens.',
'I really liked the movie!',
'Awesome action scenes, but boring characters.',
'The movie was awful! I hate alien films.',
'Space is cool! I liked the movie.',
'More space films, please!',]

tokenize_docs = [word_tokenize(doc.lower()) for doc in my_documents]
dictionary = Dictionary(tokenized_docs) # A gensim Dictionaty object
dictionary.token2id # Returns a dictionary 'token': id (int)
```

Output:

```
{'!': 11, 
',': 17, 
'.': 7, 
'a': 2, 
'about': 4, 
...}
```


<h5>Creating a gensim corpus</h5>

```python
# dictionary.doc1box(doc) create a list of tuples, each tuple is ('token_id', frequency)
corpus = [dictionary.doc2box(doc) for doc in tokenized_docs]
corpus
```

```
[[(0, 1), (1, 1), (2, 1), (3, 1), (4, 1), (5, 1), (6, 1), (7, 1), (8, 1)], 
[(0, 1), (1, 1), (9, 1), (10, 1), (11, 1), (12, 1)], 
...] 
```


- `gensim` models can be easily saved, updated, and reused.
- Our dictionary can also be updated.
- This more advanced and feature rich bag-of-words ca be used in future exercises.



## Tf-idf with gensim

- Term frequency - inverse document frequency
- Allows you to determine the most important words in each document
- Each corpus may have shared words beyond just stopwords
- These words should be down-weight in importance
- Example from astronomy: 'Sly'
- Ensures most common words don't show up as key words
- Keep document specific frequent words weighted high

**Tf-idf formula**

$$
w_{i ,\ j} = tf_{i,\ j} * \text{log}\dfrac{N}{df_i}
$$
- $w_{i ,\ j}$  = $tf_{i,\ j}$ weight for token $i$ in document $j$
- $tf_{i,\ j}$ = number of occurences of token $i$ in document $j$
- $df_i$ = number of documents that contain token $i$
- $N$ = total number of documents

**Example**
The word *computer* appears five times in a document containing 100 words. Given a corpus containing 200 documents, with 20 documents mentioning the word *computer*.

$$
w = \dfrac{5}{100} \text{log}(\dfrac{200}{20})
$$


- The weight will be low if the term doesn't appear often in the document because the $tf$ variable will then be low
- If the total number of documents $N$ divided by the number of documents that have the term $df_i$ is close to one, then our logarithm will be close to zero.
- Words that occurs across many or all documents will have a very low *tf-idf* weight.
- If the words only occurs in a few documents, that logarithm will return a higher number

<h5>Tf-idf with gensim</h5>

```python
from gensim.models.tfidfmodel import TfidfModel
# Trains a TF-IDF model using the whole `corpus` in BOW format.  
# Computes and stores the IDF values for each term in the dictionary.
tfidf = TfidfModel(corpus) # Corpus type: List[List[Tuple[token_id (int), count (int)]]]

# Takes the BOW of the second document and transforms it into TF-IDF weights.  
# Returns a list of `(word_id, tfidf_score)` tuples for that document.
tfidf[corpus[1]]
```


Output:

```
[(0, 0.1746298276735174), 
(1, 0.1746298276735174), 
(9, 0.29853166221463673), 
(10, 0.7716931521027908), 
... 
] 
```

# Named-entity recognition

- NLP task to identify important named entities in the text
	- People, places, organizations
	- Dates, states, works of art
	- ... and other categories!
- Can be used alongside topic identification
	- ... or on its own!
- Who? What? When? Where?


<div style="font-family: sans-serif; line-height: 1.6; color:black; background-color:white; padding: 2px">
    <p>
        In <span style="color: #FF1493;">1917</span>, <span style="color: #800000;">Einstein</span> applied the general theory of relativity to model the large-scale structure of the universe. He was visiting the <span style="color: #800080;">United States</span> when <span style="color: #800000;">Adolf Hitler</span> came to power in <span style="color: #FF1493;">1933</span> and did not go back to <span style="color: #800080;">Germany</span>, where he had been a professor at the <span style="color: #FF00FF;">Berlin Academy of Sciences</span>. He settled in the <span style="color: #800080;">U.S.</span>, becoming an American citizen in <span style="color: #FF1493;">1940</span>. On the eve of World War II, he endorsed a letter to President <span style="color: #800000;">Franklin D. Roosevelt</span> alerting him to the potential development of "extremely powerful bombs of a new type" and recommending that the <span style="color: #800080;">U.S.</span> begin similar research. This eventually led to what would become the <span style="color: #FF00FF;">Manhattan Project</span>. <span style="color: #800000;">Einstein</span> supported defending the Allied forces, but largely denounced using the new discovery of nuclear fission as a weapon. Later, with the British philosopher <span style="color: #800000;">Bertrand Russell</span>, <span style="color: #800000;">Einstein</span> signed the <span style="color: #FF00FF;">Russell-Einstein Manifesto</span>, which highlighted the danger of nuclear weapons. <span style="color: #800000;">Einstein</span> was affiliated with the <span style="color: #FF00FF;">Institute for Advanced Study</span> in <span style="color: #800080;">Princeton, New Jersey</span>, until his death in <span style="color: #FF1493;">1955</span>.
    </p>

    <p>
        <strong>Tag colours:</strong><br>
        <span style="color: #800080;">LOCATION</span>
        <span style="color: #FFA500;">TIME</span>
        <span style="color: #800000;">PERSON</span>
        <span style="color: #FF00FF;">ORGANIZATION</span>
        <span style="color: #FF1493;">DATE</span>
    </p>
</div>


<h5>nltk and the Stanford CoreNLP library</h5>
- Integrated into Python via `nltk`
- Java based
- Support for NER as well as coreference and dependency trees

```python
import nltk
sentence = '''In New York, I like to ride the Metro to visit MOMA and some restaurants rated well by Ruth Reichl.'''
tokenized_sent = nltk.word_tokenize(sentence)
# Applies a Part-of-Speech (POS) tagger to label each token with its grammatical category, using the Penn Treebank tagset
tagged_sent = nltk.post_tag(tokenize_sent) # List of tuples (token, tag)
tagged_sent[:3]
# Output
# [('In', 'IN'), ('New', 'NNP'), ('York', 'NNP')]
```

Examples: 
- `IN` = preposition, 
- `NNP` = proper noun, 
- `PRP` = pronoun, 
- `VBP` = verb (present), 
- `DT` = determiner, etc.


> [!tip] Part-of-Speech (POS)**
> 
> * A **Part-of-Speech** is a *grammatical category* that tells you the role of a word in a sentence.
> * Examples in English: noun, verb, adjective, adverb, pronoun, preposition, conjunction, determiner, etc.
> * In NLP, a **POS tagger** is a model that automatically assigns each token a POS label.
> * Example:
>   `"Dogs run fast"` →
>   `[("Dogs", **NNS**), ("run", **VBP**), ("fast", **RB**)]`
>   Here `NNS` = plural noun, `VBP` = present verb, `RB` = adverb.
> 


> [!tip] Penn Treebank Tagset
> 
> * The **Penn Treebank** is a large annotated corpus of English text created by the University of Pennsylvania.
> * Its **tagset** is the standardized list of short codes used to label words in POS tagging.
> * These codes are **more specific** than just “noun” or “verb” — they include tense, number, and type.
> * Examples from the tagset:
> 
>   * **NN** → noun, singular (“cat”)
>   * **NNS** → noun, plural (“cats”)
>   * **VB** → verb, base form (“run”)
>   * **VBD** → verb, past tense (“ran”)
>   * **JJ** → adjective (“happy”)
>   * **RB** → adverb (“quickly”)
>   * **IN** → preposition/subordinating conjunction (“in”, “because”)
> 



<h5>Using nltk to find named entities in an article</h5>

Imports: 

```python
import nltk
from nltk.tokenize import sent_tokenize, word_tokenize

# Descargar todos los recursos necesarios para NLTK 3.8+
nltk.download('punkt')
nltk.download('punkt_tab')
nltk.download('averaged_perceptron_tagger')
nltk.download('averaged_perceptron_tagger_eng')
nltk.download('maxent_ne_chunker')
nltk.download('maxent_ne_chunker_tab')  # NUEVO para NLTK 3.8+
nltk.download('words')
```

```python

# Texto de ejemplo
article = '''In New York, I like to ride the Metro to
visit MOMA and some restaurants rated
well by Ruth Reichl.'''

# Tokenize the article into sentences: sentences
sentences = sent_tokenize(article)

# Tokenize each sentence into words: token_sentences
token_sentences = [word_tokenize(sent) for sent in sentences]

# Tag each tokenized sentence into parts of speech: pos_sentences
# A list of list of tuples ('token', 'category')
pos_sentences = [nltk.pos_tag(sent) for sent in token_sentences] 

# Create the named entity chunks: chunked_sentences
# Is a generator that yields for each sentence a nltk.tree
# binary=True: no classify entities into specific types like PERSON, ORGANIZATION, etc
chunked_sentences = nltk.ne_chunk_sents(pos_sentences, binary=True)

# Test for stems of the tree with 'NE' tags
for sent in chunked_sentences:
    for chunk in sent:
        if hasattr(chunk, "label") and chunk.label() == "NE":
            print(chunk)
# Output
# (NE New/NNP York/NNP)
# (NE Metro/NNP)
# (NE MOMA/NNP)
# (NE Ruth/NNP Reichl/NNP)
```


> [!important] NLTK named entity chunk tree
> 1. An NLTK **named entity chunk tree** (`Tree`) represents a sentence where tokens are either plain `(word, POS)` pairs or grouped inside subtrees labeled with `"NE"` when they are part of a named entity.
> 2. The root `(S ...)` contains the full sentence, while each `(NE ...)` node groups one or more proper nouns (e.g., people, locations, organizations) detected by the chunker.
> 3. Each token inside the tree keeps its **word** and **POS tag**, allowing you to know both the syntactic role and whether it belongs to an entity.

---

**Example explained**

```scss
(S                                      # root: Tree(label='S') – the whole sentence
  (NE In/IN New/NNP York/NNP)           # subtree: NE – leaves = [('In','IN'), ('New','NNP'), ('York','NNP')]
  ,/,                                   # leaf: (',', ',') – punctuation
  I/PRP                                 # leaf: ('I','PRP') – pronoun
  like/VBP                              # leaf: ('like','VBP') – verb
  to/TO                                 # leaf: ('to','TO') – infinitive marker
  ride/VB                               # leaf: ('ride','VB')
  the/DT                                # leaf: ('the','DT')
  (NE Metro/NNP)                        # subtree: NE – leaves = [('Metro','NNP')]
  to/TO                                 # leaf: ('to','TO')
  visit/VB                              # leaf: ('visit','VB')
  (NE MOMA/NNP)                         # subtree: NE – leaves = [('MOMA','NNP')]
  and/CC                                # leaf: ('and','CC')
  some/DT                               # leaf: ('some','DT')
  restaurants/NNS                       # leaf: ('restaurants','NNS')
  rated/VBN                             # leaf: ('rated','VBN')
  well/RB                               # leaf: ('well','RB')
  by/IN                                 # leaf: ('by','IN')
  (NE Ruth/NNP Reichl/NNP)              # subtree: NE – leaves = [('Ruth','NNP'), ('Reichl','NNP')]
  ./.                                   # leaf: ('.','.') – punctuation
)
```

This means the sentence structure preserves both the **POS tagging** and the **named entity recognition** in a single hierarchical representation.



## Introduction to SpaCy

- NLP library similar to `gensim`, with different implementations
- Focus on creating NLP pipelines to generate models and corpora
- Open-source, with extra libraries and tools
	- Displacy: a visualization tool for viewing parse trees which uses Node-js to create interactive text


<h5>Displacy entity recognition visualizer</h5>
<div style="background-color:white; color:black">
  <p style="display: inline-block;">In</p>
  <span style="background-color: #ffd699; border: 1px solid #ffaa00; padding: 2px 4px; border-radius: 4px; margin: 0 5px; display: inline-block;">
    New York
    <span style="font-size: 0.7em; vertical-align: super; color: #ff8800;">GPE</span>
  </span>
  <p style="display: inline-block;">, I like to ride the Metro to visit</p>
  <span style="background-color: #b3e6ff; border: 1px solid #4da6ff; padding: 2px 4px; border-radius: 4px; margin: 0 5px; display: inline-block;">
    MOMA
    <span style="font-size: 0.7em; vertical-align: super; color: #0077cc;">ORG</span>
  </span>
  <p style="display: inline-block;">and some restaurants rated well by</p>
  <span style="background-color: #d9f7d9; border: 1px solid #8cd98c; padding: 2px 4px; border-radius: 4px; margin: 0 5px; display: inline-block;">
    Ruth Reichl
    <span style="font-size: 0.7em; vertical-align: super; color: #5cb85c;">PERSON</span>
  </span>
</div>



```python
import spacy

# Loads the pre-trained English model (sm - small)
# Includes vocabulary, part-of-speech tagging, dependency parsing, and named entity recognition (NER)
nlp = spacy.load('en_core_web_sm')

# Process the given text through the nlp pipeline
# The result is a Doc object, which stores tokens, linguistic annotations, and recognized entities
doc = nlp("""Berlin is the capital of Germany; and the residence of Chancellor Angela Merkel.""")

# Returns a tuple of named entities
doc.ents
# (Berlin, Germany, Angela Merkel)

# Print the first entity and its label. GPE: Geo-Political Entity
print(doc.ents[0], doc.ents[0].label_)
# Berlin GPE
```




**Why use SpaCy for NER?**

- Easy pipeline creation
- Different entity types compared to nltk
- Informal language corpora
	- Easily find entities in Tweets and chat messages
- Quickly growing!



## Multilingual NER with polyglot

- NLP library which uses word vectors
- Vectors for many different language (> 130 languages)

<h5>Spanish NER with polyglot</h5>
```python
from polyglot.text import Text
text = """El presidente de la Generalitat de Cataluña, 
Carles Puigdemont, ha afirmado hoy a la alcaldesa  
de Madrid, Manuela Carmena, que en su etapa de  
alcalde de Girona (de julio de 2011 a enero de 2016)  
hizo una gran promoción de Madrid.""" 
ptext = Text(text)
ptext.entities
```

Output

```
I-ORG(['Generalitat', 'de']), 
I-LOC(['Generalitat', 'de', 'Cataluña']), 
I-PER(['Carles', 'Puigdemont']), 
I-LOC(['Madrid']), 
I-PER(['Manuela', 'Carmena']), 
I-LOC(['Girona']), 
I-LOC(['Madrid'])] 
```



# Building a "fake news" classifier

## Classifying fake news using Supervised Learning with NLP

**Supervised Learning is** a form of machine learning.
- Problem has predefined training data
- This data has a label (or outcome) you want the model to learn

<h5>Supervised learning with  NLP</h5>
- `scikit-learn:` Powerful open-source library
- How to create supervised learning data from text?
	- Use bag-of-words models or tf-idf as features


<h5>Supervised learning steps</h5>
- Collect and preprocess our data
- Determine a label
- Split data into training and test sets
- Extract features from the text to help predict the label
	- Bag-of-words vector built into `scikit-learn`
- Evaluate trained model using the test set



## Building word count vectors with scikit-learn

**Predicting movie genre**
- Dataset consisting of movie plots and corresponding genre
- Goal: Create bag-of-words vectors for the movie plots
	- Can we predict genre based on the words used in the plot summary?



**IMDB Movie Dataset**

| Plot                                               | Sci-Fi | Action |
| -------------------------------------------------- | ------ | ------ |
| In a post-apocalyptic world in human decay, a ...  | 1      | 0      |
| Mohei is a wandering swordsman. He arrives in ...  | 0      | 1      |
| #137 is a SCI/FI thriller about a girl, Marla, ... | 1      | 0      |

<h5>Count Vectorizer with Python</h5>

```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklean.feature_extraction.text import CountVectorizer

df = # Load data into DataFrame
y = df['Sci-Fi']
X_train, X_test, y_train, y_test = train_test_split(
	df['plot'], y, test_size=0.33, random_state=53
)

# 
count_vectorizer = CountVectorizer(stop_words='english')

# fit: learns the vocabulary (unique words) from training data
# transform: converts each document into a vector of words counts
count_train = count_vectorizer.fit_transform(X_train.values)
count_test = count_vectorizer.transform(X_test.values)


```


> [!tip] CountVectorizer
> `from sklearn.feature_extraction.text import CountVectorizer`
> Transform text into numeric vectors following the model of *bag-of-words*
> - Splits sentences into words
> - Builds a vocabulary of all unique words
> - Creates vectors with word counts for each document
> 
> Example
> 
> ```python
> cv = CountVectorizer()
> X = cv.fit_transform(['The cat sleeps', 'The dog barks'])
> print(cv.get_feature_names_out())
> print(X.toarray())
>```
> Output
> ```lua
> ['barks', 'cat', 'dog', 'sleeps', 'the']
> [[0 1 0 1 1]   # "The cat sleeps"
> [1 0 1 0 1]]  # "The dog barks"


## Training and testing a classification model with scikit-learn

### Naive Bayes Classifier

- Naive Bayes Model
	- Commonly used for testing NLP classifications problems
	- Basis in probability
- Given a particular piece of data, how likely is a particular outcome?
- Examples
	- If the plot has a spaceship, how likely is it to be sci-fi?
	- Given a spaceship **and** an alien, how likely **now** is it sci-fi?
- Each word from `CountVectorizer` acts as a feature
- Naive Bayes: Simple and effective

<h5>Naive Bayes with scikit-learn</h5>

```python
from sklearn.naive_bayes import MultinomialNB
from sklearn import metrics

nb_classifier = MultinomialNB()
nb_classifier.fit(count_train, y_train)
pred = nb_classifier.predict(count_test)
metrics.accuracy_score(y_test, pred)
```


<h5>Confusion matrix</h5>

```python
metrics.confusion_matrix(y_test, pred, labels=[0, 1])
# Output
# array([[6410, 563],
#        [864, 2242]])
```


|        | Action | Sci-Fi |
| ------ | ------ | ------ |
| Action | 6410   | 563    |
| Sci-Fi | 864    | 2242   |



## Simple NLP, complex problems


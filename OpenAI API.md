
# Introduction to the OpenAI API



**What is an API**

API stands for Application Programming Interface, and they act as messengers between software applications, taking a request to a system and receiving a response containing data or services. 

**The OpenAI API**

We can write code to interact with the OpenAI API and request the use of one of their models. 

Our request, in this case, will specify which model we want, the data for the model to use, and any other parameters to customize the model's behavior.

The response, containing the model result, is then returned.

## Making requests to the OpenAI API

Depending on the model or services required, APIs have different access points for users called **endpoints**. 

API authentication is usually in the form of providing a unique key containing an assortment of characters.

OpenAI API have cost associated with using their services. These cost are dependent on the model requested and the size of the model input and output.

<h5>Creating an API Key</h5>
1. Create an OpenAI account
2. Go to the API keys page
3. Create a new secret key

```python
from openai import OpenAI

# Create the OpenAI client
client = OpenAI(api_key='SOME_API_KEY')
 
 # Create a request to the Chat Completions endpoint
 response = client.chat.completions.create(
	 model='gpt-4o-mini',
	 messages=[{'role': 'user', 'content':'What is the OpenAI API'}]
 )
 
 print(response)
```


```
ChatCompletion(id='chatcmpl-AEcQbQekIzxcxVAKYVAjgUAXokgrl', choices=[Choice(finish_reason='length', index=0, logprobs=None, message=ChatCompletionMessage(content='The OpenAI API is a cloud based service provided by OpenAI that allows developers to integrate advanced AI models into their applications.', refusal=None, role='assistant', function_call=None, tool_calls=None))], created=1728047673, model='gpt-4o-mini-2024-07-18', object='chat.completion', service_tier=None, system_fingerprint='fp_f85bea6784', usage=CompletionUsage(completion_tokens=25, prompt_tokens=14, total_tokens=39, prompt_tokens_details={'cached_tokens': 0}, completion_tokens_details={'reasoning_tokens': 0}))
```


**Client**: configures environment for communication with API

The chat completions endpoints is used to send a series of messages representing a conversation to a model, which returns a response.

The response from the API is a `ChatCompletion` object, which has attributes for accesing different information. It has an `id` attribute, `choices`, `created`, `model` and other atributes below.

The response message is located under the `.choices` attribute.

```python
print(response.choices) # A list with a single element
```

```
[Choice(finish_reason='length', index=0, logprobs=None,
 message=ChatCompletionMessage(content='The OpenAI API is a cloud
based service provided by OpenAI that allows developers to integrate
 advanced AI models into their applications.', refusal=None,
 role='assistant', function_call=None, tool_calls=None))]
```

The message is located underneath the `.message` attribute

```python
print(response.choices[0].message)
```

```
ChatCompletionMessage(content='The OpenAI API is a cloud-based
 service provided by OpenAI that allows developers to integrate
 advanced AI models into their applications.', refusal=None,
 role='assistant', function_call=None, tool_calls=None)
```

We need to acces the `ChatCompletion` `.message.content` attribute to retrieve the message

```python
print(response.choices[0].message.content)
```

```
The OpenAI API is a cloud-based service provided by OpenAI that
 allows developers to integrate advanced AI models into their
 applications.
```


# Prompting OpenAI Models


## Summarizing and editing text

- **Text editing**
- **Text summarization**

### Controlling response length

By default, the API limits the response length. the `max_completion_tokens` can be used to control the maximum length of the response, shortening or lengthening it.

```python
response = client.chat.completions.create(
	model='gpt-4o-mini',
	messages=[{
		'role': 'user',
		'content': 'Write a haiku about AI.'
	}],
	max_completion_token=5
)
```

```
AI so powerful
Computers
```


**Tokens**: units of text that help the AI understand and interpreted text.


<h5>Calculating the cost</h5>
- Usage cost dependent on the model and the number of **tokens**
	- Model are priced by cost/tokens
	- Input and output tokens may have different costs
- Increasing `max_completions_tokens` increases cost


>[!warning]
>Always estimate cost before deploying AI features at scale.


## Text generation


<h5>How is the output generated</h5>
When we send a prompt to a chat model, it returns the text that it believes is most likely to complete the prompt, which it infers based on the data the model was developed on.

The results in the model are **non-deterministic**, so we cannot guarantee the exact same output every time.

### Controlling response randomness

We can control the amount of randomness in the response using the temperature parameter.

Ranges from `0` (highly deterministic) to `2` (very random)

```python
response = client.chat.completions.create(
	model='gpt-4o-mini',
	messages=[{
		'role': 'user',
		'content': 'Life is like a box of chocolates.'
	}],
	temperature=2
)

print(response.choices[0].message.content)
```


```
"...you never know what you're gonna get." That quote reminds us of the unpredictability of life and the diverse set of experiences we might encounter. Whether sweet, nutty, bitter, or flashy, life holds a treasure trove of surprises.
```

## Shot prompting


**Shot prompting**: including examples to guide AI responses

- **Zero-shot**: no examples, just instructions
- **One-shot**: one example guides the response
- **Few-shot**: multiple examples provide more context


<h5>Zero-shot prompting</h5>

```python
 prompt = """Classify sentiment as 1-5 (bad-good) in the following statements: 
1. Meal was decent, but I've had better. 
2. My food was delayed, but drinks were good. 
""" 

...
```

```
1. Meal was decent, but I've had better. - 3 (Neutral) 
2. My food was delayed, but drinks were good. - 3 (Neutral) 
```


<h5>One-shot prompting</h5>

```python
 prompt = """Classify sentiment as 1-5 (bad-good) in the following statements: 
1. The service was very slow -> 1 
2. Meal was decent, but I've had better. -> 
3. My food was delayed, but drinks were good. -> 
""" 
```

```
1. The service was very slow -> 1 
2. Meal was decent, but I've had better. -> 3 
3. My food was delayed, but drinks were good. -> 4 
```

<h5>Few-shot prompting</h5>

```python
prompt = """Classify sentiment as 1-5 (bad-good) in the following statements:
 1. The service was very slow -> 1 
2. The steak was awfully good! -> 5 
3. It was ok, no massive complaints. -> 3 
4. Meal was decent, but I've had better. -> 
5. My food was delayed, but drinks were good. -> 
""" 
```

```
1. The service was very slow -> 1 
2. The steak was awfully good! -> 5 
3. It was ok, no massive complaints. -> 3 
4. Meal was decent, but I've had better. -> 4 
5. My food was delayed, but drinks were good. -> 3 
```

# Building Conversations with the OpenAI API


## Chat roles and system messages

<h5>Chat Completions</h5>

**Single-turn task**
- Text generation
- Text transformation
- Classification


With Chat Completion models, it's possible to also have multi-turn conversations, so we can build on our previous prompts depending on how the model responds.

### Roles

- **System**: controls assistant's *behavior*.
	- Sets the overall behavior, tone, or personality of the assistant. It’s usually defined once at the start of the conversation.  
    _Example:_
    
```json
{ "role": "system", "content": "You are a friendly travel guide." }
```
    
- **User**: *instruct* the assistant.
	- Represents the human asking questions or giving instructions. Every new request from the end user goes here.  
    _Example:_
    
```json
{ "role": "user", "content": "What is the best place to visit in Paris?" }
```
    
- **Assistant**: *response* to user instruction.
	- Contains the AI’s replies to the user. 
	- It can also be pre-written by the developer to show example interactions.  
    _Example:_
    
```json
{ "role": "assistant", "content": "The Eiffel Tower is one of the best places to visit in Paris." }
```


A typical chat request for a single-turn task

<h5>Request setup</h5>

```python
response = client.chat.completions.create(
	model='gpt-4o-mini',
	messages=[{'role': 'user', 'content': prompt}]
)
```

To include additional messages, we extend this messages list to include multiple dictionaries each with their own role and content.


```python
messages = [
	{
		'role':'system',
		'content': 
	}
]
```


### Mitigating misuse

One of the most popular uses of system messages is to add ***guardrails***, which places restrictions on model outputs.

<h5>Mitigating misuse with system messages</h5>

```python
sys_msg = """
You are finance education assistant that helps students study for exams.
If you are asked for specific, real-world financial advice with risk to their
finances, respond with:
I'm sorry, I am not allowed to provide financial advice.
"""
```

```python
response = client.chat.completions.create(
	model='gpt-4o-mini',
	messages=[{'role': 'system',
				'content': sys_msg},
				{'role': 'user',
				'content': 'Which stocks should I invest in?'}]
)

print(response.choices[0].message.content)
```

```
I'm sorry, I am not allowed to provide financial advice.
```


## Using the assistant role

### Providing examples

Assistant messages are primarily used for providing examples to the model.

- Steer model in the right direction
- Providing assistant messages is a more structured form of *shot-prompting*
- **Example**: Python Programming Tutor
	- Example user question and answers

This will give the application a better understanding of the desired style and tone of responses.

```python
response = client.chat.completions.create(
	model="gpt-4o-mini",
	messages=[
	{"role": "system",
	"content": "You are a Python programming tutor who speaks concisely."},
	{"role": "user"	, 
	"content": "How do you define a Python list?"},
	{"role": "assistant",
	"content": "Lists are defined by enclosing a comma-separated sequence of objects inside square brackets [ ]."},
	{"role": "user"	, 
	"content": "What is the difference between mutable and immutable objects?"}]
)
```


**The response**

```python
print(response.choices[0].message.content)
```

```
Mutable objects can be changed after creation (e.g., lists, dictionaries). Immutable objects cannot be altered once created (e.g., strings, tuples).
```


### System vs. assistant vs. user

We can even provide examples in the system message. So, where's the best place to provide examples?

**System**: Important template formatting
I the system must output specific information or in a certain format, add this to the system message.

```
Output the information in this format:
name | age | occupation
```

**Assistant**: example conversations
Example conversations should be provided as user-assistant pairs, as these will guide the model on how to continue the conversation in the same fashion

**User**: context required for the new input (often single-turn)

## Multi-turn conversations with GPT

### Building a conversation


![oai05.jpg (1081×179)](https://raw.githubusercontent.com/trenton3983/DataCamp/master/Images/2024-01-29_working_with_the_openai_api/oai05.jpg)

![oai06.jpg (1077×219)](https://raw.githubusercontent.com/trenton3983/DataCamp/master/Images/2024-01-29_working_with_the_openai_api/oai06.jpg)

![oai08.jpg (667×274)](https://raw.githubusercontent.com/trenton3983/DataCamp/master/Images/2024-01-29_working_with_the_openai_api/oai08.jpg)


![oai09.jpg (1054×285)](https://raw.githubusercontent.com/trenton3983/DataCamp/master/Images/2024-01-29_working_with_the_openai_api/oai09.jpg)


<h5>Coding a conversation</h5>

```python
messages = [{"role": "system",
	"content": "You are a data science tutor who provides short, simple explanations."}]
user_qs = ["Why is Python so popular?", "Summarize this in one sentence."]

for q in user_qs:
	print("User:", q)
	user_dict = {"role": "user", "content": q}
	messages.append(user_dict)
	
	response = client.chat.completions.create(
		model='gpt-4o-mini',
		messages=messages
	)
	
	assistant_dict = {'role': 'asistant', 
					'content': response.choices[0].message.content}
	messages.append(assistant_dict)
	print("Assistant: ", response.choices[0].message.content, "\n")
```

```
User: Why is Python so popular?
Assistant: Python is popular for many reasons, including its simplicity,
versatility, and wide range of available libraries. It has a relatively
easy-to-learn syntax that makes it accessible to beginners and experts alike. It
can be used for a variety of tasks, such as data analysis, web development,
scientific computing, and machine learning. Additionally, Python has an active
community of developers who contribute to its development and share their
knowledge through online resources and forums.

User: Summarize this in one sentence.
Assistant: Python is popular due to its simplicity, versatility, wide range of
libraries, and active community of developers.
```


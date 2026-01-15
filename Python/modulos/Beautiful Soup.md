
[Beautiful Soup: Build a Web Scraper With Python – Real Python](https://realpython.com/beautiful-soup-web-scraper-python/)

Beautiful Soup is a Python library designed for parsing HTML and XML documents. It creates parse trees that make it straightforward to extract data from HTML documents you’ve scraped from the internet. Beautiful Soup is a useful tool in your [web scraping](https://realpython.com/python-web-scraping-practical-introduction/) toolkit, allowing you to conveniently extract specific information from HTML, even from complex static websites.

## What Is Web Scraping?

**Web scraping** is the process of gathering information from the internet. Even copying and pasting the lyrics of your favorite song can be considered a form of web scraping! However, the term “web scraping” usually refers to a process that involves automation. While some websites don’t like it when automatic scrapers gather their data, which can lead to [legal issues](https://realpython.com/podcasts/rpp/12/), others don’t mind it.

### Challenges of Web Scraping

The internet is a hot mess! Because of this, you’ll run into some challenges when scraping the web:

- **Variety:** Every website is different. While you’ll encounter general structures that repeat themselves, each website is unique and will need personal treatment if you want to extract the relevant information.
    
- **Durability:** Websites constantly change. Say you’ve built a shiny new web scraper that automatically cherry-picks what you want from your resource of interest. The first time you [run your script](https://realpython.com/run-python-scripts/), it works flawlessly. But when you run the same script a while later, you run into a discouraging and lengthy stack of [tracebacks](https://realpython.com/python-traceback/)!
    

The good news is that changes to websites are often small and incremental, so you’ll likely be able to update your scraper with minimal adjustments. You can set up [continuous integration](https://realpython.com/python-continuous-integration/) to run scraping tests periodically to ensure that your main script doesn’t break without your knowledge.


## Scrape the Fake Python Job Site

In this tutorial, you’ll build a web scraper that fetches Python software developer job listings from a [fake Python job site](https://realpython.github.io/fake-jobs/). It’s an example site with fake job postings that you can freely scrape to train your skills. Your web scraper will parse the HTML on the site to pick out the relevant information and filter that content for specific words.


### Step 1: Inspect Your Data Source

Before you write any Python code, you need to get to know the website that you want to scrape. Getting to know the website should be your first step for any web scraping project that you want to tackle. You’ll need to understand the site structure to extract the information relevant for you.

![](https://realpython.com/cdn-cgi/image/width=720,format=auto/https://files.realpython.com/media/bs4-fake-python-index.b76716592442.png)


<h5>Decipher the Information in URLs</h5>

You can encode a lot of [information in a URL](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Web_mechanics/What_is_a_URL). Becoming familiar with how URLs work and what they’re made of will help you on your web scraping journey. For example, you might find yourself on a details page that has the following URL:

`https://realpython.github.io/fake-jobs/jobs/senior-python-developer-0.html`

You can deconstruct the above URL into two main parts:

1. **The base URL** points to the main location of the web resource. In the example above, the base URL is `https://realpython.github.io/`.
2. **The path** to a specific resource location points to a unique job description. In the example above, the path is `fake-jobs/jobs/senior-python-developer-0.html`.


### Step 2: Scrape HTML Content From a Page

Now that you have an idea of what you’re working with, it’s time to start using Python. First, you’ll want to get the site’s HTML code into your Python script so that you can interact with it. For this task, you’ll use Python’s [Requests](https://realpython.com/python-requests/) library.

```sh
$ python -m pip install beautifulsoup4
```

```python
import requests

URL = "https://realpython.github.io/fake-jobs/"
page = requests.get(URL)

print(page.text)
```


```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Fake Python</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.2/css/bulma.min.css">
  </head>
  <body>
  <section class="section">
    <div class="container mb-5">
      <h1 class="title is-1">
...
```

When you run this code, it issues an [HTTP `GET` request](https://realpython.com/python-requests/#the-get-request) to the given URL. It retrieves the HTML data that the server sends back and stores that data in a Python object you called `page`.

If you [print](https://realpython.com/python-print/) the `.text` attribute of `page`, then you’ll notice that it looks just like the HTML you inspected earlier with your browser’s developer tools. You’ve successfully fetched the static site content from the internet! You now have access to the site’s HTML from within your Python script.

The HTML you’ll encounter will sometimes be confusing. Luckily, the HTML of this job board has descriptive **class names** on the elements that you’re interested in:

- **`class="title is-5"`** contains the title of the job posting.
- **`class="subtitle is-6 company"`** contains the name of the company that offers the position.
- **`class="location"`** contains the location where you’d be working.

If you ever get lost in a large pile of HTML, remember that you can always go back to your browser and use the [developer tools](https://realpython.com/beautiful-soup-web-scraper-python/#inspect-the-site-using-developer-tools) to further explore the HTML structure interactively.


### Login-Protected Websites

Some pages contain information that’s hidden behind a login. This means you’ll need an account to be able to scrape anything from the page. Just like you need to log in on your browser when you want to access content on such a page, you’ll also need to log in from your Python script.

The Requests library comes with the built-in capacity to [handle authentication](https://docs.python-requests.org/en/master/user/authentication/). With these techniques, you can log in to websites when making the HTTP request from your Python script and then scrape information that’s hidden behind a login.

### Dynamic Websites

Many modern websites don’t send back static HTML content like this practice site does. If you’re dealing with a **dynamic website**, then you could receive [JavaScript](https://realpython.com/python-vs-javascript/) code as a response. This code will look completely different from what you see when you inspect the same page with your browser’s developer tools.

**Note:** In this tutorial, the term **dynamic website** refers to a website that doesn’t return the same HTML that you see when viewing the page in your browser.

Dynamic websites are designed to provide their functionality in collaboration with the clients’ browsers. Instead of sending HTML pages, these apps send **JavaScript** code that instructs your browser to _create_ the desired HTML. 

Your browser will diligently execute the JavaScript code it receives from a server and create the DOM and HTML for you locally. However, if you request a dynamic website in your Python script, then you won’t get the HTML page content.

When you use Requests, you receive only what the server sends back. In the case of a dynamic website, you’ll end up with JavaScript code without the relevant data. The only way to go from that code to the content that you’re interested in is to _execute_ the code, just like your browser does. ==The Requests library can’t do that for you==, but there are other solutions that can:

- [**Requests-HTML**](https://github.com/psf/requests-html)
- [**Selenium**](https://realpython.com/modern-web-automation-with-python-and-selenium/) 

You won’t go deeper into scraping dynamically-generated content in this tutorial. If you need to scrape a dynamic website, then you can look into one of the options mentioned above.


## Step 3: Parse HTML Code With Beautiful Soup

[Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) is a Python library for parsing structured data. It allows you to interact with HTML in a similar way to how you interact with a web page using developer tools.

```sh
$ python -m pip install beautifulsoup4
```

```python
import requests
from bs4 import BeautifulSoup

URL = "https://realpython.github.io/fake-jobs/"
page = requests.get(URL)

soup = BeautifulSoup(page.content, 'html.parser')
```

You've create a `BeautifulSoup` object that takes `page.content` as input, which is the HTML content that you scraped earlier.

> [!note]
You’ll want to pass `.content` instead of `.text` to avoid problems with character encoding. The `.content` attribute holds raw bytes, which [Python’s built-in HTML parser](https://docs.python.org/3/library/html.parser.html) can decode better than the text representation you printed earlier using the `.text` attribute.

The second argument that you pass to the [class constructor](https://realpython.com/python-class-constructor/), `"html.parser"`, makes sure that you use [an appropriate parser](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#differences-between-parsers) for HTML content.


### Find Elements by ID

In an HTML web page, every element can have an `id` attribute assigned. The `id` attribute makes the element uniquely identifiable on the page. You can begin to parse your page by selecting a specific element by its ID.

Identify the HTML object that contains all the job posting:
- The element is a `<div>` with an `id` attribute that has the value `ResultsContainer`

```html
<div id="ResultsContainer">
  <!-- All the job listings -->
</div>
```

Beautiful Soup allows you to find that specific HTML element by its ID:

```python
results = soup.find(id="ResultsContainer")
print(results.prettify())
```

```html
<div class="columns is-multiline" id="ResultsContainer">
 <div class="column is-half">
  <div class="card">
   <div class="card-content">
    <div class="media">
     <div class="media-left">
      <figure class="image is-48x48">
       <img alt="Real Python Logo" src="https://files.realpython.com/media/real-python-logo-thumbnail.7f0db70c2ed2.jpg?__no_cf_polish=1"/>
      </figure>
     </div>
     <div class="media-content">
...
```


### Find Elements by HTML Class Name

You’ve seen that every job posting is wrapped in a `<div>` element with the class `card-content`. Now you can work with your new object called `results` and select only the job postings in it. These are, after all, the parts of the HTML that you’re interested in! You can pick out all job cards in a single line of code:

```python
job_cards = results.find_all('div', class_='card_content')
```

Here, you call `.find_all()` on `results`, which is a `BeautifulSoup` object. It returns an [iterable](https://docs.python.org/3/glossary.html#term-iterable) containing all the HTML for all the job listings displayed on that page.

```python
for job_card in job_cards:
	print(job_card, end='\n' * 2)
```


```html
<div class="card-content">
 <div class="media">
  <div class="media-left">
   <figure class="image is-48x48">
    <img alt="Real Python Logo" src="https://files.realpython.com/media/real-python-logo-thumbnail.7f0db70c2ed2.jpg?__no_cf_polish=1"/>
   </figure>
  </div>
  <div class="media-content">
   <h2 class="title is-5">
    Senior Python Developer

...

<div class="card-content">
 <div class="media">
  <div class="media-left">
   <figure class="image is-48x48">
    <img alt="Real Python Logo" src="https://files.realpython.com/media/real-python-logo-thumbnail.7f0db70c2ed2.jpg?__no_cf_polish=1"/>
   </figure>
  </div>
  <div class="media-content">
   <h2 class="title is-5">
    Energy engineer
   </h2>
   <h3 class="subtitle is-6 company">
    Vasquez-Davidson
   </h3>
  </div>
 </div>
 <div class="content">
  <p class="location">
   Christopherville, AA
   
...
```


You can pick out those child elements from each job posting with `.find()`:

```python
for job_card in job_cards:
  title_element = job_card.find('h2', class_='title')
  company_element = job_card.find('h3', class_='company')
  location_element = job_card.find('p', class_='location')
  print(title_element.prettify())
  print(company_element.prettify())
  print(location_element.prettify())
  print()
```

```html
<h2 class="title is-5">
 Senior Python Developer
</h2>

<h3 class="subtitle is-6 company">
 Payne, Roberts and Davis
</h3>

<p class="location">
 Stewartbury, AA
</p>


<h2 class="title is-5">
 Energy engineer
</h2>

<h3 class="subtitle is-6 company">
 Vasquez-Davidson
</h3>

<p class="location">
 Christopherville, AA
</p>


<h2 class="title is-5">
 Legal executive
</h2>
...
```

Each `job_card` is another `BeautifulSoup()` object. Therefore, you can use the same methods on it as you did on its parent element, `results`.

### Extract Text From HTML Elements

You only want to see the title, company, and location of each job posting. And behold! Beautiful Soup has got you covered. You can add `.text` to a `BeautifulSoup` object to return only the **text content** of the HTML elements that the object contains:

```python
for job_card in job_cards:
  title_element = job_card.find('h2', class_='title')
  company_element = job_card.find('h3', class_='company')
  location_element = job_card.find('p', class_='location')
  print(title_element.text)
  print(company_element.text)
  print(location_element.text)
  print()
```


```text
Senior Python Developer
Payne, Roberts and Davis

        Stewartbury, AA
      

Energy engineer
Vasquez-Davidson

        Christopherville, AA
      

Legal executive
Jackson, Chambers and Levy

        Port Ericaburgh, AA
      

Fitness centre manager
Savage-Bradley

```


### Find Elements by Class Name and Text Content

Not all of the job listings are developer jobs. Instead of printing out _all_ the jobs listed on the website, you’ll first **filter** them using keywords.

You know that job titles in the page are kept within `<h2>` elements. To filter for only specific jobs, you can use the [`string` argument](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#the-string-argument):

```python
python_jobs = results.find_all('h2', string='Python')
print(python_jobs)
```

```text
[]
```

When you use `string` as you did above, your program looks for that string _exactly_. Any variations in the spelling, capitalization, or whitespace will prevent the element from matching


### Pass a function to a Beautiful Soup Method

In addition to strings, you can sometimes pass functions as arguments to Beautiful Soup methods. You can change the previous line of code to use a function instead:
```python
python_jobs = results.find_all(
			'h2', 
			string=lambda text: "python" in text.lower())
			
for python_job in python_jobs:
	print(python_job)
```

```
<h2 class="title is-5">Senior Python Developer</h2>
<h2 class="title is-5">Software Engineer (Python)</h2>
<h2 class="title is-5">Python Programmer (Entry-Level)</h2>
<h2 class="title is-5">Python Programmer (Entry-Level)</h2>
<h2 class="title is-5">Software Developer (Python)</h2>
<h2 class="title is-5">Python Developer</h2>
<h2 class="title is-5">Back-End Web Developer (Python, Django)</h2>
<h2 class="title is-5">Back-End Web Developer (Python, Django)</h2>
<h2 class="title is-5">Python Programmer (Entry-Level)</h2>
<h2 class="title is-5">Software Developer (Python)</h2>
```

Now you’re passing an **anonymous function** to the `string` argument. The [lambda function](https://realpython.com/python-lambda/) looks at the text of each `<h2>` element, converts it to lowercase, and checks whether the [substring](https://realpython.com/python-string-contains-substring/) `"python"` is found anywhere.


Beautiful Soup can help you select siblings, child, and parent elements of each Beautiful Soup object.

### Access Parent Elements

One way to get access to all the information for a job is to step up in the hierarchy of the DOM starting from the `<h2>` elements that you identified

```html
<div class="card">
  <div class="card-content">  # div target parent
    <div class="media">
      <div class="media-left">
        <figure class="image is-48x48">
          <img
            src="https://files.realpython.com/media/real-python-logo-thumbnail.7f0db70c2ed2.jpg"
            alt="Real Python Logo"
          />
        </figure>
      </div>
      <div class="media-content">
        <h2 class="title is-5">Senior Python Developer</h2> # h2 tag
        <h3 class="subtitle is-6 company">Payne, Roberts and Davis</h3>
      </div>
    </div>

    <div class="content">
      <p class="location">Stewartbury, AA</p>
      <p class="is-small has-text-grey">
        <time datetime="2021-04-08">2021-04-08</time>
      </p>
    </div>
    <footer class="card-footer">
      <a
        href="https://www.realpython.com"
        target="_blank"
        class="card-footer-item"
        >Learn</a
      >
      <a
        href="https://realpython.github.io/fake-jobs/jobs/senior-python-developer-0.html"
        target="_blank"
        class="card-footer-item"
        >Apply</a
      >
    </footer>
  </div>
</div>
```

The `<div>` element with the `card-content` class contains all the information you want. It’s a third-level parent of the `<h2>` title element that you found using your filter.

With this information in mind, you can now use the elements in `python_jobs` and fetch their great-grandparent elements to get access to all the information you want:

```python
python_jobs = results.find_all('h2', string=lambda text: "Python" in text)
print(len(python_jobs))

python_job_cards = [
    h2_element.parent.parent.parent for h2_element in python_jobs
]

print(len(python_job_cards))
```

```
10
10
```

You’re selecting the parent element of the parent element of the parent element of each `<h2>` title element. That’s three generations up!

Now you can adapt the code in your [`for` loop](https://realpython.com/python-for-loop/) to iterate over the parent elements instead

```python
for job_car in python_job_cards:
  title_element = job_car.find('h2', class_='title')
  company_element = job_car.find('h3', class_='company')
  location_element = job_car.find('p', class_='location')
  print(title_element.text.strip())
  print(company_element.text.strip())
  print(location_element.text.strip())
```

```text
Senior Python Developer
Payne, Roberts and Davis
Stewartbury, AA
Software Engineer (Python)
Garcia PLC
Ericberg, AE
Python Programmer (Entry-Level)
Moss, Duncan and Allen
Port Sara, AE
Python Programmer (Entry-Level)
Cooper and Sons
West Victor, AE
Software Developer (Python)
Adams-Brewer
Brockburgh, AE
Python Developer
Rivera and Sons
East Michaelfort, AA
Back-End Web Developer (Python, Django)
Stewart-Alexander
South Kimberly, AA
Back-End Web Developer (Python, Django)
Jackson, Ali and Mckee
New Elizabethside, AA
Python Programmer (Entry-Level)
Mathews Inc
Robertborough, AP
Software Developer (Python)
Moreno-Rodriguez
Martinezburgh, AE
```

 You can also access child elements and sibling elements in a similar manner. Read up on [navigating the tree](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#navigating-the-tree) for more information.

### Extract Attributes from HTML Elements

What's still missing is fetching the link to apply for a job.

The `.text` attribute leaves only the visible content of an HTML element. It strips away all HTML tags, including the HTML attributes containing the URL, and leaves you with just the link text. To get the URL instead, you need to extract the value of one of the HTML attributes instead of discarding it.

The URL of a link element is associated with the `href` HTML attribute. The specific URL that you’re looking for is the value of the `href` attribute of the second `<a>` tag at the bottom of the HTML for a single job posting:

```html
<!-- ... -->
    <footer class="card-footer">
        <a href="https://www.realpython.com" target="_blank"
           class="card-footer-item">Learn</a>
        <a href="https://realpython.github.io/fake-jobs/jobs/senior-python-developer-0.html"
           target="_blank"
           class="card-footer-item">Apply</a>
    </footer>
  </div>
</div>
```

Start by fetching all the `<a>` elements in a job card. Then, extract the value of their `href` attributes using square-bracket notation: 

```python
for job_card in python_job_cards:
  link = job_card.find('a', string='Apply')
  link_url = link['href']
  print(f"Apply here {link_url}")
```

```text
Apply: https://realpython.github.io/fake-jobs/jobs/senior-python-developer-0.html
Apply: https://realpython.github.io/fake-jobs/jobs/software-engineer-python-10.html
Apply: https://realpython.github.io/fake-jobs/jobs/python-programmer-entry-level-20.html
Apply: https://realpython.github.io/fake-jobs/jobs/python-programmer-entry-level-30.html
Apply: https://realpython.github.io/fake-jobs/jobs/software-developer-python-40.html
Apply: https://realpython.github.io/fake-jobs/jobs/python-developer-50.html
Apply: https://realpython.github.io/fake-jobs/jobs/back-end-web-developer-python-django-60.html
Apply: https://realpython.github.io/fake-jobs/jobs/back-end-web-developer-python-django-70.html
Apply: https://realpython.github.io/fake-jobs/jobs/python-programmer-entry-level-80.html
Apply: https://realpython.github.io/fake-jobs/jobs/software-developer-python-90.html
```

You extract the `href` attribute, which contains the URL, using `["href"]` and print it to your console.

Another way

```python
for job_card in python_job_cards:
	link_url = job_card.find_all("a")[1]["href"]
	print(f"Apply here: {link_url}\n")
```

In the updated code snippet, you use [indexing](https://realpython.com/python-list/#accessing-items-in-a-list-indexing) to pick the second link element from the results of `.find_all()` using its index (`[1]`). Then, you directly extract the URL using the square-bracket notation with the `"href"` key, thereby fetching the value of the `href` attribute.


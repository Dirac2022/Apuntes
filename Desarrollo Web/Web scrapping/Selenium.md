
[Selenium Python Tutorial (with Example) | BrowserStack](https://www.browserstack.com/guide/python-selenium-to-run-web-automation-test)


Selenium is an open-source automation testing tool that supports various scripting languages such as C#, Java, Perl, Ruby, JavaScript, and others.



# Selenium WebDriver

==Selenium WebDriver is the core component that drives the browser for automation. It acts like a remote control, allowing scripts to open pages, click buttons, fill forms, and check results==, just like a real user would. Each major browser (such as Chrome, Firefox, and Edge) has its own version of the WebDriver to ensure compatibility and control.


# Selenium Python Bindings

==Selenium Python bindings are a set of libraries that let Python interact with Selenium WebDriver==. These libraries provide the tools and commands needed to control a web browser using Python code. In simple terms, the bindings act as a bridge between Selenium’s core functions and Python. ==They allow test scripts written in Python to open web pages, click buttons, enter text, and check results==, just like how a real user would do in the browser.


# Selenium Python Example
**How to run your first test?**

>[!info] 
>We are using Chrome as a browser

Step1. Import the necessary classes

You need to import WebDriver and Keys classes from Selenium. ==These classes help you interact with a web browser and emulated keybord actions==

```python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.by import By
from webdriver_manager.chrome import ChromeDriverManager
```

- `webdriver` -> Allows you to control and automate a browser (open pages, click, type, etc.)
- `Service` -> Manages how the browser driver service (e.g. ChromeDriver) is started and stopped.
- `By` -> Provides a modern, flexible way to locate elements on webpage (by name, ID, CSS selector, XPath, etc.)
- `Keys` -> Lets you simulate keyboard actions, like pressing Enter, Tab, or Arrow keys.
- `ChromeDriverManager` -> Automatically installs and manages the Chrome driver version that matches your Chrome browser.

Step 2. Create a WebDriver Instance

You need to create an instance of a WebDriver to interact with a browser (e.g. Chrome).

```python
service = Service(ChromeDriverManager().install())
driver = webdriver.Chrome(service=service)
```

- `Service()` -> Defines how the browser driver process is started.
- `ChromeDriverManager().install()` -> Downloads (if needed) and sets the correct `ChromeDriver` version for your installed Chrome browser.
- `webdriver.Chrome(service=service)` -> Creates a browser session using the Service configuration. 

Step 3. Load a Website

Use the `.get()` method to navigate to a website. ==This method waits for the page to load completely.==

```python
driver.get("https://www.python.org")
```

Step 4. Check the page Title

```python
print(driver.title)
```

Output:

```
Welcome to Python.org
```


Step 5. Interact with the Search Bar

To perform a search, locate the search bar element, enter a query, and submit it.

```python
# Find search bar by its name attribute and interact with it
search_bar = driver.find_element(By.NAME, 'q')
search_bar.clear()
search_bar.send_keys('getting started with python')
search_bar.send_keys(Keys.RETURN)
```

- `find_element(By.NAME, 'q')` -> Finds the search bar element by its name attribute.
- `.clear()` -> Clears any existing text.
- `send_keys('getting ...')` -> Types the query into the search bar.
- `send_keys(Keys.RETURN)` -> Simulates pressing the Return (Enter) key.


Step 6. Verify the resulting URL

```python
print(driver.current_url)
```

You should see a URL similar to:

```
https://www.python.org/search/?q=getting+started+with+python&submit=
```


Step 7. Close the Browser

```python
driver.close()
```



# Interacting with Common Elements in Selenium

Selenium allows you to perform a variety of actions on web elements.

Assuming you want to click a button with the ID `submit-button` after entering the input in the search bar:

```python
# Locate the button by its ID attribute
button = driver.find_element(By.ID, 'submit')

# Click the button
button.click()
```

If you need to click a link by its text:

```python
link = driver.find_element(By.LINK_TEXT, 'Documentation')

# Click the link
link.click()
```

- `find_element(By.ID, 'submit')` -> Find the button with the ID `submit`.
- `find_element(By.LINK_TEXT, 'Documentation')` -> Find a link with the text `Documentation`.
- `click()` -> Simulates a mouse click on the element.



### Example: Selecting an Option from Dropdown

For dropdown menus, Selenium provides the Select class to handle options within `<select>` elements.



```python
# Open the W3Schools test page
driver.get("https://www.w3schools.com/tags/tryit.asp?filename=tryhtml_select")
print(driver.title)
# Output
# W3Schools Tryit Editor

# wait a bit to allow the iframe to load
time.sleep(2)

# Switch to the iframe that contains the dropdown element
driver.switch_to.frame('iframeResult')
```

```python
# Locate the dropdown menu by its ID attribute
dropdown = Select(driver.find_element(By.ID, 'cars'))

# Select an option by visible text
dropdown.select_by_visible_text('Audi')
```

- `Select(driver.find_element_by_id(By.ID, 'cars'))` -> Creates a Select object for the dropdown menu,
- `select_by_visible_text('audi)` -> Selects an option by its visible text.


```python
# Or select an option by value
dropdown.select_by_value('option1')

# Or select and option by index (0-basewd index)
dropdown.select_by_index(0)
```

- `select_by_value('option1)` -> Selects an option by its value attribute.
- `select_by_index(0)` -> Selects an option by its index in the dropdown.

```python
# Close the browser
driver.quit()
```


Summary

```python
#%%
from selenium import webdriver
from selenium.webdriver.edge.service import Service
from selenium.webdriver.common.by import By
from webdriver_manager.microsoft import EdgeChromiumDriverManager
from selenium.webdriver.support.ui import Select
import time

#%%
service = Service()
driver = webdriver.Edge(service=service)

#%%

# Open the W3Schools test page
driver.get("https://www.w3schools.com/tags/tryit.asp?filename=tryhtml_select")
print(driver.title)

# wait a bit to allow the iframe to load
time.sleep(2)

# Switch to the iframe that contains the dropdown element
driver.switch_to.frame('iframeResult')
# 
#%%
# Locate the dropdown menu by its ID attribute
dropdown = Select(driver.find_element(By.ID, 'cars'))

# Select an option by visible text
dropdown.select_by_visible_text('Audi')

#%%
# Or select an option by value , example: 'option1'
dropdown.select_by_value('option1')

# Or select and option by index (0-basewd index)
dropdown.select_by_index(0)

#%%
# Close the browser
driver.quit()

```

# Navigate through HTML DOM Elements

The HTML Document Object Model (DOM) represents the structure of a web page as a tree of objects. Selenium allows you to interact with theses elements using various locator strategies.


Step 1. Locate and interact with Navigation Links

Let’s consider an example: Clicking the ‘Downloads’ link

```python
# open the Python website
driver.get("https://www.python.org/")

# Locate the "Downloads" link using XPath
downloads_links = driver.find_element(By.XPATH, "//a[text()='Downloads']")

# Click the "Downloads" link
downloads_links.click()

# optionally, print the current URL to confirm navigation
print(driver.current_url)

# Close the browser
driver.close()
```

- `(By.XPATH, "//a[text()='Downloads']")` -> Find the first `<a>` element whose visible text is "Downloads".


Step 2. Access and interact with Header sections

Let’s consider an example: Accessing the Main Header

To access the main header text, you can use different locators to find the header element. For example, finding an element by its class name

```python
# open the Python website
driver.get("https://www.python.org/")


# Locate the header element using its class name
header = driver.find_element(By.CLASS_NAME, 'introduction')

# Print the text of the header
print(header.text)

# Close the browser
driver.close()
```

Step 3. Interact with Forms and Input Fields


```python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys

# Set up the webdriver
service = Service()
driver = webdriver.Chrome(service=service)

# open the Python website
driver.get("https://www.python.org/")   

# Locate the search bar using its name attribute
search_bar = driver.find_element(By.NAME, 'q')

# Clear any existing text and enter a new search term
search_bar.clear()
search_bar.send_keys("Python Documentation")
search_bar.send_keys(Keys.RETURN)

# Optionally, print the current URL to confirm search results
print(driver.current_url)
```

- `(By.NAME, 'q')` -> locates the search input field by its name attribute.


# Navigate through Windows and Frames

When working with multiple browser windows or tabs, or dealing with iframes (frames), you may need to switch contexts to interact with different elements.


Step 1. Handling Multiple Browser Windows or Tabs

Let’s consider an example: Switching Between Windows

To handle multiple browser windows or tabs:

```python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
import time

# Set up the WebDriver
service = Service()
driver = webdriver.Chrome(service=service)

# Open the Python website
driver.get("https://www.python.org/")

# open a new tab with a different URL
# It is not recommended to use google.com because of the captchas.
# script: Open the URL, the '_blank' specifies that the URL should be open in a new tab
script = "window.open('https://www.google.com', '_blank');"
driver.execute_script(script)

# Switch to new new tab
driver.switch_to.window(driver.window_handles[1])

# Perform actions in the new ta (e.g., search for 'Selenium')
search_bar = driver.find_element(By.NAME, 'q')
search_bar.clear()
search_bar.send_keys('Selenium')
search_bar.send_keys(Keys.RETURN)


# Switch back to the original tab
driver.switch_to.window(driver.window_handles[0])
print(driver.title)

# Close the browser
driver.close()
```

- `driver.execute_script()` -> Allows you to execute custom JavaScript code directly in the browser.
- `execute_script('windows.open()')` -> Opens a new tab or window.
- `driver.window_handles` -> Returns a list of all active window handles in the current browser session.
- `driver.swtich_to.window()` -> The `switch_to` property gives access to various context-switching commands. The `window(handle)` changes the driver's focus to the specified window handle.


Step 2. Switching Between Frames

Let’s consider an example: Switching to an iFrame

To switch to and interact with elements within an iframe:

```python

```




```python

```



```python

```




```python

```




```python

```




```python

```




```python

```




```python

```





```python

```

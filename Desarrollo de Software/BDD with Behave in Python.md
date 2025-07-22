[Advanced Guide to Behavior-Driven Development with Behave in Python | by Moraneus | Medium](https://medium.com/@moraneus/advanced-guide-to-behavior-driven-development-with-behave-in-python-aaa3fa5e4c54)
Behavior-driven development is an extension of Test-driven development (TDD) that emphasizes collaboration among project stakeholders. Behave operates on the principle of scenarios, which are written in a natural language that non-programmers can understand. These scenarios describe how a feature should work from the end user’s perspective.

Behave is a BDD framework for Python that follows the principles of writing tests in a human-readable format. It uses Gherkin language to describe software behaviors without detailing how that functionality is implemented.


## Key features of Behave

- **Gherkin Language**: Enables the definition of application behavior in natural language, which stakeholders can easily understand.
- **Scenario Outline**: Facilitates data-driven tests, allowing the same scenario to be run multiple times with different data sets.
- **Hooks**: Offers setup and teardown operations for scenarios or features, improving test management.


## Feature

A Feature represents a distinct aspect or functionality of the software system under test. It’s a high-level description of a software feature, and it serves as a container for a set of related scenarios. A Feature is described in a `.feature` file and typically includes:

- A title that summarize the feature being tested.
- An optional narrative that provides context, stating the role, feature, and benefit. It follows the template: “As a \[role], I want \[feature] so that \[benefit].”
- One or more Scenarios or Scenario Outlines that detail specific examples or use cases of how the feature works.


```gherkin
Feature: User login
  As an application user
  I want to log into the application
  So that I can access my personal account information
```

## Scenario Outline
A Scenario Outline is used for parameterized tests, allowing you to run the same Scenario multiple times with different data sets. It is especially useful for covering a variety of input conditions or test cases with a single template. A Scenario Outline includes:

- A title that summarizes the test case being parameterized.
- Step definitions that use placeholders.
- An Examples section that contains a table of values to substitute into the placeholders for each iteration.

```gherkin
Scenario Outline: Login with different user roles
  Given I am the login page
  When I log in as "<role>" with valid credentials
  Then I should see the "<dashboard>" specific to my role

Examples:
  | role    | dashboard    |
  | admin   | admin panel  |
  | user    | user home    |
  | guest   | guest access |
```

In this example, the Scenario Outline will be executed three times, once for each row in the Examples table, substituting the `<role>` and `<dashboard>` placeholders with the corresponding values.

## Given, When, Then, And, But

- **Given**: Describes the initial context of the system before the user starts interacting with it. It sets up the scene.
- **When**: Specifies an action or event that occurs. It describes the key action the user performs.
- **Then**: Outlines the expected outcome or result, given the context and the event that occurred. It is used to describe an assertion.
- **And**, **But**: These are used to add additional information to the previous Given, When, or Then steps without having to repeat the Given, When, or Then keyword. They help make the scenarios more readable and organized.


## Tags

Tags are not steps but are important in Gherkin. They are prefixed with an @ symbol and can be applied to Features or Scenarios. Tags allow for filtering specific scenarios to run or to apply certain behaviors through hooks based on the tagged feature or scenario.

Use Casos for Tags in Behave

#### Environment-Based testing
Suppose you have tests that should only run in specific environments, such as `development`, `staging`, or `production`. Tags allow you to mark these tests and run them selectively.

```gherkin
@development
Feature: New Feature Development
  Scenario: Test new feature in development
    Given I am on the development environment
    When I test the new feature
    Then the feature behaves as expected

@staging
Feature: Stagin Feature Testing
  Scenario: Test feature in staging
    Given I am on the staging environment
    When I test the feature
    Then the feature behaves as expected
```

With the above setup, you can run only the tests tagged with `@development` or `@staging` using Behave's command-line options, like so:

```sh
$ behave --tags=@development
```


#### Testing different aspects

Tags can differentiate between types of tests, such as `@ui`, `@api`, etc. This is useful for running only a subset of tests that are relevant at a certain time.

```gherkin
@api
Scenario: Get info test of a user send get info request

@ui
Scenario: Button click test when clicking the login button
```

To run only API test:

```sh
$ behave --tags=@api
```


#### Excluding tests
Tags can also be used to exclude certain tests from being run, which is particularly useful when you have known issues or long-running tests that you temporarily want to skip.

```gherkin
@skip
Scenario: Test feature that is not ready
```

To exclude tests tagged with `@skip`:

```sh
$ behave --tags=~@skip
```



## Data Tables

Data Tables in Behave offer a powerful way to extend the capabilities of your steps by allowing you to include structured, multi-dimensional data directly within your feature files. This feature is particularly useful for scenarios that require a more detailed set of data than what can be succinctly expressed in a single line of step text.

**Purpose of Data Tables**:

- **Parameterization**: They allow you to run the same step with multiple sets of data, making your tests more comprehensive and efficient.
	
- **Clarity**: Complex data structures are presented in a readable format, making scenarios easier to understand and maintain.
	
- **Flexibility**: They can be used to input data into a system, verify output data, or both, supporting a wide range of testing needs.


### Defining Data Tables

Data Tables are defined using the pipe symbol (`|`) to delineate columns and are placed directly below a step. Each row after the header row represents a set of data corresponding to the columns defined in the header.

```gherkin
Given I have the following products:
| Name       | Category    | Price |  
| Smartphone | Electronics |  599  |  
| Car toy    | Toys        |  199  |  
| Book       | Books       |    3  |
```

### Accessing Data Tables in Steps

When a step is executed, the Data Table is passed to the step function as an argument. Behave allows you to access this data as either a list of dictionaries (each row becomes a dictionary where the keys are the column headers) or as raw data. Here’s how you might access and use a Data Table in your step definitions (later you will learn more about the step implementation):

```python
from behave import given
@given("I have the following products:")
def step_impl(context):
	for row in context.table:
		# Each row is a dictionary where column names are keys
		product_name = row["Name"]
		category = row["Category"]
		price = row["Price"]
		print(f"Product: {product_name}, Category: {category}, Price: ${price}")
```


## Setting up your Behave Project

**1. Install Behave**

```sh
$ python3 -m pip install behave
```

**2. Directory Structure**

```text
your_project/  
|  
|-- features/  
|   |__ steps/  
|   |   |__ step_definitions.py  
│   |__ environment.py  
│   |__ your_feature.feature  
|  
|_ models/  
|   |__ custom_models.py  
|  
|__ requirements.txt
```

- `features/`: This directory holds your `.feature` files, where you define your scenarios in the Gherkin language.
- `steps/`: Contains Python files with step definitions for the scenarios described in your feature files
- `environment.py`: (Optional) Defines setup and teardown functions, among other hooks.
- `models/`:  (Optional) A directory for custom models or types you might use in your steps.
- `requirements.txt`: Lists the project's dependencies.


## Writing Scenarios in Gherkin

Gherkin is a key component of Behave, allowing you to write human-readable descriptions of software behaviors. Here’s a breakdown of a Gherkin file:

```gherkin
Feature: Shopping Cart
  As an online shopper
  I want to manage my shopping cart
  So that I can order my desired products

  Scenario Outline: Add a product to the shopping cart
    Given I am on the product page
    When I add "<product>" to the cart
    Then I should see "<product>" in the cart

    Examples:
      | product    |
      | Book       |
      | Smartphone |

```


This example showcases the use of a `Scenario Outline` with `Examples`, allowing the scenario to run multiple times with different inputs.


## Implementing Step Definitions

After defining your scenarios, you need to implement the corresponding step definitions in Python. Implement the corresponding steps in `features/steps/shopping_cart_steps.py`. The naming of these files is flexible, provided they adhere to the Python file extension (.py). There’s no need to manually specify which step files Behave should utilize; it automatically detects and executes all Python scripts present in the “steps” directory.

In Behave, the naming of the function that implements a step (commonly seen as `step_impl(context)`) is not strictly required to follow the `step_impl` convention. You can name your step implementation functions anything you like, as long as they are decorated with the appropriate Behave decorator (`@given`, `@when`, `@then`, or `@step`) and accept at least one argument, usually named `context`, which is a reference to Behave's context object.

For the above scenario, your step definitions might look like this:

```python
from behave import given, when, then

@given("I am on the product page")
def step_impl(context):
	context.browser.visit_product_page()

@when("I add '{product}' to the cart")
def step_impl(context, product):
	context.browser.add_product_to_cart(product)

@then("I should see '{product}' in the cart")
def step_impl(context, product):
	assert product in context.browser.get_cart_contents()
```


## Defining Custom Types

Behave allows you to extend its functionality by defining new types for use in your step implementations. This feature is particularly useful for matching complex patterns or specific data structures. Here’s an example:

**1. Define a New Type in `features/steps/type_definitions.py`**:

```python
from behave import register_type
import parse

class Product(object):
	def __init__(self, i_product_name):
		self.__m_product_name = i_product_name

	@property
	def name(self) -> str:
		return self.__m_product_name

@parse.with_pattern(r"[^\"].+")
def parse_product(text):
	return Product(text)

register_type(Product=parse_product)
```


**2. Use the Custom Type in your feature file**


```gherkin
Feature: Custom Product
  Scenario: Adding a product with custom type
    Given I add a product "Laptop" to the cart
    Then the product should be recognized as a Product
```

**3. Implement Step definitions using the Custom Type**

```python
from behave import given, then

# Import the Product class from where it's defined, if it's in a different file
from steps.type_definitions import Product

# Assuming you have a context attribute for the cart, which is a list
@given("I add a product '{product_name:Product}' to the cart")
def step_impl(context, product_name):
	context.cart.add_product_to_cart(product_name)

@then("the product should be recognized as a Product")
def step_impl(context):
	# Check the last added product in the cart
	last_added_product = context.cart.cart[-1]
	assert isinstance(last_added_product, Product), "The object is not an instance of product"

```


## Hooks

Hooks in Behave are special functions that allow you to run code before and after certain events during your tests. These events include the start and end of the entire test run, each feature, and each scenario. Hooks are used for setup and teardown operations, such as preparing test data, clearing caches, or managing resources like database connections and browser sessions. They play a crucial role in test management by ensuring that each test runs in a clean and controlled environment, which helps to maintain test reliability and repeatability.

**Types of Hooks in Behave**

- `before_all`: Runs once before all test.
- `after_all`: Runs once after all test.
- `before_feature`: Runs before each feature file is tested.
- `after_feature`: Runs after each feature file has been tested.
- `before_scenario`: Runs before each scenario.
- `after_scenario`: Runs after each scenario.
- `before_step`: Runs before each step.
- `after_step`: Runs after each step.


### Implementing Hooks

Hooks are defined in the `environment.py` file, which should be located in your `features` directory. Here are examples of how to use some of these hooks:

**`environment.py`**

```python
"""Before proceeding, ensure you've imported all necessary modules and 
components. In this context, we're operating under the assumption that 
both database (db) and web browser automation tools (browser) have been 
correctly imported."""


def before_all(context):
    # Setup operation that runs before all tests
    context.browser = browser.start_browser()

def after_all(context):
    # Teardown operation that runs after all tests
    context.browser.quit()

def before_feature(context, feature):
    # Setup operation specific to each feature
    if 'database' in feature.tags:
        db.create_test_database()

def after_feature(context, feature):
    # Teardown operation specific to each feature
    if 'database' in feature.tags:
        db.drop_test_database()

def before_scenario(context, scenario):
    # Setup for each scenario; e.g., logging in a user
    if 'login' in scenario.tags:
        context.user = context.browser.login_user('test_user', 'password')

def after_scenario(context, scenario):
    # Teardown for each scenario; e.g., logging out a user
    if 'logout' in scenario.tags:
        context.browser.logout_user()
```


In this example, `before_all` and `after_all` are used to start and stop a web browser for tests that require UI interaction. `before_feature` and `after_feature` manage database setup and teardown for features tagged with `database`. `before_scenario` and `after_scenario` handle user login and logout for scenarios tagged with `login` and `logout`, respectively.


## Initializing attributes in the context

Attributes within the `context` object can be initialized in various places, but two common approaches are widely used:

#### 1. Initialization in Environment Hooks

Environment hooks such as `before_all`, `before_feature`, `before_scenario`, etc., provide a structured way to initialize attributes before the execution of your tests. For example, you might establish a database connection in `before_all` and store it in `context.db` so that it's available to all scenarios:

```python
def before_all(context):
	context.db = MyDatabaseConnection()
```

Similarly, a browser instance for web testing can be initiated in a `before_scenario` hook and added to the context, ensuring that each scenario starts with a fresh browser state:

```python
def before_scenario(context, scenario):  
	context.browser = webdriver.Chrome() # Or any other browser
```


#### 2. Lazy Initialization within Steps

Sometimes, you might prefer to initialize certain data only when it’s needed within a specific step. This approach, known as lazy initialization, helps conserve resources and keeps your tests running quickly. To implement lazy initialization, you check for the existence of an attribute and initialize it if it’s not already present:

```python
@given('I am logged into the web application')  
def step_impl(context):  
	# Initializes the browser if not already done  
	if not hasattr(context, 'browser'):  
		context.browser = webdriver.Chrome()  
	# Proceed to log into the application
```


---
## Comandos básicos de Behave

- `behave`  
    Ejecuta **todos** los escenarios definidos en los archivos `.feature`.
    
- `behave --tags=@etiqueta`  
    Ejecuta **solo** los escenarios o features que tengan la etiqueta `@etiqueta`.  
    Ejemplo: `behave --tags=@development`
    
- `behave --tags=~@etiqueta`  
    **Excluye** los escenarios o features que tengan la etiqueta `@etiqueta`.  
    Ejemplo: `behave --tags=~@skip`
    
- `behave --tags=@etiqueta1,@etiqueta2`  
    Ejecuta escenarios que tengan **@etiqueta1 O @etiqueta2**.  
    Ejemplo: `behave --tags=@api,@ui`
    
- `behave --tags=@etiqueta1 --tags=@etiqueta2`  
    Ejecuta escenarios que tengan **@etiqueta1 Y @etiqueta2**.  
    Ejemplo: `behave --tags=@login --tags=@database`
    
- `behave --format pretty`  
    Muestra la salida en un formato legible (es el formato por defecto).
    
- `behave --format json -o resultado.json`  
    Exporta los resultados en **formato JSON** a un archivo.  
    Útil para integraciones con herramientas de reporte.
    
- `behave --format html -o resultado.html`  
    Exporta la ejecución como un **reporte HTML** (requiere un plugin adicional como `behave-html-formatter`).
    
- `behave --dry-run`  
    Muestra qué pasos se ejecutarían, **sin ejecutar el código**. Útil para verificar coincidencias entre pasos y definiciones.
    
- `behave --no-capture`  
    Muestra en pantalla toda la **salida estándar** (como los `print()`), ideal para depurar.
    
- `behave --no-skipped`  
    **Oculta** los escenarios marcados como `@skip` u omitidos.
    
- `behave --stop`  
    **Detiene** la ejecución al primer fallo encontrado.
    
- `behave --summary`  
    Muestra un **resumen** final de cuántos escenarios y pasos pasaron o fallaron.
    
- `behave --show-timings`  
    Muestra el **tiempo de ejecución** de cada paso.
    
- `behave features/mi_archivo.feature`  
    Ejecuta únicamente el archivo `.feature` especificado.
    
- `behave features/mi_archivo.feature:10`  
    Ejecuta el escenario que se encuentra en la **línea 10** del archivo. Muy útil para correr un solo escenario.
    
- `behave --define VAR=valor`  
    Define una variable de entorno que puedes capturar desde los hooks (`context.config.userdata`).  
    Ejemplo: `behave --define browser=chrome`
    

---

## Tipos de datos en Behave

En **Behave**, cuando defines pasos (`@given`, `@when`, `@then`) con **placeholders** tipo `{variable}` o `{variable:tipo}`, puedes usar varios **tipos de datos predefinidos** que Behave ya sabe convertir automáticamente desde el texto del `.feature`.

**Sintaxis general**

```python
@given("el usuario tiene {cantidad:d} monedas")
def step_impl(context, cantidad):
    ...
```

En este ejemplo, `{cantidad:d}` indica que `cantidad` es un número entero.

---

### Tipos de datos disponibles por defecto en Behave

|Tipo (`:tipo`)|Significado / Conversión|Ejemplo en feature|Resultado en Python|
|---|---|---|---|
|`:w`|Palabra (`\w+`)|`{nombre:w}` → "juan"|`'juan'` (str)|
|`:s`|Cadena (cualquier texto sin comillas)|`{texto:s}` → "hola mundo"|`'hola mundo'` (str)|
|`:d`|Entero (`\d+`)|`{edad:d}` → "25"|`25` (int)|
|`:f`|Float (`\d+.\d+`)|`{peso:f}` → "75.5"|`75.5` (float)|
|`:b`|Booleano (`true/false`)|`{activo:b}` → "true"|`True` (bool)|

---

### ✍️ Ejemplos de uso en `.feature`

```gherkin
Given el usuario tiene 3 monedas
When espera 1.5 horas
Then el sistema muestra "Operación completada"
```

Y en el step de Python:

```python
@given("el usuario tiene {monedas:d} monedas")
def step_impl(context, monedas):
    # monedas es int
    ...
```

---

**💡 Nota:**

- Si usas `{variable}` sin `:tipo`, Behave usa el **tipo por defecto `:w`** (una palabra).
- Si necesitas valores más complejos (fechas, listas, expresiones), puedes:
    - Procesar la variable manualmente dentro del step.
    - Definir tu **tipo personalizado** (más avanzado, opcional).

---

### 🧪 Tipos personalizados (avanzado, opcional)

Puedes registrar tus propios tipos si necesitas, por ejemplo, un tipo `:fecha` que convierta `"2025-07-01"` en un objeto `datetime`.

```python
from behave import register_type
from datetime import datetime

def parse_fecha(text):
    return datetime.strptime(text, "%Y-%m-%d")

register_type(fecha=parse_fecha)

@when("la fecha actual es {hoy:fecha}")
def step_impl(context, hoy):
    # hoy es un objeto datetime
    ...
```

---

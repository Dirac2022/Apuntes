

# Introduction to Importing Data in Python

**Import data from**

- Flat files, e.g. `.txt`, `.csv`
- Files from other software
- Relational databases

## Introduction and flat files


<h5>Reading a text file</h5>

```python
filename = 'hucki_finn.txt'
file = open(filename, mode='r)
text = file.read()
file.close()
```


<h5>Writing to a file</h5>

```python
filename = 'huck_finn.txt'
file = open(filename, mode='w'
file.close()
```


<h5>Context manager with</h5>

```python
with open('huck_finn.txt') as file:
	print(file.read())
```



<h5>Flat files</h5>
- Text files containing records, that is, table data.
- Record: row of fields or attributes
- Column: feature or atributte



### Importing flat files using NumPy

- [[numpy#`np.loadtxt()`|`loadtxt()`]]
- [[numpy#`np.genfromtxt()`|`genfromtxt()`]]

```python
import numpy as np
filename = 'MNIST.txt'
data = np.loadtxt(filename, delimeter=',')
data
```

```
[   0.    0.    0.    0.    0.] 
[  86.  250.  254.  254.  254.] 
[   0.    0.    0.    9.  254.] 
...,  
[   0.    0.    0.    0.    0.] 
[   0.    0.    0.    0.    0.] 
[   0.    0.    0.    0.    0.]] 
```


<h5>Customize your NumPy import</h5>

```python
import numpy as np
filename = 'MNIST_header.txt'
data = np.loadtxt(filename, delimiter=',', skiprows=1, usecols=[0, 2])
```

```
[[   0.    0.] 
[  86.  254.] 
[   0.    0.] 
...,  
[   0.    0.] 
[   0.    0.] 
[   0.    0.]] 
```


### Importing flat files using pandas


**Manipulating pandas DataFrames for**

- Exploratory data analysis
- Data wrangling
- Data preprocessing
- Building models
- Visualization
- Standard and best practice to use pandas


<h5>Importing using pandas</h5>

```python
import pandas as pd
filename = 'winequality-red.csv'
data = pd.read_csv(filename)
data.head()
```

|   | volatile acidity | citric acid | residual sugar |
|---|------------------|-------------|----------------|
| 0 | 0.70             | 0.00        | 1.9            |
| 1 | 0.88             | 0.00        | 2.6            |
| 2 | 0.76             | 0.04        | 2.3            |
| 3 | 0.28             | 0.56        | 1.9            |
| 4 | 0.70             | 0.00        | 1.9            |


```python
data_array = data.to_numpy()
```


---

## Importing data from other file types

**Other file types**

- Excel spreadsheets
- MATLAB files
- SAS files
- Stata files
- HDF5 files

### Pickled files
[[pickle]]

- File type native to Python
- Many datatypes for which it isn't obvious how to store them
- Pickled files are serialized
- Serialize = convert object to bytestream


```python
import pickle
with open('pickled_fruit.pkl', 'rb') as file:
	data = pickle.load(file)
print(data)
```

```python
{'peaches': 13, 'apples': 4, 'oranges': 11} 
```


### Importing Excel spreadsheets

```python
import pandas as pd

# Assign spreadsheet filename
file = 'battledeath.xls'

# Load spreadsheet
xls = pd.ExcelFile(file)

# Print sheet names
print(xls.sheet_names)
```

```
['2002', '2004']
```

```python
# Load a sheet into a DataFrame by name: df1
df1 = xls.parse('2004') # sheet name, as a string

# Load a sheet into a DataFrame by index
df2 = xls.parse(0) # sheet index, as a float
```

```python
# Parse the first sheet and rename the columns: df1
df1 = xls.parse(0, skiprows=[0], names=['Country', 'AAM due to War (2002)'])

# Parse the first column of the second sheet and rename the column
df2 = xls.parse(1, usecols=[0], skiprows=[0], names=['Country'])
```


### Importing SAS/Stata files using pandas

- SAS: Statistical Analysis System
- Stata: "Statistics"+ "data"
- SAS: business analytics and biostatistics
- Stata: academic social sciences research

<h5>Importing SAS files</h5>

```python
import pandas as pd
from sas7bdat import SAS7BDAT

with SAS7BDAT('urbanpop.sas7bdat') as file:
	df_sas = file.to_data_frame()
```


<h5>Importing Stata files</h5>

```python
import pandas as pd
data = pd.read_stata('urbanpop.dta')
```


### Importing HDF5 files

- Hierarchical Data Format version 5
- Standard for storing large quantities of numerical data
- Datasets can be hundreds of gigabytes or terabytes
- HDF5 can scale to exabytes

Organized like a file system with:
- Groups: Folder-like containers (similar to directories)
- Datasets: Array-like objects (similar to files)
- Attributes: Metadata attached to groups/datasets


```python
import numpy as  np
import h5py

# Assign filename
file = 'LIGO_data.hdf5'

# Load file
data = h5py.File(file, 'r')

# Print the datatype of the loaded file
print(type(data))
```


```
<class 'h5py._hl.files.File'>
```


```python
# Print the keys of the file
for key in data.keys(): # To get top-level groups
	print(key)
```


### Importing MATLAB files

- "Matrix Laboratory"
- Industry standard in engineering and science
- Data saved as `.mat` files

To load a save matlab files:
- `scipy.io.loadmat()` : read `.mat` files
- `scipy.io.savemat()`: write `.mat` files


<h5>Importing a .mat file</h5>

```python
import scipy.io

filename = 'workspace.mat'
mat = scipy.io.loadmat(filename)
print(type(mat))
```

```
<class 'dict'>
```

- keys: MATLAB variable names
- values: objects assigned to variables

```python
print(type(mat['x']))
```

```
<class 'numpy.ndarray'> 
```




## Working with relational databases in Python


### Creating a database engine in Python

- SQLite database: Fast and simple
- SQLAlchemy: Works with many Relational Database Management Systems

```python
from sqlalchemy import create_engine

# Create engine
engine = create_engine('sqlite:///Northwind.sqlite')
```


<h5>Getting table names</h5>

```python
from sqlalchemy import create_engine

# Create engine
engine = create_engine('sqlite:///Northwind.sqlite')

# Sabe the table names to a list: table_names
table_names = engine.table_names() # Return A List of the table names
print(table_names)
```

```
['Categories', 'Customers', 'EmployeeTerritories', 
'Employees', 'Order Details', 'Orders', 'Products', 
'Region', 'Shippers', 'Suppliers', 'Territories'] 
```


### Querying relational databases in Python

**Workflow of SQL querying**

- Import packages and functions
- Create the database engine
- Connect to the engine
- Query the databases
- Sabe query results to a DataFrame
- Close the connection

```python
from sqlalchemy import create_engine
import pandas as pd

# Create engine
engine = create_engine('sqlite:///Chinook.sqlite')

# Open engine connection: con
con = engine.connect()

# Perform query: rs
rs = con.execute('SELECT * from Album')

# Save results of the query to DataFrame
df = pd.DataFrame(rs.fetchall())

# Close connection
con.close()
```

To set the DataFrame columns you can use

```python
df.columns = rs.keys()
```


<h5>Using the context manager</h5>

```python
from sqlalchemy import create_engine
import pandas as pd
engine = create_engine('sqlite:///Northwind.sqlite')

with engine.connect() as con:
	rs = con.execute('SELECT OrderID, OrdrDate, ShipName FROM orders')
	df = pd.DataFrame(rs.fetchmany(size=5))
	df.columns = rs.keys()
	
print(df.head())
```


### Advanced querying: exploiting table relationships


We can write the results of a SQL query into a DataFrame in one swift line of Python code

```python
from sqlalchemy import create engine

# Create engine
engine = create_engine('sqlite:///Chinook.sqlite')

# Execute query and store records in DataFrame
df = pd.read_sql_query('SELECT * from Album', engine)
```
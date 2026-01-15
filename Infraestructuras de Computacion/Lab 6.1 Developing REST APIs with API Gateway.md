
## Task 1: Preparing the development environment

Me conecte a VS Code

![[Pasted image 20251025214908.png]]


Ejecuté los comandos de la guía para extraer los archivos necesarios para la gúia

```sh
wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-200-ACCDEV-2-91558/04-lab-api/code.zip -P /home/ec2-user/environment

unzip code.zip

```
![[Pasted image 20251025215124.png]]


Corrí el script para instalar boto3 y crear el sitio web del cafe

```sh
chmod +x resources/setup.sh && resources/setup.sh
```

Valide mi dirección IP mediante la página: `[What Is My IP Address? See Your Public IPv4 & IPv6](https://www.whatismyip.com/)`


Verifiqué la versión instalada de AWS CLI

![[Pasted image 20251025215706.png]]

Se puede ver que esta instalada la versión `2.30.4`

Se verifico que el SDK para python se instaló correctamente

![[Pasted image 20251025215829.png]]


Se verificó que el sitio web del cafe se puede cargar en la pestaña de un navegador:

- Fui a la consola de Amazon S3
- Elegí el bucket creado por defecto

![[Pasted image 20251025220917.png]]

- Elegí el enlace `index.html`
- Copié el Object URL: `https://c185953a4816487l12308336t1w909091487752-s3bucket-pvcfkgjyv6nj.s3.us-east-1.amazonaws.com/index.html`  en una pestaña nueva:

![[Pasted image 20251025221240.png]]



## Task 2: Creating the first API endpoint (GET)

In this task, you will create a REST API called _ProductsApi_. You will also create the first of three resources for the API.

The first API resource will be called _products_. It will make a GET request so that the website can retrieve all rows from the _FoodProducts_ DynamoDB database table. You will then deploy it in an API Gateway stage that's named _prod_. When a user visits the website, it will make an AJAX request and return a list of café menu items from API gateway (it will return mock data for now).

To complete all these tasks, you will use the SDK for Python.

- Cambié el `<FMI>` con `'apigateway'`

![[Pasted image 20251025224841.png]]

- Consulté [SDK for Python documentation](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/apigateway.html)  para entender el código
- Ejecuté el script con los comandos

```sh
cd python_3
python3 create_products_api.py
```


![[Pasted image 20251025225041.png]]


- Regresé a la pestaña de **AWS Management Console** e ingresé a la consola **API Gateway**
- Abrí `ProductsApi`
- Elegí el método **GET** definido


![[Pasted image 20251025225412.png]]


18. Take a moment to study the data flow in the GET method that you defined.
    
    **Tip**: If you have a screen that is large enough, arrange the browser tabs so that you have the VS Code IDE open next to this browser tab. This way, you can see the code and what it produced side-by-side.
    
    - On the left is the _Client_.
        
    - **Lines 28-33** - When you run the _Test_, the _Method Request_ is sent to the URL in the Amazon Resource Name (ARN) detail. The request doesn't require any authorization to invoke it.
        
    - **Lines 50-58** - The _Integration Request_ of type _MOCK_ is invoked, and the mock endpoint receives the data.
        
    - **Lines 35-48** - The mock endpoint invokes the _Integration Response_, which invokes the _Method Response_.
        
    - **Lines 61-92** - The _Method Response_ returns the REST API response back to the _Client_ that the request originated from.
        
    
    **Analysis:** To make it easier during this initial API development phase, you will use _mock data_. When you test the API call, it will not actually connect to the database. Instead, it will return the data that's hardcoded in the _responseTemplate_ part of the code (lines 67-91).
    
    This approach reduces the scope of potential errors during testing. You can stay focused in this lab on ensuring that the REST API logic is well defined.
    
    However, the structure of this mock data intentionally matches the data structure that will appear in the next lab when Lambda will be interacting with the database table.
    
    The key values will be mapped to the attributes that are defined in the DynamoDB table (which you created in the previous lab).
    
    **Note**: attributes in DynamoDB are not primatives. Instead, they are **wrapper objects** (as shown in the example code below). This is why there is a slight difference between the key names in the JSON and the attribute names in DynamoDB.
    
    product_name: {
    
     "S": "vanilla cupcake"
    
    }

- Fui al panel inferior de API Gateway
- Seleccioné el enlace **Pruebas (TEST)**

![[Pasted image 20251025235620.png]]




## Task 3: Creating the second API endpoint (GET)

In this task, you will define another API endpoint of type GET. This endpoint will eventually support calls to`/products/on_offer` from the cafe website and it will return in stock items.





20. In the VS Code IDE navigation pane, expand the **python_3** directory and open the file named **create_on_offer_api.py**.
    

21. Replace <FMI_1> and <FMI_2> with the correct values so that this code file will add another resource to the API that you defined in the previous task.


- Obtuve el `api_id` yendo a  API Gateway / ProductsApi / GET

![[Pasted image 20251026001206.png]]

- Obtuve el `parent_id`. Según la guía es el **Resource ID**

![[Pasted image 20251026002045.png]]


- Reemplacé estos valores en el archivo `create_on_offer_api.py`

```python
api_id = 'm6xyt65f0m'
parent_id = 'g675w9'
```

Luego de realizar los cambios ejecute el código:

```sh
python3 create_on_offer_api.py
```

Se observa un recurso anidado llamado `/on_offer` debajo del recurso `/products`


![[Pasted image 20251026002628.png]]


Al realizar las pruebas, similar a lo que se hizo con el recurso anterior, obtuve: 

![[Pasted image 20251026002847.png]]


## Task 4: Creating the third API endpoint (POST)

In this task, you will create a third resource for the API, `/create_report`. This resource will be configured at the same level as /products (not as a nested resource under products).

Café staff who are logged in (authenticated) will later use this API resource to request an _inventory report_.

The report details will be discussed in later labs. However, for now, you will configure the API to support this feature. You will also test that the website can make an Asynchronous JavaScript and XML (AJAX) request.

It is fully expected that the AJAX request will fail when you test it because you haven't configured an authentication mechanism yet. However, you will configure authentication in a later lab.

26. In the VS Code IDE, if the **create_products_api.py** file is not already open, open it (you ran this file in Task 2).
    

27. Next, in the **python_3** directory, also open the **create_report_api.py** file.
    

28. In the main code editor window, _right-click_ the **create_report_api.py** file tab and choose **Split Pane in Two Columns**.
    

29. Analyze and update the **create_report_api.py** code. Be sure to compare the code in this file to the **create_products_api.py** code while you do the analysis and updates.
    
    - Replace the  that appears on line 5 with the correct value.


En `create_products_api.py` reemplace `<FMI_1>` con el valor correcto:

```python
api_id = 'm6xyt65f0m'
```

Para ello, use el comando recomendado por la guía:

```sh
aws apigateway get-rest-apis --query items[0].id --output text
```


![[Pasted image 20251026004056.png]]



Ejecuté el archivo

```sh
python3 create_report_api.py
```


Se observó el nuevo recurso creado `/create_report`

![[Pasted image 20251026004455.png]]


Se ejecutó las pruebas: 

![[Pasted image 20251026004600.png]]



## Task 5: Deploying the API

> [!important]
> Cambie el idioma de la página de AWS Console a inglés

- En **Resources** seleccioné la raíz (root) `/`
- Seleccioné el botón **Deploy API**
- Deployment stage `New Stage`
- Stage name: `prod`
- Seleccioné **Deploy**

![[Pasted image 20251026005005.png]]

- Copié el **Invoke URL**: `https://m6xyt65f0m.execute-api.us-east-1.amazonaws.com/prod`




## Task 6: Updating the website to use the APIs


En  `resources/website/config.js` reemplacé `null` con el `Invoke URL`:

```python
window.COFFEE_CONFIG = {
	API_GW_BASE_URL_STR: "https://m6xyt65f0m.execute-api.us-east-1.amazonaws.com/prod",
	COGNITO_LOGIN_BASE_URL_STR: null
};
```


Hallé el nombre de mi Bucket:

```sh
[ec2-user@ip-10-0-1-206 python_3]$ aws s3 ls
2025-10-26 04:34:32 c185953a4816487l12308336t1w908642631374-s3bucket-1vvbxxwxhb8w
```

Y lo reemplace en `update_config.py`

```python
# Linea 6
bucket_name = "c185953a4816487l12308336t1w908642631374-s3bucket-1vvbxxwxhb8w"
```

Refresqué el sitio web:

![[Pasted image 20251026010527.png]]


Al seleccionar **login** me salió:

![[Pasted image 20251026010623.png]]

En **on offer** se puede ver que se muestra el data *mock*:

![[Pasted image 20251026010747.png]]

En **view all** se ven los 3 productos *mock*

![[Pasted image 20251026010818.png]]

> [!tip] Laboratorio finalizado


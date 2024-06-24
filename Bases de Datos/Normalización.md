
# Normalización de datos
Es un **proceso formal**, paso a paso, de análisis de los atributos de una relación

**Objetivo**
- Evitar redundancia, 
- inconsistencia y
- pérdida de información en la base de datos

# Anomalías

## Anomalías de actualización
Una anomalía es un estado inconsistente, incompleto o contradictorio de la base de datos.

- **Modificación / Actualización**: un cambio en la descripción del artículo A requiere cambios en varias filas.
- **inconsistencia**: no hay nada en el proyecto que impida que el producto A tenga dos o más descripciones diferentes en la base de datos
![[Pasted image 20240603233624.png]]

- **Inserción**: la inserción de un nuevo producto sin un pedido correspondiente causa problema. La clave es {ID, codP}
- **Exclusión**: si fuese eliminado el cliente Ana se perdería la información que el producto B se llama Lapicero y cuesta $\$ 1.00$.

![[Pasted image 20240603233911.png]]



# Formas de normalización

## Normalización de datos
Las restricciones que se discuten son restricciones de esquema, **propiedades permanentes de la relación**, no simplemente de alguna instancia de la relación.

Todas las formas normales son anidadas, en cuanto a que satisfacen las restricciones de las anteriores pero es una *mejor forma* porque elimina los fallos que se encuentran en la forma previa.

## Proceso de normalización

- Inicia con una relación o colección de relaciones.
- Produce una nueva colección de relaciones:
	- equivalente a la colección original
	- está libre de problemas
- Las nuevas relaciones estarán, por lo menos, en la 3FN


# 1FN Primera Forma Normal
Una tabla esta en la **1FN** si y solamente si esta no posee tablas anidadas.

El procedimiento usual es generar una tabla para cada anidamiento.
Esto significa que cada atributo en cada celda de la tabla contiene un solo valor, es decir, los dominios de los atributos de la relación son **atómicos**.

![[Pasted image 20240603234828.png]]


# Dependencia funcional (DF)
Si $R$ es un esquema de relación y $A$ y $B$ son conjuntos de atributos no vacíos en $R$, se dice que $B$ es **funcionalmente dependiente** de $A$ si y solo si cada valor de $A$ en $R$ tiene asociado exactamente un valor de $B$ en $R$.
$$
\text{Notacion:} \quad A \rightarrow B
$$
Se lee: $A$ determina funcionalmente a $B$.

Si dos tuplas tienen el mismo valor para $A$, entonces también deben tener el mismo valor para $B$. Se tienen las siguientes reglas:
- Si $t_1.A = t_2.A$, entonces $t_1.B = t_2.B$
El conjunto de atributos en el lado izquierdo de la flecha, se llama **determinante** (A) y el conjunto de atributos en el lado derecho de la flecha se llama **dependiente** (B).

Dada una relación $R$ con atributos: $A_1, \dots A_n, B_1, \dots, B_m, C_1, \dots, C_p$. Decimos que $A_1, \dots A_n$ determina funcionalmente a $B_1, \dots, B_m$
$$
A_1, \dots A_n \rightarrow B_1, \dots, B_m
$$
Siempre que dos tuplas tuvieran los mismos valores para $A_1, \dots A_n$, entonces estas tendrán el mismo valor para $B_1, \dots, B_m$.

**Ejemplo**
![[Pasted image 20240604000602.png]]

Si se tiene varios atributos funcionalmente dependientes de *idEst*:
$$
\begin{aligned}
\{idEst\} &\rightarrow \{Apellidos\} \\
\{idEst\} &\rightarrow \{Especialidad\} \\
\{idEst\} &\rightarrow \{NumSegSoc\}
\end{aligned}
$$

De forma abreviada se escribirá
$$ \{idEst\} \rightarrow \{Apellidos \, , Especialidad \, , NumSegSoc\} $$


## DF trivial
Si todos los atributos en el conjunto del lado derecho están incluidos en el conjunto del lado izquierdo de la dependencia, o si los dos lados son el mismo la **DF** es **trivial**.

$$
\begin{aligned}
\{A , \, B\} &\rightarrow \{A\} \\
\{A , \, B\} &\rightarrow \{B\} \\
\{A , \, B\} &\rightarrow \{A, \, B\}
\end{aligned}
$$

## DF parcial
Un atributo depende funcionalmente de **parte** de la clave compuesta de una tabla o **parte de la clave compuesta** identifica uno o más atributos de la tabla

## DF total
Un atributo depende funcionalmente de **todos** los atributos de la clave compuesta de una tabla. **La clave compuesta completa** identifica uno o más atributos de la tabla

**Ejemplo**
![[Pasted image 20240604001810.png]]

# 2FN Segunda Forma Normal
Una tabla esta en la **2FN** si y solamente si esta estuviera en la **1FN** y no posee **Dependencia Funcional Parcial (DF)**.

- Las tablas con **DF parciales** deben ser desglosadas en tablas con **DF totales**.
- Las tablas cuya **PK** posee solo un atributo están automáticamente en la **2FN**.

![[Pasted image 20240604002150.png]]


# Dependencia funcional transitiva
Si un atributo *no-clave* posee **DF total** de un atributo clave y también posee **DF total** de uno o más atributos *no-clave*, entonces se dice que existe una **DF transitiva** o indirecta  de la **PK** de **T**.
![[Pasted image 20240604002615.png]]


# 3FN Tercera Forma Normal
Una tabla esta en la **3FN** si y solamente si esta estuviera en la **2FN** y no posee **DF indirectas**.

- Aquellas tablas con **DF indirectas** deben ser desglosadas en tablas que no posean tales **DF**.
- Las tablas que poseen solo un atributo que no forma parte de la **PK** están automáticamente en la **3FN**.

![[Pasted image 20240604003027.png]]

# Recomendaciones

## Análisis de claves primarias (PK)
Las tablas pueden o no tener atributos que garantizan la identificación única de sus tuplas o tener una **PK** muy extensa. 
**Sugerencia**: definir una **CP**.

![[Pasted image 20240604082106.png]]

## Datos irrelevante
Las tablas pueden tener atributos que no necesitan ser mantenidos necesariamente en la base de datos.
**Sugerencia**: eliminar estos atributos

![[Pasted image 20240604082245.png]]


## Datos relevantes, sin embargo implícitos
**Sugerencia**: definir tales datos.

![[Pasted image 20240604082342.png]]

# Ejercicio
Transformar el sistema académico a la tercera forma normal
![[Pasted image 20240604083345.png]]


Es un modelo conceptual en el modelo de datos (Conceptual, Lógico, Físico)
Un modelo conceptual es un modelo **abstracto** que describe la estructura de una base de datos independiente de un SGBD.

# Modelo Entidad Relación (ER)
Este modelo proporciona una herramienta para representar información del mundo real a nivel conceptual. (Peter Chen 1976).
Se representa gráficamente a través de un **Diagrama de Entidad-Relación (DER)**.

- El término **empresa** es la organización para la cual se conserva la base de datos (pequeño negocio, corporación, universidad, agencia, etc.)
- El **esquema** de empresa es una descripción que corresponde al modelo conceptual.
- El modelo E-R es **independiente de cualquier DBMS**.
- **El minimundo es la parte del mundo real que modelará la base de datos**.

Principales conceptos
- Entidades
- Atributos
- Relaciones

## Entidad

Es un **conjunto de objetos** del mundo real sobre los cuales se desea mantener informaciones en la base de datos
- Es distinguible de otros objetos
- Se representa a través de un rectángulo
- Puede representar: objetos concretos (una persona, un estudiante, un cliente, etc.) y objetos abstractos (un departamento).
- Posee propiedades (atributos).
- Una instancia de entidad representa a un estudiante en particular, un cliente en particular, etc.


### Entidad fuerte
Una entidad es fuerte si puede existir por sí misma sin que dependa de la existencia de otra entidad.

### Entidad débil
- Es aquella que no puede existir sin participar en la relación, es decir, aquella que no puede ser unívocamente identificada solamente por sus atributos.
- Las entidades débiles se representan mediante un doble rectángulo.
- Una entidad débil **no tiene clave primaria propia**, tiene una clave parcial llamada **discriminador** que identifica de manera única las entidades débiles.

## Atributos
Es un dato que esta asociado a cada ocurrencia de una entidad o de una relación.
![[Pasted image 20240418075155.png]]



Los atributos pueden ser
- **Monovalorado**: Posee un valor único en una entidad. (Nombre, Salario)
- **Multivalorado**: Posee más de un valor para cada ocurrencia de la entidad (Telefono, un cliente, entidad, puede tener más de un teléfono).

Los atributos también pueden tener cardinalidad
- **Cardinalidad mínima**: $1$ como atributo obligatorio, $0$ como atributo opcional.
- **Cardinalidad máxima**: $1$ como atributo monovalorado, $N$ como atributo multivalorado.

![[Pasted image 20240418083607.png]]

### Dominio de atributo
Es el conjunto de valores permitidos para cada atributo.

### Valores nulos
Un valor nulo o *NULL* es un dato que se desconoce en el momento, o no esta definido para una instancia en particular. El valor **cero** o una **cadena en blanco** **no son valores nulos**.

### Atributos compuestos
Un atributo es compuesto si es posible descomponerlo en otros atributos. Ejemplo: Una dirección puede descomponerse en calle, cuidad, departamento, código postal.

### Atributos derivados
Sus valores se pueden calcular a partir de otros atributos. Por ejemplo si existe el atributo *fecha de nacimiento*, el atributo *edad* puede calcularse a través de el anterior. La *edad* sería un atributo derivado.

### Claves

#### Superclave
Es un atributo o un conjunto de atributos que identifica de manera única a una entidad.

#### Clave candidata
Es una superclave tal que ningún subconjunto propio de sus atributos sea por sí mismo una  superclave.

Puede hacer muchas claves candidatas para un conjunto de entidades. Cuando una clave consiste en más de un atributo se le llama **clave compuesta**.

#### Clave primaria (Primary key)
Es una clave candidata que se elige para identificar las entidades y acceder a los registros. Una clave primaria **se subraya en el diagrama ER**. Las otras claves candidatas se convierten en **claves alternativas**.

#### Clave secundaria
Es un atributo o conjunto de atributos cuyos valores (no necesariamente únicos) se usan como un medio de acceder a los registros.

## Relaciones
- Es una asociación entre **entidades**.
- Se representa a través de un rombo.
![[Pasted image 20240418075520.png]]

- Las relaciones **pueden tener atributos**. Estos atributos sirven para capturar información adicional sobre la asociación entre las entidades participantes en la relación.
- La función que una entidad juega en una relación se llama **rol de la entidad**.
- Si la misma entidad participa en una relación más de una vez, con diferentes roles, se dice que la relación es **recursiva**.

### Cardinalidad de Relaciones
Especifica cuantas ocurrencias de de una entidad pueden estar relacionadas a una ocurrencia de otra entidad. Se divide en **cardinalidad mínima** y **cardinalidad máxima**.
#### Cardinalidad máxima
##### Relación Uno a Uno 1:1
Una ocurrencia de $A$ esta asociada como **máximo a una** ocurrencia de $B$ y una ocurrencia de $B$ esta asociada a **no más de una** ocurrencia de $A$.
##### Relación Uno a Muchos 1:N
Una ocurrencia de $A$ esta asociada  a **varias** ocurrencias de $B$ pero una ocurrencia de $B$ esta asociada a **no más de una** ocurrencia de $A$.
##### Relación Muchos a Muchos M:N
Una ocurrencia de $A$ esta asociada a **cualquier número** de ocurrencias de $B$ y una ocurrencia de $B$ esta asociada **cualquier número** de ocurrencias de $A$.

#### Cardinalidad Mínima
Es el número mínimo de ocurrencias de una entidad $A$ con relación a otra entidad $B$. Se representa como 
$$ (\textit{cardinalidad minima, cardinalidad maxima}) $$
Por ejemplo
- $(1, 1)$
- $(1, N)$
- $(0, N)$
- $(N, N)$

Si la cardinalidad mínima es **uno**, la relación es **obligatoria**.
Si la cardinalidad mínima es **cero**, la relación es **opcional**.

**Ejemplo de relación obligatoria**. Un cliente para considerarse como tal debe tener al menos una cuenta. Una cuenta esta asociada a solamente un cliente.
![[Pasted image 20240418082637.png]]

**Ejemplo de una relación opcional**. Un empleado puede o no gerenciar un departamento, y un departamento tiene uno y solo un gerente.
![[Pasted image 20240418082650.png]]

### Auto-relación (Relación Unaria)
Es una relación entre ocurrencias de la misma entidad. Por ejemplo
- Un estudiante que es también tutor
- Un empleado que es también supervisor
![[Pasted image 20240418084139.png]]

### Relación Binaria y Ternaria
![[Pasted image 20240418084201.png]]

Es un conjunto de librerías desarrolladas por Android para el desarrollo de aplicaciones modernas de Android. Con Compose, puedes compilar tu IU a partir de la definición de un conjunto de funciones, llamadas funciones de componibilidad ([[Android#Composable functions|composable functions]]),  que toman datos y describen elementos de la IU.

# Modifier
Un `Modifier` es un objeto que se utiliza para aplicar cambios o efectos a un componente de UI en Jetpack Compose. Estos cambios pueden incluir ajustes en el tamaño, el color, el espaciado, el estilo de borde, y más. En Jetpack Compose, los `Modifiers` se aplican de manera declarativa, lo que significa que describes qué aspectos quieres modificar y Compose se encarga de aplicar estos cambios.

## Características Principales

1. **Encadenamiento:** Los `Modifiers` pueden ser encadenados para aplicar múltiples cambios a un componente. Cada `Modifier` se aplica en el orden en que se encadena, permitiendo un control detallado del diseño.

2. **Inmutabilidad:** Los `Modifiers` son inmutables. Cada vez que aplicas un `Modifier`, en realidad estás creando una nueva instancia que se aplica al componente, sin modificar el original.

3. **Flexibilidad:** Proporcionan una gran flexibilidad para ajustar y personalizar los componentes de UI. Puedes usar modificadores para establecer tamaño, alineación, padding, bordes, y mucho más.

## Ejemplo de Uso

Aquí tienes un ejemplo simple de cómo se utilizan los `Modifiers` en Jetpack Compose:

```kotlin
import androidx.compose.foundation.background
import androidx.compose.foundation.layout.*
import androidx.compose.material.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.unit.dp

@Composable
fun MyBox() {
    Box(
        modifier = Modifier
            .size(100.dp)
            .background(Color.Blue)
            .padding(16.dp)
    ) {
        Text(
            text = "Hello, World!",
            modifier = Modifier.align(Alignment.Center)
        )
    }
}
```

En este ejemplo:

- **`Modifier.size(100.dp)`** establece el tamaño del `Box`.
- **`Modifier.background(Color.Blue)`** aplica un color de fondo azul al `Box`.
- **`Modifier.padding(16.dp)`** agrega un padding interno al `Box`.
- **`Modifier.align(Alignment.Center)`** alinea el `Text` en el centro del `Box`.


# Parámetros

## `verticalArrangement`
Se utiliza en un contenedor `Column` para definir cómo se distribuyen los elementos verticalmente dentro de la columna. Ejemplos:
	- `verticalArrangement = Arrangement.SpaceBetween`: distribuye los elementos dentro de `Column`, de tal forma que el espacio entre ellos sea uniforme, ocupando toda la altura posible
	- `verticalArrangement = Arrangement.Center`:  coloca todos los elementos en el centro de la columna.

```kotlin
Column(
    verticalArrangement = Arrangement.SpaceBetween,
    modifier = Modifier.fillMaxHeight()
) {
    Text(text = "Primer elemento")
    Text(text = "Segundo elemento")
    Text(text = "Tercer elemento")
}
```

<div style="text-align: center;">
	<figure>
    <img src="https://developer.android.com/codelabs/basic-android-kotlin-compose-add-images/img/df69881d07b064d0.gif" width=400>
    <figcaption></figcaption>
    </figure>
</div>


## `horizontalArrangement`
Define el posicionamiento de los elementos secundarios dentro de un [[Android#Row|Row]].

<div style="text-align: center;">
	<figure>
    <img src="https://developer.android.com/codelabs/basic-android-kotlin-compose-add-images/img/c1e6c40e30136af2.gif">
    <figcaption></figcaption>
    </figure>
</div>


## Padding
Se utiliza para agregar **espacio alrededor** de un componente. Este modificador aplica un margen interior entre el borde del componente y su contenido, creando un espacio visual que ayuda a organizar y separar elementos en la interfaz de usuario.

```kotlin
Text(
    text = "Hola Mundo",
    modifier = Modifier.padding(16.dp)  // Aplica 16 dp de padding en todos los lados
)
```

En este ejemplo, el texto tendrá un espacio de 16 dp alrededor de todos sus bordes.

### Variantes de `padding`

Puedes aplicar `padding` de forma más específica, definiendo diferentes valores para cada lado (izquierda, derecha, arriba, abajo).

```kotlin
Modifier.padding(start = 8.dp, top = 16.dp, end = 8.dp, bottom = 0.dp)
```





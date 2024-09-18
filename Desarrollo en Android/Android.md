

# Funciones comunes

## `onCreate`
Es el equivalente a las funciones main de otros lenguajes de programación. Es el punto de entrada de la aplicación.

## `setContent`
Se usa para definir el layout a través de funciones [[#Composable functions|composables]].


## Composable functions
Son funciones anotadas con la anotación `@Composable` que permiten definir la interfaz de usuario de manera declarativa. Estas funciones describen cómo debería ser la UI en función del estado actual de la aplicación.
Las funciones composables se pueden invocar dentro de otras funciones composables para construir la interfaz de usuario.

- Los nombres de las funciones [[#Composable functions|composables]] deben estar capitalizadas.
- Se debe agregar `@composable` antes de declarar la función.
- Las funciones [[#Composable functions|composables]] no tienen sentencia de retorno.

Se puede llamar a todas las funciones marcadas con la anotación `@Composable` desde la función `setContent()` o desde otras que admitan composición.

La función de Compose tiene las siguientes características:

- _DEBE_ ser un sustantivo: `DoneButton()`.
- _NO_ debe ser un verbo ni una frase verbal: `DrawTextField()`.
- _NO_ debe ser una preposición convertida en sustantivo: `TextFieldWithLink()`.
- _NO_ debe ser un adjetivo: `Bright()`.
- _NO_ debe ser un adverbio: `Outside()`.
- Los sustantivos _PUEDEN_ estar precedidos por adjetivos descriptivos: `RoundIcon()`

# Contenedores
## `Surface`
Una `Surface` es un contenedor que representa una sección de la IU en la que puedes modificar el aspecto, como el borde o el color de fondo.

```kotlin
@Composable  
fun Greeting(name: String, modifier: Modifier = Modifier) {  
    Surface(color = Color.Magenta) {  
        Text(  
            text = "Hi, my name is $name!",  
            modifier = modifier.padding(24.dp)  
        )  
    }  
}
```




En el contexto de Jetpack Compose para Android, un **"Modifier"** es un concepto esencial que te permite modificar o decorar los componentes de la interfaz de usuario (UI). Los `Modifiers` en Compose proporcionan una manera flexible y declarativa de ajustar y personalizar el aspecto y el comportamiento de los elementos de UI.





# Anotaciones
Las anotaciones son una forma de adjuntar información adicional al código. Esta información ayuda a herramientas como el compilador de Jetpack Compose y a otros desarrolladores a comprender el código de la app.

Para aplicar una anotación, se agrega un prefijo al nombre (la anotación) con el carácter `@` al comienzo de la declaración en la que se hará la anotación. Se pueden anotar diferentes elementos de código, incluidas propiedades, funciones y clases. Por ejemplo

```kotlin
@Composable
fun Greeting(name: String, modifier: Modifier) {}
```


# Atributos
- `fontSize`: tamaño de fuente
```kotlin
fontSize = 100.sp
```

- `lineHeight`: se utiliza para definir la altura de la línea de texto en un componente `Text`.
```kotlin
lineHeight = 116.sp
```


En Jetpack Compose, `textAlign` es un **atributo** utilizado para controlar la alineación del texto dentro de un componente `Text`. Este atributo define cómo se distribuye el texto en el espacio horizontal disponible, permitiendo alinear el contenido a la izquierda, derecha, centro o justificarlo.


## `textAlign`
Es un **atributo** utilizado para controlar la alineación del texto dentro de un componente `Text`. Este atributo define cómo se distribuye el texto en el espacio horizontal disponible, permitiendo alinear el contenido a la izquierda, derecha, centro o justificarlo.

El atributo `textAlign` se aplica en el componente `Text` mediante la clase `TextAlign`. Los valores más comunes de `TextAlign` son:
- `TextAlign.Left`: Alinea el texto a la izquierda del contenedor.
- `TextAlign.Center`: Centra el texto dentro del contenedor
- `TextAlign.Justify`: Distribuye el texto equitativamente entre los bordes izquierdo y derecho, ajustando los espacios entre palabras.

```kotlin
Text(
    text = "Este es un ejemplo de alineación de texto.",
    textAlign = TextAlign.Center,
    modifier = Modifier.fillMaxWidth()
)
```




## Pixeles escalables
Son una medida para el tamaño de fuente, al igual que los *pixeles independientes de la densidad (DP)*. De forma predeterminada, la unidad de SO tiene el mismo tamaño que la unidad de DP, pero cambia según el tamaño de texto que prefiera el usuario en la configuración del teléfono.

# Jerarquía de la IU
Un componente (elemento superior) puede contener uno o más componentes (elementos secundarios). Estos a su vez contienen elementos secundarios. 
Los tres elementos de diseño estándar básicos en Compose son `Column`, `Row` y `Box`. 

![d7df7c362f507d6b_856.png (402×258) (android.com)](https://developer.android.com/static/codelabs/basic-android-kotlin-compose-text-composables/img/d7df7c362f507d6b_856.png?hl=es-419)


## Row
Un elemento `Row` que admite composición se coloca de forma horizontal uno al lado del otro en una fila.
```kotlin
Row {
	Text("First Column)
	Text("Secund Column")
}
```

## Box
Es un contenedor simple que permite apilar componentes uno encima del otro. Se utiliza para organizar elementos en capas, lo que lo convierte en una herramienta muy útil cuando deseas que los elementos se superpongan o se alineen de una manera específica.

Un `Box` es un **Composable** que organiza sus elementos hijos en una sola pila (stack). Es útil cuando necesitas apilar componentes, como imágenes, textos, o botones, en la misma posición o con un orden específico.

### Ejemplo básico

```kotlin
Box(
    modifier = Modifier
        .fillMaxSize()
        .background(Color.LightGray)
) {
    Text(
        text = "Texto en la esquina superior izquierda",
        modifier = Modifier.align(Alignment.TopStart)
    )
    Text(
        text = "Texto en el centro",
        modifier = Modifier.align(Alignment.Center)
    )
}
```

En este ejemplo, los dos elementos `Text` están apilados dentro del `Box`. Usamos el modificador `Modifier.align()` para especificar su posición dentro del `Box`. El primer texto está alineado en la parte superior izquierda (`Alignment.TopStart`), y el segundo está alineado en el centro (`Alignment.Center`).

### Relación con otros contenedores

| Contenedor | Descripción                                                                                   |
|------------|-----------------------------------------------------------------------------------------------|
| `Column`   | Organiza los elementos de forma vertical, uno debajo del otro.                                 |
| `Row`      | Organiza los elementos de forma horizontal, uno al lado del otro.                              |
| `Box`      | Permite apilar elementos, superponiéndolos o alineándolos de manera flexible dentro del contenedor. |

A diferencia de `Row` o `Column`, que organizan elementos en líneas (horizontal o vertical), `Box` permite una disposición más libre y apilada, lo que lo hace adecuado para situaciones donde los elementos necesitan compartir el mismo espacio de manera controlada.

# Recursos en JetPack Compose
Los recursos son los archivos adicionales y el contenido estático que usa tu código, como mapas de bits, strings de interfaz de usuario, instrucciones de animación, etc.

>[!tip] Se deben separar los recursos de la app para llevar un control independiente.

## Agrupando recursos
Cada tipo de recurso debe estar en un subdirectorio especifico

```
MyProject/    
	src/        
		MyActivity.kt    
	res/        
		drawable/            
			graphic.png        
		mipmap/            
			icon.png        
		values/            
			strings.xml
```


## Acceso a recursos
Se puede acceder a los recursos con los ID de recursos que se generan en la clase `R` del proyecto.
Una clase `R` es una clase en Android que se genera automáticamente y contiene los ID de los recursos en el proyecto.

```kotlin
R.drawable.graphic
```

<div style="text-align: center">
<figure>
	<img src="https://developer.android.com/static/codelabs/basic-android-kotlin-compose-add-images/img/7f95dd836a249cdc_960.png" width=400>
</figure>
</div>
## Funciones

### `painterResource`
Carga un recurso de imagen de elemento de diseño y toma el ID de recurso.


# View Binding

El concepto de **View Binding** en Android Studio es una técnica para acceder de manera segura y eficiente a las vistas en un archivo de diseño XML desde el código de Kotlin. Con View Binding, se genera automáticamente una clase de enlace (binding class) para cada archivo de diseño XML, que contiene referencias directas a las vistas.

## Activación del View Binding

Para usar View Binding, primero debes activarlo en tu proyecto. Esto se hace agregando la siguiente configuración en el archivo `build.gradle`:

```groovy
android {
    ...
    viewBinding {
        enabled = true
    }
}
```

## Ejemplo básico

Supongamos que tienes un archivo de diseño `activity_main.xml` con las siguientes vistas:

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello, World!" />

    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Click Me!" />
</LinearLayout>
```

Al activar View Binding, se generará una clase `ActivityMainBinding`, que contendrá referencias a las vistas `textView` y `button`.

### Implementación en Kotlin

Dentro de la actividad `MainActivity`, puedes usar View Binding para acceder a las vistas sin tener que usar `findViewById`:

```kotlin
import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import com.example.myapp.databinding.ActivityMainBinding

class MainActivity : AppCompatActivity() {

    private lateinit var binding: ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

        // Accediendo a las vistas con el binding
        binding.textView.text = "¡Hola, Mundo!"
        binding.button.setOnClickListener {
            binding.textView.text = "¡Botón presionado!"
        }
    }
}
```

## Ventajas de View Binding

| Ventaja                              | Descripción                                                                 |
|--------------------------------------|-----------------------------------------------------------------------------|
| **Seguridad**                        | Previene errores de tipo null pointer exception al referenciar vistas.      |
| **Mejor rendimiento**                | Solo enlaza las vistas que están presentes en el diseño.                    |
| **Más simple**                       | Elimina la necesidad de hacer `findViewById`, simplificando el código.       |
| **Compatibilidad**                   | Funciona con todas las versiones de Android y no requiere librerías externas.|

Con View Binding, el código es más legible y mantenible, evitando la sobrecarga de hacer casting o la necesidad de verificar si una vista existe antes de usarla.
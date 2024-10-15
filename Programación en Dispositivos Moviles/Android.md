

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



# AndroidManifest.xml
El **`AndroidManifest.xml`** es uno de los archivos más importantes en una aplicación Android. Este archivo sirve para definir información crucial sobre tu aplicación al sistema Android. Aquí es donde declaras todos los componentes clave de tu aplicación, así como los permisos, la versión de Android, los iconos de la aplicación, temas, entre otras configuraciones.

### ¿Para qué sirve el **`AndroidManifest.xml`**?

El **`AndroidManifest.xml`** es esencial porque:

1. **Declara componentes de la aplicación**: Todas las actividades (`Activity`), servicios (`Service`), receptores de difusión (`BroadcastReceiver`), y proveedores de contenido (`ContentProvider`) deben estar declarados aquí para que el sistema Android los reconozca y utilice.
   
2. **Especifica los permisos**: Aquí defines los **permisos** que tu aplicación necesita para funcionar, como acceso a la cámara, ubicación, internet, etc. Sin esta declaración, la aplicación no podrá solicitar los permisos al usuario.

3. **Define características del sistema**: El `Manifest` informa al sistema Android sobre características de hardware o software que tu aplicación necesita, como si utiliza GPS, Bluetooth, Wi-Fi, etc.

4. **Establece el punto de entrada**: El `Manifest` designa qué actividad se lanzará primero cuando el usuario abra la aplicación.

5. **Especifica configuraciones de la aplicación**: Incluye configuraciones generales de la aplicación como el nombre del paquete, icono, tema, orientación de pantalla, versión mínima de Android, etc.

### Estructura básica del **`AndroidManifest.xml`**

Este es un ejemplo básico de cómo se estructura el `AndroidManifest.xml`:

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.miapp">

    <!-- Permisos necesarios -->
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />

    <!-- Versión mínima de Android que soporta la aplicación -->
    <uses-sdk
        android:minSdkVersion="21"
        android:targetSdkVersion="30" />

    <!-- Declaración de componentes principales -->
    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">

        <!-- Actividades -->
        <activity android:name=".MainActivity">
            <!-- La actividad principal que se lanza al abrir la app -->
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>

        <!-- Otro ejemplo de actividad -->
        <activity android:name=".OtraActividad" />

        <!-- Servicios, receptores, y otros componentes pueden declararse aquí -->

    </application>

</manifest>
```

### Detalle de cada parte:

#### 1. **Etiqueta `<manifest>`**
La etiqueta raíz del archivo. Define el nombre del paquete de la aplicación, que debe coincidir con el nombre del paquete en el código fuente. Este nombre también actúa como el **identificador único** de la aplicación.

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.miapp">
```

- **`package="com.example.miapp"`**: El nombre del paquete de la aplicación, que debe ser único y generalmente sigue la convención de "dominio invertido" (`com.example`). Este es el identificador único de tu aplicación en la Play Store y en el sistema Android.

#### 2. **Declaración de permisos (`<uses-permission>`)**
Aquí defines los permisos que tu aplicación necesita para acceder a características sensibles del dispositivo, como el Internet, ubicación, cámara, almacenamiento, etc.

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```

- **`android.permission.INTERNET`**: Permite que la aplicación acceda a Internet.
- **`android.permission.ACCESS_FINE_LOCATION`**: Permite que la aplicación obtenga la ubicación precisa del dispositivo.

#### 3. **Compatibilidad con versiones de Android (`<uses-sdk>`)**
Define las versiones de Android con las que tu aplicación es compatible:

```xml
<uses-sdk
    android:minSdkVersion="21"
    android:targetSdkVersion="30" />
```

- **`android:minSdkVersion`**: Especifica la versión mínima de Android (API Level) que puede ejecutar tu aplicación. En este caso, `21` corresponde a Android 5.0 (Lollipop).
- **`android:targetSdkVersion`**: Especifica la versión de Android para la que tu aplicación ha sido optimizada (en este caso, Android 11 - API 30).

#### 4. **Aplicación (`<application>`)**
Esta sección define los **componentes principales** de la aplicación (actividades, servicios, proveedores de contenido, receptores de difusión) y algunas configuraciones globales.

```xml
<application
    android:allowBackup="true"
    android:icon="@mipmap/ic_launcher"
    android:label="@string/app_name"
    android:supportsRtl="true"
    android:theme="@style/AppTheme">
```

- **`android:allowBackup`**: Permite que los datos de la aplicación se respalden automáticamente en el dispositivo.
- **`android:icon`**: Define el icono que se mostrará para la aplicación en la pantalla de inicio y en la lista de aplicaciones.
- **`android:label`**: Especifica el nombre de la aplicación que aparecerá para el usuario.
- **`android:theme`**: Define el tema de la aplicación, que controla el aspecto visual.

#### 5. **Declaración de actividades (`<activity>`)**
Cada actividad que tu aplicación puede lanzar debe ser declarada en el `Manifest`. 

```xml
<activity android:name=".MainActivity">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>
```

- **`android:name=".MainActivity"`**: Esto declara la clase `MainActivity` como una actividad en la aplicación. El prefijo `.` indica que es una clase dentro del paquete declarado en la etiqueta `<manifest>`.
  
  La actividad que tiene un `intent-filter` con la acción **`android.intent.action.MAIN`** y la categoría **`android.intent.category.LAUNCHER`** es designada como la **actividad principal** que se lanzará cuando el usuario abra la aplicación desde el lanzador (pantalla de inicio).

#### 6. **Declaración de otros componentes**:
Puedes declarar otros componentes, como **servicios** (`Service`), **receptores de difusión** (`BroadcastReceiver`), y **proveedores de contenido** (`ContentProvider`), de manera similar a las actividades.

```xml
<service android:name=".MiServicio" />
<receiver android:name=".MiReceptor" />
<provider android:name=".MiProveedorDeContenido" />
```

### ¿Qué más puedo agregar al `AndroidManifest.xml`?

Además de los elementos anteriores, el `AndroidManifest.xml` puede incluir otros elementos importantes como:

- **Permisos para APIs específicas**:
  - **Cámara**:
    ```xml
    <uses-permission android:name="android.permission.CAMERA" />
    ```
  - **Acceso a la red**:
    ```xml
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    ```

- **Declarar características del hardware que tu aplicación requiere**:
    ```xml
    <uses-feature android:name="android.hardware.camera" android:required="true" />
    ```

- **Declarar acciones específicas de `Intent`**: Esto te permite definir cómo tu aplicación responde a ciertas acciones del sistema o de otras aplicaciones (como recibir un archivo o compartir contenido).
  
    ```xml
    <activity android:name=".ShareActivity">
        <intent-filter>
            <action android:name="android.intent.action.SEND" />
            <category android:name="android.intent.category.DEFAULT" />
            <data android:mimeType="text/plain" />
        </intent-filter>
    </activity>
    ```

### Resumen:

El **`AndroidManifest.xml`** es un archivo esencial que:

- **Declara los componentes** de tu aplicación (actividades, servicios, receptores, proveedores).
- **Define permisos** para funcionalidades sensibles.
- **Establece la compatibilidad con versiones de Android**.
- **Configura el punto de entrada principal** de la aplicación.
- **Especifica características** de hardware o software requeridas por la aplicación.

Cada vez que añades una nueva actividad, servicio, receptor, o necesitas permisos especiales, es importante reflejar estos cambios en el `Manifest`.

Si tienes más dudas sobre algún aspecto específico del `AndroidManifest.xml` o necesitas ayuda para configurar algo en particular, ¡no dudes en preguntar!
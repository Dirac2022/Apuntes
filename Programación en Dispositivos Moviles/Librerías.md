

# Retrofit

**Retrofit2** es una librería de código abierto desarrollada por **Square** que simplifica las llamadas a servicios **RESTful** en Android. Es muy utilizada para consumir **APIs HTTP** y convertir las respuestas en objetos Java/Kotlin directamente. **Retrofit** maneja las peticiones y respuestas HTTP de manera sencilla, haciéndola ideal para aplicaciones que interactúan con APIs web.

### Conceptos Clave en Retrofit2:

1. **HTTP Methods (GET, POST, PUT, DELETE)**: Retrofit soporta todos los métodos HTTP. Cada método HTTP se representa como una anotación en la interfaz que defines para tus endpoints.
   
2. **Call**: Es una interfaz en Retrofit que representa la solicitud HTTP que se está preparando o ejecutando. Puedes usar `Call` para realizar una solicitud sincrónica o asincrónica.

3. **@Body**: Esta anotación se usa para enviar un cuerpo de solicitud HTTP en una petición POST, PUT, o PATCH. El cuerpo de la solicitud es generalmente un objeto serializado (como JSON).

4. **@POST**: Es una anotación que indica que la función asociada es para una solicitud HTTP de tipo **POST**. Las solicitudes POST se utilizan principalmente para enviar datos al servidor.

### Cómo usar Retrofit en Android

#### 1. Agregar Retrofit a tu proyecto

Primero, debes agregar las dependencias de Retrofit en tu archivo `build.gradle` (a nivel de la app):

```groovy
implementation 'com.squareup.retrofit2:retrofit:2.9.0'
implementation 'com.squareup.retrofit2:converter-gson:2.9.0'  // Para convertir JSON a objetos
```

#### 2. Definir una API Interface

Aquí defines los endpoints (rutas) de tu API usando las anotaciones de Retrofit.

```kotlin
import retrofit2.Call
import retrofit2.http.*

data class Usuario(val nombre: String, val edad: Int)

interface ApiService {
    
    // Método HTTP GET
    @GET("usuarios")
    fun obtenerUsuarios(): Call<List<Usuario>>

    // Método HTTP POST (para enviar datos)
    @POST("usuarios")
    fun crearUsuario(@Body nuevoUsuario: Usuario): Call<Usuario>

    // Método HTTP POST con parámetros en la URL y cuerpo
    @POST("usuarios/{id}")
    fun actualizarUsuario(
        @Path("id") id: Int, 
        @Body usuarioActualizado: Usuario
    ): Call<Usuario>
}
```

#### Explicación de las anotaciones:

1. **@GET**: Usada para hacer solicitudes **GET** (obtener datos del servidor). En el ejemplo, el método `obtenerUsuarios()` solicita una lista de usuarios desde el endpoint `usuarios`.

2. **@POST**: Usada para hacer solicitudes **POST** (enviar datos al servidor). En el ejemplo, el método `crearUsuario()` envía un objeto `Usuario` al servidor para crear un nuevo usuario.

3. **@Body**: Se usa para enviar un objeto serializado en el cuerpo de la solicitud HTTP. En este caso, `@Body nuevoUsuario: Usuario` envía un objeto `Usuario` en formato JSON al servidor.

4. **@Path**: Se usa para reemplazar variables en la URL del endpoint. Por ejemplo, en `actualizarUsuario()`, `{id}` se reemplaza por el valor de la variable `id`.

#### 3. Crear una instancia de Retrofit

Luego, creas una instancia de **Retrofit** y le especificas la base URL de tu API.

```kotlin
import retrofit2.Retrofit
import retrofit2.converter.gson.GsonConverterFactory

val retrofit = Retrofit.Builder()
    .baseUrl("https://miapi.com/")  // La URL base de la API
    .addConverterFactory(GsonConverterFactory.create())  // Usamos Gson para convertir JSON
    .build()

// Crear una instancia de ApiService
val apiService = retrofit.create(ApiService::class.java)
```

- **`baseUrl()`**: Especifica la URL base de la API. Todos los endpoints definidos en la interfaz `ApiService` se concatenarán a esta URL base.
- **`addConverterFactory()`**: Le dice a Retrofit cómo convertir las respuestas de la API en objetos Kotlin. En este caso, usamos `GsonConverterFactory` para convertir JSON en objetos Kotlin.

#### 4. Hacer una solicitud HTTP

Para ejecutar una solicitud a la API, puedes usar el método `Call` que devuelve la interfaz de Retrofit. Puedes realizar la llamada de manera **sincrónica** o **asincrónica**.

##### Sincrónico:

```kotlin
val call = apiService.obtenerUsuarios()
val response = call.execute()  // Esto ejecuta la solicitud de forma sincrónica
if (response.isSuccessful) {
    val usuarios = response.body()  // Obtener el cuerpo de la respuesta
    usuarios?.forEach {
        println("Usuario: ${it.nombre}, Edad: ${it.edad}")
    }
}
```

##### Asincrónico:

Es más común hacer las llamadas de manera asincrónica en Android para no bloquear el hilo principal:

```kotlin
call.enqueue(object : retrofit2.Callback<List<Usuario>> {
    override fun onResponse(call: Call<List<Usuario>>, response: retrofit2.Response<List<Usuario>>) {
        if (response.isSuccessful) {
            val usuarios = response.body()  // Obtener la lista de usuarios
            usuarios?.forEach {
                println("Usuario: ${it.nombre}, Edad: ${it.edad}")
            }
        }
    }

    override fun onFailure(call: Call<List<Usuario>>, t: Throwable) {
        println("Error: ${t.message}")
    }
})
```

- **`enqueue()`**: Ejecuta la solicitud de manera **asincrónica** y llama a los callbacks `onResponse` o `onFailure` dependiendo del resultado.
- **`onResponse()`**: Se ejecuta cuando la respuesta es exitosa.
- **`onFailure()`**: Se ejecuta si hay un error durante la solicitud HTTP.

### Detalle de los elementos:

1. **`@GET`**: Para solicitudes HTTP GET (recuperación de datos).
2. **`@POST`**: Para solicitudes HTTP POST (envío de datos al servidor).
3. **`@Body`**: Para enviar un cuerpo de la solicitud (generalmente en formato JSON) en métodos POST o PUT.
4. **`Call`**: Representa una llamada HTTP. Puedes ejecutarla sincrónicamente con `execute()` o asincrónicamente con `enqueue()`.
5. **`enqueue()`**: Método que lanza la llamada en un hilo separado para evitar bloquear el hilo principal.

### Retrofit y otros métodos HTTP

Además de **`GET`** y **`POST`**, Retrofit soporta otros métodos HTTP como:

- **`@PUT`**: Usado para actualizar un recurso.
- **`@DELETE`**: Usado para eliminar un recurso.

Ejemplo de un método `PUT` para actualizar datos:

```kotlin
@PUT("usuarios/{id}")
fun actualizarUsuario(@Path("id") id: Int, @Body usuario: Usuario): Call<Usuario>
```

### Ventajas de usar Retrofit:
- **Simplicidad**: Hace que interactuar con APIs sea muy sencillo gracias a las anotaciones claras.
- **Conversión automática**: Convierte automáticamente el JSON de respuesta a objetos Kotlin usando `Gson` o cualquier otro convertidor que elijas.
- **Compatibilidad con métodos HTTP**: Soporta todos los métodos HTTP necesarios (GET, POST, PUT, DELETE).
- **Manejo fácil de respuestas asíncronas**: Retrofit se integra bien con **Callbacks**, **Coroutines** y **RxJava**.

### Resumen:

- **Retrofit** es una librería popular para hacer llamadas a APIs RESTful en Android.
- **`@GET`**, **`@POST`**, **`@PUT`**, **`@DELETE`** representan los métodos HTTP para interactuar con APIs.
- **`@Body`** se usa para enviar datos en el cuerpo de una solicitud POST o PUT.
- **`Call`** representa la solicitud y permite manejar la respuesta de manera sincrónica o asincrónica.

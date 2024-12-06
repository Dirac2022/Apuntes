
# `LocalDateTime`

### Clases y métodos de `LocalDateTime`

| Clase              | Descripción | Métodos relevantes |
|--------------------|-------------|---------------------|
| `LocalDateTime`    | Representa una fecha y hora sin zona horaria. Útil para definir tanto la fecha como la hora en una instancia. | `.of(int year, int month, int day, int hour, int minute)`, `.now()`, `.toLocalDate()`, `.toLocalTime()` |
| `DateTimeFormatter`| Se utiliza para formatear y parsear objetos `LocalDateTime` a un `String` y viceversa. | `.ofPattern(String pattern)`, `.format()` |

### Métodos comunes de `LocalDateTime`

| Método                | Descripción                                           |
|-----------------------|-------------------------------------------------------|
| `.now()`              | Obtiene la fecha y hora actual del sistema.           |
| `.of()`               | Crea un objeto `LocalDateTime` con la fecha y hora especificadas. |
| `.plusHours()`        | Añade horas a la instancia de `LocalDateTime`.        |
| `.minusMinutes()`     | Resta minutos de la instancia de `LocalDateTime`.     |
| `.format()`           | Formatea el objeto `LocalDateTime` en un `String` usando un `DateTimeFormatter`. |

### Ejemplo de implementación en la clase `Movilidad`

Aquí tienes un ejemplo de cómo definir los horarios de recogida en tu clase `Movilidad` usando `LocalDateTime`:

```java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class Movilidad {
    // Atributos
    private LocalDateTime horarioRecogidaAeropuerto;
    private LocalDateTime horarioRecogidaHotel;

    // Constructor
    public Movilidad(LocalDateTime horarioRecogidaAeropuerto, LocalDateTime horarioRecogidaHotel) {
        this.horarioRecogidaAeropuerto = horarioRecogidaAeropuerto;
        this.horarioRecogidaHotel = horarioRecogidaHotel;
    }

    // Métodos de acceso
    public LocalDateTime getHorarioRecogidaAeropuerto() {
        return horarioRecogidaAeropuerto;
    }

    public void setHorarioRecogidaAeropuerto(LocalDateTime horarioRecogidaAeropuerto) {
        this.horarioRecogidaAeropuerto = horarioRecogidaAeropuerto;
    }

    public LocalDateTime getHorarioRecogidaHotel() {
        return horarioRecogidaHotel;
    }

    public void setHorarioRecogidaHotel(LocalDateTime horarioRecogidaHotel) {
        this.horarioRecogidaHotel = horarioRecogidaHotel;
    }

    // Método para mostrar los horarios con formato
    public void mostrarHorarios() {
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm");
        System.out.println("Horario de recogida del aeropuerto: " + horarioRecogidaAeropuerto.format(formatter));
        System.out.println("Horario de recogida del hotel: " + horarioRecogidaHotel.format(formatter));
    }
}
```

### Ejemplo de uso

```java
public class Main {
    public static void main(String[] args) {
        // Definiendo los horarios de recogida
        LocalDateTime horarioAeropuerto = LocalDateTime.of(2023, 11, 15, 14, 30); // 15 de noviembre de 2023, 14:30
        LocalDateTime horarioHotel = LocalDateTime.of(2023, 11, 16, 10, 0); // 16 de noviembre de 2023, 10:00

        // Creando un objeto de Movilidad
        Movilidad movilidad = new Movilidad(horarioAeropuerto, horarioHotel);

        // Mostrando los horarios
        movilidad.mostrarHorarios();
    }
}
```

### Explicación
- **`LocalDateTime.of(int year, int month, int day, int hour, int minute)`**: Crea un objeto `LocalDateTime` con la fecha y hora especificadas.
- **`DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm")`**: Formatea la fecha y hora en un formato específico para que sea legible.
- **Método `mostrarHorarios()`**: Usa `format()` para convertir `LocalDateTime` en un `String` con el formato deseado.

### Ventajas de usar `LocalDateTime`
- Combina la fecha y hora en un solo objeto, simplificando la gestión.
- Métodos fáciles de usar para modificar y formatear la fecha y hora.
- Es adecuado cuando no necesitas manejar zonas horarias.

Este enfoque es ideal para manejar los horarios de recogida si operas en una sola zona horaria o si la zona no es relevante para tu aplicación.


# `LocalDate`
`LocalDate` es una clase en Java que forma parte del paquete `java.time`, introducida en Java 8 para representar fechas sin tiempo. Esto es útil para manejar fechas de una manera más intuitiva y sin los problemas de las clases anteriores como `Date` y `Calendar`.

### Propiedades clave de `LocalDate`:
- Representa solo la fecha (año, mes, día) sin la parte de hora.
- Es inmutable y thread-safe.
- Se usa principalmente en aplicaciones donde solo se requiere la fecha, sin información de hora.

### Ejemplo de uso:
```java
import java.time.LocalDate;

public class EjemploLocalDate {
    public static void main(String[] args) {
        // Crear una fecha actual
        LocalDate fechaActual = LocalDate.now();
        System.out.println("Fecha actual: " + fechaActual);

        // Crear una fecha específica
        LocalDate fechaEspecifica = LocalDate.of(2023, 11, 10);
        System.out.println("Fecha específica: " + fechaEspecifica);

        // Operaciones comunes
        LocalDate manana = fechaActual.plusDays(1);
        LocalDate mesAnterior = fechaActual.minusMonths(1);
        System.out.println("Mañana: " + manana);
        System.out.println("Mes anterior: " + mesAnterior);

        // Comparar fechas
        boolean esAntes = fechaActual.isBefore(fechaEspecifica);
        boolean esDespues = fechaActual.isAfter(fechaEspecifica);
        System.out.println("Es la fecha actual antes de la fecha específica? " + esAntes);
        System.out.println("Es la fecha actual después de la fecha específica? " + esDespues);
    }
}
```

### Métodos principales de `LocalDate`:

| Método                  | Descripción                                     | Ejemplo de uso                             |
|-------------------------|-------------------------------------------------|--------------------------------------------|
| `now()`                 | Obtiene la fecha actual del sistema.            | `LocalDate.now()`                         |
| `of(int year, int month, int dayOfMonth)` | Crea un `LocalDate` con la fecha específica. | `LocalDate.of(2024, 1, 1)`               |
| `parse(CharSequence text)` | Convierte un texto a `LocalDate`.             | `LocalDate.parse("2024-01-01")`           |
| `plusDays(long daysToAdd)` | Agrega días a la fecha.                       | `fecha.plusDays(10)`                      |
| `minusMonths(long monthsToSubtract)` | Resta meses a la fecha.                    | `fecha.minusMonths(2)`                    |
| `isBefore(ChronoLocalDate otherDate)` | Verifica si una fecha es antes de otra.     | `fechaActual.isBefore(otraFecha)`         |
| `isAfter(ChronoLocalDate otherDate)`  | Verifica si una fecha es después de otra.   | `fechaActual.isAfter(otraFecha)`          |
| `getDayOfWeek()`        | Obtiene el día de la semana.                    | `fecha.getDayOfWeek()`                    |
| `getDayOfMonth()`       | Obtiene el día del mes.                         | `fecha.getDayOfMonth()`                   |
| `getMonth()`            | Obtiene el mes.                                 | `fecha.getMonth()`                        |
| `getYear()`             | Obtiene el año.                                 | `fecha.getYear()`                         |

### Aplicaciones comunes:
- **Control de fechas de eventos**: útiles para registrar y comparar fechas de reuniones o entregas.
- **Validaciones**: se puede usar para verificar si una fecha es válida para ciertas operaciones.
- **Cálculos de periodos**: sumas o restas de días, meses o años para obtener fechas futuras o pasadas.

¿Quieres que te explique algún método en más detalle o un ejemplo más específico?
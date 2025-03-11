
# Conditionals

## `if` statement

![](https://developer.android.com/static/codelabs/basic-android-kotlin-compose-conditionals/img/f450ef5b02967486_960.png)


![](https://developer.android.com/static/codelabs/basic-android-kotlin-compose-conditionals/img/55b83c8dd179b45b_960.png)


![](https://developer.android.com/static/codelabs/basic-android-kotlin-compose-conditionals/img/6ac6583dafe2d642_960.png)


## `when` statement

`when` statements are preferred when there are more than two branches to consider.

![](https://developer.android.com/static/codelabs/basic-android-kotlin-compose-conditionals/img/2f7c0a1e312a2581_960.png)


```kotlin
fun main() {
    val x = 3

    when (x) {
        2 -> println("x is a prime number between 1 and 10.")
        3 -> println("x is a prime number between 1 and 10.")
        5 -> println("x is a prime number between 1 and 10.")
        7 -> println("x is a prime number between 1 and 10.")
        else -> println("x isn't a prime number between 1 and 10.")
    }
}
```


```kotlin
fun main() {
    val trafficLightColor = "Yellow"

    when (trafficLightColor) {
        "Red" -> println("Stop")
        "Yellow" -> println("Slow")
        "Green" -> println("Go")
        else -> println("Invalid traffic-light color")
    }
}
```

## `if` and `when` as expressions

![](https://developer.android.com/static/codelabs/basic-android-kotlin-compose-conditionals/img/a6ff7ba09d3cdea3_960.png)

If the bodies only contain a return value or expression, you can remove the curly braces to make the code more concise

![](https://developer.android.com/static/codelabs/basic-android-kotlin-compose-conditionals/img/411c2aff894a72e2_960.png)

`if/else` stament

```kotlin
fun main() {
    val trafficLightColor = "Black"

    if (trafficLightColor == "Red") {
        println("Stop")
    } else if (trafficLightColor == "Yellow") {
        println("Slow")
    } else if (trafficLightColor == "Green") {
        println("Go")
    } else {
        println("Invalid traffic-light color")
    }

}
```

as a expression
```kotlin
fun main() {
    val trafficLightColor = "Black"

    val message = 
      if (trafficLightColor == "Red") "Stop"
      else if (trafficLightColor == "Yellow") "Slow"
      else if (trafficLightColor == "Green") "Go"
      else "Invalid traffic-light color"

    println(message)
}
```



# Classes and objects

![](https://developer.android.com/static/codelabs/basic-android-kotlin-compose-classes-and-objects/img/9a07f83c06449f38_960.png)

Naming conventions
- You can choose any class name that you want, but don't use Kotlin [keywords](https://kotlinlang.org/docs/keyword-reference.html) as a class name, such as the `fun` keyword.
- The class name is written in ``PascalCase``, so each word begins with a capital letter and there are no spaces between the words

**Example**
```kotlin
class SmartDevice {

}
```


## Instance of a class

The `val` or `var` keyword is followed by the name of the variable
![](https://developer.android.com/static/codelabs/basic-android-kotlin-compose-classes-and-objects/img/f58430542f2081a9_960.png)

> [!note]
> When you define the variable with the `val` keyword to reference the object, the variable itself is read-only, but the class object remains mutable. This means that you can't reassign another object to the variable, but you can change the object's state when you update its properties' values

**Example**
```kotlin
val smartTvDevice = SmartDevice()
```

## Class methods
The syntax to define a function in a class is identical to what you learned before. The only difference is that the function is placed in the class body. When you define a _function_ in the class body, it's referred to as a member function or a _method_, and it represents the behavior of the class.

```kotlin
class SmartDevice {
    fun turnOn() {
        println("Smart device is turned on.")
    }

    fun turnOff() {
        println("Smart device is turned off.")
    }
}
```

**Call a method on an object**
```kotlin
class SmartDevice {
    fun turnOn() {
        // A valid use case to call the turnOff() method could be to turn off the TV when available power doesn't meet the requirement.
        turnOff()
        ...
    }

}
```

To call a class method outside of the class, start with the class object followed by the `.` operator, the name of the function, and a set of parentheses. If applicable, the parentheses contain arguments required by the method

![](https://developer.android.com/static/codelabs/basic-android-kotlin-compose-classes-and-objects/img/fc609c15952551ce_960.png)


```kotlin
fun main() {
    val smartTvDevice = SmartDevice()
    smartTvDevice.turnOn()
    smartTvDevice.turnOff()
}
```


## Class properties
You define an immutable property with the `val` keyword and a mutable property with the `var` keyword.

**Example**
```kotlin
class SmartDevice {

    val name = "Android TV"
    val category = "Entertainment"
    var deviceStatus = "online"

    fun turnOn() {
        println("Smart device is turned on.")
    }

    fun turnOff() {
        println("Smart device is turned off.")
    }
}

fun main() {
    val smartTvDevice = SmartDevice()
    println("Device name is: ${smartTvDevice.name}")
    smartTvDevice.turnOn()
    smartTvDevice.turnOff()
}
```


### Getter and Setter functions in properties
Before going deeper into how to implement these properties, you need to understand the full syntax to declare them. The full syntax to define a _mutable_ property starts with the variable definition followed by the optional `get()` and `set()` functions. You can see the syntax in this diagram:

![](https://developer.android.com/static/codelabs/basic-android-kotlin-compose-classes-and-objects/img/f2cf50a63485599f_960.png)

>[!important] When you don't define the getter and setter function for a property, the Kotlin compiler internally creates the functions

**Example**

- `field` es una palabra clave que hace referencia al valor de la propiedad
- Los métodos `get` y `set` no se llaman explícitamente.
- Aquí un `getter` personalizado añadiendo "Soto"
```kotlin
class Persona {
    var nombre: String = "Mitchel"
        get() = "$field Soto"
        set(value) {
            field = value
        }
}

fun main() {
    val persona = Persona()
    println(persona.nombre) // "Mitchel Soto"

    persona.nombre = "Lisbeth"
    println(persona.nombre) // "Lisbeth Soto"
}
```


## Constructor

### Default constructor

```kotlin
class SmartDevice constructor() {
    ...
}
```

Kotlin aims to be concise, so you can remove the `constructor` keyword if there are no annotations or visibility modifiers, which you learn about soon, on the constructor. You can also remove the parentheses if the constructor has no parameters as shown in this code snippet:

```kotlin
class SmartDevice {
    ...
}
```

**Example**
In `SmartDevice` class to maintain immutability but avoid hardcoded values, use a parameterized constructor to initialize them:
- In the `SmartDevice` class, move the `name` and `category` properties to the constructor without assigning default values:

```kotlin
```kotlin
class SmartDevice (val name: String, val category: String) {

    var deviceStatus = "online"

    fun turnOn() {
        println("Smart device is turned on.")
    }

    fun turnOff() {
        println("Smart device is turned off.")
    }
}

```

The constructor now accepts parameters to set up its properties, so the way to instantiate an object for such a class also changes. You can see the full syntax to instantiate an object in this diagram:

![](https://developer.android.com/static/codelabs/basic-android-kotlin-compose-classes-and-objects/img/bbe674861ec370b6_960.png)

**Creating an object

```kotlin
SmartDevice("Android TV", "Entertainment")

// or
SmartDevice(name = "Android TV", category = "Entertainment")
```


There are two main types of constructors in Kotlin:

- **Primary constructor.** A class can have only one primary constructor, which is defined as part of the class header. A primary constructor can be a default or parameterized constructor. The primary constructor doesn't have a body. That means that it can't contain any code.
- **Secondary constructor.** A class can have multiple secondary constructors. You can define the secondary constructor with or without parameters. The secondary constructor can initialize the class and has a body, which can contain initialization logic. If the class has a primary constructor, each secondary constructor needs to initialize the primary constructor.


The syntax to define a primary constructor starts with the class name followed by the `constructor` keyword and a set of parentheses. The parentheses contain the parameters for the primary constructor. If there's more than one parameter, commas separate the parameter definitions

![](https://developer.android.com/static/codelabs/basic-android-kotlin-compose-classes-and-objects/img/aa05214860533041_960.png)


The secondary constructor is enclosed in the body of the class and its syntax includes three parts:

- **Secondary constructor declaration.** The secondary constructor definition starts with the `constructor` keyword followed by parentheses. If applicable, the parentheses contain the parameters required by the secondary constructor.
- **Primary constructor initialization.** The initialization starts with a colon followed by the `this` keyword and a set of parentheses. If applicable, the parentheses contain the parameters required by the primary constructor.
- **Secondary constructor body.** Initialization of the primary constructor is followed by a set of curly braces, which contain the secondary constructor's body.

![](https://developer.android.com/static/codelabs/basic-android-kotlin-compose-classes-and-objects/img/2dc13ef136009e98_960.png)

**Example**
For example, imagine that you want to integrate an API developed by a smart-device provider. However, the API returns status code of `Int` type to indicate initial device status. The API returns a `0` value if the device is _offline_ and a `1` value if the device is _online_. For any other integer value, the status is considered _unknown_. You can create a secondary constructor in the `SmartDevice` class to convert this `statusCode` parameter to string representation as you can see in this code snippet:


```kotlin
class SmartDevice(val name: String, val category: String) {
    var deviceStatus = "online"

    constructor(name: String, category: String, statusCode: Int) : this(name, category) {
        deviceStatus = when (statusCode) {
            0 -> "offline"
            1 -> "online"
            else -> "unknown"
        }
    }
    ...
}
```



## Relationship between classes

The `SmartTvDevice` and `SmartLightDevice` classes _extend_ the `SmartDevice` parent class. The parent class is also referred to as a _superclass_ and the child class as a _subclass_. You can see the relationship between them in this diagram

![](https://developer.android.com/static/codelabs/basic-android-kotlin-compose-classes-and-objects/img/e4cb2f63c96f8c_960.png)

>[!important] However, in Kotlin, all the classes are final by default, which means that you can't extend them, so you have to define the relationships between them

**Example**
Define the relationship between the `SmartDevice` superclass and its subclasses:

1. In the `SmartDevice` superclass, add an `open` keyword before the `class` keyword to make it extendable
```kotlin
open class SmartDevice(val name: String, val category: String) {
    ...
}
```

>[!info] The `open` keyword informs the compiler that this class is extendable, so now other classes can extend it.

The syntax to create a subclass starts with the creation of the class header. The constructor's closing parenthesis is followed by a space, a colon, another space, the superclass name, and a set of parentheses. If necessary, the parentheses include the parameters required by the superclass constructor.

![](https://developer.android.com/static/codelabs/basic-android-kotlin-compose-classes-and-objects/img/1ac63b66e6b5c224_960.png)


2. Create a `SmartTvDevice` subclass that extends the `SmartDevice` superclass:
```kotlin
class SmartTvDevice(deviceName: String, deviceCategory: String) :
    SmartDevice(name = deviceName, category = deviceCategory) {
}
```

The `constructor` definition for `SmartTvDevice` doesn't specify whether the properties are mutable or immutable. This means that the `deviceName` and `deviceCategory` parameters are merely `constructor` parameters instead of class properties. You won't be able to use them in the class, but simply pass them to the superclass constructor.

3. In the `SmartTvDevice` subclass body, add the `speakerVolume` property that you created when you learned about the getter and setter functions:

4. Define a `channelNumber` property assigned to a `1` value with a setter function that specifies a `0..200` range:


5. Define an `increaseSpeakerVolume()` method that increases the volume and prints a `"Speaker` `volume` `increased` `to` `$speakerVolume."` string:

6. Add a `nextChannel()` method that increases the channel number and prints a `"Channel` `number` `increased` `to` `$channelNumber."` string:

7. On the line after the `SmartTvDevice` subclass, define a `SmartLightDevice` subclass that extends the `SmartDevice` superclass

8. In the `SmartLightDevice` subclass body, define a `brightnessLevel` property assigned to a `0` value with a setter function that specifies a `0..100` range:

9. Define an `increaseBrightness()` method that increases the brightness of the light and prints a `"Brightness` `increased` `to` `$brightnessLevel."` string:


```kotlin
class SmartTvDevice(deviceName: String, deviceCategory: String):
	SmartDevice(name = deviceName, category = deviceCategory) {
        
    
	var speakerVolume = 1
        set(value) {
            if (value in 0..100) {
                field  = value
            }
        }
        
    var channelNumber = 1 
        set(value) {
            if (value in 1..200) {
                field = value
            }
        }
        
    fun increaseSpeakerVolume() {
        speakerVolume = speakerVolume + 1
        println("Speaker volume increased to $speakerVolume")
    }
    
    fun nextChannel() {
        channelNumber ++ 
        println("Channel number increased to $channelNumber")
    }
    
}
 ```
 
```kotlin   
class SmartLightDevice(deviceName: String, deviceCategory: String):
	SmartDevice(name = deviceName, category = deviceCategory) {
        

	var brightnessLevel = 0
        set(value) {
            if (value in 0..100) {
                field = value
            }
        }
        
    fun increaseBrightness() {
        brightnessLevel ++
        println("Birghtness increased to $brightnessLevel")
    }
}	
```


When you use inheritance, you establish a relationship between two classes in something called an _IS-A relationship_. An object is also an instance of the class from which it inherits. In a _HAS-A relationship_, an object can own an instance of another class without actually being an instance of that class itself

![](https://developer.android.com/static/codelabs/basic-android-kotlin-compose-classes-and-objects/img/43ebe1f550d6c614_960.png)

### IS-A **relationships**
When you specify an IS-A relationship between the `SmartDevice` superclass and `SmartTvDevice` subclass, it means that whatever the `SmartDevice` superclass can do, the `SmartTvDevice` subclass can do

### HAS-A **relationships**
A HAS-A relationship is another way to specify the relationship between two classes. For example, you will probably use the smart TV in your home. In this case, there's a relationship between the smart TV and the home. The home contains a smart device or, in other words, the home _has a_ smart device. The _HAS-A_ relationship between two classes is also referred to as _composition_.

**Examples**
So far, you created a couple of smart devices. Now, you create the `SmartHome` class, which contains smart devices. The `SmartHome` class lets you interact with the smart devices.

1. In between the `SmartLightDevice` class and `main()` function, define a `SmartHome` class:

2. In the `SmartHome` class constructor, use the `val` keyword to create a `smartTvDevice` property of `SmartTvDevice` type:

3. In the body of the `SmartHome` class, define a `turnOnTv()`method that calls the `turnOn()` method on the `smartTvDevice` property:

4. On the line after the `turnOnTv()` method, define a `turnOffTv()` method that calls the `turnOff()` method on the `smartTvDevice` property:

5. On the line after the `turnOffTv()` method, define an `increaseTvVolume()` method that calls the `increaseSpeakerVolume()` method on the `smartTvDevice` property and then define a `changeTvChannelToNext()` method that calls the `nextChannel()` method on the `smartTvDevice` property:

6. In the `SmartHome` class constructor, move the `smartTvDevice` property parameter to its own line followed by a comma:

7. On the line after the `smartTvDevice` property, use the `val` keyword to define a `smartLightDevice` property of `SmartLightDevice` type:

8. In the `SmartHome` body, define a `turnOnLight()` method that calls the `turnOn()` method on the `smartLightDevice` object and a `turnOffLight()` method that calls the `turnOff()` method on the `smartLightDevice` object:

9. On the line after the `turnOffLight()`method, define an `increaseLightBrightness()` method that calls the `increaseBrightness()` method on the `smartLightDevice` property:

10. On the line after the `increaseLightBrightness()` method, define a `turnOffAllDevices()` method that calls the `turnOffTv()` and `turnOffLight()` methods:.

```kotlin   
class SmartHome(
    val smartTvDevice: SmartTvDevice,
    val smartLightDevice: SmartLightDevice
) {
    
    fun turnOnTv() {
        smartTvDevice.turnOn()
    }
    
    fun turnOffTv() {
        smartTvDevice.turnOff()
    }
    
    fun increaseTvVolume() {
        smartTvDevice.increaseSpeakerVolume()
    }
    
    fun changeTvChannelToNext() {
        smartTvDevice.nextChannel()
    }
    
    fun turnOnLight() {
        smartLightDevice.turnOn()
    }
    
    fun turnOffLight() {
        smartLightDevice.turnOff()
    }
    
    fun increaseLightBrightness() {
        smartLightDevice.increaseBrightness()
    }
    
    fun turnOffAllDevices() {
   		turnOffTv()
        turnOffLight()
    }
}
```


### Override superclass methods from subclasses

Override the `SmartDevice` class `turnOn()` and `turnOff()` methods


1. In the body of the `SmartDevice` superclass before the `fun` keyword of each method, add an `open` keyword:


```kotlin
open class SmartDevice(val name: String, val category: String) {
	
	...      
        
    open fun turnOn() {
        ...
    }
    
    open fun turnOff() {
        ...        
    }
}
```


2. In the body of the `SmartLightDevice` class, define a `turnOn()` method with an empty body:

3. In the body of the `turnOn()` method, set the `deviceStatus` property to the string "`on`", set the `brightnessLevel` property to a value of `2`, and add a `println()` statement and then pass it a `"$name` `turned` `on.` `The` `brightness` `level` `is` `$brightnessLevel."` string:

4. In the body of the `SmartLightDevice` class, define a `turnOff()` method with an empty body:

5. In the body of the `turnOff()` method, set the `deviceStatus` property to the string "`off`", set the `brightnessLevel` property to a value of `0`, and add a `println()` statement and then pass it a `"Smart` `Light` `turned` `off"` string:

6. In the `SmartLightDevice` subclass before the `fun` keyword of the `turnOn()` and `turnOff()` methods, add the `override` keyword:


```kotlin
class SmartLightDevice(deviceName: String, deviceCategory: String):
	SmartDevice(name = deviceName, category = deviceCategory) {
        
	var brightnessLevel = 0
        set(value) {
            if (value in 0..100) {
                field = value
            }
        }
        
   fun increaseBrightness() {
       brightnessLevel ++
       println("Brightness increased to $brightnessLevel")
   }
   
   override fun turnOn() {
       deviceStatus = "on"
       brightnessLevel = 2
       println("$name turned on. The brightness leves is $brightnessLevel")
   }
   
   override fun turnOff() {
       deviceStatus = "off"
       brightnessLevel = 0
       println("Smart Light turned off")
       
   }
}
```


>[!info] The `override` keyword informs the Kotlin runtime to execute the code enclosed in the method defined in the subclass.

>[!warning] En Kotlin, si intentas agregar `override` a un método en una subclase, pero el método en la clase padre **no está marcado con `open`**, obtendrás un **error de compilación**. Esto se debe a que, en Kotlin, todas las clases y métodos son **finales por defecto**, lo que significa que no pueden ser heredados o sobrescritos a menos que se marquen explícitamente como `open`.


7. In the body of the `SmartTvDevice` class, define a `turnOn()` method with an empty body:

8. In the body of the `turnOn()` method, set the `deviceStatus` property to the string "`on`" and add a `println()` statement and then pass it a `"$name is turned on. Speaker volume is set to $speakerVolume and channel number is " + "set to $channelNumber."` string:

9. In the body of the `SmartTvDevice` class after the `turnOn()` method, define a `turnOff()` method with an empty body:

10. In the body of the `turnOff()` method, set the `deviceStatus` property to the string "`off`" and add a `println()` statement and then pass it a `"$name` `turned` `off"` string:

11. In the `SmartTvDevice` class before the `fun` keyword of the `turnOn()` and `turnOff()` methods, add the `override` keyword:


```kotlin
class SmartTvDevice(deviceName: String, deviceCategory: String):
	SmartDevice(name = deviceName, category = deviceCategory) {
        
    
	var speakerVolume = 2
        set(value) {
            if (value in 0..100) {
                field  = value
            }
        }
        
    var channelNumber = 1 
        set(value) {
            if (value in 1..200) {
                field = value
            }
        }
        
    fun increaseSpeakerVolume() {
        speakerVolume = speakerVolume + 1
        println("Speaker volume increased to $speakerVolume")
    }
    
    fun nextChannel() {
        channelNumber ++ 
        println("Channel number increased to $channelNumber")
    }
    
    override fun turnOn() {
        deviceStatus = "on" 
        println("$name is turned on. Speaker volume is set to $speakerVolume" + "
                " and channel channel number is set to $channelNumber.")
    }
    
    override fun turnOff() {
        deviceStatus = "off"
        println("$name turned off.")
    }
    
}
```

12. In the `main()` function, use the `var` keyword to define a `smartDevice` variable of `SmartDevice` type that instantiates a `SmartTvDevice` object that takes an `"Android` `TV"` argument and an `"Entertainment"` argument:

13. On the line after the `smartDevice` variable, call the `turnOn()` method on the `smartDevice` object:

14. Run the code.

```
Android TV is turned on. Speaker volume is set to 2 and channel channel number is set to 1.
```


16. On the line after the call to the `turnOn()` method, reassign the `smartDevice` variable to instantiate a `SmartLightDevice` class that takes a `"Google` `Light"` argument and a `"Utility"` argument, and then call the `turnOn()` method on the `smartDevice` object reference:

17. Run the code.

```
Android TV is turned on. Speaker volume is set to 2 and channel channel number is set to 1. 
Google Light turned on. The brightness leves is 2
```


### Reuse superclass code in subclasses with the `super` keyword
To call the overridden method in the superclass from the subclass, you need to use the `super` keyword. Calling a method from the superclass is similar to calling the method from outside the class. Instead of using a `.` operator between the object and method, you need to use the `super` keyword, which informs the Kotlin compiler to call the method on the superclass instead of the subclass

![](https://developer.android.com/static/codelabs/basic-android-kotlin-compose-classes-and-objects/img/18cc94fefe9851e0_960.png)

Reuse the code from the `SmartDevice` superclass:

1. Remove the `println()` statements from the `turnOn()` and `turnOff()` methods and move the duplicated code from the `SmartTvDevice` and `SmartLightDevice` subclasses to the `SmartDevice` superclass:

```kotlin
open class SmartDevice(val name: String, val category: String) {
	var deviceStatus = "online"

	open fun turnOn() {
		deviceStatus = "on"
	}

	open fun turnOff() {
		deviceStatus = "off"
	}
}
```

2. Use the `super` keyword to call the methods from the `SmartDevice` class in the `SmartTvDevice` and `SmartLightDevice` subclasses:

```kotlin
class SmartTvDevice(deviceName: String, deviceCategory: String):
	SmartDevice(name = deviceName, category = deviceCategory) {
        
    
	var speakerVolume = 2
        set(value) {
            if (value in 0..100) {
                field  = value
            }
        }
        
    var channelNumber = 1 
        set(value) {
            if (value in 1..200) {
                field = value
            }
        }
        
    fun increaseSpeakerVolume() {
        speakerVolume = speakerVolume + 1
        println("Speaker volume increased to $speakerVolume")
    }
    
    fun nextChannel() {
        channelNumber ++ 
        println("Channel number increased to $channelNumber")
    }
    
    override fun turnOn() {
        super.turnOn() 
        println("$name is turned on. Speaker volume is set to $speakerVolume" + "
                " and channel channel number is set to $channelNumber.")
    }
    
    override fun turnOff() {
	    super.turnOff()
        println("$name turned off.")
    }
    
}
```



```kotlin
class SmartLightDevice(deviceName: String, deviceCategory: String):
	SmartDevice(name = deviceName, category = deviceCategory) {
        
	var brightnessLevel = 0
        set(value) {
            if (value in 0..100) {
                field = value
            }
        }
        
   fun increaseBrightness() {
       brightnessLevel ++
       println("Brightness increased to $brightnessLevel")
   }
   
   override fun turnOn() {
       super.turnOn
       brightnessLevel = 2
       println("$name turned on. The brightness leves is $brightnessLevel")
   }
   
   override fun turnOff() {
       super.turnOff()
       brightnessLevel = 0
       println("Smart Light turned off")
       
   }
}
```


### Override superclass properties from subclasses
Similar to methods, you can also override properties with the same steps.

Override the `deviceType` property:


1. In the `SmartDevice` superclass on the line after the `deviceStatus` property, use the `open` and `val` keywords to define a `deviceType` property set to an `"unknown"` string:

```kotlin
open class SmartDevice(val name: String, val category: String) {
	var deviceStatus = "online"

	open val deviceType = "unknown"
	...
}
```

2. In the `SmartTvDevice` class, use the `override` and `val` keywords to define a `deviceType` property set to a `"Smart` `TV"` string:

```kotlin
class SmartTvDevice(deviceName: String, deviceCategory: String) :
    SmartDevice(name = deviceName, category = deviceCategory) {

	...
	override val deviceType = "Smart TV"
    ...
}
```


3. In the `SmartLightDevice` class, use the `override` and `val` keywords to define a `deviceType` property set to a`"Smart` `Light"` string:

```kotlin
class SmartLightDevice(deviceName: String, deviceCategory: String) :
    SmartDevice(name = deviceName, category = deviceCategory) {

	...
    override val deviceType = "Smart Light"
    ...

}
```
Ya funciona la lista circular, para avanzar y retroceder
```kotlin
/**
 * You can edit, run, and share this code.
 * play.kotlinlang.org
 * 
 * 
 */
fun main() {
    
  var listaNumeros = ArrayList((1..5).toList())
  var listaCircularNumbers = CircularList(listaNumeros)
  
  var valor: Int? = listaCircularNumbers?.head?.value
  println(valor)
  
  listaCircularNumbers = aleatorioNumbers(listaNumeros)
  valor = listaCircularNumbers?.head?.value
  
  println("Avanzar")  
  println(valor)
  for (i in 1..20) {
      valor = listaCircularNumbers?.getNextNode(valor)?.value
      println(valor)
  }
  
  println("Retroceder")
  for (i in 1..20) {
      valor = listaCircularNumbers?.getPrevNode(valor)?.value
      println(valor)
  }
    
}

private fun nextNumber(actualNumber: Int?, listaCircular: CircularList): Int? {
    val nextNode = listaCircular.getNextNode(actualNumber)
    return nextNode?.value
}

private fun aleatorioNumbers(listaNumeros: ArrayList<Int>): CircularList {
    val newList = ArrayList(listaNumeros.shuffled())
    for(i in newList) {
        print("$i ")
    }
    val listaCircularNumbers = CircularList(newList)
    println("\nHead: ${listaCircularNumbers?.head?.value}")
    println("Tail: ${listaCircularNumbers?.tail?.value}")
    return listaCircularNumbers
}

class CircularList(numberList: ArrayList<Int>) {
    var head: Node? = null
    var tail: Node? = null

    init {
        for(number in numberList) {
            add(number)
        }
    }

    fun add(value: Int) {
        val newNode = Node(value)
        if (head == null) {
            head = newNode
            tail = newNode
            newNode.nextNode = tail
        } else {
            if (tail == null) {
                tail = newNode
                newNode.nextNode = head
            } else {
                tail?.nextNode = newNode
                tail = newNode
                tail?.nextNode = head
            }
        }
    }

    fun getNextNode(value: Int?): Node?{
        var current = head
        while(current?.value != value) {
            current = current?.nextNode
        }
        return current?.nextNode
    }

    fun getPrevNode(value: Int?): Node? {
        var current = head
        while(current?.nextNode?.value != value) {
            current = current?.nextNode
        }
        return current
    }
}

class Node(val value: Int) {
    var nextNode: Node? = null
}
```
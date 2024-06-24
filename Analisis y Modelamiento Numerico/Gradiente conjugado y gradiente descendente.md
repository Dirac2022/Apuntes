
Nuestra estimación muestra que siempre se produce una reducción del valor de q al pasar de x a x+tv, a menos que v sea ortogonal al residual, es decir, v, b-Ax=0. Si x no es una solución del sistema Ax=b, entonces existen muchos vectores v que satisfacen v, b-Ax=0. Por lo tanto, si Ax=b, la x no minimiza q. Por otro lado, si Ax=b, no hay ningún rayo que emane de x sobre el cual q toma un valor menor





La prueba precedente sugiere un método iterativo para resolver Ax=b. Procedemos minimizando q a lo largo de una sucesión de rayos. En el paso kth en tal algoritmo, x0, x1, ...xk estaría disponible. Luego, mediante el uso de alguna regla, se elige una dirección de búsqueda adecuada vk. El siguiente punto en nuestra secuencia es



para valores específicos del escalar tk, y los vectores vk. Si vk=1, entonces tk mide la distancia que nos movemos desde xk para obtener xk+1


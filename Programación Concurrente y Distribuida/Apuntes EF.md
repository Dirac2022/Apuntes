


> [!tip] Why Classes Must Be Serialized in Java for Network Transmission
> Because network protocols works with bytes. Networks transmit raw bytes, not Java objects, so serialization converts objects into a byte stream that can be transmited



> [!tip] What is payload
> The payload is the actual data being sent or received excluding headers or metadata.


>[!tip] Primary segments vs Replicas
>Primary segments are the data that the worker manages directly and can process or compute. The replicas are copies of those primary segments received from other workers to ensure availability and fault tolerance in this distributed system.



# `Message`



# `Worker`

## `private void startReplicaServer`
Inicia un `ServerSocket` en un hilo separado. Esto es crucial para que el worker pueda recibir datos de réplica de otro worker sin bloquear su comunicación principal con el Master.

## `public void start()`
This method configures the Worker to be ready to receive and process data from the Master and other Workers, managing both primary segments and replicas.
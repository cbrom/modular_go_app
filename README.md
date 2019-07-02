# Modular golang based project

The proposal is about to separate the layers with interfaces to use them as injectors within the models and the data delivery.

## CORE
The business engine will contain 3 main layers. 
Based on the known structure proposal [here](https://hackernoon.com/golang-clean-archithecture-efd6d7c43047).

Each layer will have the internal functions and structs that will be used to achieve it's objective, but **there is only one exported handler abstraction to the other layers, the INTERFACE**.

<br>
 - LAYER:
 Any layer must be independent of the rest of them. At the same type, each layer will contain:
   A **dependency injector**: which will contain the main abstraction of all the exported types through a **minimal interface**.
   One/some **types**: as struct object types (i.e: models).

### Proposed layers:

 - DATABASE LAYER:
  
The database layer will just connect to the database and handle low-level queries and inserts.

<br>

 - MODELS LAYER:

The models layer will have the structs of all the models and the methods that defines all of them.

<br>

 - BUSINESS LAYER:

The business layer will contain the rules on a sub-module [rules](github.com/sebach1/modular_go_app/core/rules) which should be internal (no other layer can have access to the rules).

<br>

 - SERVER LAYER: (optional)

The server will serve all the Interfaces through http handling. This layer isn't expected to be, and the motive is below. 
This will be **strictly** asynchronous.

## Modules

All the delivery and response handling will be on the modules that use that core. 
Example: we need to build an API. Then, we create the project totally separated from the CORE and should use the layers from the core through interfaces.

#### How?

 - If the API is written in golang, you can just import the interfaces from the layers.

 - If the API can't understand the interfaces (i.e: written in Ruby), then you'll need to use the fourth layer.

 - In case you have both types, the recommended case is to always use the server layer.


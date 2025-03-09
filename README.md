# Diagrama-de-secuencias

### **Trabajo a Realizar**

---

#### **a) Diagramas de Secuencia**

##### **1. Clases Estereotipadas (Análisis)**
A partir del diagrama de estados que hicimos antes, identificamos las clases que necesitamos para los casos de uso **CU: Validación Usuario** y **CU: Sacar Dinero**. Estas clases se dividen en tres tipos:

- **Interfaces**:
  - `IU_ValidacionUsuario`: Es la pantalla donde el usuario mete la tarjeta y el PIN.
  - `IU_SacarDinero`: Es la pantalla donde el usuario elige cuánto dinero quiere sacar.

- **Control**:
  - `C_ValidacionUsuario`: Es el "jefe" que controla si la tarjeta y el PIN son correctos.
  - `C_SacarDinero`: Es el "jefe" que controla si se puede sacar el dinero.

- **Entidad**:
  - `E_Usuario`: Aquí están los datos del usuario, como su tarjeta y PIN.
  - `E_CuentaBancaria`: Aquí está la información de la cuenta, como el saldo.

---

##### **2. Diagrama de Secuencia Básico (Estereotipado)**

###### **Código en PlantUML para CU: Validación Usuario**
```plantuml
@startuml
actor Usuario
participant "IU_ValidacionUsuario" as IU
participant "C_ValidacionUsuario" as C
participant "E_Usuario" as E

Usuario -> IU: Introduce tarjeta
IU -> C: Validar tarjeta
C -> E: Verificar tarjeta
E --> C: Tarjeta válida
C -> IU: Solicitar PIN
Usuario -> IU: Introduce PIN
IU -> C: Validar PIN
C -> E: Verificar PIN
E --> C: PIN válido
C --> IU: Usuario validado
IU --> Usuario: Acceso concedido
@enduml
```

###### **Código en PlantUML para CU: Sacar Dinero**
```plantuml
@startuml
actor Usuario
participant "IU_SacarDinero" as IU
participant "C_SacarDinero" as C
participant "E_CuentaBancaria" as E

Usuario -> IU: Selecciona "Sacar dinero"
IU -> C: Solicitar monto
Usuario -> IU: Introduce monto
IU -> C: Validar monto
C -> E: Verificar saldo
E --> C: Saldo suficiente
C -> E: Descontar monto
E --> C: Saldo actualizado
C --> IU: Transacción exitosa
IU --> Usuario: Entrega dinero
@enduml
```

---

##### **3. Clases de Diseño**
Ahora, a partir de las clases anteriores, creamos las clases de diseño, que son como las versiones "reales" que se usarían en el programa:

- **Interfaces**:
  - `PantallaValidacion`: Es la pantalla donde el usuario mete la tarjeta y el PIN.
  - `PantallaSacarDinero`: Es la pantalla donde el usuario elige cuánto dinero quiere sacar.

- **Control**:
  - `ControladorValidacion`: Es el que verifica si la tarjeta y el PIN son correctos.
  - `ControladorSacarDinero`: Es el que verifica si se puede sacar el dinero.

- **Entidad**:
  - `Usuario`: Aquí están los datos del usuario, como su tarjeta y PIN.
  - `CuentaBancaria`: Aquí está la información de la cuenta, como el saldo.

---

##### **4. Diagrama de Secuencia Final**

###### **Código en PlantUML para CU: Validación Usuario (Final)**
```plantuml
@startuml
actor Usuario
participant "PantallaValidacion" as PV
participant "ControladorValidacion" as CV
participant "Usuario" as U
participant "CuentaBancaria" as CB

Usuario -> PV: Introduce tarjeta
PV -> CV: Validar tarjeta
CV -> U: Verificar tarjeta
U --> CV: Tarjeta válida
CV -> PV: Solicitar PIN
Usuario -> PV: Introduce PIN
PV -> CV: Validar PIN
CV -> U: Verificar PIN
U --> CV: PIN válido
CV --> PV: Usuario validado
PV --> Usuario: Acceso concedido
@enduml
```

###### **Código en PlantUML para CU: Sacar Dinero (Final)**
```plantuml
@startuml
actor Usuario
participant "PantallaSacarDinero" as PS
participant "ControladorSacarDinero" as CS
participant "CuentaBancaria" as CB

Usuario -> PS: Selecciona "Sacar dinero"
PS -> CS: Solicitar monto
Usuario -> PS: Introduce monto
PS -> CS: Validar monto
CS -> CB: Verificar saldo
CB --> CS: Saldo suficiente
CS -> CB: Descontar monto
CB --> CS: Saldo actualizado
CS --> PS: Transacción exitosa
PS --> Usuario: Entrega dinero
@enduml
```

---

#### **b) Interpretación del Diagrama Final de CU: Validación Usuario**

El diagrama de secuencia final para el caso de uso **Validación Usuario** muestra cómo el usuario se valida en el cajero. Aquí está explicado paso a paso:

1. **El usuario mete la tarjeta**:
   - El usuario introduce su tarjeta en la `PantallaValidacion`.

2. **Se valida la tarjeta**:
   - La `PantallaValidacion` le dice al `ControladorValidacion` que valide la tarjeta.
   - El `ControladorValidacion` le pregunta a la clase `Usuario` si la tarjeta es válida.

3. **Tarjeta válida**:
   - Si la tarjeta es válida, el `ControladorValidacion` le pide a la `PantallaValidacion` que pida el PIN.

4. **El usuario mete el PIN**:
   - El usuario introduce su PIN en la `PantallaValidacion`.

5. **Se valida el PIN**:
   - La `PantallaValidacion` le dice al `ControladorValidacion` que valide el PIN.
   - El `ControladorValidacion` le pregunta a la clase `Usuario` si el PIN es correcto.

6. **PIN válido**:
   - Si el PIN es correcto, el `ControladorValidacion` le dice a la `PantallaValidacion` que el usuario está validado.

7. **Acceso concedido**:
   - La `PantallaValidacion` le dice al usuario que puede usar el cajero.

---

#### **c) ¿De qué manera te ayuda un diagrama de secuencias durante el proceso de desarrollo del software?**

Un diagrama de secuencias es super útil cuando estás haciendo un programa porque:

1. **Te ayuda a entender cómo funciona todo**:
   - Te muestra paso a paso cómo los objetos (como las pantallas y los controladores) interactúan entre sí.

2. **Te ayuda a encontrar errores**:
   - Si algo no está funcionando bien, puedes mirar el diagrama y ver dónde está el problema.

3. **Es fácil de explicar**:
   - Si tienes que explicarle a alguien cómo funciona el programa, el diagrama es una forma clara y sencilla de hacerlo.

4. **Te guía para escribir el código**:
   - El diagrama te dice qué tiene que hacer cada parte del programa, así que es más fácil escribir el código.

5. **Sirve como documentación**:
   - Si en el futuro alguien tiene que arreglar o mejorar el programa, el diagrama le ayuda a entender cómo está hecho.


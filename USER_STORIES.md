  # User Stories — Sistema de Venta de Entradas
> Escala de estimación: Fibonacci (1, 2, 3, 5, 8, 13) 

## Definition of Ready (DoR)

Una historia de usuario entra al sprint cuando cumple con:

- Formato Como / Quiero / Para redactado correctamente
- Valor de negocio identificable y claro
- Criterios de aceptación definidos en Gherkin
- Estimación en Story Points asignada
- Historia cargada en el tablero de GitHub Projects

## Definition of Done (DoD)

Una historia de usuario se considera terminada cuando cumple con:

- Formato Como / Quiero / Para completo y claro
- Criterios de aceptación escritos en Gherkin declarativo
- Escenarios cubren el camino feliz y los casos alternos o límite
- Tasking desglosado desde la perspectiva DEV y QA
- Estimación en Story Points asignada y justificada
- Historia registrada en el tablero de GitHub Projects
- Commit atómico subido al repositorio con mensaje descriptivo

---
## HU-01: Creación de evento de obra de teatro

**Story Points: 5**

### Historia de Usuario

Como administrador

Quiero crear un evento de obra de teatro con su información base y aforo permitido

Para prepararlo para su configuración comercial y posterior publicación

### Criterios de Aceptación (CA)
 
**CA-01. Evento creado en estado borrador**
 
```gherkin
Escenario: Creación exitosa de evento
Dado que el administrador tiene acceso previamente habilitado al sistema
Y dispone de la información obligatoria del evento
Cuando registra un evento con datos válidos
Y define un aforo dentro del máximo permitido de la sala
Entonces el sistema crea el evento en estado borrador
```
**CA-02. Rechazo por aforo superior al máximo**
 
```gherkin
Escenario: Aforo superior al máximo de la sala
Dado que el administrador tiene acceso previamente habilitado al sistema
Y la sala tiene un aforo máximo definido
Cuando intenta registrar un evento con un aforo superior al permitido
Entonces el sistema rechaza la creación del evento
```
**CA-03. Rechazo por información obligatoria incompleta**
 
```gherkin
Escenario: Información mínima incompleta
Dado que el administrador tiene acceso previamente habilitado al sistema
Cuando intenta registrar un evento sin la información mínima requerida
Entonces el sistema no crea el evento
```
---
## HU-02: Configuración de tiers y precios por evento

**Story Points: 5**

### Historia de Usuario

Como administrador

Quiero configurar los tiers, cupos y precios de una obra de teatro

Para ofrecer una estructura de venta alineada con la estrategia comercial del evento

### Criterios de Aceptación (CA)

**CA-01. Configuración válida de tiers**
```gherkin
Escenario: Configuración comercial exitosa
Dado que existe un evento en estado borrador
Cuando el administrador define los tiers VIP, General y Early Bird
Y asigna cupos y precios válidos a cada tier
Entonces el sistema guarda la configuración comercial del evento
```
**CA-02. Vigencia temporal del Early Bird**
 
```gherkin
Escenario: Early Bird con vigencia válida
Dado que existe un evento en estado borrador
Cuando el administrador define una ventana de tiempo válida para el tier Early Bird
Entonces el sistema habilita ese tier únicamente dentro del período configurado
```
**CA-03. Rechazo por precio inválido**
 
```gherkin
Escenario: Precio no válido en un tier
Dado que existe un evento en estado borrador
Cuando el administrador asigna a un tier un precio igual o menor a cero
Entonces el sistema rechaza la configuración
```
**CA-04. Rechazo por suma de cupos mayor al aforo**
 
```gherkin
Escenario: Cupos por tier exceden el aforo total
Dado que existe un evento con aforo definido
Cuando la suma de cupos asignados a los tiers supera el aforo total del evento
Entonces el sistema no permite guardar la configuración
```
---

## HU-03: Visualización de eventos y disponibilidad

**Story Points: 3**

### Historia de Usuario

Como comprador

Quiero consultar los eventos disponibles y la disponibilidad por tier

Para elegir una entrada según mis preferencias y presupuesto

### Criterios de Aceptación (CA)
**CA-01. Consulta de eventos publicados**
 
```gherkin
Escenario: Visualización de eventos disponibles
Dado que existen eventos publicados con entradas disponibles
Cuando el comprador consulta la cartelera
Entonces el sistema muestra los eventos disponibles para compra
Y presenta la disponibilidad vigente por tier
```
**CA-02. Tier agotado**
 
```gherkin
Escenario: Tier agotado
Dado que un tier ya no tiene entradas disponibles
Cuando el comprador consulta el detalle del evento
Entonces el sistema lo muestra como no disponible
```
**CA-03. Early Bird vencido**
 
```gherkin
Escenario: Early Bird fuera de vigencia
Dado que la ventana de tiempo del tier Early Bird ya finalizó
Cuando el comprador consulta el detalle del evento
Entonces el sistema no lo presenta como opción disponible
```
---
## HU-04: Reserva y compra de entrada con pago simulado

**Story Points: 8**

### Historia de Usuario

Como comprador

Quiero reservar una entrada y completar un pago simulado dentro de un tiempo límite

Para asegurar mi acceso al evento sin perder disponibilidad durante el proceso
### Criterios de Aceptación (CA)
**CA-01. Compra exitosa dentro del tiempo permitido**
```gherkin
Escenario: Compra confirmada dentro del tiempo de reserva
Dado que existe disponibilidad para el tier seleccionado
Cuando el comprador genera una reserva
Y completa un pago exitoso antes de que transcurran 10 minutos
Entonces el sistema confirma la compra
Y descuenta la entrada del inventario disponible
```
**CA-02. Compra fallida por pago rechazado**
```gherkin
Escenario: Pago simulado rechazado
Dado que existe una reserva activa dentro del tiempo permitido
Cuando el sistema recibe un resultado de pago rechazado
Entonces la compra se marca como fallida
Y la entrada no queda confirmada para el comprador
```
**CA-03. Expiración de la reserva**
```gherkin
Escenario: Reserva expirada por tiempo
Dado que existe una reserva activa sin pago exitoso
Cuando transcurren 10 minutos desde su creación
Entonces el sistema expira la reserva
```
**CA-04. Protección ante compra simultánea**
```gherkin
Escenario: Última entrada solicitada por dos compradores
Dado que solo queda una entrada disponible en un tier
Cuando dos compradores intentan completar la compra de forma concurrente
Entonces el sistema confirma la compra para un solo comprador
Y evita la duplicidad de venta
```
---
## HU-05: Liberación automática por fallo de pago o expiración

**Story Points: 8**

### Historia de Usuario

Como administrador del sistema

Quiero que las entradas reservadas se liberen automáticamente cuando el pago falla o expira

Para garantizar disponibilidad real y evitar bloqueo innecesario de inventario
### Criterios de Aceptación (CA)
 
**CA-01. Liberación por expiración de reserva**
 
```gherkin
Escenario: Entrada liberada al vencerse la reserva
Dado que una reserva permanece sin pago exitoso
Cuando se cumple el tiempo máximo de 10 minutos
Entonces el sistema libera automáticamente la entrada asociada
```
**CA-02. Liberación por pago rechazado**
 
```gherkin
Escenario: Entrada liberada tras rechazo de pago
Dado que una reserva se encuentra activa
Cuando el sistema registra un pago rechazado
Entonces la entrada reservada vuelve a estar disponible
```
**CA-03. Disponibilidad actualizada luego de la liberación**
 
```gherkin
Escenario: Entrada visible nuevamente para otros compradores
Dado que una entrada fue liberada por expiración o pago fallido
Cuando otro comprador consulta la disponibilidad del evento
Entonces el sistema refleja nuevamente esa entrada como disponible
```
**CA-04. Recuperación ante falla del mecanismo principal**
```gherkin
Escenario: Recuperación ante falla del mecanismo principal
Dado que existe una reserva vencida que no fue liberada por el proceso principal
Cuando se ejecuta un proceso de verificación de respaldo
Entonces el sistema regulariza el estado de la reserva
Y libera la entrada correspondiente
```
---
## HU-06: Notificaciones al comprador

**Story Points: 3**

### Historia de Usuario

Como comprador

Quiero recibir notificaciones inmediatas sobre el resultado de mi proceso de compra

Para conocer oportunamente el estado de mi reserva o compra
### Criterios de Aceptación (CA)
 
**CA-01. Notificación de compra exitosa**
 
```gherkin
Escenario: Notificación de compra confirmada
Dado que el comprador completa un pago exitoso
Cuando el sistema confirma la compra
Entonces el comprador recibe una notificación de compra confirmada
```
**CA-02. Notificación de pago fallido**
 
```gherkin
Escenario: Notificación de pago rechazado
Dado que el comprador intenta completar el pago de una reserva
Cuando el sistema registra un rechazo de pago
Entonces el comprador recibe una notificación de pago fallido
```
**CA-03. Notificación de liberación de reserva**
 
```gherkin
Escenario: Notificación de liberación por expiración
Dado que una reserva del comprador expira sin pago exitoso
Cuando el sistema libera la entrada
Entonces el comprador recibe una notificación informando la liberación
```
---
## HU-07: Visualización de ticket confirmado

**Story Points: 2**

### Historia de Usuario

Como comprador

Quiero visualizar el ticket confirmado de mi compra

Para disponer de la evidencia de acceso al evento adquirido
### Criterios de Aceptación (CA)
 
**CA-01. Ticket disponible tras compra exitosa**
 
```gherkin
Escenario: Ticket visible después de una compra confirmada
Dado que el comprador completó una compra exitosa
Cuando consulta sus tickets emitidos
Entonces el sistema muestra el ticket confirmado de la compra
```
**CA-02. Ticket con información correcta**
 
```gherkin
Escenario: Datos correctos en el ticket
Dado que existe un ticket confirmado asociado a una compra exitosa
Cuando el comprador lo visualiza
Entonces el sistema muestra correctamente la información del evento, el tier adquirido y la compra realizada
```
**CA-03. Ausencia de ticket en compra no confirmada**
 
```gherkin
Escenario: Compra sin ticket por no haberse confirmado
Dado que una reserva no finalizó con pago exitoso
Cuando el comprador consulta sus tickets
Entonces el sistema no genera ni muestra un ticket asociado a esa operación
```
---

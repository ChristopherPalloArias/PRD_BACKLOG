  # User Stories — Sistema de Venta de Entradas
> Escala de estimación: Fibonacci (1, 2, 3, 5, 8, 13)
> 
> Formato obligatorio: Como [rol] / Quiero [acción] / Para [beneficio]
> 
> Criterios de Aceptación: Gherkin declarativo, centrado en comportamiento de negocio
> 

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

### Casos de Prueba Funcionales (CP-F)
 
**CP-F01. Creación exitosa con datos completos**
 
```gherkin
Dado que el administrador tiene acceso al sistema
Y existe una sala con aforo máximo de 300
Cuando registra un evento con nombre "Bodas de Sangre", fecha "2026-05-10" y aforo 250
Entonces el sistema crea el evento en estado borrador con aforo 250
```
**CP-F02. Rechazo por aforo superior al máximo**
 
```gherkin
Dado que el administrador tiene acceso al sistema
Y existe una sala con aforo máximo de 200
Cuando registra un evento con aforo 201
Entonces el sistema rechaza la operación
Y el evento no queda persistido
```
**CP-F03. Rechazo por fecha faltante**
 
```gherkin
Dado que el administrador tiene acceso al sistema
Cuando registra un evento con nombre "Bodas de Sangre" y sala válida pero sin fecha
Entonces el sistema no crea el evento
```
**CP-F04. Rechazo por múltiples campos faltantes**
 
```gherkin
Dado que el administrador tiene acceso al sistema
Cuando registra un evento sin nombre y sin fecha
Entonces el sistema no crea el evento
```
### Casos de Prueba No Funcionales (CP-NF)
 
**CP-NF01. Sin registros parciales ante operación rechazada**
 
```gherkin
Dado que el administrador intenta crear un evento con aforo inválido
Cuando el sistema rechaza la operación
Entonces no quedan registros parciales del evento en base de datos
```
**CP-NF02. Trazabilidad de operaciones**
 
```gherkin
Dado que el administrador crea tres eventos consecutivos
Cuando cada operación se completa
Entonces cada una queda registrada con usuario, fecha y resultado
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
### Casos de Prueba Funcionales (CP-F)
 
**CP-F01. Configuración exitosa de los tres tiers**
 
```gherkin
Dado que existe un evento con aforo total de 300
Cuando se configura VIP con 50 cupos a $45, General con 200 cupos a $25 y Early Bird con 50 cupos a $18
Entonces el sistema guarda la configuración
Y la suma de cupos 300 no supera el aforo del evento
```
**CP-F02. Early Bird disponible solo en su ventana de tiempo**
 
```gherkin
Dado que existe un evento en estado borrador
Cuando se configura el tier Early Bird con fecha de inicio "2026-04-01" y fin "2026-04-10"
Entonces el tier está disponible únicamente dentro de ese período
Y fuera de esa ventana el tier no aparece como opción de compra
```
**CP-F03. Rechazo de precios inválidos**
 
```gherkin
Dado que existe un evento en estado borrador
Cuando se asigna precio $0 al tier General
Y precio -5 al tier VIP
Entonces el sistema rechaza ambas configuraciones
```
**CP-F04. Rechazo por cupos que exceden el aforo**
 
```gherkin
Dado que existe un evento con aforo total de 200
Cuando se configura VIP con 100 cupos, General con 100 cupos y Early Bird con 50 cupos
Entonces el sistema rechaza la configuración
Y no persiste ningún cambio
```
### Casos de Prueba No Funcionales (CP-NF)
 
**CP-NF01. Integridad referencial entre evento y tiers**
 
```gherkin
Dado que se configuran tres tiers para un evento
Cuando la configuración se guarda correctamente
Entonces cada tier queda vinculado al evento sin registros huérfanos en base de datos
```
 
**CP-NF02. Consistencia ante actualizaciones consecutivas**
 
```gherkin
Dado que el precio de un tier se actualiza dos veces consecutivas
Cuando ambas operaciones se completan
Entonces el sistema conserva únicamente el último valor registrado
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
### Casos de Prueba Funcionales (CP-F)
**CP-F01. Cartelera con eventos y tiers vigentes** 
```gherkin
Dado que existen dos eventos publicados con entradas disponibles en todos sus tiers
Cuando el comprador consulta la cartelera
Entonces el sistema muestra ambos eventos
Y presenta la disponibilidad vigente por tier para cada uno
```
**CP-F02. Tier agotado no disponible**
 
```gherkin
Dado que el evento "Bodas de Sangre" tiene el tier General con 0 entradas disponibles
Cuando el comprador consulta el detalle del evento
Entonces el sistema muestra el tier General como no disponible
Y los tiers VIP y Early Bird siguen mostrándose con su disponibilidad real
```
**CP-F03. Early Bird vencido no aparece como opción**
 
```gherkin
Dado que el tier Early Bird del evento "Bodas de Sangre" venció el "2026-04-10"
Y la fecha actual es posterior a esa fecha
Cuando el comprador consulta el detalle del evento
Entonces el sistema no presenta el tier Early Bird como opción de compra
```
### Casos de Prueba No Funcionales (CP-NF)
**CP-NF01. Tiempo de respuesta bajo carga**
 
```gherkin
Dado que 50 compradores consultan la cartelera de forma simultánea
Cuando el sistema procesa todas las solicitudes
Entonces cada consulta obtiene respuesta en un tiempo aceptable
```
**CP-NF02. Consistencia entre disponibilidad mostrada y reservas activas**
 
```gherkin
Dado que existe una entrada reservada pero aún no pagada para el tier General
Cuando el comprador consulta la disponibilidad del evento
Entonces el sistema refleja esa entrada como no disponible hasta que la reserva expire o se confirme
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
**CA-04. Protección ante compra simultánea**

## HU-05: Liberación automática por fallo de pago o expiración

*Story Points: 8*

### Historia de Usuario

Como sistema

Quiero liberar automáticamente las entradas reservadas que no se concretan

Para mantener disponibilidad real y evitar bloqueo innecesario de inventario

## HU-06: Notificaciones al comprador

*Story Points: 3*

### Historia de Usuario

Como comprador

Quiero recibir notificaciones inmediatas sobre el resultado de mi proceso de compra

Para conocer oportunamente el estado de mi reserva o compra

## HU-07: Visualización de ticket confirmado

*Story Points: 2*

### Historia de Usuario

Como comprador

Quiero visualizar el ticket confirmado de mi compra

Para disponer de la evidencia de acceso al evento adquirido

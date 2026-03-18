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

## HU-01: Creación de evento de obra de teatro

*Story Points: 5*

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


## HU-02: Configuración de tiers y precios por evento

*Story Points: 5*

### Historia de Usuario

Como administrador

Quiero configurar los tiers, cupos y precios de una obra de teatro

Para ofrecer una estructura de venta alineada con la estrategia comercial del evento


## HU-03: Visualización de eventos y disponibilidad

*Story Points: 3*

### Historia de Usuario

Como comprador

Quiero consultar los eventos disponibles y la disponibilidad por tier

Para elegir una entrada según mis preferencias y presupuesto


## HU-04: Reserva y compra de entrada con pago simulado

*Story Points: 8*

### Historia de Usuario

Como comprador

Quiero reservar una entrada y completar un pago simulado dentro de un tiempo límite

Para asegurar mi acceso al evento sin perder disponibilidad durante el proceso

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

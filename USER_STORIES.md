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
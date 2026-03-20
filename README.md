# Ticketing System — Sistema de Venta de Entradas para Obras de Teatro

## Descripción
Sistema de gestión y venta de entradas para obras de teatro que resuelve 
el problema del inventario bloqueado. Cuando un comprador no completa su 
pago, las entradas se liberan automáticamente en 10 minutos, garantizando 
disponibilidad real en todo momento.

## Integrantes
- Christopher Ismael Pallo Arias — QA
- Luis Alfredo Pinzón Quintero — DEV

## Story Map
> [Ver en FigJam](https://www.figma.com/board/BIthdjee35TGVFThd2Qqff/Story-Map-%E2%80%94-Sistema-de-Venta-de-Entradas--Ticketing-?node-id=0-1&t=MNZ1TjxddfBPOwVN-1)

> Este FigJam incluye:
> - **El flujo del MVP**, para visualizar la interacción principal de organizador y comprador.
> - **El Story Map**, como primer borrador visual para ordenar actividades, tareas e historias de usuario antes de consolidar el backlog final.
> - **La sesión de Planning Poker**, como evidencia del proceso colaborativo de estimación en Story Points.

## Estructura de nuestro repositorio
- `PRD.md`
- `USER_STORIES.md`
- `SUBTASKS.md`

## Glosario de términos
- **Tier:** categorías de las entradas disponibles para un evento.
- **Early Bird:** categoría con precio especial disponible solo durante una ventana de tiempo definida por el organizador.
- **Reserva:** bloqueo temporal de una entrada mientras el comprador completa el pago.
- **Timeout:** vencimiento automático de la reserva cuando el comprador no paga a tiempo.
- **Timer:** temporizador que le muestra al comprador cuánto tiempo le queda.
- **Scheduler:** proceso que corre en segundo plano revisando reservas vencidas.
- **Job de respaldo:** proceso secundario que actúa si el scheduler falla, para que ninguna reserva se quede bloqueada.
- **Bloqueo optimista:** control que garantiza que una entrada solo puede ser reservada por un comprador a la vez.
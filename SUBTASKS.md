  # Subtasks y Estimación — Sistema de Venta de Entradas

## HU-01: Creación de evento de obra de teatro — SP: 5

### DEV Funcional

- [ ] Crear entidad y tabla de eventos
- [ ] Implementar endpoint o servicio de creación de eventos
- [ ] Validar información obligatoria del evento
- [ ] Validar aforo contra el máximo permitido de la sala
- [ ] Persistir evento en estado borrador
- [ ] Restringir creación a usuarios con rol administrador

### DEV No Funcional

- [ ] Implementar validaciones de integridad de entrada en backend
- [ ] Registrar logs básicos de creación de eventos
- [ ] Manejar errores de validación sin exponer detalles sensibles
- [ ] Asegurar consistencia transaccional para evitar registros parciales
# Dataset - Car Selection

Dataset sintético en MySQL para la plataforma de selección y gestión de vehículos.

## Archivos del Dataset

- `usuarios (1).sql`: Tabla `usuario` con accesos y roles (administrador, cliente, vendedor).
- `capasalmacen.sql`: Tabla `vehiculo` con el catálogo de vehículos.
- `transacciones (1).sql`: Tabla `transaccion` con el registro de ventas.
- `solicitudcita.sql`: Tabla `solicitudes` para citas entre compradores y vehículos.
- `consesionario.sql`: Tabla `publicacion` para las publicaciones comerciales.

## Relaciones

- `transaccion.id_comprador` -> `usuario.id`
- `transaccion.id_vendedor` -> `usuario.id`
- `transaccion.id_vehiculo` -> `vehiculo.id_vehiculo`
- `solicitudes.id_comprador` -> `usuario.id`
- `solicitudes.id_vehiculo` -> `vehiculo.id_vehiculo`

## Uso
Importar cada archivo `.sql` en su respectiva base de datos en MySQL/MariaDB.

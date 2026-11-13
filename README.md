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

## Dataset Analítico de Fuente Abierta (Big Data - Apache Spark)

Conjunto de datos público seleccionado de Kaggle (*Car Price Prediction Dataset*) utilizado para el procesamiento distribuido a gran escala y la generación de reportes estadísticos visualizados en el dashboard.

### Archivo del Dataset
- `train.csv`: Dataset histórico del mercado automotriz compuesto por **19,237 registros** y **18 atributos** (marca, modelo, año de fabricación, precio de venta, kilometraje, tipo de combustible, categoría, transmisión, entre otros).

### Variables Procesadas (Proyección en Spark)
Para la generación de métricas del negocio se filtran y limpian las siguientes columnas clave:
- `Manufacturer` & `Model`: Identificación de marca (65 fabricantes) y modelo del vehículo.
- `Prod. year`: Año de fabricación para análisis de antigüedad.
- `Price`: Precio de venta (variable objetivo).
- `Mileage`: Kilometraje recorrido (transformado de cadena de texto a formato numérico).
- `Fuel type` & `Category`: Tipo de combustible y segmento de carrocería.

### Flujo de Procesamiento e Integración
1. El clúster de **Apache Spark (PySpark)** ingiere el archivo `train.csv`.
2. Se ejecutan transformaciones de limpieza y agregaciones distribuidas (precio promedio por marca, distribución por combustible y análisis de kilometraje).
3. Los resultados consolidados se exportan para ser consultados a través de la **API REST** y renderizados en las gráficas del **Dashboard** web.

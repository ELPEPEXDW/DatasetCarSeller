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

Conjunto de datos público seleccionado de Kaggle (*Car Price Prediction Dataset*) utilizado para el procesamiento distribuido a gran escala y la generación de reportes estadísticos visualizados en el dashboard[cite: 1].

### Archivo del Dataset
- `train.csv`: Dataset histórico del mercado automotriz compuesto por **19,237 registros** y **18 atributos** originales[cite: 1].

### Variables Elegidas del Dataset (`train.csv`)
De las 18 columnas disponibles en el archivo original, se proyectaron y limpiaron únicamente las **7 variables clave** necesarias para el análisis del negocio (descartando campos irrelevantes como impuestos locales `Levy`, posición del volante `Wheel` o número de `Airbags`)[cite: 1]:
1. `Manufacturer`: Marca o fabricante del vehículo (65 firmas automotrices).
2. `Model`: Modelo específico del vehículo.
3. `Prod. year`: Año de fabricación para análisis de antigüedad y depreciación.
4. `Price`: Precio comercial de venta (variable financiera objetivo).
5. `Mileage`: Kilometraje recorrido (transformado de texto a valor numérico continuo en Spark).
6. `Fuel type`: Tipo de combustible (Gasolina, Diésel, Híbrido, Eléctrico, etc.).
7. `Category`: Tipo o segmento de carrocería (Sedán, SUV/Jeep, Hatchback, etc.).

### ¿Por qué lo elegimos?
- **Volumen ideal para Spark:** Sus más de 19,000 registros completos (sin valores nulos) permiten aprovechar el procesamiento distribuido en memoria de **Apache Spark** para limpiar datos y calcular agregaciones de alto rendimiento[cite: 1].
- **Valor de negocio (Inteligencia de Mercado):** Permite complementar la operación transaccional del concesionario con reportes estadísticos externos (precios promedio por marca, depreciación por kilometraje y oferta por tipo de combustible) visualizados en el dashboard[cite: 1].

### Coincidencia con el Dataset de Car Seller (`capasalmacen.sql`)
Las variables elegidas de `train.csv` coinciden directamente con la estructura y el dominio de nuestra entidad principal `vehiculo` (`capasalmacen.sql`) y `transaccion` (`transacciones.sql`)[cite: 1]:
- `Manufacturer` $\leftrightarrow$ Marca del vehículo en nuestro catálogo.
- `Model` $\leftrightarrow$ Modelo específico del vehículo.
- `Prod. year` $\leftrightarrow$ Año de fabricación / modelo.
- `Price` $\leftrightarrow$ Precio comercial de venta (`transaccion` / `vehiculo`).
- `Mileage` $\leftrightarrow$ Kilometraje recorrido.
- `Fuel type` & `Category` $\leftrightarrow$ Especificaciones técnicas y segmento de carrocería.

### Flujo de Procesamiento e Integración
1. El clúster de **Apache Spark (PySpark)** ingiere el archivo `train.csv`[cite: 1].
2. Se proyectan y limpian únicamente las 7 variables elegidas[cite: 1].
3. Los resultados consolidados se exportan para ser consultados a través de la **API REST** y renderizados en las gráficas del **Dashboard** web[cite: 1].

# 🧹 Data Cleaning & Normalization Pipeline (Paquete Standard)

Pipeline automatizado en **Python (Pandas & NumPy)** desarrollado para procesar, estandarizar, deduplicar y aplicar lógica de rechazo en datasets de clientes y pedidos de comercio electrónico con errores de formato, codificación y registros inconsistentes.

## 🎯 Objetivos del Proyecto

Transformar un set de datos transaccional crudo (con más de 5.200 registros de pedidos y clientes) en archivos limpios y validados (`customers_clean.csv`, `orders_clean.csv`, `orders_rejected.csv`), preservando la integridad de los datos reales sin inventar información (*nulls* genuinos).

## ⚙️ Transformaciones Aplicadas

* **Clientes (`customers_clean.csv`)**:
  * Normalización de nombres en formato *Title Case*.
  * Limpieza estricta de correos electrónicos (minúsculas, sin espacios).
  * Estandarización y unificación geográfica de ciudades (Córdoba, Rosario, Mendoza, Buenos Aires).
  * Fusión inteligente de registros duplicados por correo electrónico.

* **Pedidos y Deduplicación (`orders_clean.csv`)**:
  * **Deduplicación por `order_id`**: Consolidación conservando siempre la versión más reciente según el campo `updated_at`.
  * **Fechas**: Normalización a formato estándar ISO (`YYYY-MM-DD`) soportando múltiples formatos mixtos y fechas en inglés.
  * **Catálogo de Productos**: Mapeo y corrección de errores tipográficos contra un catálogo de referencia de 12 productos.
  * **Cantidades y Precios**: Conversión de cantidades en texto (*uno, dos, tres*) a numéricas, y parseo de precios con formato monetario local ($, puntos y comas decimales).
  * **Columnas Calculadas**: Cálculo de importe total (`quantity * unit_price`) y cruce de validación con la base de clientes (`customer_found`).

## 🛑 Lógica de Rechazos (`orders_rejected.csv`)

Aplicación estricta de reglas de rechazo en orden de prioridad:
1. `invalid_quantity`: Cantidades menores o iguales a 0 o mayores a 50.
2. `future_date`: Fechas de pedido posteriores a la fecha de corte establecida.
3. `missing_price`: Registros con precio unitario vacío.

## 📂 Estructura del Repositorio

* `/Data`: Datasets originales sin procesar (`pedido_standard_customers.csv`, `pedido_standard_orders.csv`, `pedido_standard_products.csv`).
* `/Output`: Datasets finales limpios y reporte de rechazos.
* `data_cleaning_standard.ipynb`: Cuaderno con el código ejecutable paso a paso.

## 🛠️ Tecnologías Utilizadas

* Python 3, Pandas, NumPy, Expresiones Regulares (re), Difflib.

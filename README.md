# Sistema de Cotización - Don Lucho

Proyecto final de Base de Datos desarrollado en **SQLite** para gestionar el proceso de cotización de productos en la empresa Don Lucho.

## Descripción

Este proyecto implementa una base de datos relacional para administrar clientes, categorías, productos, cotizaciones y órdenes de trabajo. El sistema utiliza restricciones de integridad, claves primarias, claves foráneas, vistas y triggers para garantizar la consistencia de la información y automatizar reglas de negocio.

---

## Estructura del proyecto

```
Sistema_Cotizacion_SQLite/
│
├── Sistema_Cotizacion_SQLite.sql
├── Datos.sql
├── ConsultasDB.txt
├── Trigger_y_prueba.txt
├── Vista_y_prueba.txt
└── README.md
```

| Archivo | Descripción |
|----------|-------------|
| Sistema_Cotizacion_SQLite.db | Script de creación de la base de datos. |
| ConsultasDB.txt | Consultas SQL para demostrar el funcionamiento del sistema. |
| Trigger_y_prueba.txt | Implementación y pruebas del trigger. |
| Vista_y_prueba.txt | Creación y pruebas de la vista. |

---

### Esquema Entidad-Relación

<div align="center">

<img src="img/ModeloER_PoryectoBD.png" alt="Esquema Entidad-Relación" width="850"/>

</div>

## Modelo de datos

El sistema está conformado por las siguientes entidades:

- Cliente
- Categoría
- Producto
- Cotización
- Detalle_Cotización
- Orden_Trabajo
- Historial_Estado

### Relaciones principales

- Un cliente puede registrar varias cotizaciones.
- Una categoría puede contener múltiples productos.
- Una cotización puede incluir varios productos mediante la tabla `Detalle_Cotización`.
- Cada cotización puede generar una única orden de trabajo.
- Todos los cambios de estado de una cotización se registran en `Historial_Estado`.

---

## Tablas

### Cliente

| Campo | Tipo |
|-------|------|
| cliente_id | INTEGER |
| identificacion | TEXT |
| nombre | TEXT |
| tipo_cliente | TEXT |
| telefono | TEXT |
| correo | TEXT |
| direccion | TEXT |

### Categoría

| Campo | Tipo |
|-------|------|
| categoria_id | INTEGER |
| nombre_categoria | TEXT |
| descripcion | TEXT |

### Producto

| Campo | Tipo |
|-------|------|
| producto_id | INTEGER |
| categoria_id | INTEGER |
| nombre_producto | TEXT |
| descripcion | TEXT |
| precio_base | REAL |
| stock_disponible | INTEGER |
| activo | INTEGER |

### Cotización

| Campo | Tipo |
|-------|------|
| cotizacion_id | INTEGER |
| cliente_id | INTEGER |
| fecha_creacion | TEXT |
| estado | TEXT |
| descuento | REAL |
| observaciones | TEXT |
| total | REAL |

### Detalle_Cotización

| Campo | Tipo |
|-------|------|
| detalle_id | INTEGER |
| cotizacion_id | INTEGER |
| producto_id | INTEGER |
| cantidad | INTEGER |
| precio_unitario | REAL |
| subtotal | REAL |

### Orden_Trabajo

| Campo | Tipo |
|-------|------|
| orden_id | INTEGER |
| cotizacion_id | INTEGER |
| fecha_inicio | TEXT |
| fecha_entrega | TEXT |
| estado_produccion | TEXT |

### Historial_Estado

| Campo | Tipo |
|-------|------|
| historial_id | INTEGER |
| cotizacion_id | INTEGER |
| estado_anterior | TEXT |
| estado_nuevo | TEXT |
| fecha_cambio | TEXT |

---

## Restricciones implementadas

La base de datos utiliza distintos mecanismos para garantizar la integridad de la información:

- Claves primarias (`PRIMARY KEY`).
- Claves foráneas (`FOREIGN KEY`).
- Restricciones de unicidad (`UNIQUE`).
- Campos obligatorios (`NOT NULL`).
- Restricciones (`CHECK`).
- Valores por defecto (`DEFAULT`).

---

## Trigger

El proyecto implementa un trigger para automatizar una regla de negocio dentro de la base de datos. Su definición y prueba se encuentran en el archivo:

```
Trigger_y_prueba.txt
```

---

## Vista

Se creó una vista para simplificar consultas frecuentes que requieren información proveniente de varias tablas relacionadas.

La implementación y pruebas se encuentran en:

```
Vista_y_prueba.txt
```

---

## Consultas

El archivo `ConsultasDB.txt` contiene consultas SQL para demostrar el funcionamiento del sistema, incluyendo:

- JOIN entre tablas.
- Funciones de agregación.
- Consultas con `GROUP BY`.
- Filtros con `WHERE` y `HAVING`.
- Ordenamientos.
- Subconsultas.

---

## Ejecución

1. Crear una base de datos en SQLite.
2. Ejecutar el script `Sistema_Cotizacion_SQLite.sql`.
3. Ejecutar `Datos.sql` para cargar la información de prueba.
4. Ejecutar las consultas, la vista y el trigger para verificar el funcionamiento del sistema.

---

## Justificación del modelo relacional

Se eligió un modelo relacional porque la información mantiene relaciones claramente definidas entre clientes, productos, categorías, cotizaciones y órdenes de trabajo. El uso de claves primarias, claves foráneas y restricciones permite preservar la integridad de los datos y realizar consultas mediante `JOIN`.

Una consulta menos eficiente en este modelo consiste en recuperar una cotización completa junto con todos sus productos y detalles en una sola estructura. En una base de datos documental como MongoDB esta información podría almacenarse como un único documento anidado, evitando múltiples uniones entre tablas. Sin embargo, el modelo relacional ofrece una mejor integridad referencial, reduce la duplicación de datos y facilita el mantenimiento de la información, por lo que resulta más adecuado para este proyecto.

---

## Autor

**Erick Sebastián Torres Suárez**

Código: **00334347**

Proyecto Final de Base de Datos

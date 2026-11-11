# Modelo Relacional de Bases de Datos 18



## Descripción



Este documento detalla el esquema y la estructura del modelo relacional de bases de datos para un sistema de gestión de producción industrial, enfocado en el control de empleados, líneas de montaje, productos, órdenes de fabricación, componentes, unidades producidas, inspecciones de calidad y la estructura de listas de materiales (BOM).

---

## Estructura de Tablas y Atributos



### 1. Empleado



* **PK (Clave Primaria):** `id_empleado`


* **Atributos:**
* `DNI`


* `apellido`


* `Rol`


* `nombre`





### 2. Linea-de-montaje



* **PK (Clave Primaria):** `id_Codigo_linea`


* **Atributos:**
* `descripción`


* `capacidad:producción`


* `ubicación`




* **FK (Claves Foráneas):**
* `id_empleado` (asociado a la tabla Empleado)





### 3. Producto



* **PK (Clave Primaria):** `id_Codigo_articulo`


* **Atributos:**
* `nombre_comercial`


* `descripción`


* `tiempo_faricación` (o `tiempo_fabricación`)


* `tipo_producto`





### 4. Orden-de-Fabricación



* **PK (Clave Primaria):** `id_Numero_de_orden`


* **Atributos:**
* `fecha_de_emision`


* `cantidad_planificada`




* **FK (Claves Foráneas):**
* `id_Codigo_linea` (asociado a la tabla Linea-de-montaje)


* `id_Codigo_articulo` (asociado a la tabla Producto)





### 5. Componente



* **PK (Clave Primaria):** `id_codigo_componente`


* **Atributos:**
* `nombre`


* `descripción`


* `tipo_de_componente`


* `unidad_de_producto`





### 6. Composición



* **PK (Clave Primaria):** `id_codigo_componente`


* **Atributos:**
* `cantidad_necesaria`




* **FK (Claves Foráneas):**
* `id_codigo_componente` (asociado a la tabla Componente)





### 7. Unidad



* **PK (Clave Primaria):** `id_Unidad`


* **Atributos:**
* `cantidad_producida`


* `fecha_producida`


* `estado`




* **FK (Claves Foráneas):**
* `id_Codigo_articulo` (asociado a la tabla Producto)





### 8. Inspección_de_calidad



* **Atributos:**
* `cantidad_producida`


* `fecha_de_producción`


* `estado`


* `observaciones`




* **FK (Claves Foráneas):**
* `id_Unidad` (asociado a la tabla Unidad)





### 9. Detalle-BOM-producto



* **PK (Clave Primaria):** `id_detalle_bom`


* **FK (Claves Foráneas):**
* `id_Codigo_articulo` (asociado a la tabla Producto)


* `id_codigo_componente` (asociado a la tabla Componente)





---

## Relaciones Principales



* **Empleado y Linea-de-montaje:** Las líneas de montaje se encuentran bajo la supervisión o gestión de un empleado (`id_empleado`).


* **Linea-de-montaje y Orden-de-Fabricación:** Las órdenes de fabricación se asignan y ejecutan en una línea de montaje específica (`id_Codigo_linea`).


* **Producto y Orden-de-Fabricación:** Cada orden de fabricación especifica la producción de un artículo o producto determinado (`id_Codigo_articulo`).


* **Producto y Componente (Detalle-BOM-producto):** La estructura de materiales (Bill of Materials) relaciona los productos fabricados con los componentes necesarios mediante la tabla intermedia `Detalle-BOM-producto` (`id_Codigo_articulo` e `id_codigo_componente`).


* **Producto y Unidad:** La fabricación genera registros individuales o lotes de producción representados en la tabla `Unidad` y vinculados al producto.


* **Unidad e Inspección_de_calidad:** Las unidades producidas se someten a controles y revisiones registradas en la tabla `Inspección_de_calidad` utilizando `id_Unidad`.

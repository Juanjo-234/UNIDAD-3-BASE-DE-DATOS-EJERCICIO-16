# UNIDAD-3-BASE-DE-DATOS-EJERCICIO-16
Este diagrama entidad-relación (o modelo relacional) representa la estructura lógica de una **base de datos para la gestión de una inmobiliaria o administración de alquileres**, diseñada para administrar propietarios, propiedades inmobiliarias, contratos de arrendamiento, inquilinos, empleados que gestionan las operaciones y el registro de pagos o cobros.

A continuación se detalla qué representa cada tabla y cómo se relacionan entre sí:

### 1. Entidades Principales (Tablas)

* **`PROPIETARIO`**: Almacena los datos personales y de contacto de los dueños de los inmuebles.


* *Campos:* `DNI/CUIT` (Clave Primaria), `NOMBRE`, `APELLIDO`, `TELEFONO` y `CORREO`.




* **`PROPIEDAD`**: Contiene el inventario de bienes raíces registrados en la inmobiliaria.


* *Campos:* `ID_PROPIEDAD` (Clave Primaria), `CODIGO_CASTRAL`, `CIUDAD`, `SUPERFICIE`, `CANTIDAD_HABIENTES` (ambientes), `DIRECCION` y `DNI/CUIT_PROPIETARIO` (Clave Foránea que indica a qué dueño pertenece).




* **`INQUILINO`**: Registra la información de las personas que alquilan las propiedades.


* *Campos:* `DNI/CUIT` (Clave Primaria), `NOMBRE`, `APELLIDO`, `TELEFONO` y `CORREO`.




* **`EMPLEADO`**: Contiene los datos del personal de la inmobiliaria encargado de gestionar las operaciones y contratos.


* *Campos:* `ID_LEGAJO` (Clave Primaria), `CARGO`, `NOMBRE`, `APELLIDO` y `CORREO`.




* **`CONTRATO`**: Formaliza el acuerdo legal de arrendamiento entre las partes involucradas.


* *Campos:* `ID_CONTRATO` (Clave Primaria), `FECHA_INICIO`, `FECHA_FIN`, `MONTO`, `DEPOSITO_GARANTIA`, además de las claves foráneas `ID_LEGAJO` (empleado responsable), `DNI/CUIT_INQUILINO` y `ID_PROPIEDAD`.




* **`PAGO`**: Registra los comprobantes o transacciones mensuales correspondientes al cobro de los alquileres.


* *Campos:* `ID_PAGO` (Clave Primaria), `MEDIO_PAGO`, `RECARGO_DEMORA`, `PERIODO_ABONADO`, `MONTO_ABONADO` y las claves foráneas `ID_CONTRATO`, `DNI/CUIT_INQUILINO` e `ID_PROPIEDAD`.





---

### 2. Relaciones Principales

* **Propietarios y Propiedades:** Un propietario puede registrar una o varias propiedades en la inmobiliaria, pero cada propiedad pertenece a un único dueño (relación de 1 a N).


* **Gestión de Contratos:** Un contrato vincula de manera directa una propiedad específica, un inquilino y un empleado que gestiona la operación.


* **Seguimiento de Pagos:** Cada contrato genera registros periódicos en la tabla `PAGO`, permitiendo asociar las transacciones financieras al contrato, al inquilino y a la propiedad correspondiente.
<img width="1442" height="932" alt="EJERCICIO 16-MR drawio" src="https://github.com/user-attachments/assets/9875c12b-b8f7-4e7d-8931-aa9b7edf3723" />

Este diagrama muestra el **proceso completo de normalización de bases de datos** aplicado a un sistema de gestión para una inmobiliaria o administración de alquileres, transformando una estructura inicial desnormalizada (Forma Normal 0) hasta llegar al diseño relacional optimizado en Tercera Forma Normal (3FN).

A continuación se detalla cada una de las fases representadas:

### 1. Fase Normal 0 (FN0) — Tabla No Normalizada

* Se parte de una **única tabla plana y masiva** que concentra toda la información de la inmobiliaria en una sola estructura: datos del contrato, fechas, montos, depósitos, propiedades con sus dueños anidados, empleados a cargo, inquilinos y un grupo repetitivo anidado en una misma celda que contiene la lista de pagos realizados.


* **Problema:** Contiene colecciones de datos multivaluados y anidados dentro de las celdas, lo que genera una enorme redundancia de información y dificulta cualquier operación de actualización o consulta estructurada.



---

### 2. Primera Forma Normal (1FN)

* Se eliminan los grupos repetitivos y se asegura que **todos los atributos sean atómicos** (cada celda contiene un único valor), expandiendo los registros para que cada fila represente una combinación individual y libre de valores anidados.


* Se obtiene una tabla tabular plana (`TABLA PLANTILLA`) donde cada campo es indivisible, definiéndose claves primarias compuestas, aunque todavía persiste una alta duplicidad de datos en los perfiles de propietarios, inquilinos, empleados y propiedades.



---

### 3. Segunda Forma Normal (2FN)

* Se parte de la 1FN y se eliminan las **dependencias parciales**. Se separan los atributos basándose en sus claves principales correspondientes, desglosando la información en cinco tablas independientes y normalizadas:


* **`TABLA PROPIETARIO`**: Almacena la información personal de los dueños.


* **`TABLA PROPIEDAD`**: Contiene el inventario de inmuebles y sus características.


* **`TABLA INQUILINO`**: Gestiona los datos de los arrendatarios.


* **`TABLA EMPLEADO`**: Registra al personal de la inmobiliaria.


* **`TABLA CONTRATO`**: Vincula las operaciones de alquiler.


* **`TABLA PAGO`**: Registra los abonos y transacciones financieras asociadas.





---

### 4. Tercera Forma Normal (3FN)

* Se eliminan las **dependencias transitivas**, garantizando que ningún atributo no clave dependa de otro atributo no clave. El diseño se consolida en un modelo relacional robusto y totalmente normalizado, interconectado mediante claves foráneas (FK), lo que asegura la integridad referencial y evita anomalías para la gestión inmobiliaria.
<img width="5202" height="2932" alt="EJERCICIO 16-FASE DE NORMALIZACION drawio" src="https://github.com/user-attachments/assets/df1fc687-e0cf-4452-9788-2b5e98885eab" />



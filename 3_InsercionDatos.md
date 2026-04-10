# 03. Inserción y edición de datos.

Una vez creada la estructura, toca empezar a añadir y modificar datos a las tablas.

</br>

## 1. Añadir registros.
Se deben especificar las columnas donde se van a introducir los datos, y a continuación los datos:

```sql
INSERT INTO Alumnos (nombre, nivel) 
VALUES ('Juan', 'Master');
```

</br>

## 2. Borrar registros.

Se usa para eliminar filas (registros) de la tabla.

La Sintaxis:
```SQL
DELETE FROM nombre_tabla 
WHERE condicion;
```

Ejemplo en CodeMaker:
"Juan ha decidido dejar el curso y queremos borrar sus datos".

```SQL
DELETE FROM alumnos 
WHERE nombre = 'Juan';
```

> **BORRADO TOTAL:** Si ejecutas DELETE FROM alumnos; (sin el WHERE), vaciarás la tabla por completo. La estructura de la tabla (las columnas) seguirá existiendo, pero estará vacía.

## 3. Actualizar registros.

Se usa cuando un dato ya existe pero ha cambiado. Por ejemplo, un alumno sube de nivel o cambia su número de teléfono.

La Sintaxis:
```SQL
UPDATE nombre_tabla 
SET columna1 = valor1, columna2 = valor2 
WHERE condicion;
```

Ejemplo en CodeMaker:
"Antonio ha cumplido años y ahora es nivel Senior".

```SQL
UPDATE alumnos 
SET edad = 21, nivel = 'Senior' 
WHERE nombre = 'Antonio';
```

> **EL PELIGRO DEL WHERE:** Si olvidas poner el WHERE, SQL no te preguntará. Pondrá a todos los alumnos de la academia con 21 años y nivel Senior.

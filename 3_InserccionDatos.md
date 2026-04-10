# 03. Inserción de Datos (DML)

Una vez creada la estructura, toca alimentar la base de datos. Para ello usamos el comando `INSERT INTO` de SQL.

</br>

## 1. Añadir elementos
Se deben especificar las columnas donde se van a introducir los datos, y a continuación los datos:

```sql
INSERT INTO Cursos (tecnologia, nivel) 
VALUES ('Unity 3D', 'Master');
```

</br>

## 2. Borrar elementos

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

## 3. ACTUALIZAR DATOS

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

En el mundo real, la información no está en una sola tabla gigante. Está repartida en varias tablas que se "conectan" entre sí. Esto evita repetir datos y mantiene la base de datos organizada.
</br>

## 1. El concepto de Clave Foránea (Foreign Key)

Para conectar dos tablas, usamos una Foreign Key (FK). Es una columna en una tabla que hace referencia al ID (Primary Key, PK) de otra tabla.

- Tabla Padre (**`Cursos`**): Tiene clave primaria (PK) `id_curso`.
- Tabla Hija (**`Alumnos`**): Tiene clave primaria (PK) `id_alumno` y una clave foránea (FK) `id_curso`.

</br>

## 2. Creación de tablas con relaciones

Al crear la tabla "hija", debemos avisar a SQL de que una de sus columnas está conectada a otra tabla.

```SQL
-- Primero creamos la tabla independiente (Cursos)
CREATE TABLE cursos (
    id_curso INTEGER PRIMARY KEY AUTOINCREMENT,
    nombre_curso TEXT NOT NULL
);

-- Luego la tabla dependiente (Alumnos)
CREATE TABLE alumnos (
    id_alumno INTEGER PRIMARY KEY AUTOINCREMENT,
    nombre TEXT NOT NULL,
    id_curso INTEGER, -- Esta es la columna que conectará
    FOREIGN KEY (id_curso) REFERENCES cursos(id_curso)
);
```
</br>

## 3. Inserción de datos con relaciones

¡Importante! No puedes inscribir a un alumno en un curso que no existe, por lo que primero debes insertar los datos de los cursos, y después el de los alumnos.

```SQL
-- Paso 0: Activar las FK en SQLite
PRAGMA foreign_keys = ON;

-- Paso 1: Crear el curso
INSERT INTO cursos (nombre_curso) VALUES ('Codemaker Master'); -- Supongamos que genera el ID 1

-- Paso 2: Crear al alumno vinculado a ese curso
INSERT INTO alumnos (nombre, id_curso) VALUES ('Juan', 1);
```
</br>

## 4. Consultas con relaciones (El INNER JOIN)

Cuando queremos ver el nombre del alumno Y el nombre de su curso a la vez, usamos el "superpoder" del JOIN. Es como decirle a SQL: "Junta estas dos tablas usando el ID que tienen en común".

Estructura del JOIN:
```sql
SELECT alumnos.nombre, cursos.nombre_curso
FROM alumnos
INNER JOIN cursos ON alumnos.id_curso = cursos.id_curso;
```

¿Qué está pasando aquí?
- **SELECT**: Eliges qué columnas quieres ver de cada tabla (usando tabla.columna).
- **FROM**: Eliges la tabla principal.
- **INNER JOIN**: Eliges la tabla que quieres "pegar".
- **ON**: Explicas cuál es el conector (donde el ID de uno coincida con el ID del otro).

</br>

## 5. Ejemplo de Resultado

Siguiendo el ejemplo anterior, y como las consultas de SQL siempre devuelven (contestan) una nueva tabla con la información solicitada, el resultado de la consulta sería:
| nombre | nombre_curso |
| --- | --- |
| Marcos | Programación en Java |

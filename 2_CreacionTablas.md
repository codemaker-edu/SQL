# Creación de la base de datos

Una vez que tenemos claras nuestras entidades (e incluso hemos creado el diagrama), el siguiente paso es "picar código" para que la base de datos cobre vida. Para ello usamos los comandos **DDL** de **SQL** que se muestran a continuación.

</br>


## 1. Comandos Fundamentales

### `CREATE TABLE`
Es el comando principal para definir la estructura de una tabla. La sintaxis básica es:

```sql
CREATE TABLE nombre_tabla (
    columna1 tipo_dato restricciones,
    columna2 tipo_dato restricciones,
    ...
    PRIMARY KEY (columna1)
);
```

### `DROP TABLE`
Borra una tabla por completo (y todos sus datos). Úsalo con cuidado.
```sql
DROP TABLE Alumnos;
```

</br>


## 2. Tipos de Datos (Data Types)
Al igual que en Java o Python, en SQL debemos decirle a la base de datos qué tipo de información guardará cada columna:

| Tipo SQL      | Descripción                                             | Equivalente en Java/C# |
| :---          | :---                                                    | :---                   |
| INTEGER	          | Números enteros (IDs, edades)                           | int                    |
| TEXT    | Texto de longitud variable (n = máximo de caracteres)   | String                 |
| REAL         | Decimales de precisión simple. Rápido pero con posibles errores de redondeo.                                   | float                  |


</br>


## 3. Restricciones (Constraints)
Las restricciones aseguran que los datos sean correctos y sigan las reglas del negocio:

- `PRIMARY KEY (PK)`: Identificador único. No puede haber dos iguales y no puede ser nulo.
- `NOT NULL`: Obliga a que el campo siempre tenga un valor (ej. el nombre de un alumno).
- `UNIQUE`: Asegura que todos los valores en una columna sean diferentes (ej. el email).
- `AUTO_INCREMENT`: Genera el ID automáticamente (+1) cada vez que añadimos un registro.
- `CHECK`: Valida condiciones
- `FOREIGN KEY (FK)`: La "llave foránea" que conecta una tabla con otra.

</br>


## 4. Ejemplo Práctico: Implementando la base de datos de CodeMaker
Vamos a crear tres tablas relacionadas. Fíjate en cómo conectamos `Alumnos` con `Cursos` y `Proyectos` con `Alumnos`.

**A. Tabla de Cursos (La base)**
```SQL
CREATE TABLE Cursos (
    id_curso INTEGER PRIMARY KEY AUTOINCREMENT,
    tecnologia TEXT NOT NULL,
    nivel TEXT CHECK (nivel IN ('Junior', 'Senior', 'Master', 'PRO'))
);
```
`Tip: fíjate en CHECK, comprueba que el valor sea uno de los especificados, no vale cualquier cosa.`

**B. Tabla de Alumnos (Relacionada con Cursos)**
Aquí añadimos una Foreign Key. Decimos que `id_curso` en esta tabla debe existir previamente en la tabla `Cursos`.

```SQL
CREATE TABLE Alumnos (
    id_alumno INTEGER PRIMARY KEY AUTOINCREMENT,
    nombre TEXT NOT NULL,
    email TEXT UNIQUE,
    id_curso INTEGER,
    -- Definimos la relación
    FOREIGN KEY (id_curso) REFERENCES Cursos(id_curso)
);
```

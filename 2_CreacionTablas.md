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
| INT	          | Números enteros (IDs, edades)                           | int                    |
| VARCHAR(n)    | Texto de longitud variable (n = máximo de caracteres)   | String                 |
| FLOAT         | Decimales de precisión simple. Rápido pero con posibles errores de redondeo.                                   | float                  |
| DATE          | Fechas (YYYY-MM-DD)                                     | LocalDate              |
| BOOLEAN	      | Verdadero o Falso (1 o 0)                               |	boolean                |

</br>


## 3. Restricciones (Constraints)
Las restricciones aseguran que los datos sean correctos y sigan las reglas del negocio:

- `PRIMARY KEY (PK)`: Identificador único. No puede haber dos iguales y no puede ser nulo.
- `NOT NULL`: Obliga a que el campo siempre tenga un valor (ej. el nombre de un alumno).
- `UNIQUE`: Asegura que todos los valores en una columna sean diferentes (ej. el email).
- `AUTO_INCREMENT`: Genera el ID automáticamente (+1) cada vez que añadimos un registro.
- `FOREIGN KEY (FK)`: La "llave foránea" que conecta una tabla con otra.

</br>


## 4. Ejemplo Práctico: Implementando la base de datos de CodeMaker
Vamos a crear tres tablas relacionadas. Fíjate en cómo conectamos `Alumnos` con `Cursos` y `Proyectos` con `Alumnos`.

**A. Tabla de Cursos (La base)**
```SQL
CREATE TABLE Cursos (
    id_curso INT PRIMARY KEY AUTO_INCREMENT,
    tecnologia VARCHAR(50) NOT NULL,
    nivel VARCHAR(20) CHECK (nivel IN ('Junior', 'Senior', 'Master', 'PRO'))
);
```
`Tip: fíjate en `CHECK`, comprueba que el valor sea uno de los especificados, no vale cualquier cosa.`

**B. Tabla de Alumnos (Relacionada con Cursos)**
Aquí añadimos una Foreign Key. Decimos que `id_curso` en esta tabla debe existir previamente en la tabla `Cursos`.

```SQL
CREATE TABLE Alumnos (
    id_alumno INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    id_curso INT,
    -- Definimos la relación
    FOREIGN KEY (id_curso) REFERENCES Cursos(id_curso)
);
```

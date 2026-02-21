# 04. Consultas de Datos (SELECT)

El comando `SELECT` es la herramienta que usamos para "preguntar" a la base de datos. Es el corazón del **DML (Data Manipulation Language)**.

> **Regla de Oro:** Cuando consultamos datos de tablas, SQL siempre nos responderá mostrando los resultados en una **nueva tabla** temporal.

</br>

## 1. Estructura Básica: La Regla de Oro
Casi todas las consultas siguen este orden:
1. **SELECT**: ¿Qué columnas quiero ver?
2. **FROM**: ¿De qué tabla saco la información?
3. **WHERE**: ¿Qué condiciones deben cumplirse? (Filtro)
4. **ORDER BY**: ¿Cómo quiero ordenar los resultados?

**Ejemplo**:
```sql
SELECT nombre, email 
FROM Alumnos 
WHERE id_curso = 1 
ORDER BY nombre ASC;
```
**Explicación:** Coge los nombres y emails de los alumnos matriculados en el curso 1, y muéstramelos ordenados alfabéticamente.

</br>

## 2. Filtrado y Operadores
- **Comparación**: `=`, `<>` (distinto), `>`, `<`, `>=`, `<=`.
- **Rangos**: `BETWEEN` (Ej: *WHERE id_alumno BETWEEN 10 AND 20*).
- **Listas**: `IN` (Ej: *WHERE tecnologia IN ('Unity', 'Python')*).
- **Patrones**: `LIKE` (Ej: *LIKE '%gmail.com'* termina en gmail.com).

</br>

## 3. Funciones de Agregación (Estadísticas)
Si queremos obtener datos globales de nuestra academia CodeMaker, usamos estas funciones:

| Función       | Descripción                              |
| :---          | :---                                     |
| COUNT()       | Cuenta el número de filas                |
| SUM()         | Suma los valores de una columna numérica |
| AVG()         | Calcula el promedio (media               |
| MAX() / MIN() | Busca el valor más alto o más bajo       |

**Ejemplo**:
```SQL
SELECT COUNT(*) AS total_proyectos FROM Proyectos;
```
**Explicación:** cuenta cuántas filas hay en `Proyectos`. El resultado lo pondrá en una tabla con una columna llamada `total_proyectos`.

</br>

## 4. El Superpoder de SQL: JOINS (Uniones)

A veces la información está repartida. Por ejemplo: el nombre del alumno está en la tabla `Alumnos`, pero el título de su trabajo está en la tabla `Proyectos`. Para juntarlos usamos el `JOIN`.

**`INNER JOIN`**
Nos devuelve solo las filas donde hay una coincidencia en ambas tablas.

**Ejemplo**:
```SQL
SELECT Alumnos.nombre, Proyectos.titulo
FROM Alumnos
INNER JOIN Proyectos ON Alumnos.id_alumno = Proyectos.id_alumno;
```
**Explicación**: muéstrame el nombre del alumno y el título de su proyecto uniendo ambas tablas por el ID del alumno. El resultado sería algo así:
| nombre | titulo |
| :--- | :--- |
| Marcos | Juego Unity 2D |
| María | Reto de programación en Java |
| Juan | Modelo 3D de personaje en Blender |

</br>

## 5. Agrupamiento (GROUP BY)
Esto es esencial para reportes. Por ejemplo, saber cuántos alumnos hay en cada nivel educativo.
**Ejemplo**:
```SQL
SELECT nivel, COUNT(id_alumno) as total
FROM Alumnos
GROUP BY nivel;
```
**Explicación**: entra en la tabla `Alumnos`, los agrupa o reparte por niveles, cuenta cuántos alumnos hay en cada nivel (y a la columna donde anotará el total de alumnos la llama *total*) y la muestra. El resultado sería algo así:
| nivel | total |
| :--- | :--- |
| Junior | 58 |
| Senior | 49 |
| Master | 30 |
| PRO | 10 |

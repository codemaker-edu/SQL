# 04. Consultas de Datos (SELECT)

El comando `SELECT` de SQL es la herramienta que usamos para "preguntar" a la base de datos.

> **Regla de Oro:** Cuando consultamos datos de tablas, SQL siempre nos responderá mostrando los resultados en una **nueva tabla** temporal.

</br>

## 1. Estructura Básica de una consulta
Casi todas las consultas siguen este orden:
1. **SELECT**: Qué columnas quiero ver
2. **FROM**: De qué tabla saco la información
3. **WHERE**: Qué condiciones deben cumplirse (Filtro)
4. **ORDER BY**: Cómo quiero ordenar los resultados

**Ejemplo**:
```sql
SELECT nombre, email 
FROM Alumnos 
WHERE id_curso = 1 
ORDER BY nombre ASC;
```
**Explicación:** Coge los nombres y emails de los alumnos matriculados en el curso 1, y muéstramelos ordenados alfabéticamente.

</br>

## 2. Filtrado y Operadores para 'WHERE' 
- **Comparación**: `=`, `<>` (distinto), `>`, `<`, `>=`, `<=`.
- **Rangos**: `BETWEEN` (Ej: *WHERE id_alumno BETWEEN 10 AND 20*).

## 3. Formas de ordenar los resultados con ' ORDER BY'
- **ASC**: ordenar ascendentemente (orden alfabético o numérico).
- **DESC**: ordenar descendentemente (orden alfabético o numérico).

## 4. Funciones de agregación
- **COUNT()** para contar: `SELECT COUNT(*) FROM alumnos;`
- **AVG()** para hacer promedios: `SELECT AVG(edad) FROM alumnos;`
- **SUM()** para sumar: `SELECT SUM(pago) FROM alumnos;`
- **MAX()** para buscar el valor máximo: `SELECT MAX(edad) FROM alumnos;`
- **MIN()** para buscar el valor mínimo: `SELECT MIN(edad) FROM alumnos;`

Ejemplo:
```sql
SELECT COUNT(*) FROM Alumnos;
```

## 5. Búsqueda por patrones
A veces no queremos buscar algo exacto, si no algo que *empiece por*, *termine por* o *contenga* algo. Para esto está **`LIKE`** junto al comodín `%`:
- `LIKE 'A%'`: Busca textos que empiecen por "A".
- `LIKE '%a'`: Busca textos que terminen en "a".
- `LIKE '%gmail%'`: Busca textos que contengan "gmail" en cualquier parte.

Ejemplo:
```sql
SELECT * FROM alumnos WHERE nombre LIKE 'An%'; 
-- Devolvería nombres como 'Antonio', 'Ana', 'Andrés'...
```
</br>

## 6. El operador de negación (NOT)
Sirve para excluir registros. Es el "lo contrario de".
`WHERE NOT nivel = 'Junior': Muestra a todos los que NO son Junior.`
`WHERE nombre NOT LIKE 'A%': Muestra a todos cuyo nombre NO empiece por A.`

</br>

## 7. Limitar resultados (LIMIT)
Se utiliza para que la tabla de resultados no sea infinita. Solo nos devuelve el número de filas que le pidamos. Se pone siempre al final de la consulta.

Ejemplo (El "Top 3" más jóvenes):
```sql
SELECT nombre, edad 
FROM alumnos 
ORDER BY edad ASC 
LIMIT 3;
```

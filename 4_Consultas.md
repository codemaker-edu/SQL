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

## 3. Formas de ordenar con ' ORDER BY'
- **ASC**: ordenar ascendentemente (orden alfabético o numérico).
- **DESC**: ordenar descendentemente (orden alfabético o numérico).

## 4. Funciones de agregación
- **COUNT()** para contar: `SELECT COUNT(*) FROM alumnos;`
- **AVG()** para hacer promedios: `SELECT AVG(edad) FROM alumnos;`
- **SUM()** para sumar: `SELECT SUM(pago) FROM alumnos;`
- **MAX()** para buscar el valor máximo: `SELECT MAX(edad) FROM alumnos;`
- **MIN()** para buscar el valor mínimo: `SELECT MIN(edad) FROM alumnos;`

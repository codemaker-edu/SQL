# 03. Inserción de Datos (DML)

Una vez creada la estructura, toca alimentar la base de datos. Para ello usamos el comando `INSERT INTO`.

</br>

## 1. Sintaxis Básica
Se deben especificar las columnas donde se van a introducir los datos, y a continuación los datos:

```sql
INSERT INTO Cursos (tecnologia, nivel) 
VALUES ('Unity 3D', 'Master');
```

</br>

## 2. El Orden de los Factores SÍ Altera el Producto
Debido a la Integridad Referencial (las Foreign Keys), no podemos saltarnos el orden lógico.
- Primero: Insertamos en tablas "independientes" (como Cursos).
- Segundo: Insertamos en tablas que dependen de otras (como Alumnos, que necesita un id_curso).
- Tercero: Insertamos en las hojas del árbol (como Proyectos, que necesita un id_alumno).

> [!IMPORTANT]
> Piénsalo, si para introducir un alumno necesitamos especificar un curso, no podremos introducir alumnos hasta que no hayamos introducido los cursos

Ejemplo Práctico:
```SQL
-- Paso 1: Creamos el curso
INSERT INTO Cursos (id_curso, tecnologia, nivel) VALUES (10, 'Blender 3D', 'Master');

-- Paso 2: Registramos al alumno en ese curso (id 10)
INSERT INTO Alumnos (id_alumno, nombre, email, id_curso) 
VALUES (1, 'Sara Code', 'sara@codemaker.es', 10);

-- Paso 3: Sara crea su primer proyecto
INSERT INTO Proyectos (titulo, software, id_alumno) 
VALUES ('Escenario Cyberpunk', 'Blender', 1);
```

</br>

## 3. Errores Comunes (Para debugear)
Los errores más comunes que podemos encontrarnos al introducir datos son los siguientes:

> [!CAUTION]
> **Error de Clave Foránea**: Intentar añadir un alumno al curso id 99 cuando ese curso no existe. SQL lanzará un error y no guardará nada.

> [!CAUTION]
> **Error de Clave Primaria**: Intentar insertar dos alumnos con el mismo id_alumno.

> [!CAUTION]
> **Error de Tipo**: Intentar meter un texto largo en un VARCHAR(5) o un número con 4 decimales en un DECIMAL(5,1). 

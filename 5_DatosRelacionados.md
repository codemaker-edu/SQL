En el mundo real, la información no está en una sola tabla gigante. Está repartida en varias tablas que se "conectan" entre sí. Esto evita repetir datos y mantiene la base de datos organizada.
</br>

## 1. El concepto de Clave Foránea (Foreign Key)

Para conectar dos tablas, usamos una Foreign Key (FK). Es una columna en una tabla que hace referencia al ID (Primary Key, PK) de otra tabla.

- Tabla Padre (**`Alumnos`**): Tiene clave primaria (PK) `id_alumno`.
- Tabla Hija (**`Padres`**): Tiene clave primaria (PK) `id_padre` y una clave foránea (FK) `id_alumno`.

Importante! SQLite tiene desactivadas por defecto las relaciones. En cada sesión (cada vez que abras DBeaver u otro software) debes ejecutar el siguiente comando para activarlas:
```SQL
-- Paso 0: Activar las FK en SQLite
PRAGMA foreign_keys = ON;
```
</br>

## 2. Creación de tablas con relaciones

Al crear la tabla "hija", debemos avisar a SQL de que una de sus columnas está conectada a otra tabla.

```SQL
-- Primero creamos la tabla independiente (Alumnos)
CREATE TABLE alumnos (
	id_alumno INTEGER PRIMARY KEY AUTOINCREMENT,
	nombre TEXT NOT NULL,
	dni TEXT UNIQUE,
	-- resto de atributos
);

-- Luego la tabla dependiente (Alumnos)
CREATE TABLE tutor (
	id_tutor INTEGER PRIMARY KEY AUTOINCREMENT,
	nombre TEXT NOT NULL,
	pago TEXT NOT NULL CHECK(pago in('Efectivo', 'Bizum')),
	id_alumno INTEGER,
	FOREIGN KEY (id_alumno) REFERENCES alumnos(id_alumno)
);
```
</br>

## 3. Inserción de datos con relaciones

¡Importante! No puedes inscribir a un alumno en un curso que no existe, por lo que primero debes insertar los datos de los cursos, y después el de los alumnos.

```SQL

-- Paso 1: Insertar alumnos
INSERT INTO alumnos (nombre, edad, telefono, nivel, genero) VALUES 
('Antonio', 20, '655443322', 'Master', 'masculino'),
('Maria', 21, '666553344', 'Master', 'femenino'),
('Juan', 16, '666554433', 'Senior', 'femenino'),
('Elena', 15, '666557788', 'Junior', 'masculino');

-- Paso 2: Insertar padres
INSERT INTO tutor (nombre, pago, id_alumno) VALUES 
('Paco', 'Bizum', 2),
('Juana', 'Efectivo', 1),
('Pepe', 'Bizum', 3),
('Marta', 'Efectivo', 4);
```
</br>

## 4. Consultas con relaciones (El INNER JOIN)

Cuando queremos ver el nombre del alumno Y el nombre de su curso a la vez, usamos el "superpoder" del JOIN. Es como decirle a SQL: "Junta estas dos tablas usando el ID que tienen en común".

Estructura del JOIN:
```sql
SELECT alumnos.nombre, tutor.nombre, tutor.pago
FROM alumnos INNER JOIN tutor ON tutor.id_alumno = alumnos.id_alumno;
```

¿Qué está pasando aquí?
- **SELECT**: Eliges qué columnas quieres ver de cada tabla (usando tabla.columna).
- **FROM**: Eliges la tabla principal.
- **INNER JOIN**: Eliges la tabla que quieres "pegar".
- **ON**: Explicas cuál es el conector (donde el ID de uno coincida con el ID del otro).

</br>

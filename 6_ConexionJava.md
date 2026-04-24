Ahora llega la parte más interesante, que consiste en conectar Java a SQL para juntar lo mejor de los 2 mundos: la programación y las bases de datos.

## 1. Preparar la BBDD.

En primer lugar, debemos tener la Base de Datos creada y su tabla o tablas también creadas. Desde Java insertaremos datos y haremos consultas.

## 2. Crear un Proyecto de Java e Instalar el Driver JDBC.

Java por sí solo no puede conectarse a una Base de Datos, necesita un software adicional que se llama el driver JDBC.
Debemos crear un proyecto de Java y colocar el `.jar` del **SQLite JDBC Driver** en la carpeta *lib*.

Enlace de descarga: https://repo1.maven.org/maven2/org/xerial/sqlite-jdbc/ (buscar la versión más reciente y descargar el `.jar`).

## 3. Programar la conexión.

En nuestros programa de Java debemos de usar algunas instrucciones para conectarnos y para lanzar inserciones de datos y consultas. Lo primero es importar la librería de SQL:

```java
import java.sql.*;
```

Lo siguiente, ya dentro de nuestra clase, será guardar en una variable privada (para que nadie acceda a ella), static (para que podamos usarla desde distintas partes de nuestro programa) y final (para que no podamos cambiarla), la ruta a la base de datos. **Importante: debemos tener la bbdd en la carpeta raíz del proyecto de Java**.

```java
private static final String URL = "jdbc:sqlite:codemaker.db";
```

Una vez configurado lo anterior, podemos ya pasar a leer o escribir en la base de datos.

**Leer la base de datos:**

```java
String sqlSelect = "SELECT * FROM alumnos";

try (Connection conn = DriverManager.getConnection(URL);
     PreparedStatement pstmt = conn.prepareStatement(sqlSelect)) {
    
    ResultSet rs = pstmt.executeQuery(); // Se usa solo para SELECT

    System.out.println("\n--- LISTA DE ALUMNOS ---");
    
    // El bucle rs.next() recorre la tabla fila por fila
    while (rs.next()) {
        // Sacamos los datos de las columnas por su nombre o posición
        int id = rs.getInt("id");
        String nombre = rs.getString("nombre");
        String nivel = rs.getString("nivel");

        System.out.println("ID: " + id + " | Nombre: " + nombre + " | Nivel: " + nivel);
    }

} catch (SQLException e) {
    System.out.println("Error en la consulta: " + e.getMessage());
}
```

**Escribir en la base de datos:**

```java
String sqlInsert = "INSERT INTO alumnos (nombre, nivel) VALUES (?, ?)";

try (Connection conn = DriverManager.getConnection(URL);
     PreparedStatement pstmt = conn.prepareStatement(sqlInsert)) {
    
    // Sustituimos los ? por los datos reales
    pstmt.setString(1, "Marcos");
    pstmt.setString(2, "Master");
    
    pstmt.executeUpdate(); // Se usa para INSERT, UPDATE, DELETE
    System.out.println("¡Registro completado con éxito!");

} catch (SQLException e) {
    System.out.println("Error al registrar: " + e.getMessage());
}
```

## 4.Usos avanzados

Para consultas más complejas, actualización de datos (UPDATE) o borrado de datos (DELETE), puedes usar el código anterior simplemente teniendo en cuenta:
- **La variable String SQL:** Cambiamos la consulta en la variable.
- **Los parámetros (?):** Nos debemos asegurar de que el número de ? coincida con los pstmt.set... que añadan debajo.
- **Escritura VS Lectura:**
    - Si vas a hacer consultas para obtener información (SELECT), usamos el ejemplo de "Leer en la base de datos" porque usa pstmt.executeQuery() (ya que espera recibir una tabla de datos o ResultSet).
    - Por el contrario, si queremos hacer actualizaciones, inserciones o eliminar datos (INSERT, UPDATE, DELETE), usamos el ejemplo de "Escribir en la base de datos" porque usa pstmt.executeUpdate() (ya que solo necesita devolver un número entero que indica cuántas filas han sido modificadas).
 
Recuerda:
| Si tu SQL es... | Método a usar | ¿Por qué? |
| --- | --- | --- |
| `SELECT` | `.executeQuery()` | Porque quiero que la Base de Datos me devuelva una lista de datos (ResultSet). |
| `INSERT` / `UPDATE` / `DELETE` | `.executeUpdate()` | Porque solo quiero quiero que la Base de Datos realice una acción (y me informe sobre cuántas filas cambiaron). |

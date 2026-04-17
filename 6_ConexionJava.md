Ahora llega la parte más interesante, que consiste en conectar Java a SQL para juntar lo mejor de los 2 mundos: la programación y las bases de datos.

## 1. Preparar la BBDD.

En primer lugar, debemos tener la Base de Datos creada y su tabla o tablas también creadas. Desde Java insertaremos datos y haremos consultas.

## 2. Crear un Proyecto de Java e Instalar el Driver JDBC.

Java por sí solo no puede conectarse a una Base de Datos, necesita un software adicional que se llama el driver JDBC.
Debemos crear un proyecto de Java y colocar el `.jar` del **SQLite JDBC Driver** en la carpeta *Libraries* o *Referenced Libraries*.

Enlace de descarga: https://repo1.maven.org/maven2/org/xerial/sqlite-jdbc/ (buscar la versión más reciente y descargar el `.jar`).

## 3. Programar la conexión.

En nuestros programa de Java debemos de usar algunas instrucciones para conectarnos y para lanzar inserciones de datos y consultas.

En concreto usaremos estos objetos de Java:
- **`Connection`**: El túnel hacia el archivo .db.
- **`PreparedStatement`**: La forma de enviar SQL.
- **`ResultSet`**: El objeto que guarda los datos que nos devuelve un SELECT.

```java
import java.sql.*;

public class EjemploJDBC {

    // 1. La URL de conexión al archivo de base de datos
    private static final String URL = "jdbc:sqlite:C:/ruta/a/tu/archivo/codemaker.db";

    public static void main(String[] args) {

        // --- PARTE 1: INSERTAR UN DATO ---
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


        // --- PARTE 2: CONSULTAR LOS DATOS ---
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
    }
}
```

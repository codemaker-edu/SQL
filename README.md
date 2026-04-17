# Fundamentos de Bases de Datos - SQL

¡Bienvenido al módulo de Bases de Datos! Si has llegado hasta aquí, ya sabes programar lógica en Python, Java o C#. Pero ahora vamos a resolver el gran problema de cualquier desarrollador: **¿Qué pasa con los datos cuando cerramos el programa?**.

Hasta ahora, tus programas piden datos a los usuarios por consola, los guardan en variables o estructuras como arrays o listas, y funcionan perfectamente... hasta que cierras el programa y lo vuelves a abrir, y dichos datos han desaparecido, las variables de reinicializan. ¿Cómo guarda entonces una red social mi nombre de usuario, contraseña, lista de amigos, etc., sin que se le borre al cerrar y abrir la app?

Para eso están las bases de datos, una pieza fundamental en el desarrollo de software. Tanto que la gran mayoría de programas del mundo están formados por código de programación + bases de datos.

</br>

## 1. ¿Para qué sirven las Bases de Datos?

En tus proyectos de Unity o tus programas de Java, has usado variables para guardar puntuaciones, nombres, etc. Sin embargo, las Bases de Datos (BBDD) son herramientas especializadas en **organizar, almacenar y recuperar** grandes cantidades de información de forma eficiente.

En el desarrollo de software se usan para:
* **Gestión de Usuarios:** Guardar logins y contraseñas de forma segura.
* **Inventarios:** Saber qué objetos tiene cada jugador en un RPG o qué productos tiene Amazon.
* **Rankings:** Guardar las mejores puntuaciones de todos los jugadores del mundo, los productos más vendidos en Amazon o las publicaciones más vistas en Instagram.
* Etc.

</br>

## 2. Variables y arrays VS Bases de Datos

Para entender por qué necesitamos SQL, debemos diferenciar dónde vive la información mientras programamos:

### Memoria Volátil (RAM)
Cuando creas un `int puntuacion = 10;` en Java o C#, ese dato se guarda en la memoria RAM.
* **Ventaja:** Es extremadamente rápida.
* **Problema:** Si el programa se cierra, se produce un error o se apaga el PC, **el dato desaparece para siempre**.

Es como escribir en una pizarra: cuando termina la clase, se borra.

### Memoria Persistente (Disco duro)
Una Base de Datos guarda la información en el almacenamiento secundario (Disco duro/SSD).
* **Ventaja:** Los datos sobreviven al cierre del programa y a los apagones.
* **Problema:** Las acciones de consultar y guardar datos son algo más lentas.

Es como escribir en un libro: la información permanece ahí aunque cierres el libro y lo guardes en la estantería.

| Característica | Variables (Código)                    | Base de Datos (SQL)                   |
| :---           | :---                                  | :---                                  |
| **Duración**   | Temporal (mientras corre el programa) | Permanente (hasta que se borre)       |
| **Acceso**     | Solo desde el programa actual         | Accesible por múltiples apps a la vez |

> [!IMPORTANT]
> Pero entonces, cuando aprendamos bases de datos... ¿dejaremos de usar variables y arrays?
> 
> **NO**, siempre usaremos variables, arrays y otras estructuras de código. Si tu programa debe preguntarle el nombre y la edad al usuario, debe guardarlas en variables (los lenguajes de programación no tienen otra opción).
>
> Sin embargo, tú como desarrollador deberás saber cuáles de los datos que maneja tu programa pueden perderse al salir y cuales no. Los que no puedan perderse, los mandaremos desde nuestro código a una Base de Datos. En el futuro, cuando el usuario abra la app, nuestro código podrá preguntar esos datos a la Base de Datos y traerlos de vuelta a una variable para poder volver a utilizarlo.

</br>

## Razónalo tú mismo
Imagina que estás creando un clon de **Minecraft** y necesitas guardar la siguiente información:
- Posición (coordenadas) del jugador en cada momento.
- Posición (coordenadas) de cada bloque utilizado para construir una casa.

¿Dónde guardarías la posición del jugador? ¿Es importante que mañana cuando vuelva a abrir el juego el jugador esté en el mismo sitio... o puede empezar siempre desde un origen?

¿Y la posición de la casa?¿Es importante que mañana siga ahí?

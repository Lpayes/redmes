# instrucciones claras para compilar y ejecutar

Para garantizar el funcionamiento correcto de los proyectos y la resolución de dependencias entre ellos, se deben seguir los siguientes pasos desde la terminal.

### 1. Preparación de la Librería Local
Antes de compilar el proyecto principal, es necesario instalar la librería de la pila manual en el repositorio local de Maven. Desde la carpeta `umg.edu.gt.data-structure.stack`, ejecute:

```bash
mvn clean install
mvn clean package -Pobfuscate

###Luego para lo de porbar si funcionan la main tanto el jar nomrmal como ofuscado
java -cp "target/stackHandler-0.0.1-SNAPSHOT.jar;target/libs/*" stackHandler.handler.Main
java -cp "target/stackHandler-0.0.1-SNAPSHOT-obf.jar;target/libs/*" stackHandler.handler.Main


#Parte D - Ingeniería inversa

Al realizar la descompilación del archivo stackHandler-0.0.1-SNAPSHOT-obf.jar con la herramienta JD-GUI, se observan cambios significativos que impactan la legibilidad del código original, cumpliendo con el objetivo de la ofuscación.

#### 1. ¿Qué tanto se dificulta la lectura?
La lectura se dificulta considerablemente debido al renombrado de componentes clave. En el código original de Eclipse, las clases y métodos tienen nombres descriptivos como SymbolValidator e isValid. En la versión descompilada, estos han sido reemplazados por identificadores de un solo carácter como class a y el método a.a().

Se puede observar la pérdida de nombres en las variables locales dentro del método main:
* La variable original expresion ahora se identifica como str.
* Las variables originales caso1 y caso2 ahora aparecen como str1 y str2.
* La variable booleana esValida ahora se muestra simplemente como bool.

#### 2. ¿Se pierde claridad estructural?
La claridad estructural se mantiene parcialmente, pero se pierde el contexto semántico. Aunque JD-GUI logra reconstruir la estructura de los ciclos for y las condiciones if, la eliminación de todos los comentarios de desarrollo, como las notas de autor y recordatorios de requisitos de la parte b, hace que el código parezca una caja negra donde solo se ve la lógica cruda sin explicaciones adicionales.

Un detalle técnico detectado es la optimización del iterador en la clase del validador: el tipo original int i fue transformado por el ofuscador en un byte b para optimizar el uso de memoria, lo cual añade una capa de confusión al comparar el código fuente con el descompilado.

#### 3. ¿Sigue siendo posible entender la lógica?
Es posible entender la lógica, pero requiere un esfuerzo analítico mayor. Un analista podría deducir el propósito del programa gracias a factores que la ofuscación no puede ocultar:
* Strings literales: Los mensajes de consola como "Tamaño actual (getsize):" y "Peek:" permanecen intactos, revelando la función de cada línea de ejecución.
* Constantes de comparación: Los caracteres de agrupación como paréntesis, corchetes y llaves son visibles, permitiendo identificar que se trata de un validador de símbolos.
* Llamadas a librerías: Se nota claramente la interacción con la librería StackLinked, confirmando el uso de una estructura de datos tipo pila.

---
Conclusión: La ofuscación fue exitosa al eliminar la identidad de los métodos de negocio, aunque la lógica estructural sea reversible mediante un análisis técnico detallado.

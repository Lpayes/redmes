### 🔎 Parte D: Análisis de Ingeniería Inversa

Al realizar la descompilación del archivo `stackHandler-0.0.1-SNAPSHOT-obf.jar` con la herramienta **JD-GUI**, se observan cambios significativos que impactan la legibilidad del código original, cumpliendo con el objetivo de la ofuscación.

#### 1. ¿Qué tanto se dificulta la lectura?
La lectura se dificulta considerablemente debido al **renombrado de componentes clave**. En el código original de Eclipse, las clases y métodos tienen nombres descriptivos como `SymbolValidator` e `isValid`. En la versión descompilada, estos han sido reemplazados por identificadores de un solo carácter como **`class a`** y el método **`a.a()`**.

Además, las variables internas dentro del `Main` perdieron su nombre original:
* `expresion` pasó a ser **`str`**.
* `caso1` y `caso2` pasaron a ser **`str1`** y **`str2`**.
* `esValida` pasó a ser un simple **`bool`**.

#### 2. ¿Se pierde claridad estructural?
La **claridad estructural se mantiene parcialmente**, pero se pierde el contexto semántico. Aunque JD-GUI logra reconstruir la estructura de los ciclos `for` y las condiciones `if`, la eliminación de todos los comentarios de desarrollo (como "Pruebas de la estructura de datos - Lester") hace que el código parezca una "caja negra" donde solo se ve la lógica cruda sin explicaciones.

Un detalle técnico interesante es la optimización del iterador en el `SymbolValidator`: el original `int i` fue transformado por el ofuscador en un **`byte b`** para ahorrar recursos, lo cual añade una pequeña capa extra de confusión al comparar ambos archivos.

#### 3. ¿Sigue siendo posible entender la lógica?
Sí, **sigue siendo posible entender la lógica**, pero requiere un esfuerzo analítico mayor. Un analista podría deducir el propósito del programa gracias a factores que la ofuscación no oculta:
* **Strings literales**: Los mensajes de consola como `"Tamaño actual (getsize):"` y `"Peek:"` permanecen intactos, revelando qué hace el programa en cada paso.
* **Constantes de comparación**: Los caracteres de agrupación (`'('`, `'['`, `'{'`) son visibles, permitiendo identificar que se trata de un validador de símbolos.
* **Llamadas a librerías externas**: Se nota claramente la interacción con `StackLinked`, lo que confirma el uso de una estructura de datos tipo pila.

---
**Conclusión:** La ofuscación fue exitosa al eliminar la propiedad intelectual de los nombres de métodos de negocio, aunque la lógica estructural sea reversible mediante un análisis detallado.

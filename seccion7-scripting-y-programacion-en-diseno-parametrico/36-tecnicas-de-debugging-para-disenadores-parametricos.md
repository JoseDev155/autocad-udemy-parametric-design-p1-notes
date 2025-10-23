# 36. Técnicas de Debugging para Diseñadores Paramétricos

![imagen28-clase36](seccion7-imagenes/2024-09-28_11-09-53-ea8d945bf930a3ec284946d0ee71fcf5.webp)

El **debugging** es una habilidad esencial para cualquier diseñador que trabaje con **scripting** en entornos de diseño paramétrico, como
**Grasshopper**, **Dynamo**, o cualquier plataforma que permita el uso de lenguajes como **Python** o **C#**. A medida que los scripts y
algoritmos se vuelven más complejos, es común encontrar errores que pueden afectar el resultado de un diseño. Por lo tanto, saber cómo
**identificar**, **comprender** y **solucionar** estos problemas es crucial para asegurar que el proceso de diseño fluya sin interrupciones.

En este artículo, exploraremos algunas de las **técnicas de debugging** más útiles para diseñadores paramétricos que trabajan con scripts, y cómo
aplicar estos métodos para mejorar la **eficiencia**, **precisión** y **eficacia** en la creación de geometrías y soluciones paramétricas.

## 1. ¿Qué es el debugging y por qué es importante?

El **debugging** es el proceso de identificar y corregir errores (bugs) en un script o algoritmo. Estos errores pueden presentarse en diferentes
formas, como:

* **Errores sintácticos**: Problemas en la estructura del código, como comas mal colocadas, paréntesis faltantes o variables mal escritas.

* **Errores lógicos**: Cuando el script se ejecuta sin errores visibles, pero no produce los resultados esperados debido a un error en la lógica del algoritmo.

* **Errores de ejecución**: Estos ocurren cuando el código intenta ejecutar una operación imposible, como dividir entre cero o intentar acceder a una variable que no ha sido definida.

El debugging es importante porque permite al diseñador corregir estos problemas y asegurar que el script funcione correctamente. También es una
herramienta clave para **optimizar** y **refinar** los scripts, mejorando su rendimiento y eficacia.

## 2. Técnicas de debugging en Grasshopper y Python

Cuando trabajas con **scripting en Grasshopper**, particularmente con **Python**, es fundamental contar con un conjunto de técnicas de
debugging que te permitan identificar errores de manera rápida y eficiente.

### a) **Uso de la consola de salida**

Una de las herramientas más importantes en **Python Script** es la **consola de salida** o **panel de salida** en Grasshopper, que te
muestra mensajes, advertencias y errores que ocurren durante la ejecución del script.

Para depurar el código, puedes usar la función `print()` para mostrar los valores de las variables en diferentes puntos del script. Esto te
permite verificar si las variables contienen los valores correctos y si el flujo del programa es el esperado.

**Ejemplo**:

```python
python
Copiar códigoimport Rhino.Geometry as rg
 
# Definir una variable
radio = x  # Entrada desde Grasshopper
 
# Imprimir el valor de la variable en la consola para verificar
print("El radio es:", radio)
 
# Crear una geometría
centro = rg.Point3d(0, 0, 0)
circulo = rg.Circle(centro, radio)
 
# Devolver el círculo a Grasshopper
A = circulo
```

En este ejemplo, la función `print()` mostrará el valor de `radio` en la consola. Si el valor no es el esperado, podrás identificar rápidamente
dónde está el problema.

### b) **Uso de bloques `try-except` para manejar errores**

El manejo de excepciones mediante el bloque `try-except` es otra técnica valiosa para evitar que el script se detenga abruptamente debido a
errores inesperados. Esto es útil cuando tu script depende de entradas que pueden no estar definidas o cuando existen operaciones que podrían
fallar, como dividir entre cero o trabajar con geometrías inválidas.

**Ejemplo**:

```python
python
Copiar códigotry:
    # Intentar ejecutar este bloque de código
    resultado = 10 / x  # x es la entrada de Grasshopper
except ZeroDivisionError:
    # Mostrar un mensaje de error si ocurre una división por cero
    print("Error: No se puede dividir entre cero.")
    resultado = None  # Definir un valor predeterminado
```

El bloque `try-except` permite que el script continúe ejecutándose incluso si se produce un error, lo que es especialmente útil cuando estás
explorando diferentes parámetros de entrada en Grasshopper y no quieres que el script se detenga cada vez que ocurre un error.

### c) **Verificación de tipos de datos**

Otro error común en el scripting es trabajar con **tipos de datos incorrectos**. Grasshopper a menudo trabaja con listas, números y
geometrías, y a veces el script espera un tipo de dato diferente del que se está pasando. Puedes verificar el tipo de una variable utilizando la
función `type()`.

**Ejemplo**:

```python
python
Copiar código# Verificar el tipo de dato de la entrada
if isinstance(x, int):
    print("x es un entero")
else:
    print("x no es un entero, es de tipo:", type(x))
```

Esto es útil cuando estás manipulando múltiples tipos de datos en un solo script, como listas de puntos o geometrías, y necesitas asegurarte
de que estás trabajando con el tipo correcto.

### d) **Dividir el script en bloques más pequeños**

Cuando trabajas con scripts largos y complejos, es una buena práctica **dividir el script en bloques más pequeños** y depurar cada sección por
separado. Esto facilita la identificación de errores y te permite concentrarte en resolver un problema a la vez.

Por ejemplo, si estás trabajando en un script que genera una superficie paramétrica y luego realiza operaciones booleanas en ella, puedes depurar
primero la generación de la superficie antes de pasar a la segunda parte.

```python
python
Copiar código# Parte 1: Generación de la superficie
superficie = rg.Surface.CreateRuledSurface(curva1, curva2)
print("Superficie generada")
 
# Parte 2: Operaciones booleanas (se debugeará después)
# ...
```

## 3. Técnicas de debugging en Dynamo y C#

En **Dynamo**, las técnicas de debugging son similares, aunque el lenguaje de scripting más común es **C#**. Al igual que en Grasshopper,
Dynamo tiene un **panel de salida** que muestra los errores y advertencias generados por el script.

### a) **Uso de mensajes de salida**

En C#, puedes usar `System.Console.WriteLine()` para imprimir mensajes en la consola y verificar el estado de las variables.

**Ejemplo**:

```csharp
csharp
Copiar códigodouble radio = x;  // Valor de entrada
System.Console.WriteLine("El radio es: " + radio);
 
// Generar una esfera
Sphere esfera = new Sphere(Point3d.Origin, radio);
A = esfera;
```

Este mensaje se mostrará en el **Editor de Scripts de Dynamo** o en el panel de mensajes de la consola, y te ayudará a confirmar que los valores
se están manejando correctamente.

### b) **Manejo de excepciones en C#**

El manejo de excepciones también es esencial en C#. Usar bloques `try-catch` te permitirá manejar errores de manera eficiente y prevenir
que el script se detenga.

**Ejemplo**:

```csharp
csharp
Copiar códigotry
{
    // Intentar realizar una división
    double resultado = 10 / x;
    A = resultado;
}
catch (DivideByZeroException)
{
    // Mostrar un mensaje si ocurre una división por cero
    System.Console.WriteLine("Error: División por cero.");
    A = null;
}
```

### c) **Uso de depuradores integrados**

Si estás trabajando con un entorno más avanzado, como **Visual Studio** para C#, puedes aprovechar los depuradores integrados que permiten
**establecer puntos de interrupción** en el código y **ejecutar el script paso a paso**. Esto te permite examinar el valor de las variables
en cada paso y observar cómo cambia el flujo de ejecución del programa.

## 4. Depuración en flujos de trabajo complejos

Cuando trabajas en proyectos de diseño paramétrico más complejos que involucran múltiples scripts, es importante estructurar tu flujo de
trabajo de manera que te permita **aislar problemas** y resolverlos por etapas.

### a) Aislar el problema

Si un script complejo no funciona como esperas, intenta **aislar el problema** ejecutando solo una parte del script para ver si el error
proviene de esa sección. Esto es especialmente útil cuando tienes flujos de trabajo que incluyen múltiples funciones o bucles.

Por ejemplo, si estás trabajando en un script que genera geometrías paramétricas y luego realiza análisis estructurales, puedes ejecutar
primero la parte de generación geométrica y verificar los resultados antes de proceder al análisis.

### b) Documentar el proceso de depuración

Una práctica recomendada en proyectos más grandes es **documentar el proceso de depuración**. Esto incluye registrar los errores que has
encontrado y cómo los has solucionado. Llevar un registro te ayudará a recordar las soluciones y aplicar técnicas similares en problemas futuros.

## 5. Herramientas adicionales para debugging

Existen herramientas adicionales que pueden facilitar el proceso de debugging en entornos de diseño paramétrico:

* **Editor de código externo**: Usar editores de código externos como **Sublime Text** o **Visual Studio Code** te permite trabajar con un entorno más potente para escribir y depurar scripts en Python o C#.

* **Plugins de análisis**: En Grasshopper y Dynamo, hay plugins disponibles que te permiten analizar y depurar tus scripts con más detalle. Estos plugins proporcionan información sobre cómo se están manejando los datos dentro del flujo de trabajo.
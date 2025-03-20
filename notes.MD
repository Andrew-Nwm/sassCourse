# TOP LEVEL STATEMENTS: Declaraciones que solo pueden estar en la parte superior de la hoja de estilos.
1. Imports: (@import) esta directiva permite incluir contenido de un archivo SASS en otro.
2. Definición de un Mixin: Son bloques de código CSS reutilizables que se definen usando @mixin y se incluyen en otros selectores usando @include. Pueden aceptar parámetros y ayudan a reducir código repetitivo.
3. Definición de una función: Son bloques de código que realizan cálculos y retornan un único valor. Se definen usando @function y deben incluir la palabra clave @return. A diferencia de los mixins, las funciones se utilizan para operaciones computacionales y no para generar bloques CSS directamente.
 Son archivos SASS independientes que contienen código reutilizable. Se pueden separar en archivos parciales (que comienzan con guión bajo, como _variables.scss) y luego importarlos en un archivo principal. Los módulos ayudan a:
    - Organizar el código en componentes lógicos
    - Mejorar la mantenibilidad
    - Facilitar la reutilización de estilos
    - Evitar archivos SASS demasiado grandes

# UNIVERSAL STATEMENTS: son statements que pueden usarse en cualquier parte del código:
1. Variables
2. Estructuras de control
3. Reglas como @error, @warn y @debug
4. Declaraciones CSS como reglas de estilo (at-rules) y mixins

# TIPOS DE VARIABLES
1. Una variable es un espacio asignado en memoria.
2. Las variables en sass pueden ser declaradas en cualquier parte del código, pero por buenas prácticas se crean en la parte de arriba.
3. ejemplo de creación: 
~~~css
$primary-color: #0099ff
~~~
4. Las variables en sass son imperativas, en el momento que se actualice su valor, cambiará automaticamente.
5. Existe una bandera en sass llamada default: `!default` esta va a tomar un valor nulo hasta que se le asigne un nuevo valor.

# Uso de selectores, scope de variables y shadowing
1. Los selectores en css definen sobre qué elementos se aplicarán un conjunto de reglas:
    - Clase
    - Id
    - Tipo
    - Atributo

2. Dentro de Sass hace referencia al contexto en el que son declaradas las variables y donde es posible hacer uso de las mismas, hay dos tipos de variables:
    - Variables locales: están declaradas en un bloque dentro de llaves, cualquier selector anidado puede acceder a las variables locales declaradas dentro del selector.
    - Variables globales: son todas las variables declaradas en cualquier parte de la hoja de estilos, por consecuente, podemos acceder a ellas en cualquier parte del código.

3. Shadowing: dice que las variables globales y locales pueden tener el mismo nombre siempre y cuando estén a diferente nivel del scope. Esto ayuda a que no se llege a modificar por error el valor de las variables globales. Ejemplo:
~~~css
    $text-color: #333; // Variable global

    .container {
    // Dentro de este scope, la variable local $text-color "shadowing" a la global
    $text-color: #888; 
    
    color: $text-color; // Usa #888
    
    .nested-element {
        // Hereda el valor de $text-color del scope padre (.container)
        border: 1px solid $text-color; // Usa #888
    }
    }

    .footer {
    // Fuera del scope de .container, se usa el valor global
    color: $text-color; // Usa #333
    }
~~~

4. !global flag: en caso de que se quiera modificar el valor de una variable global dentro del scope de una variable local, se hace uso de la flag !global. Ejemplo:
~~~css
    $button-color: #0099ff; // Variable global

    .button {
    // Modificamos la variable global desde un scope local
    $button-color: #ff5500 !global;
    
    background-color: $button-color; // Usa #ff5500
    }

    .link {
    // La variable global fue modificada permanentemente
    color: $button-color; // Usa #ff5500, no #0099ff
    }
~~~
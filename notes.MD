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
3 Reglas como @error, @warn y @debug
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
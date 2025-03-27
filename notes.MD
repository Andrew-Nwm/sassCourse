# TOP LEVEL STATEMENTS: Declaraciones que solo pueden estar en la parte superior de la hoja de estilos.

1. Imports: (@import) esta directiva permite incluir contenido de un archivo SASS en otro.
2. Definición de un Mixin: Son bloques de código CSS reutilizables que se definen usando @mixin y se incluyen en otros selectores usando @include. Pueden aceptar parámetros y ayudan a reducir código repetitivo.
3. Definición de una función: Son bloques de código que realizan cálculos y retornan un único valor. Se definen usando @function y deben incluir la palabra clave @return. A diferencia de los mixins, las funciones se utilizan para operaciones computacionales y no para generar bloques CSS directamente.
   Son archivos SASS independientes que contienen código reutilizable. Se pueden separar en archivos parciales (que comienzan con guión bajo, como \_variables.scss) y luego importarlos en un archivo principal. Los módulos ayudan a:
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

```css
$primary-color: #0099ff;
```

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

```css
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
```

4. !global flag: en caso de que se quiera modificar el valor de una variable global dentro del scope de una variable local, se hace uso de la flag !global. Ejemplo:

```css
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
```

5. At Rules: si se tienen muchas hojas de estilos, se pueden modularizar usando at rules:
   - Es una declaracion que cumple con funciones, se inicializa con un arroba (@).
   - Ayudan a mantener compatibilidad con futuras versiones de CSS.
   - Ejemplos de at rules son:
     - @use: sirve para importar los modulos, estilos y funciones de otras hojas de estilos
     - @import: import se encarga de hacer los estilos globales
     - @function: permite crear funciones personalizadas, sin embargo, sass cuenta con funciones ya existentes
     - @forward: recibe como parametro una url y ayuda a cargar los estilos de una hoja de estilos
     - @extend: es una directiva que permite compartir una serie de propiedades css de un selector a otro, es una forma de heredar todos los estilos de una clase en otra, esto ayuda a evitar la duplicación de códgio, mantener una estilización consistente y crear relaciones entre estilos.
     - @at-root: se encarga del manejo (carga) de los estilos del root de la aplicación
   - Ejemplos de ar rules de compilación podemos encontrar:
     - @error: se presenta cuando hay errores de compilación
     - @warn: se presenta para mostrar posibles cambios o mejoras en el código
     - @debug: se utiliza para resolver y encontrar errores de una manera más sencilla
     - @include: se utiliza para invocar los mixins
     - @for, @if, @each, @while: se usan para estructuras de control (se pueden usar dentro de funciones)
   - Nesting: se trata de la anidación de selectores, esto ayuda a la simplificación del código. Estos deben escribirse en el orden que aparecen en el HTML

# Expresiones

1. Una expresión es todo aquello que va del lado derecho de una variable, esto admite diferentes tipos de valores
2. Las expresiones son mucho más poderosas que los valor CSS simples ya que se pueden pasar como argumentos a los mixins y a las funciones.
3. Ejemplos de expresiones literales:
   - Números
   - Strings
   - Colores
   - Booleanos
   - Null
   - Listas
   - Mapas

# Herencia en Sass

1. es un mecanismo que permite que un selector reutilice estilos que fueron usados anteriormente, ejemplo:
```css
.error {
  border: 1px #f00;
  background-color: #fdd;

  &--serious {
    @extend error;
    border-width: 3px;
  }
}
```
2. Como se evidenció en el ejemplo anterior, para hacer uso de la herencia debemos utilizar la directiva @extend junto a los estilos de la clase que será reutilizada.

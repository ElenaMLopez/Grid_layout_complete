# Grid_layout

En esta caso, más que una introducción a grid, que ya se ha realizado en el curso de [iniciación](https://github.com/ElenaMLopez/playing_grid), nos adentramos en más características de esta nueva especificación de CSS para explotar su potencial. 

Se seguira el curso gratuito online del gran [Juan Andrés Núñez](https://www.youtube.com/playlist?list=PLM-Y_YQmMEqBxmylkI5WJn9ouUxWlJNOW) que no se cansa de compartir conocimiento con la comunidad. Mil gracias por tu labor. 

El temario será el siguiente:

- Práctico 01: Introducción al curso y primera demo
- Práctico 02: Terminología y primeros pasos
- Práctico 03: Separación entre los elementos GRID
- Práctico 04: Usando GRID lines por su nombre
- Práctico 05: GRID start & end lines
- Práctico 06: La unidad fr
- Práctico 07: GRID template areas
- Práctico 08: Establecer límites con minmax()
- Práctico 09: Repetir valores y patrones con repeat()
- Práctico 10: GRID dinámico con auto-fill y auto-fit
- Práctico 11: GRID auto-placement y packing modes
- Práctico 12: Implicit & explicit GRID
- Práctico 13: Re-ordena GRID items con la propiedad order
- Práctico 14: GRID dentro de otro GRID
- Práctico 15: Propiedad acortada grid-template
- Práctico 16: Propiedad acortada grid
- Práctico 17: Alineamiento de GRID items con justify-items
- Práctico 18: Alineamiento de GRID items con justify-items
- Práctico 19: Alineamiento de GRID ítems con justify-self
- Práctico 20: Alineamiento de GRID ítems con align-self
- Práctico 21: Ejercicio final 1/3
- Práctico 22: Ejercicio final 2/3
- Práctico 23: Ejercicio final 3/3



Como consulta y complemento a lo que se explica, podemos utilizar la guía de [CSS Triks para grid](https://css-tricks.com/snippets/css/complete-guide-grid/), que es muy completa.

---

## Práctico 01: Introducción al curso y primera demo

Utilizaremos como ejemplo los archivos contenidos en Ejemplo_1 que tiene [este resultado](ejemplo_1/index.html).

Grid ha venido para quedarse y es necesario conocer cómo funciona. 
A modo motivacional vamos a ver un sencillo ejemplo que tendrá un responsive muy simple también, y de esta forma comprobar el gran potencial de esta especificación. De momento no nos detenemos demasiado a explicar conceptos, tan sólo fijémonos en lo que se puede hacer fácilmente.

Tenemos un elemento *main* que deseamos que a partir de 500px para abajo, se vea en una sóla columna y para el resto de otra forma. 
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="style.css">
    <title>Grid</title>
</head>
<body>
    <main>
        <header> Header </header>
        <aside> Izquerda </aside>
        <article> Contenido </article>
        <aside> Derecha </aside>
        <footer> Footer </footer>
    </main>
    
</body>
</html>
```

En el archivo de estilos, tenemos lo básico desde dónde arrancamos:
```css
main > * {
    background-color: goldenrod;
    border-radius: .25em;
    font-size: 3em;
    padding: 1em;
}

/* Definimos el Grid container */
main {
    display: grid;
    grid-gap: 1em; /* espacio entre celdas del grid
}
```

Lo primero que haremos será nombrar cada elemento del html, mediante la propiedad grid-area, de esta forma asignamos a cada elemento un nombre, para poder trabajar con el en grid.
```css

/* Nombramos los elementos (las áreas) */

header {
    grid-area: header;
}

aside:first-of-type {
    grid-area: izquierda;
}

aside:last-of-type {
    grid-area: derecha;
}

article {
    grid-area: contenido;
}

footer {
    grid-area: footer;
}

```
Con otra propiedad defino que disposición que quiero que tengan esas areas. Como partimos de mobile, empezamos con eso, así dentro del contenedor, debo especificar cómo quiero que se distribuyan esas áreas de la siguiente forma:
```css
main {
    display: grid;
    grid-gap: 1em;
    /* definimos el grid-template-area que distribuye los elementos según se le diga */
    grid-template-areas: 
        "header"
        "izquierda"
        "contenido"
        "derecha"
        "footer";
}
```
De esta forma definimos el orden, y en este caso es tan solo una sola columna, pero hagamos ahora la versión desktop:
```css
/* Desktop */

@media (min-width: 500px){
    main {
        grid-template-areas: 
            "header header header"
            "izquierda contenido derecha"
            "footer footer footer"
    }
}
```
De esta sencilla forma tenemos un típico layout que de otra forma suele ser más complicado hacer. Tan solo anotar que en caso de que por algún motivo kisieramos que el header por ejemplo, sólo ocupase dos de las 3 columnas, puede dejarse el espacio vacío poniendo un punto:
```css
/* Desktop */

@media (min-width: 500px){
    main {
        grid-template-areas: 
            "header header ."
            "izquierda contenido derecha"
            "footer footer footer"
    }
}
```


## Práctico 02: Terminología y primeros pasos

Es fundamental conocer la terminología de grid para entender cómo funciona. Por otra parte, se ha de ver la diferencia con FlexBox que opera en una dimensión y Grid Layout opera en dos dimensiones, por lo que pueden complementarse.

Conceptos:

**Grid container**: Elemento que hace de rejilla/contenedor. En el ejemplo *main*:
```css
main {
    display: grid;
}
```

**Grid Item**: Cada uno de los items hijos de un Grid container. La relación *parent/children* se denomina **GRID Context**.

**Grid Line**: El contenedor Grid, está formado por dos tipos de líneas, las horizontales y las verticales. Se puede hacer referencia a las líneas o bien por número o por nombre. La primera línea (borde del grid) se identifica ya con el 1.

**Grid Track**: Nombre genérico para un GRID row o GRID column. Es el espacio verticla u horizontal entre dos GRID lines **consecutivas**. Define de esta forma, el alto de un Grid Column o el ancho de un GRID row.

**Grid Cell**: Es la intersección entre un track vertical y otro horizontal, lo equivalente a una celda de una tabla. Es la unidad más pequeña a nuestra disposición para colocar un item

**Grid Area**: Cualquier porción del GRID contenido entre **4 líneas** del grid. Tiene N número de GRID Cells.

**Ejemplo 1:**

Veamos como declarar un grid y distribuir en el 4 columnas y tres filas:
```css
main > div {
    background-color: goldenrod;
    border-radius: .25em;
    font-size: 1em;
    padding: 1em;
}

/* Definimos el Grid container */

main {
    height: 100vh;
    /* Declaramos el display como grid */
    display: grid;
    grid-gap: 1em;
    /* Vamos a definir las columnas y las filas */
    grid-template-columns: 100px 100px 100px 100px;
    grid-template-rows: 100px 100px 100px;
}
```
**Ejemplo 2:**

Imaginemos ahora que lo que deseamos es que el elemento 10 ocupe más, 2 espacios por ejemplo. Para ello debemos primero acceder al elemento y luego con las propiedades *grid-colum-start* y *grid-colum-end* definimos el origen y el final:
```css
.item2:nth-child(10) {
    background-color: blueviolet;
    grid-column-start: 3;
    grid-column-end: 5;
     /* Formas abreviadas:
    grid-column: 3 / 5; /*--> de la columna 3 a la 5. 
    grid-column: 3 / -1; /*--> de la columna 3 al final. 
    */
}
```
**Ejemplo 3:**

Ahora queremos que el elemento 6 ocupe dos filas, la fila 2 y 3, pero sólo ese elemento. Se puede hacer de la siguiente forma:
```css
    /* Ejemplo 3 */
.item2:nth-child(6) {
    background-color: rgb(194, 0, 194);
    grid-column: 2 / 3;
    grid-row-start: 2;
    grid-row-end: 4; 
    /* Formas abreviadas:*/
    /* grid-row: 2 / 4; 
}
```
Es necesario poner en este caso el *grid-column: 2 / 3;*, puesto que si no mueve el elemento 6 al principio (comentar la línea de código que setea las columnas para ver que pasa).

Existe una propiedad que es la de *span* y esto extiende los elementos, pero tan sólo de momento saber q está ahí. 
```css
.item2:nth-child(6) {
    background-color: rgb(194, 0, 194);
    grid-column: 2 / 3;
    /* grid-row-start: 2;*/
    /* grid-row-end: 4;  */
     /* Formas abreviadas: */
    /* grid-row: 2 / 4;  */
    grid-row: span 2;
}
```

Y por supuesto podemos cambiar la estructura según el viewport.

## Práctico 03: Separación entre los elementos GRID:

El *grid-gap* determina la separación que habrá entre grid tracks, se puede poner de varias formas:
```css
main {
    display: grid;
    height: 100vh;
    /* Grid gap:*/
    grid-gap: 1rem;
     /* otras formas:*/
    /* grid-column-gap: 1rem; */
    /* grid-column-gap: 2rem; */
    /* grid-gap: 1rem 2rem; */    
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(3, 1fr);
}
```
Se ha dejado un elemento comentado en el html, el elemento 10, si se descomenta, grid no lo elimina, tan sólo lo añade como elemento implicito. Expliquemos esto. 

Todos los elementos que no estaban comentados (los div's del 1 al 9) han sido explicitamente definidos, se les ha dado un ancho y un alto dentro del grid con el *grid-template*, pero este último no, puesto que se sale (sobrepasa) los límites del grid (que se ha definido para 9 elementos 3 columnas por 3 filas). Grid en este caso lo añade, pero ocupa el espacio de su contenido a lo alto, y a lo ancho, lo que ocupe la columna. Si por algún motivo (por ejemplo una página dinámica) aparecen más elementos hay unas propiedades en grid, que determinan el tamaño de las celdas que irán ocupando. Ésta son *grid-auto-rows* (determinará el alto) y *grid-auto-columns* (determinará el ancho, por defecto el que esté en el grid-template para la columna donde se inserte).
```css
main {
    display: grid;
    height: 100vh;
    grid-gap: 1rem;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(3, 1fr);
        /* Inplicit grid */
    grid-auto-rows: 1fr;
}
```
Descomentando el div 10 vemos como mantiene la proporción con el resto.

## Práctico 04: Usando GRID lines por su nombre.

Vamos a ver como describir un Grid de otra forma, nombrando líneas, y poder referirnos a ellas. Es algo parecido a nombrar las áreas. Con esto conseguimos más control sobre el Grid.

Partiendo de este html:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="style.css">
    <title>Grid</title>
</head>
<body>
    <main>
        <header> Header </header>
        <aside> Sidebar </aside>
        <article> Contenido </article>
        <footer> Footer </footer>
    </main>
</body>
</html>
```
Ponemos este css:
```css
main {
    display: grid;
    height: 100vh;
    gap: 10px;
    /*nombrar líneas:*/
    grid-template-columns:
        [sidebar-start] 1fr
        [contenido-start] 2fr;
    grid-template-rows: 
        [header-start] 1fr
        [contenido-start] 2fr
        [footer-start] 1fr;
}

main > * {
    background-color: goldenrod;
    border-radius: .25em;
    display: flex;
    font-family: sans-serif;
    font-size: 3em;
    justify-content: center;
    align-items: center;
}
```
Fijándonos en las propiedades *grid-template-columns* y *grid-template-rows*, vemos como se han nombrado las líneas donde empieza el sidebar y el contenido, para las columnas, y dónde comienzan y terminan las filas header, contenido y footer. 

Ahora tan sólo queda colocar los elementos entre las líneas que deseemos:

```css
header {
    grid-column: sidebar-start / span 2; /* con esto le decimos que el header: empieza en la línea sidebar-start y se extiende 2 */
}

footer {
    grid-column: sidebar-start / span 2; /* con esto le decimos que el footer: empieza en la línea sidebar-start y se extiende 2 */
}
```
Respecto a la altura se mantiene.

Imaginemos que ahora queremos cambiar la disposición y que el sidebar llegue hasta abajo y el footer se corte:
```css
header {
    grid-column: sidebar-start / span 2; /* con esto le decimos que el header: empieza en la línea sidebar-start y se extiende 2 */
}

aside {
    grid-row: contenido-start / span 2; /* con esto le decimos que el asode: empieza en la línea contenido-start y se extiende 2 acia abajo, porque son rows*/
}
```

## Práctico 05: GRID start & end lines.

Si a parte de nombrar los inicios de los tracks podríamos nombrar el final de las líneas, y ser aun más explicito a la hora de dimensionar los tracks. 

Nombrar las líneas que suponen el final del track es  tan sencillo como esto:
```css
main {
    display: grid;
    height: 100vh;
    gap: 10px;
    /*nombrar líneas:*/
    grid-template-columns:
        [sidebar-start] 1fr
        [sidebar-end contenido-start] 2fr
        [contenido-end]; /*no es necesario darle tamaño, porque es la última línea!*/

    grid-template-rows: 
        [header-start] 1fr
        [header-end contenido-start] 2fr
        [contenido-end footer-start] 1fr
        [footer-end];
}
```
En todos los casos, las líneas que son end, son el start de otro track también, a excepción de la última línea vertical y la última línea horizontal claro, por lo que a la hora de definir el inicio de un track, se nombra también el final del anterior. 

Veamos como podemos ser de explícitos en el layout, con esto nos ahorramos también el tener que usar span, teniendo más control sobre lo que hacemos.
```css
main {
    display: grid;
    height: 100vh;
    gap: 10px;
    /*nombrar líneas:*/
    grid-template-columns:
        [sidebar-start] 1fr
        [sidebar-end contenido-start] 2fr
        [contenido-end]; /*no es necesario darle tamaño, porque es la última línea!*/

    grid-template-rows: 
        [header-start] 1fr
        [header-end contenido-start] 2fr
        [contenido-end footer-start] 1fr
        [footer-end];
}
/* confil default del main */

header {
    grid-column: sidebar-start / contenido-end; /*comienzas donde empieza el sidebar y acabas donde acaba el contenido*/
}

aside {
    grid-row: header-end / footer-end; /* con esto le decimos que el footer: empieza en la línea sidebar-start y se extiende 2 */
}

footer {
    grid-column: contenido-start / contenido-end; /* Ocupas sólo desde que empieza el contenido hasta que acaba */
}
```

## Práctico 06: La unidad fr

Vamos a ver que es exactamente una unidad fr (fraction unit). Una fr es una unidad de medida que aprobecha el espacio ya sea vertical u horizontal disponible que quede después de distribuir otras filas y otras columnas. 

Comenzamos con un template sencillo:
```css
main {
    display: grid;
    height: 100vh;
    grid-gap: 1rem;
    font-family: sans-serif;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 1fr 2fr 1fr;
}
```
La unidad fr tiene más peso que poner auto:
```css
main {
    display: grid;
    height: 100vh;
    grid-gap: 1rem;
    font-family: sans-serif;
    grid-template-columns: auto 1fr auto; /* fr toma el espacio disponible, escepto lo que ocupe
    el contenido de las dos primeras columnas seteadas a auto */
    grid-template-rows: 1fr 2fr 1fr;
}
```
Se puede combinar con px, porcentaje, rem...
```css
main {
    display: grid;
    height: 100vh;
    grid-gap: 1rem;
    font-family: sans-serif;
    grid-template-columns: 20rem 1fr 150px;
    grid-template-rows: 10% 2fr 50px;
}
```
Juguemos un poco con el responsive, para ver como se comporta:
```css
main {
    display: grid;
    height: 100vh;
    grid-gap: 1rem;
    font-family: sans-serif;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 1fr 2fr 1fr;
}

@media (max-width: 600px) {
    main {
        grid-template-columns: 1fr 1fr;
        grid-template-rows: repeat(5, 1fr);
    }
}
@media (max-width: 400px) {
    main {
        grid-template-columns: 1fr;
        grid-template-rows: repeat(9, 1fr);
    }
}
```
Con esto vemos cómo utilizar la unidad fr y distribuir según el espacio **disponible**.

## Práctico 07: GRID template areas

Una grid area, es el espacio delimitado por cuatro grid-lines. Es decir será siempre cuadrada o rectangular. Hay varias formas de definir un grid area, pero la más habitual y cómoda, es nombrala. 
```css
/* Nombrar las áreas: */

header {
    grid-area: header;
}
aside:first-of-type {
    grid-area: izquierda;
}
article {
    grid-area: contenido;
}
aside:last-of-type {
    grid-area: derecha;
}
footer {
    grid-area: footer;
}
```
Y ahora en el elemento main, hay que decir como se distribuyen estas áreas, y pensando en mobile-first podemos empezar con la versión mobil, q será una columna solo:
```css
main {
    display: grid;
    font-family: sans-serif;
    height: 100vh;
    grid-gap: 10px;

    grid-template-areas: 
        "header"
        "contenido"
        "izquierda"
        "derecha"
        "footer";
}
```
Ahora introducimos otro diseño para un viewport superior:
```css
@media (min-width: 600px) {
    grid-template-areas: 
        "header header header"
        "izquierda contenido derecha"
        "footer footer footer";
}
```

Esto es totalmente compatible con aplicar medidas a cada track, así que probemos a hacerlo:
```css
@media (min-width: 600px) {
    main {
        grid-template-areas: 
            "header header header"
            "izquierda contenido derecha"
            "footer footer footer";
        grid-template-columns: 1fr 2fr 1fr;
        grid-template-rows: 2fr 5fr 1fr;
    }
}
```

Si deseamos que un elemento no ocupe todo el espacio se puede poner un punto en el *grid-template-area*:
```css
    main {
        grid-template-areas: 
            "header header header"
            "izquierda contenido derecha"
            "footer footer ."; /* Poniendo un punto se deja esa sección sin footer*/
        grid-template-columns: 1fr 2fr 1fr;
        grid-template-rows: 2fr 5fr 1fr;
    }
```
Y si por algún motivo deseamos que una columna ocupe hasta el final o se meta en otra columna, podemos querer que la parte derecha ocupe las tres filas, y con tan solo nombrarlo en el *grid-template-area* lo podemos hacer:
```css
    main {
        grid-template-areas: 
            "header header derecha"
            "izquierda contenido derecha"
            "footer footer derecha";
        grid-template-columns: 1fr 2fr 1fr;
        grid-template-rows: 2fr 5fr 1fr;
    }
```

## Práctico 08: Establecer límites con minmax()

La función minmax() es tremendamente útil a la hora de determinar los tamaños maximos y mínimos de los tracks. La sintaxis es sencilla ``` minmax(tamaño_minimo, tamaño_maximo)```, donde ambos pueden expresarse en cualquier forma aceptada por css grid: fr, px, %, rem...

Veamos unos ejemplos:

```css
main {
    display: grid;
    font-family: sans-serif;
    height: 100vh;
    grid-gap: 10px;
    /* definiendo la distribución del grid: */
    grid-template-columns: repeat(8, minmax(60px, 150px));
}
```
Pueden hacerse patrones, por ejemplo en este caso repeat(numero_repeticiones, medida_primera_columna_del_patron minmax(10%, 1fr)), donde minmax dice la medida mínima y máxima de la segunda columna del patrón:

```css
/* 8 columnas con un patrón de dos (30px y minimo 10% y máximo flexible (1fr)*/

main {
    display: grid;
    font-family: sans-serif;
    height: 100vh;
    grid-gap: 10px;
    /* definiendo la distribución del grid: */
    grid-template-columns: repeat(4, 60px minmax(10%, 1fr));
}
```
Minmax() viene acompañado de dos formas de evitar q haya overflow del contenedor, estos son min-content y max-content, el primero es para un mínimo del contenido y el otro para que no ocupe más del máximo del contenido.
```css
/* 8 columnas con un tamaño mínimo determinado por el contenido*/
 main {
    display: grid;
    font-family: sans-serif;
    height: 100vh;
    grid-gap: 10px;
    /* definiendo la distribución del grid: */
    grid-template-columns: repeat(8, minmax(min-content, 1fr));
} 
```
Y lo mismo para max-content:
```css
/* 8 columnas con un tamaño máximo y mínimo determinado por el contenido*/
main {
    display: grid;
    font-family: sans-serif;
    height: 100vh;
    grid-gap: 10px;
    /* definiendo la distribución del grid: */
    grid-template-columns: repeat(8, minmax(min-content, max-content));
}
```
## Práctico 09: Repetir valores y patrones con repeat()

No hay mucho que explicar, tan solo ver diversas formas de realizar patrones y repeticiones de estos.
Comenzamos con una repetición básica de 12 columnas:
```css
main {
    display: grid;
    font-family: sans-serif;
    height: 100vh;
    grid-gap: 10px;
    /* definiendo la distribución del grid: */
    grid-template-columns: repeat(12, 1fr);
```
Podemos insertar un patrón de repetición de columnas de distintos tamaños (minimos en este caso):
```css
    /* patron de 3 columnas repetidas 4 veces y que las columnas tuviesen diferentes valores */
    grid-template-columns: 
        repeat(4,
            minmax(80px, 1fr)
            minmax(40px, 1fr)
            minmax(20px, 1fr)
        );
```
Incluso, podemos nombrar las líneas en el momento, por si alguien hecha de menos Bootstrap...
```css
    /* Podemos determinar donde empieza y acaba el grid y a la vez nombrar las lineas, para luego 
    poder distribuir los elementos */
    grid-template-columns: 
        [start]
        repeat(4,
            [col-xl-start] minmax(80px, 1fr)
            [col-xl-end col-m-start] minmax(40px, 1fr)
            [col-m-end col-s-start] minmax(20px, 1fr)
        )
        [end]
        ;
}

div:first-of-type {
    background-color: purple;
    grid-column: col-xl-start / col-m-end;
}

```
Hacer todo esto con css sin grid es una barbaridad. 
Incluso podemos hacer que el primer elemento vaya hasta el final de todas las columnas:
```css
div:first-of-type {
    background-color: purple;
    /* grid-column: col-xl-start / col-m-end; */
    grid-column: col-xl-start / end;

}
```

## Práctico 10: GRID dinámico con auto-fill y auto-fit.


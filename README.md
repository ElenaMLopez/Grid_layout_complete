# Grid_layout

En esta caso, más que una introducción a grid, que ya se ha realizado en el curso de [iniciación](https://github.com/ElenaMLopez/playing_grid), nos adentramos en más características de esta nueva especificación de CSS para explotar su potencial. 

Se seguira el curso gratuito online del gran [Juan Andrés Núñez](https://www.youtube.com/playlist?list=PLM-Y_YQmMEqBxmylkI5WJn9ouUxWlJNOW) que no se cansa de compartir conocimiento con la comunidad. Mil gracias por tu labor. 

El temario será el siguiente:

- Práctico 01: Introducción al curso y primera demo
- Práctico 02: Terminología y primeros pasos
- Práctico 03: Separación entre los elementos GRID
- Práctico 04: Usando GRID lines por su nombre
- Práctico 05: GRID start & end lines
- Práctico 06: GRID start & end lines
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
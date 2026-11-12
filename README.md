# Catálogo de Productos

Simulador de entrenamiento: maquetado semántico, jerarquía de estilos, modelo de caja, identidad visual, interactividad y arquitectura modular con BEM en CSS.

## Estructura del proyecto

css/
├── index.html
├── estilos.css
├── header.jpg
├── img/
└── css/
    ├── base.css
    ├── encabezado.css
    ├── menu-lateral.css
    ├── catalogo.css
    ├── tarjeta.css
    ├── botones.css
    └── pie-pagina.css

## Cálculo de puntos de especificidad

| Tipo de selector | Puntos |
|------------------|--------|
| Etiqueta (`p`, `a`, `li`) | 1 pt |
| Clase o pseudoclase (`.btn`, `:hover`) | 10 pts |
| ID (`#btn-destacado`) | 100 pts |

### Ejemplos del proyecto

| Selector | Cálculo | Total |
|----------|---------|-------|
| `body` | 1 etiqueta | 1 pt |
| `aside ul li a` (antes de BEM) | 4 etiquetas | 4 pts |
| `header nav ul li a` (antes de BEM) | 5 etiquetas | 5 pts |
| `.btn` | 1 clase | 10 pts |
| `.sidebar__link:hover` | 1 clase + 1 pseudoclase | 20 pts |
| `.card--destacada .card__title::after` | 2 clases + 1 pseudoelemento | 21 pts |
| `#btn-destacado` | 1 ID | 100 pts |

## Resumen

- **Herencia:** la fuente y el color declarados en `body` los heredan los títulos, párrafos y listas sin repetirlos.
- **Selectores combinados:** permiten dar un color distinto a los enlaces según su zona (menú, filtros y pie de página) sin afectar a los demás.
- **Cascada vs. especificidad:** el selector con ID (100 pts) ganó sobre la clase (10 pts) aunque la clase estaba escrita después.
<<<<<<< HEAD
- **Solución:** se eliminó el ID del CSS y se usó un sistema plano de etiquetas y clases, sin usar `!important`.

## Hallazgos: El Modelo de Caja

**1. Diferencia entre Margin y Padding**
El padding es el espacio de adentro de la caja, entre el contenido y el borde, y se pinta con el fondo del elemento. El margin es el espacio de afuera, que separa una caja de las demás y es transparente. En el catálogo, el padding (24px) evita que el texto de la tarjeta toque su borde, y el margin (16px) evita que las tarjetas se peguen entre sí.

- **Solución:** se eliminó el ID del CSS y se usó un sistema plano de etiquetas y clases (`.btn-comprar.btn-destacado`, 20 pts), sin usar `!important`.
## Hallazgos: El Modelo de Caja

**1. Diferencia entre Margin y Padding**
El padding es el espacio de adentro de la caja, entre el contenido y el borde, y se pinta con el fondo del elemento. El margin es el espacio de afuera, que separa una caja de las demás y es transparente. En el catálogo, el padding (20px) evita que el texto de la tarjeta toque su borde, y el margin (15px) evita que las tarjetas se peguen entre sí.
>>>>>>> 1336c5bd07885b4829dbdf82bcf1773128dc2a95

**2. Por qué es obligatorio usar box-sizing: border-box**
Sin esa regla, el navegador suma el padding y el borde al ancho declarado, y la caja termina más grande de lo esperado y puede romper el contenedor padre. Con `border-box`, el padding y el borde se cuentan dentro del ancho, y la caja mantiene el tamaño que le definimos.

**3. Efecto del margen grande en los elementos hermanos**
Cuando una tarjeta tiene un margen grande, empuja a las tarjetas vecinas y aumenta la distancia entre ellas, porque ese espacio exterior no se puede ocupar. Todo el bloque se desplaza y cambia la distribución de la página.
<<<<<<< HEAD

=======
>>>>>>> 1336c5bd07885b4829dbdf82bcf1773128dc2a95
## Hallazgos: Centralización de Identidad Visual y Espaciado

**1. Variables declaradas en :root**

| Variable | Valor |
|----------|-------|
<<<<<<< HEAD
| `--color-primario` | #2F4F4F |
| `--color-secundario` | #B8860B |
| `--color-secundario-oscuro` | #8B4513 |
| `--color-acento` | #2F4F4F |
| `--color-click` | #556B2F |
| `--color-texto` | #333333 |
| `--color-fondo` | #FAF0E6 |
| `--color-fondo-lateral` | #FFF8DC |
| `--color-tarjeta-hover` | #E0FFFF |
| `--color-superficie` | #FFFFFF |
| `--color-claro` | #FFFAF0 |
| `--color-borde` | #D2B48C |
| `--color-panel` | rgba(255, 255, 255, 0.88) |
=======
| `--color-primario` | #191970 |
| `--color-secundario` | #D2691E |
| `--color-acento` | #DC143C |
| `--color-texto` | #2F4F4F |
| `--color-fondo` | #FDF5E6 |
| `--color-fondo-lateral` | #FFF8DC |
| `--color-superficie` | #FFFFFF |
| `--color-claro` | #FFFAF0 |
| `--color-borde` | #D2B48C |
| `--color-panel` | rgba(255, 255, 255, 0.85) |
>>>>>>> 1336c5bd07885b4829dbdf82bcf1773128dc2a95
| `--fuente-principal` | 'Poppins', Arial, Helvetica, sans-serif |
| `--espaciado-pequeno` | 8px |
| `--espaciado-medio` | 16px |
| `--espaciado-grande` | 24px |
<<<<<<< HEAD
| `--radio` | 6px |
| `--transicion` | 0.3s ease |
| `--sombra` | 0 8px 20px rgba(47, 79, 79, 0.3) |
=======
>>>>>>> 1336c5bd07885b4829dbdf82bcf1773128dc2a95

**2. Ventaja de reutilizar medidas de margen y relleno**
Si uso siempre los mismos tres valores, todas las tarjetas y secciones tienen la misma cantidad de aire y el diseño se ve ordenado. Además, si el cliente pide más o menos separación, cambio un solo número en `:root` en vez de buscar valores sueltos en muchos selectores.

**3. Cómo :root previene colisiones visuales**
Cuando la hoja de estilos crece, es fácil que dos selectores usen colores parecidos pero distintos o espacios que no coinciden. Al tener todo en `:root`, cada selector solo pide una variable y no inventa valores, así que el diseño sigue una sola paleta y una sola escala de espaciado, sin desajustes.

## Hallazgos: Pseudoclases y Pseudoelementos

**1. Diferencia entre pseudoclase y pseudoelemento**
Una pseudoclase (`:hover`, `:active`, `:focus`) reacciona a lo que hace el usuario: pasar el cursor, hacer clic o navegar con el teclado, y cambia el estilo de un elemento que ya existe. Un pseudoelemento (`::before`, `::after`) crea contenido virtual antes o después de un elemento, como el ▸ del menú o la insignia "¡Oferta!", sin que exista en el HTML.

**2. Importancia de :focus para la accesibilidad**
Hay personas que no usan mouse y navegan con la tecla Tab. Con `:focus` y un contorno visible (`outline`) saben en qué enlace están parados. Sin esa señal se pierden en la página, así que es una práctica básica de accesibilidad web.

**3. Por qué decorar con ::before y ::after en vez de HTML**
Los adornos (insignias, iconos, líneas) son solo presentación y no tienen significado. Si los pongo con etiquetas vacías, ensucio el HTML y lo mezclo con el diseño. Con `::before` y `::after` el HTML queda limpio y semántico: la insignia "¡Oferta!", el ▸ del menú y la línea de las tarjetas viven solo en el CSS, y para cambiarlos o quitarlos edito un solo archivo.
<<<<<<< HEAD

## Hallazgos: Arquitectura BEM y Modularidad

**1. Qué significa BEM y cómo se escribe**
BEM significa Bloque, Elemento, Modificador. Se escribe `bloque__elemento--modificador`: el bloque es el componente (`.card`), el elemento es una parte que depende de él y se une con doble guion bajo (`.card__title`), y el modificador es una variación que se une con doble guion medio (`.card--destacada`, `.btn--secundario`).

**2. Por qué dividir el CSS en varios archivos facilita el trabajo colaborativo**
Cuando cada componente vive en su propio archivo (`tarjeta.css`, `botones.css`, `menu-lateral.css`), varias personas pueden trabajar a la vez sin pisarse el mismo archivo, y en Git hay menos conflictos al unir ramas. Además es más fácil encontrar dónde hacer un cambio: si falla el botón, abro `botones.css` y no busco en cientos de líneas.

**3. Cómo BEM evita la guerra de especificidad**
Antes usaba selectores anidados como `article h2` o `header nav ul li a`, que pesan más y se pisan entre sí. Con BEM cada regla usa una sola clase (peso 10), sin depender de dónde está el elemento en el HTML. Como todas pesan lo mismo, ninguna le gana a otra por accidente, y solo cambia el orden cuando de verdad hace falta. Las únicas reglas con más peso son los estados (`:hover`, `:focus`, `:active`), y es a propósito.
=======
>>>>>>> 1336c5bd07885b4829dbdf82bcf1773128dc2a95

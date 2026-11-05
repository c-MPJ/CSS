# Catálogo de Productos

Simulador de entrenamiento: maquetado semántico y jerarquía de estilos en CSS.

## Cálculo de puntos de especificidad

| Tipo de selector | Puntos |
|------------------|--------|
| Etiqueta (`p`, `a`, `li`) | 1 pt |
| Clase (`.btn-comprar`) | 10 pts |
| ID (`#btn-destacado`) | 100 pts |

### Ejemplos del proyecto

| Selector | Cálculo | Total |
|----------|---------|-------|
| `body` | 1 etiqueta | 1 pt |
| `aside ul li a` | 4 etiquetas | 4 pts |
| `footer ul li a` | 4 etiquetas | 4 pts |
| `header nav ul li a` | 5 etiquetas | 5 pts |
| `.btn-comprar` | 1 clase | 10 pts |
| `.btn-comprar.btn-destacado` | 2 clases | 20 pts |
| `#btn-destacado` | 1 ID | 100 pts |

## Resumen

- **Herencia:** la fuente y el color declarados en `body` los heredan los títulos, párrafos y listas sin repetirlos.
- **Selectores combinados:** permiten dar un color distinto a los enlaces según su zona (menú, filtros y pie de página) sin afectar a los demás.
- **Cascada vs. especificidad:** el selector con ID (100 pts) ganó sobre la clase (10 pts) aunque la clase estaba escrita después.
- **Solución:** se eliminó el ID del CSS y se usó un sistema plano de etiquetas y clases (`.btn-comprar.btn-destacado`, 20 pts), sin usar `!important`.
## Hallazgos: El Modelo de Caja

**1. Diferencia entre Margin y Padding**
El padding es el espacio de adentro de la caja, entre el contenido y el borde, y se pinta con el fondo del elemento. El margin es el espacio de afuera, que separa una caja de las demás y es transparente. En el catálogo, el padding (20px) evita que el texto de la tarjeta toque su borde, y el margin (15px) evita que las tarjetas se peguen entre sí.

**2. Por qué es obligatorio usar box-sizing: border-box**
Sin esa regla, el navegador suma el padding y el borde al ancho declarado, y la caja termina más grande de lo esperado y puede romper el contenedor padre. Con `border-box`, el padding y el borde se cuentan dentro del ancho, y la caja mantiene el tamaño que le definimos.

**3. Efecto del margen grande en los elementos hermanos**
Cuando una tarjeta tiene un margen grande, empuja a las tarjetas vecinas y aumenta la distancia entre ellas, porque ese espacio exterior no se puede ocupar. Todo el bloque se desplaza y cambia la distribución de la página.
## Hallazgos: Centralización de Identidad Visual y Espaciado

**1. Variables declaradas en :root**

| Variable | Valor |
|----------|-------|
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
| `--fuente-principal` | 'Poppins', Arial, Helvetica, sans-serif |
| `--espaciado-pequeno` | 8px |
| `--espaciado-medio` | 16px |
| `--espaciado-grande` | 24px |

**2. Ventaja de reutilizar medidas de margen y relleno**
Si uso siempre los mismos tres valores, todas las tarjetas y secciones tienen la misma cantidad de aire y el diseño se ve ordenado. Además, si el cliente pide más o menos separación, cambio un solo número en `:root` en vez de buscar valores sueltos en muchos selectores.

**3. Cómo :root previene colisiones visuales**
Cuando la hoja de estilos crece, es fácil que dos selectores usen colores parecidos pero distintos o espacios que no coinciden. Al tener todo en `:root`, cada selector solo pide una variable y no inventa valores, así que el diseño sigue una sola paleta y una sola escala de espaciado, sin desajustes.

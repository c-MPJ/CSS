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

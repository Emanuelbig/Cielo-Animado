# Cielo animado

Fondo animado de cielo con nubes suaves (lavanda / azul / blanco), hecho con un shader WebGL.
Es una versión propia inspirada en el estilo del fondo de la página de Codex de OpenAI
(el original es un video de ellos; este no lo usa, genera las nubes por código).

## Cómo verlo
Abrir `cielo-animado.html` con doble clic en cualquier navegador.

## Cómo ajustarlo
Todo se cambia dentro del `<script>` del HTML:

- **Colores:** variables `azul`, `lavanda` y `blanco` en el shader (RGB de 0 a 1).
  Ej.: `vec3(0.55, 0.62, 0.95)` = azul cielo.
- **Velocidad:** `uTime * 0.03` → más alto = nubes más rápidas.
- **Calidad / rendimiento:** `const ESCALA = 0.5` → 1 = resolución completa (más pesado).

## Cómo usarlo en otra página
Copiar estas tres partes:
1. El `<canvas id="cielo"></canvas>`
2. El CSS de `#cielo` (`position: fixed; inset: 0; ...`)
3. Todo el `<script>`

El contenido que va encima necesita `position: relative; z-index: 1;`.

## Cómo funciona (resumen)
- **Ruido fBm:** ruido sumado en varias escalas, es la base de las nubes.
- **Domain warping:** las coordenadas se deforman con otro ruido antes de calcular
  las nubes; eso da las formas "algodonosas".
- **Resolución reducida:** como las nubes son borrosas, se renderiza a la mitad
  y la GPU trabaja 4 veces menos.
- **Grano sutil:** evita que se vean escalones (banding) en los degradados.
- Si el sistema tiene activado "reducir movimiento", el cielo se muestra quieto.

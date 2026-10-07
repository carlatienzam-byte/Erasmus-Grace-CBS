# GRACE · Rozšířená realita (RA con marcador)

Versión en checo de la plantilla de RA con marcador del portal Colombine. Al apuntar con el móvil o la tablet al logotipo de GRACE aparece el modelo 3D de los dados. Usa **A-Frame 1.5.0** y **MindAR 1.2.5**, y funciona en el navegador sin instalar ninguna app.

## Contenido

```
Erasmus-Grace-CBS/
├── index.html               ← la experiencia completa (interfaz en checo)
├── marcador-imprimir.pdf    ← el logotipo GRACE listo para imprimir en A4 (textos en checo)
└── assets/
    ├── targets.mind         ← el logotipo GRACE compilado como marcador
    ├── grace-dice.glb       ← el modelo optimizado (Draco)
    ├── logo.png             ← el logotipo para la interfaz
    └── draco/               ← decodificador Draco en local
```

## Publicarlo

Va en la raíz del repositorio `carlatienzam-byte/Erasmus-Grace-CBS`, con GitHub Pages activado desde la rama `main` (carpeta raíz). La dirección es `https://carlatienzam-byte.github.io/Erasmus-Grace-CBS/`, que es a la que apunta el QR del cartel. Tiene que abrirse con https para que funcione la cámara.

## Optimización del modelo

| | Original | Optimizado |
|---|---|---|
| Triángulos | 105.214 | 52.606 |
| Texturas | 2 × 4096 px + 2048 px (≈ 200 MB en GPU) | 3 × 1024 px |
| Tamaño | 20,3 MB | 0,34 MB |

Pasos con glTF-Transform: `resize 1024 → jpeg → dedup → prune → weld → simplify (ratio 0,5) → draco`. Sin WebP.

## Ajustes rápidos (en `index.html`)

- **Tamaño del modelo**: `scale="3.5 3.5 3.5"` de `#modelo`. El modelo tiene el origen en la base, así que no hace falta elevarlo.
- **Posición sobre el logotipo**: objeto `MODOS` del script (`pos` de *mesa* y *pared*).
- **Texto de la ficha**: bloque `<p class="poema">` del panel informativo.

## Sobre el marcador

El logotipo GRACE tiene formas planas y pocos detalles, así que ofrece menos puntos de seguimiento que el de Carmen de Burgos. En la prueba con cámara simulada se reconoció en unos 3,5 segundos y no se perdió, pero conviene imprimirlo grande (unos 15 cm de ancho), en papel mate y con buena luz. Si tienes el logotipo en vectorial o en más resolución, se puede regenerar `targets.mind` y el PDF con más calidad.

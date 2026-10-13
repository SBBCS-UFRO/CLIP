# Preparar la publicación de CLIP! en GitHub

Esta entrega corresponde a **CLIP! 1.0.0** y no presupone una dirección de repositorio.
El nombre visible conserva «!», mientras los archivos y el paquete usan `CLIP`.
Si ya publicaste PLIP-Xplorer con la etiqueta `v1.0.0` en el mismo repositorio,
utiliza `clip-v1.0.0` para esta entrega sin sobrescribir la anterior.

## Contenido del repositorio

1. Descomprime `CLIP-1.0.0.zip`.
2. Crea un repositorio en tu cuenta con el nombre `CLIP`.
3. Sube **el contenido de la carpeta descomprimida**, para que `README.md` aparezca
   en la raíz y GitHub pueda mostrar el código. No subas solo el ZIP como único archivo.
4. Conserva `LICENSE.txt`, los créditos y `README_PLIP.md`: el motor original se
   distribuye bajo GPLv2 y mantiene la autoría de PLIP.

La entrega incluye una carpeta `install/` con el wheel listo para instalar. No contiene
entornos Conda, cachés, resultados de análisis, configuraciones privadas ni rutas de
usuario específicas. El código del motor y sus ejemplos sí se incluyen para que el
script de instalación funcione desde una copia nueva del repositorio.

## Publicación descargable

1. En GitHub abre **Releases → Draft a new release**.
2. Crea la etiqueta `v1.0.0` y el título **CLIP! 1.0.0**.
3. Adjunta:
   - `CLIP-1.0.0.zip` (fuentes, documentación y wheel).
   - `chimerax_clip-1.0.0-py3-none-any.whl` (plugin independiente).
   - `SHA256SUMS.txt` (sumas de verificación de ambos archivos).
4. Describe la versión como experimental y probada en ChimeraX 1.12/macOS.
   Enlaza `INSTALLATION.md` en la descripción de la release.
5. Publica cuando hayas revisado los archivos y el texto de la release.

No confundas una release de GitHub con una publicación en el Toolshed de UCSF:
esta distribución usa un wheel local mediante `toolshed install`.

## Volver a generar la entrega

En ChimeraX:

```text
devel build "/ruta/CLIP/chimerax"
```

En una terminal, desde la raíz del proyecto:

```sh
python3 chimerax/package_release.py
```

El script comprueba que el wheel coincide con las fuentes, genera `release/`, copia
el wheel a `install/` y crea el ZIP junto a `SHA256SUMS.txt`. El ZIP incluye un
manifiesto SHA256 interno de todos sus archivos. Las carpetas de resultados y los
entornos locales se excluyen por una lista explícita de archivos y extensiones.

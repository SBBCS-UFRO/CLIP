# CLIP! 1.0.0

<img src="chimerax/src/assets/clip.png" alt="CLIP!" width="160">

**Análisis y visualización de interacciones proteína–ligando en UCSF ChimeraX.**

CLIP! combina ChimeraX y PLIP en un plugin para analizar complejos moleculares,
explorar sus interacciones y preparar figuras desde una interfaz gráfica.
El análisis utiliza el motor PLIP y la representación utiliza los modelos,
etiquetas y renderizado nativos de ChimeraX.

## Empezar

1. Descarga y descomprime `CLIP-1.0.0.zip`.
2. Sigue la [instalación paso a paso](INSTALLATION.md) para instalar el plugin y
   configurar su entorno de análisis.
3. En ChimeraX, abre **Tools → Structure Analysis → CLIP!**.
4. Elige el idioma, abre un complejo proteína–ligando y pulsa **Analizar estructura**.
5. Explora el resultado, personaliza la escena y exporta tu figura.

Si ya tienes un informe XML compatible y su estructura correspondiente, puedes
utilizar CLIP! para visualizarlo sin instalar el motor de análisis.

## Qué puedes hacer

- Explorar ocho tipos de interacción y filtrar su visualización por ligando y categoría.
- Seleccionar residuos desde la tabla de resultados y enfocar el sitio de unión.
- Ajustar fondo, luces, materiales, colores, representaciones y transparencia.
- Mostrar residuos y distancias como etiquetas 3D y colocarlas manualmente.
- Guardar y compartir estilos visuales en JSON.
- Exportar figuras PNG, TIFF o JPEG, incluyendo transparencia en PNG y TIFF.
- Exportar interacciones en CSV y guardar la escena como sesión `.cxs` de ChimeraX.

## Idiomas

English · Español · Deutsch · Français · 中文（简体） · 日本語 · Português

El selector de la cabecera cambia el idioma del panel y recuerda la preferencia.
Se incluyen chino simplificado y portugués de Brasil. Cambiar de idioma conserva
los resultados, filtros, estilos y la posición manual de las etiquetas.

## Documentación

| Archivo | Contenido |
|---|---|
| [INSTALLATION.md](INSTALLATION.md) | Instalación, actualización y resolución de problemas |
| [DOCUMENTATION.md](DOCUMENTATION.md) | Manual de uso, personalización, exportación y comandos |
| [MANIFEST.md](MANIFEST.md) | Identidad del plugin y contenido de la distribución |
| [GITHUB_RELEASE.md](GITHUB_RELEASE.md) | Preparación de una publicación en GitHub |
| [chimerax/README.md](chimerax/README.md) | Compilación y desarrollo del plugin |
| [chimerax/VALIDATION.md](chimerax/VALIDATION.md) | Pruebas realizadas y alcance de la validación |

## Compatibilidad

CLIP! 1.0.0 es una integración experimental validada en **ChimeraX 1.12 para macOS**,
con PLIP 3.0.1 y Open Babel 3.2.1. Las instrucciones para Windows y Linux están
incluidas; su funcionamiento aún requiere validación en esas plataformas.

El plugin se instala mediante un archivo `.whl`. Para calcular nuevas interacciones
necesita un entorno Python externo con sus dependencias; el ZIP incluye el asistente
para prepararlo con Conda/Miniforge. No se necesita PyMOL.

Los resultados corresponden a una instantánea de las coordenadas analizadas.
Consulta las [limitaciones](DOCUMENTATION.md#alcance-y-limitaciones) antes de trabajar
con trayectorias, estructuras grandes o modos avanzados de análisis.

## Licencia y reconocimiento científico

CLIP! se distribuye bajo **GPL-2.0-only**; consulta [LICENSE.txt](LICENSE.txt).
Integra PLIP como motor de análisis y conserva su autoría y créditos en
[README_PLIP.md](README_PLIP.md). Para la cita científica, consulta la información de
citación del informe generado por el motor. CLIP! no es una publicación oficial
de UCSF ni de PharmAI.

© 2026 Structural Bioinformatics & Bioactive Compound Synthesis Lab - UFRO

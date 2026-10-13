# CLIP! 1.0.0 — Desarrollo del plugin

<img src="src/assets/clip.png" alt="CLIP!" width="140">

Bundle de UCSF ChimeraX 1.12 que integra análisis de interacciones, visualización
nativa, personalización de figuras y siete idiomas.

La documentación para usuarios está en la raíz del proyecto:

- [Presentación de CLIP!](../README.md)
- [Instalación y actualización](../INSTALLATION.md)
- [Manual de uso](../DOCUMENTATION.md)
- [Manifiesto de distribución](../MANIFEST.md)

## Organización del código

| Archivo o carpeta | Función |
|---|---|
| `bundle_info.xml` | Identidad, dependencias, herramientas y comandos registrados |
| `src/tool.py` | Panel de análisis y selector de idioma |
| `src/appearance_ui.py`, `src/appearance.py` | Controles de estilo, etiquetas y exportación |
| `src/commands.py`, `src/job.py`, `src/backend.py` | Comandos, análisis asíncrono y ejecución del motor |
| `src/report.py`, `src/visualize.py` | Lectura de XML/CSV y representación de interacciones |
| `src/settings.py` | Preferencias persistentes |
| `src/i18n.py`, `src/locales/` | Traducciones del panel |
| `src/assets/`, `src/docs/` | Logo y ayuda integrada |
| `setup_backend.py`, `environment.yml` | Preparación del entorno externo |
| `package_release.py` | ZIP, wheel distribuible y sumas SHA256 |
| `test/` | Pruebas unitarias e integración en ChimeraX |

El nombre visible es **CLIP!**, la distribución es `ChimeraX-CLIP` y la versión
es **1.0.0**. El módulo `chimerax.plip`, los comandos `plip` y el espacio de
preferencias `PLIP` conservan sus identificadores por compatibilidad.

## Compilar y empaquetar

En la línea de comandos de ChimeraX:

```text
devel build "/ruta/CLIP-1.0.0/chimerax"
```

En una terminal del sistema, desde la raíz del proyecto:

```sh
python3 chimerax/package_release.py
```

El script comprueba que las fuentes y recursos coinciden con el wheel, genera
`release/CLIP-1.0.0.zip`, copia el wheel a `release/` e `install/` y actualiza
las sumas SHA256. No incluye entornos, resultados ni preferencias locales.
Consulta [GITHUB_RELEASE.md](../GITHUB_RELEASE.md) para publicar la entrega.

El `pyproject.toml` de la raíz corresponde al motor externo requerido por el
asistente de instalación; el bundle de CLIP! se construye con `bundle_info.xml`.

## Validación

Desde la raíz del proyecto:

```sh
python3 -m unittest discover -s chimerax/test -v
```

Las pruebas de integración de `test/` se ejecutan con ChimeraX y algunas necesitan
interfaz gráfica o resultados previos. Por ejemplo, en macOS, después de instalar
el bundle:

```sh
/Applications/ChimeraX-1.12.app/Contents/bin/ChimeraX --exit \
  --script 'chimerax/test/languages_in_chimerax.py /ruta/CLIP-1.0.0'
```

Revisa el informe `chimerax/validation/languages-check.json`: ChimeraX puede
finalizar con código cero aunque un script haya informado de un error.
Consulta [VALIDATION.md](VALIDATION.md) para los entornos, resultados y límites
comprobados. Los artefactos de validación se excluyen del ZIP.

## Licencia

GPL-2.0-only. Se mantienen la licencia y autoría del motor de análisis integrado.

© 2026 Structural Bioinformatics & Bioactive Compound Synthesis Lab - UFRO

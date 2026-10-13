# CLIP! 1.0.0 — Manifiesto de distribución

Este documento identifica el plugin CLIP! y los archivos necesarios para instalarlo,
utilizarlo y reconstruir su distribución.

## Identidad del plugin

| Campo | Valor |
|---|---|
| Nombre visible | CLIP! |
| Versión | 1.0.0 |
| Distribución de ChimeraX | `ChimeraX-CLIP` |
| Plataforma objetivo | UCSF ChimeraX 1.12 |
| Menú | Tools → Structure Analysis → CLIP! |
| Licencia | GPL-2.0-only |
| Wheel | `chimerax_clip-1.0.0-py3-none-any.whl` |
| ZIP | `CLIP-1.0.0.zip` |
| Módulo interno | `chimerax.plip` |
| Comandos | `plip analyze`, `plip load`, `plip settings` |
| Logo | `chimerax/src/assets/clip.png` |
| Idiomas | `en`, `es`, `de`, `fr`, `zh`, `ja`, `pt` |

Los identificadores internos se conservan por compatibilidad. El nombre técnico de
los archivos utiliza `CLIP` sin el signo de exclamación.

## Archivos de publicación

| Archivo | Destino y contenido |
|---|---|
| `release/CLIP-1.0.0.zip` | Fuentes, documentación, ejemplos y wheel para GitHub |
| `release/chimerax_clip-1.0.0-py3-none-any.whl` | Instalador del plugin para ChimeraX |
| `release/SHA256SUMS.txt` | Sumas SHA256 del ZIP y del wheel |
| `MANIFEST-SHA256.txt`, dentro del ZIP | Hash SHA256 de cada archivo incluido, excepto del propio manifiesto |

El ZIP contiene una carpeta raíz `CLIP-1.0.0/`. No se instala directamente en
ChimeraX: se descomprime y se instala el wheel de `install/`.

## Contenido del ZIP

| Ruta | Papel en CLIP! |
|---|---|
| `README.md` | Presentación y acceso a las guías |
| `INSTALLATION.md` | Instalación, configuración, actualización y diagnóstico |
| `DOCUMENTATION.md` | Manual del plugin |
| `MANIFEST.md` | Este manifiesto |
| `GITHUB_RELEASE.md` | Preparación de la publicación |
| `LICENSE.txt` | Licencia de distribución |
| `install/` | Wheel de CLIP! 1.0.0 |
| `chimerax/bundle_info.xml` | Metadatos, dependencias y registro del plugin en ChimeraX |
| `chimerax/src/` | Interfaz, análisis, lectura de informes, visualización y exportación |
| `chimerax/src/assets/` | Logo del plugin |
| `chimerax/src/locales/` | Los siete catálogos de traducción |
| `chimerax/src/docs/` | Ayuda integrada en ChimeraX y enlaces de compatibilidad |
| `chimerax/setup_backend.py` | Asistente para preparar el entorno de análisis |
| `chimerax/environment.yml` | Dependencias del entorno externo |
| `chimerax/package_release.py` | Generador del ZIP y sus manifiestos SHA256 |
| `chimerax/test/` | Pruebas del plugin |
| `chimerax/README.md`, `chimerax/VALIDATION.md` | Desarrollo y validación |
| `plip/` | Motor de análisis incluido como dependencia, con estructuras e informes de ejemplo |
| `pyproject.toml`, `MANIFEST.in` | Empaquetado del motor incluido para el asistente de instalación |
| `README_PLIP.md`, `upstream/DOCUMENTATION_PLIP.md`, `CHANGES.txt` | Referencia, autoría e historial del motor original |
| `.gitignore` | Exclusiones para el desarrollo local |

La documentación principal corresponde a CLIP!. Los archivos de referencia del
motor se conservan para mantener su procedencia y permitir su instalación.

## Qué declara cada manifiesto

- **`chimerax/bundle_info.xml`:** manifiesto instalable de CLIP!; define versión,
  categoría, comandos, dependencias de ChimeraX, recursos y paquetes anteriores sustituidos.
- **`MANIFEST.in`:** reglas de la distribución fuente del motor que usa el asistente;
  no instala el plugin en ChimeraX ni determina el contenido del ZIP de CLIP!.
- **`chimerax/package_release.py`:** selecciona explícitamente los archivos del ZIP
  y comprueba que el wheel coincide con el código y recursos del plugin.
- **`MANIFEST-SHA256.txt`:** inventario de integridad generado al crear el ZIP.

## Dependencias de ejecución

El wheel requiere los bundles Core, Atomic, PDB, Markers y UI declarados en
`bundle_info.xml`. El código Python puro del wheel no incorpora las bibliotecas
nativas del motor de análisis.

Para calcular nuevas interacciones, el asistente prepara un entorno externo con
Python 3.11, Open Babel, NumPy, lxml y PLIP. El análisis se ejecuta localmente.
Para cargar un XML existente, basta el plugin y la estructura correspondiente.
Consulta [INSTALLATION.md](INSTALLATION.md) para configurar cada modalidad.

## Contenido excluido

La distribución no incluye entornos Conda, preferencias personales, resultados de
análisis, sesiones de trabajo, capturas de validación, cachés, directorios de
compilación ni credenciales. Los ejemplos del motor incluidos en las fuentes son
archivos de prueba, no resultados privados del usuario.

## Regeneración y comprobación

En la línea de comandos de ChimeraX:

```text
devel build "/ruta/CLIP-1.0.0/chimerax"
```

En una terminal del sistema, desde la carpeta del proyecto:

```sh
python3 chimerax/package_release.py
```

El script genera el ZIP, copia el wheel a `release/` e `install/` y actualiza las
sumas. Si las fuentes del plugin cambiaron después de compilar el wheel, detiene
el empaquetado para evitar distribuir versiones distintas.

© 2026 Structural Bioinformatics & Bioactive Compound Synthesis Lab - UFRO

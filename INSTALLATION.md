# CLIP! 1.0.0 — Instalación en ChimeraX

Esta guía instala el plugin CLIP!, configura su entorno de análisis y comprueba
que está listo para utilizarse. El archivo ZIP se descomprime; el archivo `.whl`
se instala desde **ChimeraX**.

## Requisitos

| Componente | Cuándo se necesita |
|---|---|
| UCSF ChimeraX 1.12 | Siempre |
| Wheel de CLIP! 1.0.0 | Siempre |
| ZIP completo de CLIP! | Para preparar el entorno con el asistente incluido |
| Conda o Miniforge y acceso a Internet | Para descargar las dependencias del entorno de análisis |
| Complejo proteína–ligando | Para realizar un análisis |
| Informe XML y estructura correspondiente | Para visualizar un resultado ya calculado |

Validado en **ChimeraX 1.12 para macOS**. Se incluyen instrucciones para Windows y
Linux, cuyo funcionamiento aún requiere validación en esas plataformas.

CLIP! no necesita PyMOL. Si solo vas a cargar informes existentes, completa los
pasos 1 y 2 y sigue la sección **Visualizar un informe existente**.

## 1. Descargar y descomprimir CLIP!

Descarga `CLIP-1.0.0.zip` de la publicación que distribuya el proyecto. Descomprímelo
en una ubicación estable, por ejemplo `Documentos/CLIP-1.0.0`.

```text
CLIP-1.0.0/
  README.md
  DOCUMENTATION.md
  INSTALLATION.md
  MANIFEST.md
  MANIFEST-SHA256.txt
  install/chimerax_clip-1.0.0-py3-none-any.whl
  chimerax/setup_backend.py
  chimerax/environment.yml
  chimerax/src/
  plip/
```

Si tienes una versión anterior llamada PLIP, PLIP-Explorer o PLIP-Xplorer,
consulta **Actualizar una instalación anterior** antes de continuar.

## 2. Instalar el plugin desde ChimeraX

Abre ChimeraX 1.12. Activa su línea de comandos con
**Tools → General → Command Line** si no está visible.

En la línea de comandos de ChimeraX, ejecuta:

```text
toolshed install "/ruta/CLIP-1.0.0/install/chimerax_clip-1.0.0-py3-none-any.whl"
```

En Windows puedes utilizar barras `/`:

```text
toolshed install "C:/ruta/CLIP-1.0.0/install/chimerax_clip-1.0.0-py3-none-any.whl"
```

Sustituye la ruta de ejemplo por la ubicación real del archivo. Conserva las comillas.
El registro **Log** debe confirmar la instalación de **ChimeraX-CLIP 1.0.0**.
Reinicia ChimeraX si lo solicita.

CLIP! se distribuye como wheel local. Esta entrega no está publicada en el Toolshed
público: debes indicar la ruta al archivo.

## 3. Preparar el entorno de análisis una vez

Para calcular nuevas interacciones, CLIP! utiliza un Python externo con el motor
PLIP y Open Babel. Si ya tienes un entorno compatible que funciona, reutilízalo
en el paso 4 y omite la creación de otro.

Instala [Miniforge](https://github.com/conda-forge/miniforge) si todavía no tienes
Conda. Los siguientes comandos se ejecutan en la **terminal del sistema**, fuera de
ChimeraX, desde la carpeta descomprimida.

macOS y Linux:

```sh
cd "/ruta/CLIP-1.0.0"
python3 chimerax/setup_backend.py
```

Windows, en Miniforge Prompt:

```text
cd /d "C:\ruta\CLIP-1.0.0"
python chimerax/setup_backend.py
```

El asistente descarga las dependencias, crea `.plip-env`, instala el motor incluido
y genera `.plip-env/configure-chimerax.cxc`. Espera a que termine sin errores.
Los análisis posteriores se ejecutan localmente.

Si no encuentra Conda, indica su ejecutable:

```sh
python3 chimerax/setup_backend.py --conda "/ruta/a/conda"
```

En Windows, sustituye `python3` por `python` cuando corresponda.
El asistente rechaza un directorio de entorno que ya exista. Para crear otro,
utiliza una ubicación nueva:

```sh
python3 chimerax/setup_backend.py --prefix "/ruta/nuevo-entorno-clip"
```

En ese caso, el archivo `configure-chimerax.cxc` quedará dentro del nuevo entorno.
Conserva el entorno en su ubicación: no muevas la carpeta después de instalarlo.

## 4. Conectar CLIP! con el entorno

Vuelve a la línea de comandos de **ChimeraX** y abre el archivo generado:

```text
open "/ruta/CLIP-1.0.0/.plip-env/configure-chimerax.cxc"
```

También puedes introducir directamente la ruta al Python del entorno.

macOS y Linux:

```text
plip settings python "/ruta/CLIP-1.0.0/.plip-env/bin/python"
```

Windows:

```text
plip settings python "C:/ruta/CLIP-1.0.0/.plip-env/python.exe"
```

CLIP! conserva el prefijo de comandos `plip` por compatibilidad. Para consultar
el ejecutable configurado, utiliza `plip settings`.

Como alternativa, abre el panel y usa **Examinar… / Browse…** junto a
**Python de PLIP / PLIP Python**. Selecciona el Python del entorno preparado,
no el Python interno de ChimeraX.

## 5. Abrir CLIP! y realizar una prueba

1. Abre **Tools → Structure Analysis → CLIP!**, o ejecuta:

   ```text
   ui tool show "CLIP!"
   ```

2. En **Language**, selecciona **Español** o el idioma que prefieras.
3. En **File → Open**, abre `plip/test/pdb/1vsn.pdb` de la carpeta descomprimida.
4. En **Análisis**, selecciona esa estructura, comprueba el Python y elige una
   carpeta de resultados.
5. Pulsa **Analizar estructura**. Al finalizar, el panel debe mostrar un sitio
   con interacciones y sus representaciones en la escena.
6. Usa **Apariencia** para modificar el estilo y **Exportar imagen** para guardar una figura.

La estructura debe contener receptor y ligando. El número de contactos puede variar
según la preparación de hidrógenos y las versiones de las dependencias.
El [manual de CLIP!](DOCUMENTATION.md) explica los filtros, etiquetas 3D, estilos y exportación.

## Visualizar un informe existente

Después de instalar el wheel:

1. Abre en ChimeraX la estructura utilizada para generar el informe, con las mismas coordenadas.
2. Abre CLIP! y selecciónala en **Estructura**.
3. Pulsa **Cargar XML de PLIP…** y selecciona `report.xml`.

Esta modalidad no ejecuta el motor y no requiere preparar el entorno externo.

## Actualizar una instalación anterior

Los entornos de análisis y las preferencias existentes pueden reutilizarse.
Si ya tienes **ChimeraX-CLIP**, instala el wheel de la nueva versión y reinicia
ChimeraX. Para reinstalar esta misma versión, utiliza:

```text
toolshed install "/ruta/chimerax_clip-1.0.0-py3-none-any.whl" reinstall true
```

Si la instalación anterior tiene otro nombre:

1. Guarda la sesión que necesites y reinicia ChimeraX sin abrir el panel antiguo.
2. Ejecuta `toolshed list installed` y comprueba el nombre exacto del paquete.
3. Desinstala únicamente el paquete anterior que aparezca instalado, usando la tabla.
4. Reinicia si se solicita e instala CLIP! con el paso 2.
5. Abre CLIP! y comprueba el Python configurado y el estilo guardado.

| Paquete anterior instalado | Comando en ChimeraX, antes de instalar CLIP! |
|---|---|
| `ChimeraX-PLIP` | `toolshed uninstall ChimeraX-PLIP` |
| `ChimeraX-PLIP-Explorer` | `toolshed uninstall ChimeraX-PLIP-Explorer` |
| `ChimeraX-PLIP-Xplorer` | `toolshed uninstall ChimeraX-PLIP-Xplorer` |

Retira el paquete antiguo **antes** de instalar CLIP!: comparten el módulo interno.
No ejecutes una desinstalación con el nombre anterior después de instalar CLIP!,
porque ChimeraX puede resolverlo como alias del nuevo plugin.

## Resolver problemas

| Síntoma | Acción |
|---|---|
| CLIP! no aparece en el menú | Revisa Log, reinicia y verifica `ChimeraX-CLIP` con `toolshed list installed` |
| `No module named plip` u `openbabel` | Consulta `plip settings` y selecciona el Python del entorno de análisis |
| Conda no se encuentra | Ejecuta el asistente con `--conda` y la ruta real de su ejecutable |
| `.plip-env` ya existe | Reutilízalo si funciona o crea un entorno nuevo con `--prefix` |
| Cambió la ubicación del entorno | Recrea el entorno en una ruta estable y vuelve a configurar su Python |
| Se rechaza el XML | Selecciona la estructura correspondiente al informe, con las mismas coordenadas |
| No se detecta ningún ligando | Comprueba el complejo de entrada y los mensajes del registro de análisis |
| El análisis falla o supera diez minutos | Revisa `engine.log` en la subcarpeta de resultados y la preparación de la estructura |
| La imagen es demasiado grande | Reduce dimensiones o supermuestreo en Exportar imagen |

## Desinstalar CLIP!

En ChimeraX, con el panel cerrado:

```text
toolshed uninstall ChimeraX-CLIP
```

La desinstalación retira el plugin. Los informes, imágenes y el entorno externo
permanecen en disco.

© 2026 Structural Bioinformatics & Bioactive Compound Synthesis Lab - UFRO

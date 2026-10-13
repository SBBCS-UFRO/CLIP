# CLIP! 1.0.0 — Manual de uso

CLIP! es un plugin de UCSF ChimeraX para analizar interacciones proteína–ligando,
explorar los contactos detectados y preparar figuras personalizadas.
Esta guía describe las funciones disponibles en CLIP! 1.0.0.

Para instalarlo o actualizarlo, consulta [INSTALLATION.md](INSTALLATION.md).
Los nombres de los controles se presentan en español; el panel permite seleccionar
otros seis idiomas.

## Abrir el plugin

En ChimeraX, selecciona **Tools → Structure Analysis → CLIP!**, o ejecuta en su
línea de comandos:

```text
ui tool show "CLIP!"
```

El panel tiene un selector de idioma y tres pestañas: **Análisis**, **Apariencia**
y **Exportar imagen**. La cabecera muestra el nombre, versión y logo de CLIP!.

## Analizar una estructura

1. Abre en ChimeraX el complejo que contiene el receptor y su ligando.
2. En **Análisis**, selecciona el modelo en **Estructura**.
3. Comprueba que **Python de PLIP** apunta al entorno configurado durante la instalación.
4. Selecciona la **Carpeta de resultados**.
5. Pulsa **Analizar estructura**. El panel permanece disponible mientras se realiza
   el cálculo; **Cancelar** permite detenerlo.
6. Al finalizar, selecciona un sitio de unión en la lista de ligandos.

CLIP! analiza una copia de las coordenadas activas del modelo. Cuando el cálculo
termina correctamente, muestra esa copia con las interacciones y oculta la estructura
original. Puedes volver a mostrar la original desde el panel **Models** de ChimeraX.
Los modelos de interacción siguen los movimientos rígidos de la copia analizada.

**Conservar hidrógenos existentes** utiliza los hidrógenos que ya tiene la estructura.
Activa esta opción solo si la preparación de hidrógenos ya está completa. Para comparar
análisis reproducibles, utiliza la misma estructura preparada, versiones del motor
y opciones; la protonación puede cambiar los contactos detectados.

## Explorar las interacciones

La lista de sitios permite elegir un ligando. Las casillas de las ocho categorías
controlan las interacciones visibles y las filas mostradas en la tabla.

| Categoría | Representación |
|---|---|
| Contactos hidrofóbicos | Segmentos entre los átomos indicados en el informe |
| Puentes de hidrógeno | Segmentos donante–aceptor; distancia D–A |
| Puentes de agua | Dos segmentos que conectan ligando, agua y receptor |
| Puentes salinos | Segmentos entre los centros de los grupos cargados |
| Apilamiento π | Segmentos entre los centros de los anillos |
| Interacciones π–catión | Segmentos entre anillo y grupo cargado |
| Enlaces de halógeno | Segmentos entre los extremos reportados |
| Coordinación metálica | Segmentos entre el metal y su átomo coordinante |

Haz clic en una fila para seleccionar el residuo receptor. Pasa el cursor sobre
la fila para consultar las medidas y campos del informe. **Centrar sitio de unión**
ajusta la vista al sitio elegido y conserva el estilo visual configurado.

Las distancias se expresan en ångströms (Å). En la tabla, los puentes de agua muestran
**aceptor–agua / donante–agua**. Cada puente de agua cuenta como una interacción,
aunque se dibuje mediante dos segmentos. Las etiquetas de anillos y grupos muestran
las distancias entre sus centros cuando así las reporta el motor.

Los filtros cambian la visualización. **Exportar CSV** incluye todas las interacciones
y todos los sitios del informe, incluso los que estén ocultos.

## Cargar un informe existente

1. Abre la estructura correspondiente al informe, con las mismas coordenadas utilizadas
   para calcularlo.
2. Selecciónala en **Estructura**.
3. Pulsa **Cargar XML de PLIP…** y elige `report.xml`.
4. Explora los sitios e interacciones con los mismos controles del panel.

Esta operación no requiere el entorno de análisis. CLIP! comprueba los extremos
atómicos disponibles en el informe y puede rechazar coordenadas incompatibles.
En interacciones descritas únicamente por centros de grupos, esta comprobación
no garantiza la correspondencia del modelo: debes seleccionar la estructura correcta.

## Personalizar la apariencia

Los controles de **Apariencia** actualizan la vista automáticamente. Fondo, iluminación
y cámara afectan a la escena completa de ChimeraX.

### Preajustes

| Preajuste | Uso visual |
|---|---|
| Original | Apariencia inicial de CLIP! |
| Publicación | Fondo blanco, luz suave, etiquetas de residuos y distancias |
| Presentación oscura | Fondo oscuro, iluminación completa y material brillante |
| Ilustración | Luz plana, contornos y etiquetas de residuos |

Selecciona uno y pulsa **Aplicar preajuste**. Puedes modificar sus parámetros después.
**Guardar como predeterminado** recuerda el estilo para nuevos paneles.
**Guardar estilo…** y **Cargar estilo…** permiten compartirlo mediante un archivo JSON.

### Escena y molécula

- **Escena:** color de fondo, iluminación simple/suave/completa/tenue/plana,
  material, cámara perspectiva u ortográfica, contornos y niebla de profundidad.
- **Molécula:** cinta de la proteína y su transparencia, colores del receptor y
  ligando, conservación de colores por elemento, varillas/bolas y varillas/esferas,
  radio de enlaces, hidrógenos disponibles, aguas de los puentes y puntos de interacción.
- **Colores y líneas de interacción:** color, radio y número de trazos por categoría.
  Un valor de cero trazos produce una línea continua.

### Etiquetas de residuos y distancias 3D

Activa las etiquetas de residuos, ligando o distancias según la figura que necesites.
Puedes elegir el formato del residuo, fuente, altura, color, fondo y visualización
al frente. Los desplazamientos X/Y/Z se configuran por separado para residuos y distancias.
El contraste automático adapta el texto al fondo de la escena.

Para mover una etiqueta individualmente:

1. Termina de elegir los estilos y filtros.
2. Activa **Mover etiquetas individualmente arrastrando con el botón derecho**.
3. Arrastra las etiquetas hasta evitar superposiciones.
4. Exporta la imagen o guarda la sesión `.cxs`.

Cambiar estilos o filtros reconstruye las etiquetas; realiza la colocación manual
al final. Desactivar esta opción o cerrar CLIP! restaura la función anterior del
botón derecho. Cambiar el idioma conserva la colocación manual.

Las distancias de las etiquetas proceden del informe de análisis. Los ajustes de
apariencia no modifican los criterios de detección, coordenadas ni resultados.

## Exportar imágenes

Orienta y amplía la estructura con los controles de ChimeraX. Después, en
**Exportar imagen**, configura:

| Control | Función |
|---|---|
| Formato | PNG, TIFF o JPEG |
| Ancho y alto | Dimensiones de salida en píxeles, entre 64 y 8192 en los controles |
| Conservar proporción de la vista actual | Calcula el alto a partir del ancho y la vista |
| Suavizado | Supermuestreo entre 1 y 4 |
| Calidad JPEG | Calidad de compresión entre 1 y 100 |
| Fondo transparente | Disponible para PNG y TIFF |
| Solo la estructura actual y sus representaciones | Aísla temporalmente el resultado para exportarlo |

Pulsa **Exportar imagen…** y selecciona el archivo de destino. La visibilidad de
los demás modelos se restaura después de exportar, incluso si la exportación falla.
Desactiva el aislamiento si quieres incluir otros modelos visibles en la figura.

La exportación utiliza la vista actual. Cambiar la proporción puede modificar el
encuadre. La combinación de dimensiones y supermuestreo tiene un límite de
100 millones de píxeles internos, además de los límites del equipo.

Para usar una imagen transparente sobre otro fondo, elige un color de etiquetas
que contraste con el fondo de destino. La resolución se configura en píxeles;
el panel no ofrece un ajuste de DPI.

## Guardar resultados y continuar una sesión

Cada análisis crea una subcarpeta independiente dentro de la carpeta de resultados.

| Archivo | Contenido |
|---|---|
| `input.pdb` | Instantánea enviada al motor |
| `report.xml` | Resultado que CLIP! puede volver a cargar |
| `report.txt` | Informe de texto del motor |
| `engine.log` | Registro de ejecución y diagnósticos |
| `provenance.json` | Comando, versión y hashes de entrada/salida |

El motor también puede generar una estructura protonada. Los resultados quedan
en disco al cerrar ChimeraX.

| Archivo que guardas desde el panel | Qué conserva |
|---|---|
| CSV | Todas las interacciones del informe |
| JSON de estilo | Parámetros visuales globales; no guarda posiciones manuales individuales |
| Sesión `.cxs` | Estructuras, dibujos y etiquetas, incluida su colocación manual |
| PNG/TIFF/JPEG | Figura renderizada desde la vista actual |

**Guardar sesión de ChimeraX…** guarda la escena. La tabla y el estado del panel
no se restauran desde `.cxs`: vuelve a abrir CLIP! y carga `report.xml` sobre la copia
analizada para reconstruirlos. Cargar el XML crea otro grupo de dibujos; cierra el
anterior si ya no lo necesitas.

## Cambiar de idioma

El selector de la cabecera ofrece inglés, español, alemán, francés, chino simplificado,
japonés y portugués de Brasil. La preferencia se recuerda entre aperturas.

Se traducen controles, opciones, categorías y mensajes propios del panel.
Los identificadores de residuos, comandos, claves de archivos y diagnósticos externos
mantienen su forma original. El selector no cambia el idioma de ChimeraX ni del
sistema operativo. Este manual está en español y la ayuda integrada está en inglés.

## Comandos de CLIP! en ChimeraX

Los comandos del plugin conservan el prefijo `plip`. Se ejecutan en la línea de
comandos de **ChimeraX**, no en la terminal del sistema. Sustituye `#1` por el
identificador del modelo que deseas analizar.

```text
ui tool show "CLIP!"
plip settings
plip settings python "/ruta/al/entorno/bin/python"
plip analyze #1 output "/ruta/resultados"
plip analyze #1 output "/ruta/resultados" wait true
plip analyze #1 output "/ruta/resultados" noHydro true wait true
plip load "/ruta/report.xml" structure #1
```

| Opción | Efecto |
|---|---|
| `python` | Selecciona el ejecutable del entorno de análisis |
| `output` | Carpeta base donde se crea una subcarpeta para el cálculo |
| `noHydro true` | Conserva los hidrógenos existentes |
| `wait true` | Espera a que termine el cálculo; sin interfaz gráfica se espera siempre |

El comando de análisis admite también `python` para esa ejecución. Si omites
`output`, se utiliza un directorio temporal; indica una carpeta permanente para
conservar el trabajo. Los resultados creados mediante comandos se muestran en la
escena; para explorarlos en la tabla del panel, carga su XML sobre la copia analizada.

## Alcance y limitaciones

- Una estructura y su conjunto de coordenadas activo por ejecución.
- Modo estándar de análisis de moléculas pequeñas y sitios metálicos.
- Exportación PDB: hasta 99.999 átomos, identificadores de cadena de un carácter
  y números de residuo entre −999 y 9999. Un mmCIF debe poder exportarse dentro de esos límites.
- Las figuras son estáticas. Cambiar conformación, coordenadas o fotograma requiere
  un nuevo análisis; no se siguen trayectorias automáticamente.
- El panel no expone modos péptido, intracadena, regiones ni todos los umbrales del motor.
- La ejecución tiene un límite de diez minutos; los diagnósticos se conservan en el registro.
- Para calcular se necesita el entorno externo. El wheel no incluye Open Babel.
- Validación realizada en ChimeraX 1.12/macOS. Windows y Linux siguen pendientes.

Consulta [VALIDATION.md](chimerax/VALIDATION.md) para el detalle de las comprobaciones.
Para problemas de configuración, utiliza la sección de diagnóstico de
[INSTALLATION.md](INSTALLATION.md#resolver-problemas).

## Licencia y créditos

CLIP! se distribuye bajo [GPL-2.0-only](LICENSE.txt). El motor PLIP conserva
su autoría y créditos científicos; consulta [README_PLIP.md](README_PLIP.md)
y la información de citación del informe de análisis.

© 2026 Structural Bioinformatics & Bioactive Compound Synthesis Lab - UFRO

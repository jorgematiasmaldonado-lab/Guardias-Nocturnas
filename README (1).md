# Guardias Nocturnas · Guardia A · ETAC

App web para organizar las guardias nocturnas de la Guardia A de ETAC (Base Punilla) con un reparto **equitativo y transparente**.

**Autor:** Maldonado Jorge Matias. Sistema desarrollado por **JMM Gestiones y Tecnologías**.

## Archivos

| Archivo | Para qué sirve |
|---|---|
| `index.html` | Toda la app (HTML + Tailwind por CDN + JavaScript puro) |
| `manifest.json` | Permite instalarla como app en el celular o la notebook |
| `sw.js` | Hace que funcione sin conexión |
| `icon-192.png`, `icon-512.png`, `icon-maskable-512.png` | Íconos de la app |
| `logo-etac.png`, `logo-jmm.png` | Logos de ETAC y de JMM (pantalla y PDF) |

## Publicar en GitHub Pages

1. En GitHub Desktop: **File → New repository** (por ejemplo `NOCTURNAS-GUARDIA-A`).
2. Copiá todos estos archivos a la carpeta del repositorio, hacé **Commit** y **Publish repository** (público).
3. En github.com, entrá al repo y andá a **Settings → Pages → Branch: main / (root) → Save**.
4. A los minutos queda en `https://jorgematiasmaldonado-lab.github.io/NOCTURNAS-GUARDIA-A/`.

La primera vez hay que abrirla con internet. Después funciona sin conexión.

> ⚠️ Los datos se guardan **en el dispositivo** donde se usa (en el navegador). Conviene que la cargue siempre la misma persona, desde el mismo equipo. Para pasar los datos a otro equipo: **Descargar respaldo** en uno y **Restaurar respaldo** en el otro.

## Cómo se reparte

Para cada noche de guardia y cada franja (22–00, 00–03:30, 03:30–07):

1. Solo entran las personas **disponibles**: activas, que hacen nocturna y sin licencia ni ausencia ese día.
2. Se elige a quien tiene la **tasa más baja**: turnos realizados ÷ guardias en que estuvo disponible. Así, quien vuelve de una licencia **no arrastra deuda**. En Configuración se puede cambiar a la regla “recupera turnos”.
3. Se **rotan las franjas**, para que la de 00:00–03:30 no le toque siempre al mismo.
4. Se evita, si se puede, que alguien haga nocturna en **dos guardias seguidas**.
5. Al final se prueban intercambios mientras se achique la diferencia entre la persona más cargada y la menos cargada.
6. Los empates se resuelven por sorteo con una semilla fija: el mismo dato da siempre el mismo resultado.

Al regenerar un mes se respetan las noches que ya pasaron, los casilleros con 🔒 candado y los ⇄ cambios entre compañeros. Los turnos cuentan para la equidad cuando el mes está **publicado** y la fecha **ya pasó**.

## Importar licencias (CSV)

Andá a **Licencias → Importar CSV de licencias**. El archivo tiene que tener este formato (separado por `;`):

```
APELLIDO Y NOMBRE;GUARDIA;DÍAS DISPONIBLES;DÍAS USADOS;DÍAS RESTANTES;1ª FRANJA (INICIO - FIN);…;6ª FRANJA (INICIO - FIN)
AGUIRRE JUAN PABLO;A;20;20;0;05/02/2027 - 11/02/2027;07/05/2027 - 01/06/2027;;;;
```

- Las licencias anuales de cada persona encontrada **se reemplazan** por las del archivo.
- Los nombres que no están en Personal se informan y no se cargan.
- Si una licencia choca con turnos ya armados, **esos turnos se reasignan solos**.

## Licencia médica con un tilde

En **Personal**, activá el interruptor **“De licencia médica”** y poné la fecha de inicio. Pasa esto:

- Todos sus turnos desde esa fecha se **reasignan solos** con el mismo criterio de equidad.
- Se muestra el detalle de los cambios, con botones para reimprimir el PDF y copiar el cronograma para WhatsApp.
- Queda registrado en el Historial.
- No se guarda ningún diagnóstico: solo “Licencia médica” y las fechas.

Cuando vuelve, desactivá el interruptor y poné la **fecha de regreso**. Hay dos opciones:

- **Reincorporarlo en las noches que faltan del mes**: se reequilibran las noches futuras que no tienen candado.
- **Esperar al próximo mes**: no se toca lo que ya está armado.

## Copia de respaldo

- **Configuración → Descargar respaldo** baja el archivo `nocturnas-guardiaA-AAAA-MM-DD.json` con todo: personal, licencias, meses, historial y configuración. Guardalo en Drive o en la PC.
- **Restaurar respaldo** muestra un resumen y pide confirmación antes de reemplazar los datos.
- La app avisa cuando pasaron más de 7 días sin descargar un respaldo.

## PDF e informes

Todo documento se abre primero en **vista previa**. Recién si está bien, se toca **Descargar PDF** (en la ventana de impresión: “Guardar como PDF”). Lo mismo con el mensaje de WhatsApp y el respaldo: primero se ve, después se descarga o copia.


- **Cronograma → PDF del mes**: la planilla con el mismo formato de siempre, más una hoja de resumen con turnos por persona y ausentes del mes. En el diálogo de impresión, elegí “Guardar como PDF”.
- **Informes → Informe individual**: todos los turnos de la persona, cuándo no estuvo disponible y por qué, la comparación con el promedio, mínimo y máximo de la guardia, las modificaciones que lo afectaron y espacio para firmas. Sirve para responder reclamos.

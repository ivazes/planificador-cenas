# Planificador de cenas — Versión 1

Aplicación web de un solo archivo (`index.html`). Funciona sin conexión, sin cuentas, sin servidor y sin librerías externas.
Los datos se guardan solo en el navegador del dispositivo (localStorage).

> Herramienta de organización. No ofrece recomendaciones médicas ni nutricionales. La revisión final de ingredientes y alérgenos es siempre tuya.

## Archivos

| Archivo | Para qué sirve |
|---|---|
| `index.html` | La aplicación completa (HTML + CSS + JavaScript). |
| `pruebas/pruebas.html` | Pruebas automáticas con datos ficticios (no hace falta para usar la app). |

---

## 1. Cómo abrir la aplicación en el móvil (Chrome para Android)

**Opción recomendada: publicarla en GitHub Pages**
1. Sube la carpeta a un repositorio público de GitHub.
2. En el repositorio, ve a *Settings → Pages* y activa la rama `main`.
3. GitHub te da una dirección (por ejemplo, `https://usuario.github.io/planificador-cenas/`). Ábrela en Chrome en el móvil.
4. En Chrome, pulsa ⋮ → **Añadir a pantalla de inicio** para tener un acceso directo.

En GitHub solo se publica el HTML, que no contiene datos personales. Tus recetas y menús **se quedan en el móvil**.

**Alternativa: abrir el archivo directamente**
Copia `index.html` al móvil y ábrelo con Chrome. Funciona, pero Chrome para Android trata los archivos locales de forma especial: localStorage puede no guardarse de forma fiable y es más incómodo de abrir. Si usas esta opción, haz copias de seguridad a menudo.

> Cada navegador y cada dirección tienen su propio almacenamiento. Si abres la app desde dos sitios distintos (GitHub Pages y el archivo local), verás datos distintos.

## 2. Copias de seguridad

Los datos **no se sincronizan** entre dispositivos. Si borras los datos de Chrome, lo reinstalas o cambias de móvil, los pierdes, salvo que tengas una copia.

- **Exportar:** *Ajustes → Exportar copia (JSON)*. Se descarga `planificador-cenas-AAAA-MM-DD.json`. Guárdalo fuera del móvil (correo, nube, ordenador).
- **Importar:** *Ajustes → Importar copia* y elige el archivo.
  - La app comprueba el archivo antes de usarlo. Si algo está mal, te dice qué falla y no cambia nada.
  - Antes de sustituir tus datos actuales te pide confirmación y te muestra cuántos elementos hay en cada lado.
- **Recomendación:** exporta una copia cada vez que añadas recetas o cambies las reglas.
- La copia incluye ingredientes, recetas, reglas, menús, palabras clave, categorías y tus términos de alérgenos. Los términos de serie y las exclusiones fijas están en el código, así que no se pueden alterar con una copia.

## 3. Cómo añadir ingredientes y recetas

**Primero los ingredientes** (sección *Ingredientes → + Nuevo*). Cada ficha se puede usar en todas las recetas que quieras. Rellena:
- **Nombre**, **categoría** y, si quieres que funcionen las reglas de "variar el tipo", un **tipo** (arroz, pasta, patata, pollo…).
- **Hidratos:** gramos de HC *por cada* X gramos (normalmente 100), y si ese dato es para el alimento **crudo**, **cocido** o **no aplica**.
- **Fuente** del dato y la casilla **"He comprobado este dato"**. Sin fuente o sin comprobar, el cálculo queda *pendiente de confirmar*.
- **Composición y alérgenos:**
  - Si es un producto procesado, márcalo y copia la lista de ingredientes de la etiqueta.
  - Indica para cada exclusión si *contiene*, *puede contener trazas* o *no contiene*. Mientras alguna esté "Sin indicar", el ingrediente queda pendiente de revisión.
  - Al escribir, la ficha muestra en directo la **comprobación automática**.
- Si el mismo alimento se pesa a veces crudo y a veces cocido, crea **dos fichas** (por ejemplo, "Arroz" y "Arroz cocido"). La app nunca convierte de uno a otro.

**Después la receta** (sección *Recetas → + Nueva receta*):
1. Añade cada ingrediente con sus **gramos** y si están pesados **crudos o cocidos**.
2. Abajo verás la tabla de hidratos, el total, su estado y la comprobación de alérgenos.

Para trabajar con las recetas:
- **Duplicar** sirve para crear variantes.
- No se puede eliminar un ingrediente que usa alguna receta.
- Los datos de ejemplo (marcados *EJEMPLO FICTICIO*) se borran en *Ajustes → Eliminar datos de ejemplo*.

## 4. Menú del colegio

En *Menú cole*, escribe o pega el menú de cada día:
1. Pulsa **Sugerir componentes**. Las sugerencias aparecen **sin confirmar**.
2. Revisa cada componente: corrige la categoría o el tipo, y marca **Confirmado**. El planificador solo usa los confirmados.
3. Con **+ Componente** añades uno a mano.

Si el menú menciona algo de la lista de exclusiones (por ejemplo, pescado), el resumen semanal muestra un aviso. Las palabras que sirven para sugerir se pueden editar al final de esa sección.

## 5. Cómo modificar las reglas

Sección *Reglas*. Cada regla se lee como una frase:

> **Si la comida** [incluye / NO incluye] [categoría] (tipo opcional) **→ la cena debe** [incluir / evitar / no repetir el tipo de] [categoría].

- **Prioridad:** 1 es la más importante. La app elige la receta que cumple las reglas de prioridad más alta. Si hay empate, mira las de la siguiente prioridad, y así hasta el final.
- **Activa:** solo se aplican las reglas activas. Las reglas de ejemplo vienen **desactivadas**: revísalas y actívalas si te sirven.
- Si dos reglas se contradicen (incluir frente a evitar lo mismo):
  - Con distinta prioridad, gana la más importante y la explicación lo dice.
  - Con la misma prioridad, el día queda *pendiente* hasta que cambies una de ellas.
- **Desempates fijos**, en este orden: la receta sin revisión de alérgenos pendiente, luego la que tiene el cálculo de hidratos más documentado y, por último, el orden alfabético.
- Las **exclusiones de alérgenos se aplican siempre antes** que cualquier regla. Una receta bloqueada nunca se propone y no se puede elegir a mano.
- En el resumen semanal puedes **cambiar la cena** de un día. La app la evalúa igual y te dice qué reglas cumple.

**Estados de cada día:**
- ✓ Compatible con tus reglas.
- ! Pendiente de revisar. Indica el motivo: falta el menú, hay componentes sin confirmar, no se aplica ninguna regla, no se cumplen todas, el cálculo está incompleto o hay alérgenos por revisar.
- – Sin propuesta disponible.
- ✕ Bloqueada por una exclusión.

## 6. Revisión de alérgenos

En la sección *Alérgenos*:
- Ves las cenas de la semana con sus ingredientes, composición, trazas y avisos.
- Confirmas la **primera revisión** y después la **segunda**.
- Si después cambia alguna cena, receta, ingrediente o término, la confirmación **caduca** y tienes que repetirla.
- Puedes **añadir términos** (y elegir si bloquean o piden revisión). Los de serie (🔒) no se pueden quitar.

Cómo busca la app los términos:
- No tiene en cuenta tildes ni mayúsculas, y admite plurales.
- Busca en el nombre, la composición, las trazas y las notas de cada ingrediente.
- Si un término aparece tras "sin" o "no contiene" (por ejemplo, "pasta sin huevo"), **no se da por bueno**: queda *a revisar*. Puedes resolverlo con la casilla "He revisado las coincidencias", pero esa casilla nunca anula un bloqueo ni un alérgeno "Sin indicar".

## 7. Cómo ampliar el proyecto en el futuro

El código de `index.html` está dividido en dos bloques:
- `<script id="nucleo">`: la lógica, sin interfaz. Módulos `Util`, `Constantes`, `Datos`, `Ingredientes`, `Recetas`, `MenuEscolar`, `Alergenos`, `Hidratos`, `Reglas`, `Planificador`, `Revision`, `Almacen` y `CopiaSeguridad`.
- `<script id="interfaz">`: las pantallas y los eventos.

Dónde tocar según lo que quieras hacer:
- **Nuevos términos de serie:** `Constantes.TERMINOS_BASE`.
- **Nuevos tipos de regla:** `Reglas.evaluarAccion`, `Reglas.describir` y el formulario `formularioRegla`.
- **Cambios en la estructura de datos:** sube `VERSION_DATOS` y completa `Datos.normalizarDatos`, que rellena los campos nuevos en datos antiguos.
- **PWA (app instalable):** añadir un `manifest.json` y un *service worker*. Hay comentarios marcados "PWA" que indican dónde.
- **Después de cada cambio,** ejecuta las pruebas (abajo).

## 8. Pruebas realizadas

Las pruebas están en `pruebas/pruebas.html` y usan solo datos ficticios. Para ejecutarlas, desde una terminal en esta carpeta:

```bash
python3 -m http.server 8000
```

Después abre `http://localhost:8000/pruebas/pruebas.html` en el navegador.

**Resultado (22/11/2026, Firefox de escritorio): 141 de 141 superadas.**

| Requisito | Qué se comprobó |
|---|---|
| Ingredientes: crear, editar y eliminar | Crear, editar sin duplicar, nombre obligatorio, rechazo de HC no numérico o negativo, no eliminar si está en uso |
| Recetas: crear, editar y eliminar | Crear, editar, duplicar, rechazar líneas vacías, eliminar y limpiar la elección manual |
| Reutilización de ingredientes | Un ingrediente en dos recetas; al cambiar la ficha se recalculan ambas |
| Cálculo de hidratos | 35×80/100 + 50×10/100 = 33 g; base distinta de 100; no modifica cantidades |
| Peso crudo y cocido | Si el estado no coincide, no se calcula y queda pendiente; con ficha "cocido" sí se calcula |
| Información incompleta | Sin dato o sin cantidad → incompleto; sin verificar o sin fuente → pendiente de confirmar |
| Posibles alérgenos | Pasta al huevo, plurales, tildes, espinacas ≠ piña, piñones, salsa de soja, judías verdes, gambas, cacahuete (doble), ovoalbúmina, lecitina, rebozados, salsas, trazas, "sin huevo", procesados sin composición, términos propios, términos de serie protegidos |
| Bloqueo de recetas | Nunca se propone una receta bloqueada, aunque sea la única que cumple; la elección manual bloqueada → estado bloqueada; nombre de la receta |
| Reglas | Condiciones, activa e inactiva, tipos concretos, componentes sin confirmar, tipo desconocido → indeterminado, resultado determinista |
| Conflictos | Gana la prioridad más alta; misma prioridad → pendiente; desempate alfabético explicado |
| Pendientes | Sin menú, sin reglas, ninguna cumple (se muestra la más cercana), recetario vacío → sin propuesta, HC sin verificar; los ejemplos nunca salen como compatibles |
| Exportación e importación JSON | Ida y vuelta idéntica; JSON roto, otra app, versión futura, referencias rotas, listas ausentes, valores inválidos |
| localStorage | Guardar y cargar, datos dañados (aviso + copia aparte), almacenamiento lleno, el menú persiste tras recargar la página |
| Exclusiones médicas | El código no contiene insulina, dosis ni glucosa; no hay librerías ni URLs externas |
| Visualización móvil | Las 7 pantallas se pintan sin errores y sin desplazamiento horizontal a 390 px de ancho; se abren los formularios |

**Pendiente de comprobar por ti en Chrome para Android** (no puedo probar en tu móvil):
- La app se abre y los datos siguen ahí al cerrarla y volver a abrirla.
- Los formularios se ven bien a pantalla completa y el teclado no tapa los botones.
- *Exportar copia* descarga el archivo e *Importar copia* lo recupera.

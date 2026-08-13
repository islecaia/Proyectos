# Especificación de Feature: Dashboard de seguimiento de sprints (Jira CSV)

**Rama**: `001-dashboard-sprints-jira`
**Creada**: 2026-08-13
**Estado**: Borrador
**Input**: Descripción del usuario: "Quiero hacer un cuadro de mando, un dashboard, para poder leer de herramientas típicas de gestión, como es Jira. Además, quiero utilizar los datos que extraigo de este Jira, que es un CSV, para ver cómo van los sprints y cómo va este sprint en concreto."

## Escenarios de usuario y pruebas *(obligatorio)*

### Historia de Usuario 1 - Ver el resumen del sprint actual (Prioridad: P1)

Como Scrum Master/Agile Coach, quiero subir el CSV del sprint actual y ver un resumen (KPIs, distribución por estado y horas restantes), para saber de un vistazo si el sprint va bien encaminado.

**Por qué esta prioridad**: es el valor mínimo que resuelve el problema principal. El resto de vistas (por persona, por épica, histórico) no tienen sentido sin esta base.

**Test independiente**: se puede probar subiendo un único CSV de un sprint y comprobando que la pestaña "Resumen" muestra los KPIs y gráficos correctos, sin depender de ninguna otra pestaña.

**Escenarios de aceptación**:
1. **Dado** que subo el CSV de un sprint con nombre reconocible (p. ej. "Sprint-3.csv"), **Cuando** el sistema lo procesa, **Entonces** veo en la pestaña "Resumen" tarjetas KPI con: total de tareas, cerradas (con % sobre el total), en curso, no iniciadas y bloqueadas.
2. **Dado** que estoy en la pestaña "Resumen", **Cuando** consulto el dashboard, **Entonces** veo un gráfico de barras horizontales con el número de tareas por estado, ordenado de mayor a menor.
3. **Dado** que estoy en la pestaña "Resumen", **Cuando** consulto el dashboard, **Entonces** veo un gráfico de donut con el avance del sprint (cerradas / en curso / no iniciadas) y un gráfico de barras con las horas restantes (Remaining Estimate) agrupadas por estado.
4. **Dado** que subo un CSV cuyo nombre no permite identificar el sprint (p. ej. "export_final.csv"), **Cuando** el sistema lo procesa, **Entonces** la carga queda en estado "pendiente de revisión" y no se muestra en ningún resumen hasta que yo indique manualmente a qué sprint corresponde.
5. **Dado** que estoy cargando un CSV de un sprint, **Cuando** lo subo, **Entonces** el sistema me pide la fecha de inicio y fin de ese sprint.

### Historia de Usuario 2 - Ver la carga de trabajo por persona (Prioridad: P2)

Como Scrum Master, quiero ver cuántas tareas y cuántas horas restantes tiene cada persona del equipo en el sprint actual, para detectar desequilibrios de carga.

**Por qué esta prioridad**: aporta valor de gestión del equipo, pero depende de que el resumen del sprint (Historia 1) ya funcione.

**Test independiente**: se puede probar con un único sprint cargado, comprobando que la pestaña "Por persona" agrega correctamente las tareas y horas de cada asignado.

**Escenarios de aceptación**:
1. **Dado** que hay un sprint cargado, **Cuando** entro en la pestaña "Por persona", **Entonces** veo dos listas de barras horizontales lado a lado (peticiones por persona y horas restantes por persona), ambas ordenadas de mayor a menor, con el valor numérico visible sobre cada barra sin necesidad de pasar el ratón.
2. **Dado** que estoy en la pestaña "Por persona", **Cuando** consulto la tabla inferior, **Entonces** veo, por cada persona: nº de peticiones, horas restantes, cerradas, en curso y no iniciadas, y puedo ordenar la tabla haciendo click en cualquier cabecera.
3. **Dado** que una tarea no tiene asignado (Assignee vacío), **Cuando** se calculan los totales por persona, **Entonces** esa tarea se agrupa bajo la etiqueta "(sin asignar)".

### Historia de Usuario 3 - Ver el desglose por épica (Prioridad: P3)

Como Scrum Master, quiero ver cómo se agrupan las tareas del sprint por épica (Parent), para saber qué iniciativas concentran más trabajo y cuáles están más cerca de cerrarse.

**Por qué esta prioridad**: es un nivel de detalle adicional útil pero no imprescindible frente a las Historias 1 y 2.

**Test independiente**: se puede probar con un único sprint cargado, comprobando que la pestaña "Por épica" agrupa correctamente las tareas por Parent summary.

**Escenarios de aceptación**:
1. **Dado** que hay un sprint cargado, **Cuando** entro en la pestaña "Por épica", **Entonces** veo KPIs con: nº de épicas, épica con más elementos, media de elementos por épica y nº de épicas 100% cerradas.
2. **Dado** que estoy en la pestaña "Por épica", **Cuando** consulto el gráfico, **Entonces** veo un gráfico de barras horizontales apiladas con el top 15 de épicas por nº de elementos, diferenciando tareas cerradas del resto.
3. **Dado** que una tarea no tiene épica (Parent summary vacío), **Cuando** se agrupan las tareas por épica, **Entonces** esa tarea se agrupa bajo la etiqueta "(sin épica)".
4. **Dado** que estoy en la tabla de épicas, **Cuando** la consulto, **Entonces** veo por cada épica: nº de elementos, horas restantes, cerrados y % de avance, y puedo ordenar por cualquier columna.

### Historia de Usuario 4 - Buscar y filtrar el detalle de tareas (Prioridad: P2)

Como Scrum Master, quiero ver el listado completo de tareas del sprint con filtros combinables, para localizar rápidamente una tarea concreta o un subconjunto (p. ej. todas las bloqueadas de una persona).

**Por qué esta prioridad**: complementa las vistas agregadas con la capacidad de "bajar al detalle", muy usada en el día a día, pero no es lo primero que se necesita para saber cómo va el sprint.

**Test independiente**: se puede probar con un único sprint cargado, comprobando que la tabla de detalle lista todas las tareas y que los filtros combinados reducen correctamente el resultado.

**Escenarios de aceptación**:
1. **Dado** que hay un sprint cargado, **Cuando** entro en la pestaña "Detalle", **Entonces** veo una tabla con todas las tareas: clave, tipo, resumen, estado (con badge de color), persona, épica, prioridad (con badge de color) y horas restantes.
2. **Dado** que estoy en la pestaña "Detalle", **Cuando** uso el buscador de texto, el desplegable de estado, de persona, de prioridad y/o de tipo de forma combinada, **Entonces** la tabla se filtra según todos los criterios activos a la vez y veo un contador con el número de resultados visibles.
3. **Dado** que estoy en la tabla de detalle, **Cuando** hago click en la cabecera de una columna, **Entonces** la tabla se ordena por esa columna.

### Historia de Usuario 5 - Comparar la evolución entre varios sprints (Prioridad: P2)

Como Scrum Master, quiero cargar los CSV de varios sprints (incluyendo carga masiva de varios ficheros a la vez) para ver cómo ha evolucionado el equipo entre sprints.

**Por qué esta prioridad**: aporta valor de mejora continua, pero depende de que la lectura de un sprint individual (Historia 1) ya funcione.

**Test independiente**: se puede probar subiendo dos o más CSV de sprints distintos (de uno en uno o en carga masiva) y comprobando que el dashboard muestra la comparación entre ellos.

**Escenarios de aceptación**:
1. **Dado** que tengo varios ficheros CSV de distintos sprints, **Cuando** los subo todos a la vez en la zona de carga masiva, **Entonces** el sistema procesa cada fichero de forma independiente, asignando cada uno a su sprint según su nombre.
2. **Dado** que he subido los CSV de varios sprints anteriores, **Cuando** consulto la vista histórica, **Entonces** veo la evolución de la velocidad del equipo sprint a sprint, medida tanto en horas de Remaining Estimate consumidas como en número de tareas cerradas.
3. **Dado** que tengo cargado el histórico de sprints, **Cuando** consulto el dashboard, **Entonces** veo qué porcentaje de cada sprint se completó respecto a lo planificado inicialmente.
4. **Dado** que subo un nuevo CSV de un sprint ya cargado anteriormente, **Cuando** el sistema lo detecta, **Entonces** se me pregunta si quiero sustituir los datos existentes de ese sprint o mantener los anteriores.

### Casos límite

- Un CSV trae un estado del workflow que no está contemplado en ninguna de las listas de Cerrado/No iniciado (p. ej. un estado nuevo no visto antes). Por la regla dada, cae en "En curso" por defecto.
- Dos sprints cargados tienen fechas de inicio/fin solapadas.
- Se sube un CSV vacío (sin filas de tareas).
- En una carga masiva, uno de los ficheros falla al interpretarse (columnas no reconocidas) mientras el resto son correctos.

## Requisitos *(obligatorio)*

### Requisitos funcionales

**Carga de datos**
- **FR-001**: El sistema DEBE permitir al usuario subir manualmente un fichero CSV exportado de Jira.
- **FR-002**: El sistema DEBE permitir la carga masiva de varios ficheros CSV a la vez, procesando cada uno de forma independiente.
- **FR-002b**: El sistema DEBE ser un único fichero autocontenido (tipo .html), ejecutable abriéndolo directamente sin proceso de instalación, servidor propio, ni dependencias externas que instalar. Todos sus recursos (librería de gráficos incluida) DEBEN ir empaquetados en el propio fichero, sin depender de un CDN externo. El flujo debe ser: abrir el dashboard → subir el/los CSV → ver el dashboard interactivo actualizado con esos datos.
- **FR-002c**: El fichero DEBE poder alojarse en una ruta de SharePoint y abrirse directamente desde ahí por cualquier persona con acceso a esa ruta, además de poder usarse igualmente como fichero local en un ordenador. El dashboard NO implementa login propio; el acceso lo controla SharePoint (o el sistema de ficheros, si se usa en local).
- **FR-002d**: Cuando el dashboard se usa desde SharePoint, los datos de los CSV cargados por una persona DEBEN quedar disponibles automáticamente para cualquier otra persona que abra el mismo dashboard después, sin que cada una tenga que volver a subir el CSV. Esto se resuelve mediante escritura compartida en SharePoint: el propio dashboard guarda los datos procesados de vuelta en la misma ruta de SharePoint. **Visualizar** el dashboard y los datos ya cargados NO requiere sesión iniciada. **Subir un CSV** (escribir) SÍ requiere que la persona tenga sesión iniciada en SharePoint/Microsoft 365 en su navegador.
- **FR-002e**: Si una persona intenta subir un CSV mientras otra persona ha subido un CSV hace menos de 5 minutos, el sistema DEBE avisar del conflicto a quien está intentando subir en ese momento antes de completar la subida (en vez de sobrescribir en silencio).
- **FR-003**: El sistema DEBE identificar el sprint de cada CSV a partir del nombre del fichero subido (p. ej. "Sprint-3.csv" → Sprint 3).
- **FR-004**: Si el sistema no puede determinar el sprint a partir del nombre del fichero, DEBE dejar esa carga en estado "pendiente de revisión" y no incluirla en ningún resumen hasta que el usuario indique manualmente el sprint correspondiente.
- **FR-005**: Al cargar el CSV de un sprint, el sistema DEBE solicitar al usuario la fecha de inicio y la fecha de fin de ese sprint.
- **FR-006**: El sistema DEBE conservar los datos de los sprints ya cargados entre visitas, tanto en el mismo navegador/usuario (uso local) como de forma compartida entre distintas personas cuando se usa desde SharePoint (ver FR-002d), sin necesidad de volver a subir el CSV cada vez que alguien abre el fichero.
- **FR-007**: Si se sube un CSV correspondiente a un sprint ya cargado, el sistema DEBE preguntar al usuario si quiere sustituir los datos existentes o conservar los anteriores.
- **FR-008**: El sistema DEBE informar de forma clara cuándo un CSV no se puede interpretar (columnas faltantes o formato no reconocido), y en una carga masiva DEBE indicar qué ficheros concretos han fallado sin bloquear el procesamiento del resto.

**Interpretación de los datos**
- **FR-009**: El sistema DEBE interpretar el CSV usando únicamente estas columnas: Issue Type, Issue key, Summary, Project name, Parent summary, Status, Assignee, Custom field (Prioridad Negocio), Remaining Estimate, Resolved, Custom field (Flagged). El resto de columnas presentes en el CSV (Issue id, Project key, Project type, Project lead, Project lead id, Project description, Parent, Parent key, Assignee Id, Original estimate, Time Spent, Reporter, Reporter Id, Created, Due date, Labels, Σ Time Spent, Σ Remaining Estimate) se DEBEN ignorar a efectos de esta feature.
- **FR-010**: Los campos de tiempo (Remaining Estimate, y cualquier otro campo de tiempo usado) vienen en el CSV en segundos; el sistema DEBE convertirlos a horas dividiendo entre 3600 y redondeando a 1 decimal.
- **FR-011**: Si el campo Parent summary está vacío, el sistema DEBE mostrarlo como "(sin épica)". Si el campo Assignee está vacío, DEBE mostrarlo como "(sin asignar)".
- **FR-012**: El sistema DEBE clasificar cada tarea en una de estas 4 categorías según su Status: **Cerrado** = Status en {Finalizado, Cerrado, Implantado}; **No iniciado** = Status en {No Iniciado, Planificado, Valoracion}; **Bloqueado** = el campo "Custom field (Flagged)" no está vacío (valor observado: "Impedimento"); **En curso** = cualquier otro estado no incluido en las categorías anteriores.
- **FR-013**: La carga de trabajo de cada sprint (y su velocidad) se DEBE medir tanto en horas de Remaining Estimate como en número de tareas, no en story points.

**Vista "Resumen"**
- **FR-014**: El sistema DEBE mostrar, para el sprint actual: tarjetas KPI (total de tareas, cerradas con % sobre el total, en curso, no iniciadas, bloqueadas), un gráfico de barras horizontales por estado (orden descendente), un gráfico de donut con el avance del sprint, y un gráfico de barras con las horas restantes agrupadas por estado.

**Vista "Por persona"**
- **FR-015**: El sistema DEBE mostrar, por cada persona asignada: número de tareas y horas restantes, en gráficos de barras horizontales ordenados de mayor a menor, con el valor visible sobre cada barra sin necesidad de interacción.
- **FR-016**: El sistema DEBE mostrar una tabla ordenable por persona con: nº de peticiones, horas restantes, cerradas, en curso y no iniciadas.

**Vista "Por épica"**
- **FR-017**: El sistema DEBE mostrar KPIs de épicas (nº de épicas, épica con más elementos, media de elementos por épica, nº de épicas 100% cerradas) y un gráfico de barras apiladas con el top 15 de épicas por nº de elementos (cerradas vs. resto).
- **FR-018**: El sistema DEBE mostrar una tabla ordenable por épica con: nº de elementos, horas restantes, cerrados y % de avance.

**Vista "Detalle"**
- **FR-019**: El sistema DEBE mostrar una tabla con todas las tareas del sprint (clave, tipo, resumen, estado, persona, épica, prioridad, horas restantes), con columnas ordenables por click en cabecera.
- **FR-020**: El sistema DEBE permitir filtrar la tabla de detalle combinando: búsqueda de texto (por clave o resumen), estado, persona, prioridad y tipo, mostrando en todo momento un contador de resultados visibles.

**Comparación entre sprints**
- **FR-021**: El sistema DEBE mostrar la evolución de la velocidad del equipo entre los sprints cargados (en horas Remaining Estimate y en nº de tareas cerradas).
- **FR-022**: El sistema DEBE mostrar el porcentaje de cumplimiento (completado vs. planificado) de cada sprint cargado.

### Entidades clave

- **Sprint**: identificado por el nombre del fichero CSV cargado (o pendiente de asignación manual si no se pudo determinar); tiene fecha de inicio y fin (indicadas por el usuario al cargar) y un conjunto de tareas asociadas.
- **Tarea**: unidad de trabajo importada de Jira, con tipo, clave, resumen, estado (Status del workflow, mapeado a Cerrado/No iniciado/Bloqueado/En curso), persona asignada, épica (Parent summary), prioridad de negocio y horas restantes (Remaining Estimate en horas).
- **Persona**: asignado (Assignee) de una o varias tareas; agrupa tareas y horas restantes.
- **Épica**: agrupación de tareas por Parent summary.
- **Carga de datos (importación CSV)**: registro de cada fichero subido (individual o como parte de una carga masiva), con el sprint al que corresponde y su estado (cargado / pendiente de revisión).

## Criterios de éxito *(obligatorio)*

### Resultados medibles

- **SC-001**: El Scrum Master puede saber el estado del sprint actual (KPIs de la pestaña Resumen) en menos de 1 minuto desde que sube el CSV, sin necesidad de revisar Jira directamente.
- **SC-002**: El Scrum Master puede identificar quién tiene más carga de trabajo (tareas y horas) en el sprint actual usando únicamente la pestaña "Por persona", sin recurrir a hojas de cálculo adicionales.
- **SC-003**: El Scrum Master puede localizar cualquier tarea concreta del sprint (p. ej. todas las bloqueadas de una persona) en menos de 30 segundos usando los filtros de la pestaña "Detalle".
- **SC-004**: Tras 3 sprints usando el dashboard, el equipo puede explicar la tendencia de velocidad del equipo (horas y nº de tareas) usando únicamente la vista histórica.

## Suposiciones

- El usuario exporta manualmente el CSV desde Jira; esta feature NO incluye una integración/API directa con Jira.
- Queda FUERA de alcance: la edición de tareas desde el dashboard y la escritura de vuelta hacia Jira.
- La estructura de cabeceras del CSV exportado (Issue Type, Issue key, Issue id, Summary, Project key, Project name, Project type, Project lead, Project lead id, Project description, Parent, Parent key, Parent summary, Status, Assignee, Assignee Id, Original estimate, Remaining Estimate, Time Spent, Custom field (Prioridad Negocio), Reporter, Reporter Id, Created, Resolved, Labels, Labels, Labels) se mantiene estable entre sprints. Si Jira cambia las columnas exportadas, el sistema lo debe poder detectar (FR-008) en vez de fallar en silencio.
- El sprint se identifica únicamente por el nombre del fichero, no por ningún campo dentro del CSV.
- El dashboard puede ser usado por cualquier persona con acceso a la ruta de SharePoint donde se aloje (o al fichero local, si se usa así); no es exclusivo del Scrum Master, aunque el caso de uso principal descrito en esta spec sigue siendo el suyo. Compartir roles o vistas distintas según el tipo de usuario queda fuera de alcance de esta spec.
- **Autenticación mínima**: el dashboard NO implementa un login propio (no hay pantalla de usuario/contraseña de la aplicación). Ver visualización y subir CSV en local no requiere ninguna sesión. Al usarse desde SharePoint, visualizar tampoco requiere sesión, pero subir un CSV sí requiere que la persona tenga sesión iniciada en SharePoint/Microsoft 365 en su navegador (FR-002d), ya que es esa sesión la que permite escribir en la ruta compartida.
- **Distribución y ejecución**: el dashboard DEBE ser un único fichero autocontenido (tipo .html) que se pueda abrir directamente, sin proceso de instalación, servidor propio, ni dependencias externas que instalar (los gráficos y librerías van empaquetados en el propio fichero, no cargados desde un CDN). Preferiblemente, este fichero se aloja en una ruta de SharePoint y se abre directamente desde ahí en el navegador; también debe poder abrirse igual como fichero local en un ordenador. El flujo de uso es: abrir el dashboard (localmente o desde SharePoint) → subir el/los CSV → ver el dashboard interactivo.
- **Acceso**: al abrirse desde SharePoint, el dashboard DEBE poder ser usado por cualquier persona con acceso a esa ruta de SharePoint, sin login propio de la aplicación (el control de acceso, si lo hay, lo gestiona el propio SharePoint, no el dashboard).
- Esta spec define el QUÉ y el PORQUÉ funcional del dashboard (datos, reglas de negocio, vistas y su contenido). Las decisiones puramente visuales y técnicas indicadas por el usuario (paleta de colores corporativa, tipografías, uso de Chart.js, efectos hover/transiciones, título de cabecera) se recogen a continuación como **notas para la fase de plan/diseño**, no como requisitos funcionales de esta spec.

## Notas para la fase de plan/diseño (no forman parte de los requisitos funcionales)

- Modo claro, estética profesional y sobria (entorno bancario) con dinamismo: tarjetas KPI con sombra suave y ligero efecto de elevación al hover, transiciones en las barras, badges de estado con color.
- Paleta corporativa: azul oscuro #034E67, cyan #00B5DD, verde #80BC00, naranja #FF8300, púrpura #AA004F, gris #747678.
- Colores de estado: Verde = Cerrado, Azul = En curso, Rojo = Bloqueado, Gris = No iniciado.
- Tipografía sans-serif limpia para textos y monoespaciada para las cifras.
- Gráficos con Chart.js, empaquetado localmente en el propio fichero (no cargado desde CDN, para cumplir el requisito de funcionamiento 100% offline).
- Cabecera con título "SPRINT · PAGOS CON TARJETA" y subtítulo indicando que la carga se mide en Remaining Estimate.

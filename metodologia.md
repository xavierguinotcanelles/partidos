# Metodología

Criterios editoriales del proyecto, tal y como están decididos. Cada apartado es una decisión registrada (ADR) y numerada; solo se publican las vigentes.


<!-- ADR-0003-fuentes-neutralidad.md -->
## ADR-0003 · Fuentes, procedencia y neutralidad

## Contexto

Una web divulgativa sobre partidos políticos solo es útil si quien la consulta puede comprobar cada dato y conocer los criterios con que se ha organizado. El proyecto cubre todo el arco político, con imparcialidad declarada y comprobable.

## Decisión

### Fuentes

1. **Primero las fuentes primarias oficiales**; las secundarias solo como semilla o contexto, y siempre verificadas contra una primaria antes de publicar.

| Fuente | Para qué | Carácter |
| --- | --- | --- |
| Ministerio del Interior, resultados electorales | Votos, escaños, censo y participación por circunscripción desde 1977 | Primaria |
| BOE: decretos de convocatoria, candidaturas presentadas y proclamadas, acuerdos de la Junta Electoral Central | Fechas, escaños por circunscripción, composición de coaliciones y listas, resultados oficiales | Primaria |
| Ministerio del Interior, Registro de Partidos Políticos | Inscripción, tipo jurídico y fechas de partidos y federaciones | Primaria |
| Congreso de los Diputados | Diputados, grupos parlamentarios y sus cambios | Primaria |
| Documentos de la propia organización (estatutos, web oficial) | Autodefinición, liderazgos, nombre | Primaria para lo que la organización dice de sí misma |
| Wikidata | Semilla estructurada de relaciones e identificadores | Secundaria; nunca se publica sin verificar |
| Codificaciones académicas (Chapel Hill, ParlGov, Manifesto Project) | Posiciones ideológicas codificadas por terceros | Externa; se citan como tales (ADR-0006) |
| Prensa | Contexto y negociaciones; única fuente disponible para hechos recientes hasta que exista una primaria | Secundaria; obliga a `dudoso` si no hay primaria |

2. **Toda fila publicada apunta a una o varias fuentes**, con la localización dentro de la fuente cuando sea posible. Sin fuente no hay fila: lo impide la integración continua.
3. **Copia de cada fuente** antes de leerla: documentos oficiales y datos reutilizables se guardan en el repositorio de trabajo (o como adjuntos si pesan); de la prensa solo URL, enlace a copia archivada y cita breve, por derechos de autor. Nunca texto completo de prensa en la web pública.
4. **Fecha con precisión e incertidumbre explícita**: cada hecho fechado declara si la fecha es exacta, de mes, de año o aproximada; cada hecho declara si está confirmado, es dudoso o está en disputa entre fuentes. La web lo enseña; el proyecto no resuelve disputas por criterio propio.

### Neutralidad

5. **Las decisiones editoriales son ADR públicos.** Qué cuenta como sucesor de qué, cómo se registra un cambio de nombre, una refundación o una confluencia territorial, qué se publica y qué no: todo queda escrito, numerado y fechado en esta Metodología, y solo se cambia con un nuevo ADR que sustituya o enmiende al anterior.
6. **El proyecto no asigna posiciones ideológicas propias.** Toda etiqueta que aparece está atribuida: a la propia organización, a una codificación externa citada o a historiografía citada (ADR-0006).
7. **Las estimaciones nunca se presentan como datos.** Lo que no sale de una fuente se marca como estimación, con sus supuestos a la vista (ADR-0004).
8. **Logos: no se usan.** Cada organización se identifica por color e iniciales. El color se elige por una regla documentada en la ficha (el que la organización usa en su propia identidad, con fuente; si no consta, uno neutro asignado).
9. **Todo el arco político, mismo tratamiento**: mismas tablas, mismas reglas, misma profundidad objetivo. Los ejemplos del diseño no condicionan la cobertura.
10. **Corrección abierta**: cualquier persona puede señalar un error desde la web pública, aportando fuente. Las correcciones aceptadas se registran con su fuente como cualquier otro dato.

## Consecuencias

- Las elecciones recientes se publican primero con lo que dice el BOE; el contexto narrativo (negociaciones, motivos) llega después o no llega.
- La cobertura real de cada fuente oficial hacia atrás en el tiempo está por comprobar; es la primera tarea del piloto y puede obligar a marcar como `dudoso` tramos enteros.
- Publicar esta Metodología convierte la neutralidad en algo verificable; también en algo criticable, que es el objetivo.


<!-- ADR-0004-simulador.md -->
## ADR-0004 · Simulador electoral: lo exacto separado de los supuestos

## Contexto

La web incluirá una herramienta para recalcular resultados del Congreso bajo otras reglas o combinaciones de candidaturas. El riesgo es presentar una conjetura como un dato. La regla es separar siempre dos clases de cálculo y decirlo en pantalla.

## Decisión

| Clase | Ejemplos | Carácter |
| --- | --- | --- |
| **Recálculo mecánico** | Otra fórmula (Sainte-Laguë en vez de D'Hondt), sin barrera o con otra, circunscripción única, otro reparto de escaños por provincia | **Exacto**: aritmética sobre los votos oficiales; el parámetro cambiado se muestra |
| **Indicadores** | Votos del último escaño en cada circunscripción, votos por escaño, votos sin escaño, índice de Gallagher, número efectivo de partidos | **Exacto** |
| **Contrafactual de unión** | Dos candidaturas presentadas juntas | **Depende de un supuesto de comportamiento**, que se muestra |
| **Contrafactual de separación** | Una coalición dividida en sus componentes | **Depende de un supuesto de reparto**, que se muestra |

Reglas del contrafactual:

1. Por defecto, **suma simple con el supuesto escrito en pantalla**: «si el 100 % de los votantes de A y de B hubiese votado a A+B». Un control de fidelidad permite fijar qué porcentaje se mantiene y adónde va el resto.
2. En la separación **no hay reparto automático por defecto**: la proporción en una elección anterior rara vez existe o es comparable. El usuario fija los porcentajes o no hay cálculo.
3. Escenarios con fuente (p. ej. transferencias de voto de una encuesta postelectoral) solo si existe una fuente que lo permita; se citan y se marcan como **estimación ajena**.
4. **Imparcialidad**: ningún escenario destacado ni precargado. Cualquier combinación de cualquier candidatura, compartible por URL.
5. La barrera se aplica como dice la ley de cada elección: en el Congreso, 3 % de los votos válidos de la circunscripción, blancos incluidos (LOREG, art. 163). Los empates se resuelven por mayor número de votos y, si persisten, se indica.

Alcance: Congreso de los Diputados, elecciones desde 1977. El Senado y las elecciones anteriores a 1977 usan otros sistemas y quedan fuera. Ejecución en el navegador sobre los JSON publicados; no hay servidor.

## Consecuencias

- El código del reparto (`simulador/reparto.py`) tiene tests con el ejemplo del artículo 163 de la LOREG y es la referencia también para la versión en el navegador: ambas deben dar lo mismo.
- Un contrafactual nunca aparece en la web sin su frase de supuesto visible junto al resultado.


<!-- ADR-0006-etiquetas-linaje.md -->
## ADR-0006 · Etiquetas ideológicas atribuidas y linaje estructural

## Contexto

A quien navega le ayuda saber que un partido es, o se considera, conservador, socialdemócrata o nacionalista. Pero el proyecto no asigna posiciones ideológicas propias (ADR-0003). Además, medir «fragmentación por espacio político» exigiría decidir qué partidos forman un espacio, que es en sí una clasificación ideológica.

## Decisión

### Etiquetas: siempre atribuidas

1. Una etiqueta ideológica se publica **solo con su atribución y su fuente**: quién dice que la organización es eso, y dónde.
2. Atribuciones admitidas, que la web muestra literalmente:
   - **autodefinicion**: la propia organización (estatutos, web oficial, programa). Se presenta como «se define como…».
   - **externa**: una codificación de terceros con metodología publicada (Chapel Hill Expert Survey, ParlGov, Manifesto Project u otra que se cite). Se presenta como «clasificado por X (año) como…», con el valor tal cual lo publica la fuente.
   - **historiografia**: obra académica citada (autor, título, año, página). Se presenta como «según X…».
   - **prensa**: solo para organizaciones recientes sin autodefinición ni codificación disponible, marcada `dudoso`, y sustituida en cuanto exista otra.
3. Varias atribuciones pueden coexistir y contradecirse; se muestran todas con su intervalo de vigencia. El proyecto no elige entre ellas ni las resume.
4. Ninguna etiqueta se hereda: la de una organización no se aplica a sus escisiones, sucesoras ni coaligadas.

### Linaje: estructural, sin ideología

5. El **linaje** de una organización es la componente conexa del grafo de relaciones (escisión, fusión, absorción, refundación, renombre, sucesión, pertenencia). Se calcula; no se decide. No usa etiquetas.
6. La **tasa de fragmentación** y cualquier indicador de ruptura se calculan por linaje y por tipo de relación (ADR-0002, principio 5), nunca por «espacio político».
7. Si se publica una agrupación por familias ideológicas, se hace solo a partir de una codificación externa citada, como capa opcional y etiquetada, nunca como organización por defecto de la web.

## Consecuencias

- Las elecciones recientes mostrarán menos etiquetas (no hay codificación externa aún) y más autodefiniciones.
- Una etiqueta sin `atribucion` y `atribuida_por` no pasa la validación de datos.
- La discusión sobre «a qué espacio pertenece X» queda fuera del proyecto por diseño; lo que el proyecto ofrece es el grafo y las atribuciones para que cada cual juzgue.


<!-- ADR-0020-fuentes-del-linaje.md -->
## ADR-0020 · Fuentes que confirman una relación de linaje

## Contexto

Decisión de Xavier (#67, `confirmo` del 17-10-2026; criterio editorial, su lista cerrada). La cata de fuentes del piloto (F1.1, `docs/FUENTES.md`) muestra que las escisiones, fusiones, refundaciones y sucesiones entre organizaciones **no son actos registrales**: ni el BOE ni el Registro de Partidos las documentan como tales, y el Registro no responde a clientes automáticos. Con la regla de ADR-0003 (solo primaria oficial para confirmar) el piloto no podría confirmar casi ninguna relación de linaje; aceptar Wikidata como fuente suficiente rompería ADR-0003. Los documentos de la propia organización y la historiografía citada son comprobables por cualquiera y ya figuran en ADR-0003 y ADR-0006 como fuentes admitidas para otros hechos.

## Decisión

Se aplica a las relaciones de **linaje**: `escision_de`, `fusion_en`, `absorcion_por`, `refundacion_en`, `renombre_a` y `sucesion_de` (ADR-0002). `miembro_de` y `coaligada_en` siguen con ADR-0003 (pactos de coalición de la JEC, BOE, estatutos).

1. **Qué confirma.** Una relación de linaje solo está `confirmado` con al menos una fuente de estas clases, enlazada por `fuente_de`:
   - **BOE o Registro de Partidos** (`tipo: boe` o `registro_partidos`): inscripción, modificación o extinción.
   - **Documento de la propia organización** (`tipo: organizacion`): estatutos, acta o resolución de congreso, comunicado oficial. El título de la fuente dice qué documento es y de qué fecha; se copia en `fuentes/organizaciones/`.
   - **Historiografía citada** (`tipo: academica`): obra con autor, título, año y página. La cita completa va en `fuente_de.cita`; sin cita, la fuente no cuenta.
2. **Wikidata es semilla y nunca basta sola.** Una relación de linaje cuya única fuente sea Wikidata se carga como `dudoso` y **no se publica** (ADR-0003, punto 1). Sirve para saber qué buscar, no para afirmar.
3. **Prensa**: permite cargar la relación como `dudoso` y publicarla marcada así, con URL, copia archivada y cita breve (ADR-0003, punto 3).
4. **Contradicción**: si dos fuentes de las clases del punto 1 se contradicen (fecha, tipo de relación, organizaciones), la relación queda `en_disputa` con las dos citadas en `fuente_de`. El proyecto no elige (ADR-0003, punto 4): una relación `en_disputa` lleva al menos dos fuentes.
5. **Lo hace cumplir el validador**, no el criterio de quien carga: `scripts/validar_datos.py` rechaza una relación de linaje `confirmado` sin fuente de las clases del punto 1, una fuente `academica` enlazada sin `cita`, y una relación `en_disputa` con menos de dos fuentes; `scripts/construir.py` deja fuera de la web las relaciones de linaje cuyas fuentes sean solo Wikidata.
6. **Qué obras se citan** lo decide cada tanda según el linaje, con la cita completa; no hay lista cerrada de historiografía.

## Enmienda a ADR-0003

- Punto 1 («Primero las fuentes primarias oficiales; las secundarias solo como semilla o contexto, y siempre verificadas contra una primaria antes de publicar»): para las relaciones de linaje, «verificadas contra una primaria» queda como «confirmadas con una fuente del punto 1 de ADR-0020»; los documentos de la propia organización y la historiografía citada confirman una relación de linaje sin que haga falta BOE ni Registro.
- Tabla de fuentes: la fila «Documentos de la propia organización» añade «relaciones de linaje (ADR-0020)» a su «Para qué»; se añade la fila «Historiografía citada (autor, obra, año y página) | Relaciones de linaje y contexto | Confirma una relación de linaje si la cita es completa (ADR-0020)»; la fila «Wikidata» queda «Secundaria; una relación de linaje que solo esté en Wikidata es `dudoso` y no se publica».

## Amplía ADR-0006

- Punto 5 (linaje estructural): el grafo de linaje se calcula sobre las relaciones `confirmado` y `dudoso` cargadas con este criterio; las de solo Wikidata no entran en el grafo publicado.

## Consecuencias

- Habrá menos relaciones `confirmado` y más `dudoso` al principio; la web las enseña como tales (ADR-0002, principio 3).
- `fuentes/README.md` gana la carpeta `organizaciones/` (documentos propios); `datos/fuentes.csv` usa `tipo: organizacion` y `tipo: academica` con `caracter` según ADR-0003.
- Primera tanda de F1.2: el validador (regla y tests); después los linajes (PLAN F1.2).


<!-- ADR-0022-genealogia-como-historiador.md -->
## ADR-0022 · La genealogía se lee como historiador, con justificación publicada, y los datos permiten navegar en el tiempo y con zoom

## Contexto

Decisión de Xavier (#81, `confirmo` del 17-10-2026; criterio editorial y alcance de la web: su lista cerrada). En la tanda #72 la historiografía decía «escisión» y la relación Más Madrid → Podemos quedó `dudoso` porque `escision_de` se leyó como ruptura formal de una organización. Con esa lectura casi ningún linaje de partidos recientes llega a `confirmado`. El proyecto quiere contar la genealogía como la contaría un historiador: con fuentes, pero interpretándolas, y haciendo visible la interpretación para que no pase por dato bruto («ninguna estimación presentada como dato»). A la vez, la web que se quiere se navega en dos ejes (scroll temporal y zoom con tamaño según peso) y el modelo tiene que permitirlo antes de cargar los linajes que faltan.

Lo que aquí es técnico (cómo se guarda la justificación, cómo se modelan los varios orígenes, la fórmula del peso, qué cuenta como medio de referencia) lo decide este ADR por delegación de #81 («Abierto a propósito») y es reversible sin volver a Xavier.

## Decisión

### A. Criterio de genealogía

1. **La etiqueta de linaje describe lo que pasó políticamente, no el acto formal.** Hay `escision_de` cuando un grupo relevante de dirigentes o militantes sale de A y funda B o le da forma de manera decisiva, aunque A no se parta formalmente. Lo mismo para `fusion_en`, `absorcion_por`, `refundacion_en` y `sucesion_de`: se elige la que usaría un historiador del periodo. La relación lleva **`lectura`**: `literal` (o vacío) si la fuente que la confirma la nombra con ese tipo y esas organizaciones; `interpretada` si el proyecto ha elegido el tipo, la identidad o las organizaciones leyendo las fuentes. Una relación `interpretada` exige justificación (punto 4).
2. **Una organización puede tener más de un origen.** Cada procedencia es una relación de linaje propia con la organización nueva como `origen` (B `escision_de` A y B `sucesion_de` C, por ejemplo), cada una con sus fuentes, su estado y su lectura. El grafo de linaje (ADR-0006, punto 5) admite varios padres; nada se calcula suponiendo uno solo.
3. **La misma organización con otro nombre es una sola ficha.** La ficha lleva `nombres`, una lista fechada (`nombre`, `siglas`, `desde`/`desde_precision`, `hasta`/`hasta_precision`, `nota`); `nombre` y `siglas` de la ficha son los del último nombre. Vale aunque se inscriba o registre de nuevo (una coalición que se vuelve a registrar en cada elección con el mismo proyecto y socios que cambian es una ficha; cada registro es una fila de `candidaturas`). Si Wikidata tiene varias entradas para la misma organización, `wikidata` es la principal y `wikidata_otros` las demás. **`renombre_a` desaparece** del modelo: un cambio de nombre no es una relación entre dos organizaciones. Cuando el historiador dice que nació otro proyecto (nuevos estatutos, nueva dirección, absorción de otros) aunque siga la inscripción, son dos fichas unidas por `refundacion_en` con `lectura: interpretada`. Una ficha con dos o más `nombres` o con `wikidata_otros` exige justificación: decir que dos nombres son una organización es una lectura.
4. **Justificación en los casos discutibles**, guardada como fichero `datos/justificaciones/<id>.md` con cabecera YAML (`id`, `tabla`: `relaciones` u `organizaciones`, `fila`, `fuentes`: ids de `fuentes.csv`, al menos uno) y tres apartados obligatorios: «## Qué dicen las fuentes», «## Qué concluye el proyecto» y «## Por qué». La fila justificada apunta a él en su campo `justificacion`. **Se publica en la web** junto a la relación o la ficha («por qué decimos esto»): `construir.py` la lleva a `datos/justificaciones.json`. Es obligatoria cuando la relación es `interpretada`, cuando una relación de linaje se confirma por prensa convergente (punto 5) o cuando una ficha une varios nombres o varias entradas de Wikidata (punto 3); cualquier tanda puede añadirla a otra fila si hay otra lectura razonable. Plantilla: `docs/plantillas/justificacion.md`.
5. **Prensa convergente.** Cuando no haya documento propio ni historiografía (ADR-0020, punto 1), **dos medios de referencia independientes** que coincidan, más una justificación, confirman una relación de linaje. Un solo medio la deja `dudoso`. Wikidata sigue siendo solo semilla. Medio de referencia: periódico, agencia o radiotelevisión con redacción propia identificable, hemeroteca consultable y estable (URL que resuelve o copia en Wayback), que no es órgano de una organización política, de ámbito estatal o autonómico. Independientes = de grupo editorial distinto. La lista es abierta y vive en `datos/medios.csv` (`id`, `nombre`, `grupo`, `ambito`, `url`, `motivo`); cada fuente `prensa` de `fuentes.csv` dice su `medio`, y solo las que lo tienen cuentan. Una pieza de agencia reproducida por un periódico cuenta una vez, por la agencia. La lista inicial va en el anexo.
6. **Casos del linaje Sumar/IU** (fijados por Xavier; la tanda de revisión los carga así, con las fuentes que los sostengan y justificación):
   - Más Madrid es **escisión de Podemos** (sector de Errejón, enero de 2019, tras Vistalegre II de 2017) y además procede de la plataforma de Manuela Carmena, venida de Ahora Madrid: dos orígenes (punto 2), el segundo con el tipo que den las fuentes.
   - Unidos Podemos y Unidas Podemos son **la misma coalición** con cambio de nombre en 2019: una ficha, `unidas_podemos`, con `nombres` fechados.
   - Més-Compromís es **el Bloc Nacionalista Valencià refundado** en 2021: `refundacion_en`, no coalición nueva. La coalición es Compromís. Fecha exacta y continuidad de la inscripción se comprueban en el Registro (ADR-0021, tanda #73): hasta entonces, el estado que den documentos propios o historiografía.

### B. Lo que la capa de datos permite (la web que se quiere)

7. **Dos ejes.** *Scroll temporal*: para cualquier fecha entre 1977 y hoy, qué organizaciones existían, con qué nombre y de quién se componía cada coalición o federación. *Zoom*: de lejos, las organizaciones principales con tamaño según su peso; de cerca, cada coalición o federación abierta en sus componentes. El recurso visual (río, metro, burbujas u otro) se decide tras el piloto; aquí se fija que los datos lo permitan.
8. **Consulta «estado en una fecha»**, implementada en `scripts/consultar.py` y usada por `construir.py`, sin código de la web. Una fila con intervalo está *vigente* en la fecha F si `desde ≤ F` y (`hasta` vacío o `F ≤ hasta`), expandiendo la precisión: `anio` → del 1 de enero al 31 de diciembre; `mes` → del día 1 al último; `aprox` → como la granularidad escrita y marcada `aprox`. Una fila sin `desde` ni `hasta` se devuelve con `sin_fecha: true`: la web la enseña como «sin fecha conocida», nunca con un intervalo inventado. Toda respuesta lleva la precisión de los límites y el `estado` de cada fila. Composición de X en F = relaciones `miembro_de` y `coaligada_en` hacia X vigentes en F, con su `ambito`; el nombre de X en F sale de `nombres`.
9. **El peso se calcula, no se decide.** Por elección cargada y candidatura: `votos` = suma de `resultados.votos` de sus listas; `votos_pct` = `votos` / suma de `resultados_circunscripcion.validos` de todas las circunscripciones de la elección (si falta alguna, `votos_pct` es nulo: hueco, no estimación); `escanos` y `escanos_pct` = `escanos` / `elecciones.escanos_total`. El **peso** de una organización en la fecha F es el `votos_pct` de su candidatura en la última elección cargada de tipo `generales` con fecha ≤ F (otras elecciones entrarán por `tipo` cuando se carguen; la web usa generales por defecto). Una organización que concurrió **dentro de una coalición** no tiene peso propio: lleva `peso: null` y `via: <coalición>` (con `via_ambito` si su `coaligada_en` tiene ámbito); la web la dibuja dentro del nodo de la coalición. No se reparte a ojo ni a partes iguales: sería una estimación presentada como dato (ADR-0003, ADR-0006). `construir.py` publica `datos/pesos.json` con estas filas y la fórmula es la de este punto.
10. **Todo lo que la web necesita para los dos ejes está fechado y con fuente**: nombres, pertenencias, entradas y salidas de coaliciones, relaciones de linaje y peso por fecha. Sin fecha → `sin_fecha`; con fecha imprecisa → su precisión.
11. **Se mantiene lo ya previsto**: fichas al tocar un nodo, simulador (ADR-0004), trayectorias de personas, etiquetas atribuidas (ADR-0006), tipología de rupturas e índices.

### C. Lo hace cumplir el validador

`scripts/validar_datos.py` rechaza: (a) `lectura: interpretada` sin `justificacion`; (b) una relación de linaje `confirmado` sin fuente de ADR-0020 punto 1 que no tenga al menos dos fuentes `prensa` con `medio` de `grupo` distinto **y** `justificacion`; (c) una ficha con dos o más `nombres` o con `wikidata_otros` sin `justificacion`; (d) una `justificacion` que no apunte a un fichero existente cuyo `tabla`/`fila` coincidan con la fila, con al menos una fuente existente y los tres apartados; (e) `renombre_a` como tipo; (f) `medio` en una fuente que no sea `prensa`, o un `medio` que no esté en `medios.csv`; (g) una entrada de `nombres` sin `nombre` o con fechas incoherentes con su precisión, o una ficha cuyo `nombre` no figure en su lista `nombres`. `construir.py` sigue dejando fuera de la web las relaciones de linaje de solo Wikidata (ADR-0020) y publica `justificaciones.json` y `pesos.json`.

## Enmienda a ADR-0002

- Tabla de entidades, fila `organizacion`: la ficha lleva además `nombres` (lista fechada), `wikidata_otros` y `justificacion`. Fila `relacion`: los tipos son `miembro_de`, `coaligada_en`, `escision_de`, `fusion_en`, `absorcion_por`, `refundacion_en` y `sucesion_de`; se añaden `lectura` y `justificacion`. Nueva entidad `justificacion` (`datos/justificaciones/<id>.md`) y nueva tabla `medios` (`datos/medios.csv`).
- Principio 7, última frase («si una organización cambia de nombre, la relación `renombre_a` lo registra») queda: «si una organización cambia de nombre, la lista `nombres` de su ficha lo registra con fechas; el `id` no cambia».
- Principio 5: la tipología de rupturas es escisión, fusión, absorción, refundación y sucesión; el cambio de nombre no es ruptura.

## Enmienda a ADR-0020

- La lista de relaciones de linaje pierde `renombre_a`.
- Punto 3 («Prensa: permite cargar la relación como `dudoso`…») queda: «Prensa: un solo medio permite cargar la relación como `dudoso` y publicarla marcada así; dos medios de referencia independientes (ADR-0022, punto 5) que coincidan, con justificación publicada, la confirman cuando no hay fuente del punto 1».
- Punto 5: el validador aplica además las reglas de ADR-0022, apartado C.

## Amplía ADR-0006

- Punto 5: el grafo de linaje admite varios orígenes por organización y se calcula sobre relaciones cuyo tipo describe lo que pasó políticamente (ADR-0022, punto 1), con la lectura y la justificación visibles.
- Nuevo punto 8: el tamaño de un nodo en la web sale solo del peso calculado del punto 9 de ADR-0022; nunca de una apreciación.

## Consecuencias

- Tandas: modelo (esquemas, validador, `construir`, plantilla y `medios.csv`); consulta en el tiempo y peso (`consultar.py`, `pesos.json`); revisión de Sumar/IU con los casos del punto 6; composición de IU en 1986, 1989, 2016 y 2023 con las consultas anotadas; carga del 23J para Sumar y peso en esa fecha. Las tandas #74-#77 citan este ADR y cargan ya con `lectura`, `nombres` y justificaciones.
- La PR que fusiona dos fichas quita la sobrante con `git rm` dentro del worktree (queda en el historial; es el único borrado que admite el flujo, FLUJO §6) y reapunta sus relaciones sin cambiar sus ids.
- Habrá más relaciones `confirmado` y cada una `interpretada` llevará su «por qué» publicado; lo que las fuentes no den sigue siendo `dudoso` o hueco.

## Anexo · lista inicial de medios de referencia (`datos/medios.csv`)

Abierta: una tanda añade una fila con su `motivo` si cumple el criterio del punto 5; el verificador lo comprueba. `grupo` es el grupo editorial o propietario, que decide la independencia.

| id | nombre | grupo | ambito |
| --- | --- | --- | --- |
| elpais | El País | Prisa | estatal |
| elmundo | El Mundo | Unidad Editorial | estatal |
| abc | ABC | Vocento | estatal |
| lavanguardia | La Vanguardia | Godó | estatal |
| elperiodico | El Periódico de Catalunya | Prensa Ibérica | estatal |
| eldiario | elDiario.es | Diario de Prensa Digital | estatal |
| elconfidencial | El Confidencial | Titania | estatal |
| elespanol | El Español | El León de El Español Publicaciones | estatal |
| publico | Público | Display Connectors | estatal |
| infolibre | infoLibre | Ediciones Prensa Libre | estatal |
| 20minutos | 20minutos | Henneo | estatal |
| efe | Agencia EFE | Agencia EFE | estatal |
| europapress | Europa Press | Europa Press | estatal |
| rtve | RTVE | Corporación RTVE | estatal |
| elsalto | El Salto | El Salto (cooperativa) | estatal |
| lamarea | La Marea | MásPúblico (cooperativa) | estatal |
| heraldo | Heraldo de Aragón | Henneo | autonomico |
| elcorreo | El Correo | Vocento | autonomico |
| diariovasco | El Diario Vasco | Vocento | autonomico |
| lavozdegalicia | La Voz de Galicia | Corporación Voz de Galicia | autonomico |
| levante | Levante-EMV | Prensa Ibérica | autonomico |
| lasprovincias | Las Provincias | Vocento | autonomico |
| lanuevaespana | La Nueva España | Prensa Ibérica | autonomico |
| ara | Ara | Edició de Premsa Periòdica Ara | autonomico |
| vilaweb | VilaWeb | Partal, Maresma & Associats | autonomico |
| naciodigital | Nació Digital | Nació Digital | autonomico |
| berria | Berria | Euskal Editorea | autonomico |
| diariodenavarra | Diario de Navarra | La Información | autonomico |
| canarias7 | Canarias7 | Vocento | autonomico |
| diariodemallorca | Diario de Mallorca | Prensa Ibérica | autonomico |

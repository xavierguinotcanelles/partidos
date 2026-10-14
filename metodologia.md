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

---
id: junts_identidad
tabla: organizaciones
fila: junts
fuentes:
  - acad-gec-junts-per-catalunya
  - acad-tornos-2020-iccaa-cataluna
  - org-junts-estatuts-2020
  - registro-descarga-2026-10-17
  - jec-pacto-coalicion-junts-2019-04
  - wikidata-q97155800-junts
  - wikidata-q43228047-jxcat-2017
---

## Qué dicen las fuentes

- Gran Enciclopèdia Catalana, entrada única «Junts per Catalunya»: «Coalició electoral. Es formà per a concórrer a les eleccions al Parlament de Catalunya del 21 de desembre de 2017»; la candidatura, «integrada en bona part per membres del PDeCAT», fue «Registrada el novembre del 2017». Más adelante: «Hi tingué també un pes considerable la iniciativa de Carles Puigdemont de convertir la coalició en un partit polític», y «El juliol del 2020 s'inicià el congrés fundacional de JxCat com a partit polític, que culminà el 3 d'octubre». La misma entrada sigue con las elecciones de 2021, 2023 y 2024.
- Tornos (2021), «Cataluña», en Informe Comunidades Autónomas 2020 (IDP), pág. 174: «la batalla interna por el dominio del nombre de la coalición. El PdeCAT planteó una demanda ante el Tribunal Superior de Justicia de Cataluña por el registro del nombre a favor de los partidarios de Puigdemont».
- Registro de Partidos (descarga del 17-10-2026): «JUNTS PER CATALUNYA (JxCat)», Pasaje de Bofill 9-11, Barcelona, inscrito el 11/07/2018.
- JEC: en el pacto de la coalición JUNTS para el 28-04-2019 (13-03-2019) firma «JUNTS PER CATALUNYA» por su presidenta, junto al PDeCAT y CDC.
- Estatutos (2020), art. 1: «es constitueix el partit polític denominat JUNTS PER CATALUNYA, que té per sigles l'acrònim JxCat»; disposición final 2: en vigor desde la aprobación de la ponencia organizativa del 3-10-2020.
- Wikidata: dos entradas, Q43228047 (alianza electoral, 13-11-2017 a 21-12-2020, con PDeCAT y CDC como partes) y Q97155800 (partido, desde el 25-07-2020).

## Qué concluye el proyecto

- Junts per Catalunya es una sola ficha desde noviembre de 2017, con dos entradas en `nombres` (mismo nombre y siglas): coalición electoral hasta el 3-10-2020 y partido desde entonces.
- Tipo de la ficha: partido, su última forma. El paso de coalición a partido se ve en las relaciones: `pdecat_coaligada_en_junts_2017` hasta la ruptura del 7-09-2020 y `junts_escision_de_pdecat_2020`.
- Wikidata principal: Q97155800 (el partido); Q43228047 va en `wikidata_otros`.

## Por qué

La obra de referencia trata a Junts per Catalunya como un solo sujeto que se «converteix» de coalición en partido, y Tornos llama al pleito de 2020 una pelea por «el nombre de la coalición», es decir, por quién sigue el mismo proyecto; nombre, siglas y sede no cambian, y el partido que firma los pactos de 2019 ya está inscrito en 2018 con ese nombre. Es el mismo razonamiento que la CiU de 1978 y 2001 (`ciu_identidad`): conversión de forma, no proyecto nuevo. La otra lectura defendible son dos fichas, coalición de 2017 y partido de 2020, unidas por `refundacion_en`, porque la enciclopedia habla de «congrés fundacional» y de «nou partit»; no se toma porque lo nuevo de 2020 respecto al PDeCAT ya se expresa con `escision_de`. Wikidata pone a CDC como parte de la coalición de 2017 y CDC firma el pacto de 2019 ante la JEC, pero su ficha cierra en julio de 2016 (baja política): no se carga esa relación (ver FUENTES.md). Queda abierto por qué la inscripción del Registro (11-07-2018) precede en dos años al congreso fundacional.

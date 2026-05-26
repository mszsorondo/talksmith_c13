---
source_file: alphafold-db-protein-Q8W3K0.webp
source_type: image
ingested_at: 2026-05-26
---

# AlphaFold DB — proteína Q8W3K0 (vista 3D con confianza por color)

## Provenance
- Original location: research/articles/alphafold-db-protein-Q8W3K0.webp
- Format: WebP (552×510, ~33KB)
- Author / source (if known): EMBL-EBI / DeepMind — AlphaFold Protein Structure Database (`alphafold.ebi.ac.uk/assets/img/Q8W3K0.webp`)
- Date of original (if known): 2021+ (AF DB lanzada Jul 2021)

## Key claims

Imagen oficial de la AlphaFold DB para la entrada UniProt **Q8W3K0**. Muestra la estructura 3D predicha por AF2 con el código de color de **pLDDT** (per-residue confidence): azul oscuro = alta confianza, naranja/amarillo = baja. Es la representación canónica con la que la comunidad consulta AlphaFold DB en producción.

Slide objetivo: **Sección 3 — "AlphaFold DB: 200 millones de estructuras, libres"** (marcador `[IMAGEN SUGERIDA]` correspondiente). Reemplaza visualmente al "screenshot" que pedía el marcador — funciona mejor como render limpio que como UI screenshot.

## Definitions and terminology

(N/A para un record de imagen.)

## Evidence and examples

- **pLDDT (predicted Local Distance Difference Test)**: métrica de confianza per-residuo que AF2 emite junto con la estructura. Escala 0–100; los colores en la imagen siguen el gradient estándar de AF DB (azul = >90 confianza muy alta, celeste = 70–90 alta, amarillo = 50–70 baja, naranja = <50 muy baja). Útil mencionarlo en el slide para que el alumno entienda qué significa el color.

## Inconsistencies / open questions

- La identidad biológica concreta de Q8W3K0 (qué proteína, qué organismo) no está en el filename. Si se quiere usar el nombre biológico real en el slide, conviene chequear la entrada UniProt antes (probable: una proteína de planta — el prefijo Q8 con esa numeración suele caer en Arabidopsis o similar). No bloqueante.

## Images / diagrams

- **alphafold-db-protein-Q8W3K0.webp/images/alphafold-db-protein-Q8W3K0.webp** — Estructura 3D predicha por AF2 (UniProt Q8W3K0) con color por pLDDT
  - Depiction: Render cartoon/ribbon de una proteína grande sobre fondo blanco. Geometría general en forma de **herradura abierta** — un solenoide curvo con muchos giros, dominado por **alfa-hélices en forma de cilindro** y algunas **láminas-beta planas**. Cientos de residuos visibles. **Coloreado por pLDDT** siguiendo el gradient estándar de AF DB: **azul oscuro/medio en la mayor parte del cuerpo** (regiones plegadas con alta confianza, pLDDT >80), **cyan/turquesa** en bordes (~70–80), **amarillo** en algunos giros y loops (~50–70), y **manchas naranja-rojo** en los extremos N- y C- terminales (regiones probablemente desordenadas, pLDDT <50). El predominio azul muestra que el core de la proteína es muy confiable; los apéndices "colgantes" son los que el modelo marca como inciertos.
  - Why it matters: Es **exactamente** el output canónico de AlphaFold DB. Comunica dos cosas al alumno con una sola figura: (1) el tipo de visualización 3D que devuelve la base (cartoon, no surface ni sticks); (2) que AF2 no escupe una estructura ciega — viene con una **medida de confianza per-residuo** que dice al usuario qué partes creer y cuáles no. El slide debería mostrar la imagen + una mini-leyenda del color (azul = alta confianza, naranja = baja).
  - Transcribed text: (sin texto sobre la imagen — render limpio sin etiquetas, leyenda ni ejes)

## Raw / preserved excerpts

(N/A — image stub.)

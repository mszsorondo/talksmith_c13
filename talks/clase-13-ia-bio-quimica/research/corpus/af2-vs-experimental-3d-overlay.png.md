---
source_file: af2-vs-experimental-3d-overlay.png
source_type: image
ingested_at: 2026-05-26
---

# AF2 vs experimental — dos estructuras 3D superpuestas (CASP14)

## Provenance
- Original location: research/articles/af2-vs-experimental-3d-overlay.png
- Format: PNG (~189KB)
- Author / source (if known): Nature (figura del editorial CASP14 / AF2), republicada en francis.naukas.com
- Date of original (if known): Diciembre 2020

## Key claims

Imagen de **dos targets específicos de CASP14** mostrados con la predicción de AF2 (azul) y la estructura experimental (verde) **superpuestas**. La superposición casi indistinguible es la evidencia visual del salto AF2 que comunica el slide: la predicción no es "buena" — es prácticamente equivalente a la verdad experimental.

Los dos targets identificados en la imagen:
- **T1037 / PDB 6vr4** — *RNA polymerase domain* — GDT_TS = **90.7**.
- **T1049 / PDB 6y4f** — *adhesin tip* — GDT_TS = **93.3**.

Es exactamente la imagen que la teórica pide en el marcador `[IMAGEN SUGERIDA]` de la sección "AlphaFold 2 (2020) — el salto":

> dos estructuras 3D superpuestas — predicción de AF2 vs estructura experimental — casi indistinguibles. Subtítulo: GDT_TS ~92.

Los dos GDT_TS específicos (90.7 y 93.3) refuerzan el número "~92" que se cita en prosa.

Originalmente no estaba en la lista del presenter (la describió como "no encuentro"); apareció en la misma página de naukas.com que la otra figura CASP14.

Slide objetivo: **Sección 2 — "AlphaFold 2 (2020) — el salto"**.

## Definitions and terminology

(N/A.)

## Evidence and examples

- **T1037 GDT = 90.7** — RNA polymerase domain (PDB 6vr4).
- **T1049 GDT = 93.3** — adhesin tip (PDB 6y4f).
- Promedio aproximado de los dos = ~92 — soporta directamente el número "~92" citado en prosa en la teórica.

## Inconsistencies / open questions

- Ningúna; los targets quedaron identificados explícitamente al transcribir la imagen (T1037 y T1049). Si se quiere mostrar los nombres en el slide, ya está toda la información.

## Images / diagrams

- **af2-vs-experimental-3d-overlay.png/images/af2-vs-experimental-3d-overlay.png** — Dos targets CASP14 (T1037 + T1049): predicción AF2 (azul) superpuesta a estructura experimental (verde), casi indistinguibles
  - Depiction: Composición horizontal en dos paneles sobre fondo gris claro. **Panel izquierdo**: render cartoon de una proteína plegada compleja, mezcla de alfa-hélices y láminas-beta, con **dos capas superpuestas en azul (AF2) y verde (experimental)** prácticamente coincidentes — los giros de hélice y las flechas-beta de ambas vistas se solapan punto por punto. Debajo, en texto negro: *"T1037 / 6vr4 — 90.7 GDT"* y entre paréntesis *"(RNA polymerase domain)"*. **Panel derecho**: render cartoon de una proteína más pequeña, dominada por **láminas-beta apiladas en un sandwich-fold** (forma característica de adhesinas / dominios beta), también con doble capa azul-verde casi indistinguible. Debajo: *"T1049 / 6y4f — 93.3 GDT"* y *"(adhesin tip)"*. Sin escala, sin ejes, sin leyenda explícita del código de color (el viewer asume azul=predicción, verde=experimental por convención del editorial Nature).
  - Why it matters: La métrica GDT_TS ~92 es abstracta para el alumno — un número en un eje. **Esta imagen es el número hecho carne**: dos proteínas reales, dos casos del torneo CASP14, predicción y verdad uno encima del otro, y lo que se ve es **lo mismo dos veces**. Es la prueba visual de que "resuelto" no es jerga académica. Además, mostrar dos targets con folds estructuralmente distintos (alfa-beta mixto + beta-sandwich) ayuda a comunicar generalización: no es que AF2 acierte un tipo de plegado y falle otro — acierta los dos.
  - Transcribed text:
    - Panel izquierdo: "T1037 / 6vr4" — "90.7 GDT" — "(RNA polymerase domain)"
    - Panel derecho: "T1049 / 6y4f" — "93.3 GDT" — "(adhesin tip)"

## Raw / preserved excerpts

(N/A — image stub.)

---
source_file: AIG4B-Clase-13-IA-Bio-Quimica-Practica-Resuelta.ipynb
source_type: article
ingested_at: 2026-05-26
---

# Clase 13 — Práctica resuelta: GCN sobre BBBP + VAE/difusión SMILES + ESMFold

## Provenance
- Original location: research/articles/AIG4B-Clase-13-IA-Bio-Quimica-Practica-Resuelta.ipynb
- Format: ipynb (Jupyter notebook, 48 cells: 27 code + 21 markdown; sin outputs ejecutados)
- Author / source (if known): Marco Sanchez Sorondo y Paulo Veiga (Universidad Austral)
- Date of original (if known): Mayo 2026

## Key claims

**Estructura general** — tres ejercicios prácticos, uno por cada bloque conceptual de la teórica:

1. **Ejercicio 1 — GCN sobre BBBP (clasificación binaria de penetración hematoencefálica).**
   - Pipeline: descargar BBBP → filtrar SMILES válidos (RDKit) → featurización SMILES→grafo PyG → split estratificado 70/15/15 → entrenar GCN → evaluar.
   - Features de átomo: tipo atómico (one-hot), grado, carga formal, hibridación, aromaticidad, número H, en ciclo.
   - Modelo: GCN simple (2–3 capas) + global pooling + MLP head.
   - Métricas: AUC ROC + accuracy; "===  SOLUCIÓN ===" en 3 celdas (probablemente: train loop, eval loop, métricas).
   - Cierra con 1 celda de **preguntas conceptuales 1.1** (cell 16) + solución (cell 17 con comentario HTML `<!-- SOLUCIÓN -->`).

2. **Ejercicio 2 — VAE de SMILES + comparación con difusión latente.**
   - Carga dataset (cell 19 — `urllib.request`), define tokenizer + VAE (encoder LSTM/GRU + decoder autoregresivo + bottleneck latente).
   - Entrenamiento con **free bits + KL annealing** (cell 24) — manejo del posterior collapse típico del VAE.
   - Helper de muestreo autoregresivo desde z (cell 25).
   - Métricas explícitas: **validez, unicidad, novedad** (cell 26) — set canónico contra train.
   - 5 celdas "=== SOLUCIÓN ===" (cells 29–33) — probablemente: muestreo baseline N(0,I), modelo de difusión sobre z, entrenamiento del difusor, muestreo con difusión, evaluación comparativa.
   - **Preguntas conceptuales 2.1** (cell 34) + solución (cell 35).

3. **Ejercicio 3 — ESMFold (predicción de estructura de proteínas).**
   - Imports `transformers` + `EsmForProteinFolding` (cell 37) — modelo de HuggingFace.
   - Define 3 proteínas de prueba con tamaños y composiciones distintas (cell 38).
   - Helper provisto: predecir estructura + visualizar (cell 40, `@torch.no_grad()`).
   - 3 celdas "=== SOLUCIÓN ===" (cells 42–44) — predicción + análisis.
   - **Preguntas conceptuales 3.1** (cell 45) + solución (cell 46).

**Soporte para alumnos** — el notebook es la **versión resuelta**. Las celdas marcadas `# === SOLUCIÓN ===` y los bloques `<!-- SOLUCIÓN -->` corresponden a partes que el alumno completaría en la versión sin resolver. Para la práctica en clase se distribuiría una versión sin esas resoluciones.

## Definitions and terminology

- **BBBP** (Blood-Brain Barrier Penetration): dataset binario `p_np` (penetra / no penetra). Reutiliza el contexto de la teórica.
- **PyG (PyTorch Geometric)**: librería estándar para GNNs en PyTorch; `Data(x, edge_index, edge_attr, y)`.
- **RDKit**: librería estándar para cheminformatics; parseo SMILES, filtrado, canonización, fingerprints.
- **Free bits**: técnica para mitigar posterior collapse — exime una cuota mínima de KL por dimensión latente.
- **KL annealing**: rampa de `β_KL` desde 0 hasta 1 a lo largo del entrenamiento, para que el decoder aprenda a reconstruir antes de exigirle KL.
- **Validez / unicidad / novedad** (metrics de generación molecular):
  - validez = % de SMILES sampleados que son parseables por RDKit;
  - unicidad = % distintos dentro del batch generado;
  - novedad = % no presentes en el train set (canonicalizado).
- **EsmForProteinFolding**: HuggingFace wrapper alrededor de ESMFold (Meta AI).

## Evidence and examples

- **Cell 06** filtra SMILES inválidos con RDKit antes de featurizar.
- **Cell 11** hace `train/val/test 70/15/15` estratificado por `p_np` para BBBP.
- **Cell 13–15** son las tres celdas de solución del Ejercicio 1.
- **Cell 21** declara la config del VAE (probablemente: vocab_size, hidden_dim, latent_dim, max_len).
- **Cell 24** combina **free bits + KL annealing** — dos técnicas estándar contra posterior collapse, importante mencionarlas si se explican.
- **Cell 27** construye `train_set_canon = set()` para medir novedad post-canonicalización.
- **Cell 38** corre ESMFold sobre tres proteínas distintas — pensadas para mostrar variabilidad en confianza y tamaño.
- **Cell 40** usa `@torch.no_grad()` (inferencia sin gradientes — práctica obligada con LLMs proteicos).

## Inconsistencies / open questions

- El notebook **no tiene outputs ejecutados** (sin imágenes, sin tablas, sin pesos guardados). La versión que ven los alumnos en clase debería ser la "Resuelta-ejecutada" (267KB en el directorio original) o requerir ejecución en vivo.
- No queda explícito en el notebook **qué pesos pre-entrenados** se usan en el Ejercicio 2 (¿se entrena el VAE desde cero en clase? ¿hay checkpoint?) — la celda 19 hace `urllib.request` pero el detalle no aparece en el outline.
- No queda explícito cuál es **el dataset de pre-entrenamiento del VAE** (¿ZINC? ¿ChEMBL? ¿el mismo BBBP?). Importante para slides que comparen baseline VAE vs difusión.
- ESMFold corre localmente: dependiendo del hardware del aula puede ser lento (~minutos por proteína). Conviene anticipar.

## Images / diagrams

Sin imágenes embebidas en el notebook (`embedded_images=0` confirmado por inspección programática). La versión `Resuelta-ejecutada` del directorio original (267KB) sí tendría plots matplotlib post-ejecución; si se necesita un screenshot de output para slide (ej. la curva de loss del VAE, las moléculas sampleadas, la estructura ESMFold), debe ejecutarse el notebook primero.

## Raw / preserved excerpts

### Outline de cells (verbatim por primera línea)

```
[00 md]   # Clase 13 — IA aplicada a problemas biológicos y químicos · versión resuelta
[01 md]   ## Setup
[02 code] import sys, subprocess
[03 code] import torch
[05 code] # Descargar dataset BBBP
[06 code] # Filtrar SMILES válidos
[07 md]   ### Visualización: 4 moléculas
[08 code] samples_pos = df[df["p_np"] == 1].sample(2, random_state=0)
[09 md]   ### Featurización: SMILES → grafo PyG
[10 code] ATOM_FEATURES = {
[11 code] # Split train/val/test estratificado 70/15/15
[13-15 code] # === SOLUCIÓN ===  (×3)
[16 md]   ### Preguntas conceptuales — Ejercicio 1.1
[17 md]   <!-- SOLUCIÓN -->
[19 code] import os, random, urllib.request
[20 md]   ### Arquitectura del VAE de SMILES
[21 code] # Configuración del VAE
[22 code] # Arquitectura VAE
[23 md]   ### Entrenamiento del VAE
[24 code] # Loss con free bits + KL annealing
[25 code] # Helper de muestreo del VAE (autoregresivo desde z)
[26 md]   ### Métricas: validez, unicidad, novedad
[27 code] train_set_canon = set()
[29-33 code] # === SOLUCIÓN ===  (×5)
[34 md]   ### Preguntas conceptuales — Ejercicio 2.1
[35 md]   <!-- SOLUCIÓN -->
[37 code] from transformers import AutoTokenizer, EsmForProteinFolding
[38 code] # Tres proteínas con tamaños y composiciones estructurales distintas
[39 md]   ### Helper provisto: predecir estructura + visualización
[40 code] @torch.no_grad()
[42-44 code] # === SOLUCIÓN ===  (×3)
[45 md]   ### Preguntas conceptuales — Ejercicio 3.1
[46 md]   <!-- SOLUCIÓN -->
```

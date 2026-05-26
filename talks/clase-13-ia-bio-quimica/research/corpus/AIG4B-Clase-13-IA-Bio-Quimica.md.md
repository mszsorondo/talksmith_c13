---
source_file: AIG4B-Clase-13-IA-Bio-Quimica.md
source_type: article
ingested_at: 2026-05-26
---

# Clase 13: IA aplicada a problemas biológicos y químicos (teórica)

## Provenance
- Original location: research/articles/AIG4B-Clase-13-IA-Bio-Quimica.md
- Format: markdown
- Author / source (if known): Marco Sanchez Sorondo y Paulo Veiga (Universidad Austral, Facultad de Ingeniería)
- Date of original (if known): Mayo 2026

## Key claims

**Contexto / cambio de era**
- Hasta hace poco, biología/química/física estaban fuera del alcance de la IA generativa, que vivía en "lenguaje y píxeles".
- En 2020 AlphaFold 2 ganó CASP14 y **resolvió** el problema del plegamiento de proteínas — un problema abierto desde 1972 (Anfinsen).
- En 2024 el Nobel de Química fue para Hassabis + Jumper (DeepMind, AlphaFold) y Baker (UW, diseño computacional). **Primera vez** que el Nobel premia un método cuyo core es una red neuronal entrenada.
- Hoy la IA está moviendo dominios estancados hace décadas: plegamiento, clima (GraphCast), materiales (GNoME), drug design (RFdiffusion, DiffDock).

**Plegamiento de proteínas**
- Una proteína es una cadena de aminoácidos (20 tipos). Cuerpo humano: cientos de miles distintas.
- Tres niveles: secuencia (texto, barato) → estructura 3D (caro, cristalografía/crio-EM) → función (años de biología).
- **La estructura 3D determina la función.**
- Cuello de botella histórico: secuencias hay millones; estructuras en PDB ~200.000.
- Aplicaciones del plegamiento resuelto: drug discovery, enfermedades genéticas, diseño de enzimas, biología básica.
- CASP (1994 en adelante) es el torneo bianual; métrica GDT_TS (% átomos correctamente posicionados).
- Pre-2018 el mejor GDT_TS rondaba ~40; lejos de utilidad clínica.

**Evolución AlphaFold**
- **AF1 (CASP13, 2018):** CNN que predice mapa de distancias 2D, reconstrucción geométrica clásica. Gana CASP13 pero **no resuelve** el problema. Breakthrough conceptual: el deep learning puede atacar el plegamiento.
- **AF2 (CASP14, 2020):** GDT_TS ~92. **Resuelve** el problema. Tres ideas conceptuales clave:
  1. Información evolutiva profunda vía **MSA (multiple sequence alignment)** — coevolución de posiciones implica proximidad 3D.
  2. **Refinamiento iterativo** de dos representaciones en paralelo (secuencia + relaciones por pares de residuos), actualizadas alternadamente.
  3. **Salida geométrica con simetrías físicas** (predice geometrías locales respetando rotaciones/traslaciones) en lugar de coordenadas crudas.
- **ESMFold (Meta AI, 2022):** ESM-2 es un LLM de proteínas (~15B params) entrenado sobre 200M secuencias predict-next-amino-acid. ESMFold = ESM-2 + cabeza estructural. ~60× más rápido que AF2 (sin MSA), precisión cercana. Breakthrough conceptual: **la información evolutiva puede vivir internalizada en un LLM**, no necesita venir explícita en un alineamiento.
- **AF3 (2024):** generaliza a complejos (proteína + ligando + ADN/ARN + iones). El módulo final es un **modelo de difusión** que genera coordenadas 3D desde ruido. Breakthrough conceptual: **el mismo paradigma de Stable Diffusion aplicado a moléculas 3D**.

**Recursos abiertos**
- AlphaFold DB: ~200 millones de estructuras predichas sobre UniProt, libres en `alphafold.ebi.ac.uk`. Pre-2020 PDB tenía ~200.000.
- Aplicaciones en producción hoy: drug discovery (binding sites), diseño de enzimas (Baker lab — degradación de plásticos, vacunas, sensores), anticuerpos terapéuticos, enfermedades raras (efecto de mutaciones).
- No reemplaza experimento — filtra y prioriza candidatos.

**Limitaciones honestas de AlphaFold**
- Estructura estática promedio: no captura dinámica conformacional (apertura/cierre de bolsillos).
- Mutaciones puntuales: efecto fino muchas veces por debajo de la resolución del modelo.
- No conoce condiciones fisiológicas (pH, temperatura, iones, entorno celular).
- Proteínas intrínsecamente desordenadas: AF no las representa bien.

**Representaciones moleculares**
- Tres estándares: **SMILES** (string, ej. cafeína = `CN1C=NC2=C1C(=O)N(C(=O)N2C)C`), **grafo molecular** (átomos=nodos, enlaces=aristas), **fingerprint** (vector binario ~2048 bits).
- SMILES: legible, formato estándar (ZINC, ChEMBL, PubChem), input natural para modelos secuenciales. Limitación: no canónico por defecto (varias formas para la misma molécula).
- Grafos: estructura sin ambigüedad, simetrías explícitas. Input correcto para GNNs.
- Fingerprints: rápidos para búsqueda (Tanimoto), pero vector fijo, no se adapta.

**GNNs para predicción de propiedades**
- **Message passing**: cada nodo actualiza su representación combinando información de sus vecinos. k capas = información a distancia k.
- Pooling global (suma/promedio) → MLP final → predicción.
- Variantes: GCN (Kipf 2016, simple, promedio), GIN (Xu 2018, suma+MLP, más expresivo), MPNN (Gilmer 2017, generalización con features de enlaces).
- Aplicaciones industriales: toxicidad, solubilidad, ADMET, binding affinity.
- En la práctica: GCN sobre **BBBP (Blood-Brain Barrier Penetration)** — predicción crítica para fármacos del SNC (Alzheimer, Parkinson, depresión, dolor crónico).

**Generación de moléculas**
- Espacio drug-like ~10⁶⁰ — no enumerable.
- **VAE de SMILES (2018, paradigma clásico):** encoder SMILES → z (~64-D); decoder z → SMILES. Muestreo `z ~ N(0,I)` cae en zonas vacías del latente → SMILES inválidos.
- **Difusión latente (paradigma actual):** difusión sobre el latente del VAE en lugar de muestreo ingenuo de N(0,I). Mismo paradigma que Stable Diffusion: cambia el dominio (moléculas en lugar de imágenes), no el método.
- Showcase en producción: **RFdiffusion** (Baker, 2023, proteínas de novo), **DiffDock** (MIT, 2023, docking), **AlphaFold 3** (módulo final de difusión).

**Síntesis (cierre)**
- Patrón común de los casos exitosos:
  1. Representación correcta del dominio (grafos, MSA, LLM, voxels, tokens de ADN).
  2. Arquitectura escalable (GNNs, transformers, difusión).
  3. Datos masivos abiertos (PDB, UniProt, ZINC, AF DB, ChEMBL).
- Otros dominios en la misma curva: GraphCast (clima), GNoME (2.2M cristales nuevos), single-cell genomics.
- Mensaje final: la IA generativa dejó de ser solo lenguaje e imágenes; cuando hay buena representación + arquitectura + datos, entra al dominio y lo cambia.

## Definitions and terminology

- **Aminoácido**: monómero de las proteínas. 20 tipos en el cuerpo humano.
- **Secuencia / estructura 3D / función**: los tres niveles de descripción de una proteína. La estructura determina la función.
- **CASP (Critical Assessment of Structure Prediction)**: torneo bianual desde 1994; predicción de estructuras recién resueltas no publicadas. CASP13 (2018) → AF1 gana; CASP14 (2020) → AF2 resuelve.
- **GDT_TS (Global Distance Test — Total Score)**: métrica de CASP, % de átomos correctamente posicionados respecto a la estructura experimental. Útil clínicamente desde ~90.
- **PDB (Protein Data Bank)**: base de datos histórica de estructuras experimentales (~200K).
- **MSA (Multiple Sequence Alignment)**: alineamiento de proteínas evolutivamente relacionadas. Información de coevolución → proximidad 3D.
- **ESM-2**: LLM de proteínas de Meta AI (~15B parámetros, 200M secuencias).
- **UniProt**: base universal de secuencias proteicas.
- **AlphaFold DB**: ~200M estructuras predichas por AF2 sobre UniProt, libre en `alphafold.ebi.ac.uk`.
- **SMILES (Simplified Molecular-Input Line-Entry System)**: string que codifica una molécula con gramática específica.
- **Fingerprint molecular**: vector binario fijo, 1 = contiene cierta subestructura. Similitud de Tanimoto.
- **GNN (Graph Neural Network)**: red sobre grafos. Operación base = message passing.
- **GCN / GIN / MPNN**: variantes de GNN (promedio ponderado / suma+MLP / general con features de enlaces).
- **Pooling global**: agregación de representaciones de todos los nodos en un solo vector.
- **BBBP (Blood-Brain Barrier Penetration)**: dataset/tarea de clasificar si una molécula cruza la barrera hematoencefálica.
- **ADMET**: absorción, distribución, metabolismo, excreción, toxicidad — filtro estándar de drug discovery.
- **VAE (Variational Autoencoder)**: encoder → latente continuo → decoder; loss = reconstrucción + KL.
- **Latent diffusion**: difusión sobre el espacio latente de un autoencoder (paradigma de Stable Diffusion).
- **RFdiffusion / DiffDock**: aplicaciones de difusión a proteínas de novo / docking molecular.
- **Proteína intrínsecamente desordenada**: proteína sin estructura plegada estable por diseño.

## Evidence and examples

- **CASP14 GDT_TS:** AF2 promedió ~92, histórico ~40. Salto sin precedentes — gráfico CASP por edición desde 1994.
- **AlphaFold DB:** ~200M estructuras vs ~200K experimentales (1000× crecimiento).
- **ESMFold velocidad:** ~60× más rápido que AF2 al saltarse el MSA.
- **ESM-2 escala:** ~15B parámetros, 200M secuencias de entrenamiento.
- **VAE latente:** típicamente ~64 dimensiones.
- **Espacio drug-like:** ~10⁶⁰ moléculas estimadas.
- **GNoME:** 2.2M cristales nuevos estables descubiertos (Google, 2023).
- **Cafeína SMILES:** `CN1C=NC2=C1C(=O)N(C(=O)N2C)C` (ejemplo de representación textual).
- **Tabla niveles de proteína:** secuencia (DNA seq, rutina/barato) / estructura 3D (cristalografía-crio-EM, caro/meses) / función (biología experimental, años).
- **Tabla representaciones moleculares:** SMILES (string) / grafo (nodos+aristas) / fingerprint (vector binario ~2048 bits).

## Inconsistencies / open questions

- Ninguna detectada — el texto está internamente consistente. El propio autor surface limitaciones honestas de AF en la Sección 3 (dinámica conformacional, mutaciones puntuales, condiciones fisiológicas, proteínas desordenadas).
- Conexión explícita con Clase 9 (Stable Diffusion) no tiene cita formal — el lector que no haya cursado Clase 9 puede no captar el callback. Solucionable con una mini-recap en el slide de AF3 o el de difusión latente.

## Images / diagrams

El `.md` fuente **no contiene bytes de imagen** — la propia carpeta `research/articles/` tiene 4 archivos de imagen relacionados (ver records de imagen individuales). Lo que sí contiene son **15 marcadores `[IMAGEN SUGERIDA]`** en prosa, que son hints para el Illustrator del Paso 6 (no son referencias a archivos existentes). Los listo abajo para que el Editor en Step 4 sepa dónde sugerir asset vs. dónde pedir SVG generado:

### Marcadores `[IMAGEN SUGERIDA]` en el source (texto, no bytes)

1. **Intro:** foto Nobel 2024 al lado del gráfico CASP14 mostrando el salto AF2. → asset existe (`nobel-2024-hassabis-jumper-baker.jpg` + `casp14-gdt-ts-progression.png`).
2. **Mapa de la clase:** diagrama de dos columnas — Proteínas (cadena AA → 3D), Química (SMILES/grafo → propiedad o molécula generada). → SVG en Paso 6.
3. **Niveles de proteína:** misma proteína en secuencia → cinta plegada 3D → función ilustrada. → SVG en Paso 6.
4. **CASP por edición:** gráfico de barras GDT_TS 1994 → 2024 con salto en 2020. → asset existe (`casp14-gdt-ts-progression.png`).
5. **AF1 esquema:** entrada secuencia → mapa de distancias 2D → reconstrucción 3D. → SVG en Paso 6.
6. **AF2 comparación:** dos estructuras 3D superpuestas (predicción vs experimental), GDT_TS ~92. → asset existe (`af2-vs-experimental-3d-overlay.png`).
7. **ESMFold vs AF2:** comparativo AF2 (sec + MSA → struct) vs ESMFold (sec → LLM → struct) con cronómetro. → SVG en Paso 6.
8. **AF3 difusión:** secuencia de denoising — nube de átomos al azar → complejo proteína-ligando 3D limpio. → SVG en Paso 6.
9. **Nobel 2024:** foto oficial de los tres premiados. → asset existe (`nobel-2024-hassabis-jumper-baker.jpg`, ya cubierto en marcador 1).
10. **AF DB screenshot:** proteína consultada (3D + confianza por color). → asset existe (`alphafold-db-protein-Q8W3K0.webp`).
11. **Cafeína 3 representaciones:** SMILES + grafo 2D + fingerprint, lado a lado. → SVG en Paso 6.
12. **Message passing:** secuencia de 3 grafos mostrando propagación capa 1/2/3, color de intensidad. → SVG en Paso 6.
13. **VAE esquema:** encoder SMILES → z + decoder z → SMILES, pérdida (reconstrucción + KL). → SVG en Paso 6.
14. **VAE vs difusión latente:** dos pipelines superpuestos — N(0,I) directo vs difusión sobre el mismo VAE. → SVG en Paso 6.
15. **Showcase:** tres mini-figuras — RFdiffusion (proteína de novo) + DiffDock (complejo prot-lig) + AF3 (multi-cadena). → SVG en Paso 6.

(Conteo: 15 marcadores totales, 4 con asset existente, 11 pendientes de SVG en Paso 6. El marcador 1 reutiliza los archivos 4 y 9.)

## Raw / preserved excerpts

### Tabla — niveles de descripción de una proteína (verbatim)

| Nivel | Qué es | Cómo se obtiene |
|---|---|---|
| **Secuencia** | El texto: "MKTLW...AVGI" — qué aminoácidos y en qué orden | Secuenciación de ADN/proteína (rutina, barato) |
| **Estructura 3D** | La forma que adopta la cadena al plegarse en el espacio | Cristalografía / crio-EM (caro, meses, no siempre funciona) |
| **Función** | Qué hace la proteína en la célula | Experimentación biológica (años) |

### Tabla — representaciones moleculares (verbatim)

| Representación | Qué es | Ejemplo (cafeína) |
|---|---|---|
| **SMILES** | String de texto que codifica átomos y enlaces siguiendo una gramática | `CN1C=NC2=C1C(=O)N(C(=O)N2C)C` |
| **Grafo molecular** | Átomos como nodos, enlaces como aristas (estructura, no texto) | Diagrama 2D con átomos y bonds |
| **Fingerprint** | Vector binario fijo (~2048 bits): 1 si la molécula contiene cierta subestructura | `[0,1,0,1,1,0,...,0,1]` |

### Tabla — antes vs AlphaFold DB (verbatim)

| Antes (2020) | Después (AlphaFold DB) |
|---|---|
| ~200.000 estructuras experimentales en PDB | ~200.000.000 estructuras predichas |
| Décadas de trabajo de cristalografía | Predicciones en horas |
| Acceso restringido a proteínas "interesantes" | Cualquier proteína secuenciada en UniProt |

### Cierre — el patrón común (verbatim)

> Todos los casos que vimos hoy —AlphaFold, ESMFold, AF3, RFdiffusion, DiffDock, GNNs sobre BBBP, difusión latente sobre moléculas— comparten la misma receta:
>
> 1. Representación correcta del dominio. Grafos para moléculas, MSA o LLM para proteínas, voxels para imágenes médicas, secuencias de tokens para ADN. La elección de cómo le damos los datos al modelo es la mitad del problema.
> 2. Arquitectura escalable. GNNs, transformers, modelos de difusión. Arquitecturas que aprovechan estructura del dominio y escalan con compute y datos.
> 3. Datos masivos abiertos. PDB, UniProt, ZINC, AlphaFold DB, ChEMBL. La parte que la academia y la industria llevan décadas construyendo.

### Mensaje final (verbatim)

> La idea general que se llevan de esta clase: la IA generativa dejó de ser un tema solo de lenguaje e imágenes. Cuando hay buena representación, buena arquitectura y datos abiertos, entra al dominio que sea — y suele cambiarlo. Biología, química, física, materiales: están todos en distintos puntos de la misma curva.

# Inteligencia Artificial Generativa Aplicada en Biomedicina

## Clase 13: IA aplicada a problemas biológicos y químicos

Profesores: Marco Sanchez Sorondo y Paulo Veiga
Última modificación: Mayo 2026

---

# Tabla de contenidos

1. Intro: el cambio de era
2. El problema del plegamiento de proteínas
3. La evolución de AlphaFold — breakthroughs conceptuales
4. Impacto y recursos abiertos
5. Cómo representamos moléculas
6. GNNs para predicción de propiedades
7. Generación de moléculas: VAE y difusión
8. Cierre, síntesis y horizontes

---

# Sección 0

## Intro: el cambio de era

---

# Hasta hace poco, ciencias duras y IA estaban en mundos distintos

La ola de IA generativa que vimos en este curso —GPT, Stable Diffusion, agentes— vive en **lenguaje y píxeles**. Las **ciencias duras** —biología, química, física— eran territorio aparte: otro vocabulario, otras representaciones, sin datasets gigantes tipo internet.

Dos eventos marcaron que eso cambió:

- **2020** — AlphaFold 2 gana CASP14 y **resuelve** el plegamiento de proteínas, un problema abierto hace 50 años.
- **2024** — Nobel de Química a Hassabis, Jumper y Baker. Primera vez que se premia un trabajo cuyo método principal es una red neuronal entrenada.

Hoy la IA está resolviendo problemas que estaban estancados hace décadas: plegamiento, predicción meteorológica (GraphCast), síntesis de materiales (GNoME), diseño de drugs (RFdiffusion, DiffDock).

> **[IMAGEN SUGERIDA]:** foto del Nobel 2024 (Hassabis, Jumper, Baker) al lado del gráfico CASP14 mostrando el salto de AF2.

---

# Mapa de la clase

**Primera mitad — Proteínas.** El problema del plegamiento y la evolución de AlphaFold desde 2018. Contamos los breakthroughs conceptuales, no los detalles arquitectónicos.

**Segunda mitad — Química.** Cómo se representa una molécula para una red neuronal. GNNs para predicción de propiedades. VAE y difusión para diseñar moléculas nuevas. La práctica cae sobre esta mitad.

> **[IMAGEN SUGERIDA]:** diagrama de dos columnas — izquierda "Proteínas" (cadena de aminoácidos → estructura 3D), derecha "Química" (SMILES/grafo → propiedad o molécula generada).

---

# Sección 1

## El problema del plegamiento de proteínas

---

# ¿Qué es una proteína?

Una proteína es una cadena lineal de **aminoácidos** (20 tipos posibles, cada uno con propiedades químicas distintas). El cuerpo humano tiene cientos de miles de proteínas distintas: enzimas, anticuerpos, receptores, hormonas, transportadores.

Tres niveles importantes para entender el problema:

| Nivel | Qué es | Cómo se obtiene |
|---|---|---|
| **Secuencia** | El texto: "MKTLW...AVGI" — qué aminoácidos y en qué orden | Secuenciación de ADN/proteína (rutina, barato) |
| **Estructura 3D** | La forma que adopta la cadena al plegarse en el espacio | Cristalografía / crio-EM (caro, meses, no siempre funciona) |
| **Función** | Qué hace la proteína en la célula | Experimentación biológica (años) |

La **estructura 3D determina la función**: si dos proteínas tienen formas distintas, hacen cosas distintas, aunque las secuencias se parezcan.

> **[IMAGEN SUGERIDA]:** la misma proteína mostrada en sus tres niveles — secuencia de letras → diagrama de cinta plegada en 3D → ilustración de su función (ej. enzima cortando un sustrato).

---

# Por qué importa resolver el plegamiento

Si pudiéramos predecir la estructura 3D **directamente desde la secuencia**, ahorramos años y millones de dólares en cada problema biológico:

- **Drug discovery:** la mayoría de los fármacos funcionan uniéndose a una proteína. Sin la estructura 3D, no se puede diseñar bien.
- **Enfermedades genéticas:** una mutación cambia un aminoácido, y la proteína se pliega mal. Ver la estructura explica por qué falla.
- **Diseño de enzimas:** crear proteínas nuevas a medida (vacunas, biocombustibles, plásticos biodegradables).
- **Biología básica:** muchas proteínas humanas todavía no tienen función conocida. La estructura es la primera pista.

**El cuello de botella histórico:** secuencias hay millones, estructuras experimentales (PDB) apenas ~200 mil. La inmensa mayoría de las proteínas nunca tuvieron su estructura resuelta.

---

# 50 años de problema abierto

El plegamiento fue planteado como problema en **1972** (Anfinsen, Nobel de Química): "la secuencia contiene toda la información necesaria para determinar la estructura". Es decir: en principio, deberíamos poder predecirla por computadora.

Pero **no se podía**. Décadas de intentos con física (simulación de dinámica molecular), homología (copiar de proteínas parecidas con estructura conocida), y heurísticas de fragmentos. Mejoras lentas, sin solución.

Desde 1994 existe **CASP** (Critical Assessment of Structure Prediction): un torneo bianual donde los equipos predicen estructuras de proteínas recién resueltas en el laboratorio (todavía no publicadas), y se compara contra el resultado real. La métrica clave es **GDT_TS**: porcentaje de átomos correctamente posicionados respecto a la estructura experimental.

Hasta CASP13 (2018), el mejor equipo apenas alcanzaba GDT_TS ~40 — muy lejos de ser útil clínicamente. La sensación era que **el problema era irresoluble** sin órdenes de magnitud más de datos.

Después llegó AlphaFold.

> **[IMAGEN SUGERIDA]:** gráfico de barras mostrando el mejor GDT_TS por edición de CASP (1994 → 2024). Crecimiento lento hasta 2018, salto enorme en 2020 con AF2 (~92).

---

# Sección 2

## La evolución de AlphaFold — breakthroughs conceptuales

---

# AlphaFold 1 (2018) — entra deep learning al problema

DeepMind aparece en CASP13 (2018) con un enfoque distinto: en vez de simulación física o homología, **una red neuronal**. CNN que predice un **mapa de distancias** —matriz de cuán cerca está cada par de aminoácidos— y a partir de ahí se reconstruye la geometría 3D.

Resultado: gana CASP13 con margen, pero **no resuelve** el problema. GDT_TS subió pero seguía lejos de la utilidad clínica. La estructura final venía de pasos clásicos de optimización física, no del modelo.

**Breakthrough conceptual:** después de décadas de física pura, demostró que **el plegamiento se puede atacar con redes neuronales**. Cambió el ánimo de la comunidad: ya no era cuestión de si el deep learning iba a entrar, sino cuándo iba a resolverlo.

> **[IMAGEN SUGERIDA]:** esquema de AF1 — entrada secuencia, salida mapa de distancias 2D, reconstrucción 3D.

---

# AlphaFold 2 (2020) — el salto

CASP14 (2020). DeepMind vuelve con AF2 y **resuelve** el plegamiento para la mayoría de proteínas. GDT_TS promedio ~92, cuando lo histórico era ~40. La comunidad declaró el problema "solved".

Tres ideas clave —al nivel conceptual, sin entrar en la arquitectura interna— que hicieron posible el salto:

1. **Información evolutiva profunda.** El modelo no recibe solo la secuencia; recibe un **alineamiento múltiple (MSA)** de proteínas evolutivamente relacionadas. Las posiciones que mutan juntas a lo largo de la evolución suelen estar cerca en 3D — es información estructural escondida en la historia evolutiva.

2. **Refinamiento iterativo de dos representaciones.** El modelo mantiene dos vistas en paralelo (la secuencia y las relaciones entre pares de residuos) y las actualiza alternadamente, cada una informando a la otra. La estructura emerge de ese diálogo iterativo.

3. **Salida geométrica con simetrías físicas.** El modelo no predice coordenadas crudas — predice geometrías locales respetando las simetrías del espacio 3D (rotaciones, traslaciones). Esto le saca al modelo el trabajo de "aprender" cosas que ya sabe la física.

> **[IMAGEN SUGERIDA]:** dos estructuras 3D superpuestas — predicción de AF2 vs estructura experimental — casi indistinguibles. Subtítulo: GDT_TS ~92.

---

# ESMFold (2022) — ¿hace falta el MSA?

El MSA es caro y lento: hay que buscar proteínas relacionadas en bases de datos de millones de secuencias, alinearlas, y eso tarda minutos por proteína. ¿Se puede prescindir?

Meta AI entrenó **ESM-2**, un **modelo de lenguaje gigante de proteínas** (transformer, ~15 mil millones de parámetros) sobre 200 millones de secuencias — sin estructuras, sin MSA, solo predecir el próximo aminoácido. El modelo aprende implícitamente las regularidades evolutivas a través del entrenamiento masivo.

**ESMFold** = ESM-2 + un módulo final que predice estructura. Resultado: precisión cercana a AF2, pero **60 veces más rápido** porque no hay que armar MSA. Posibilita predecir cientos de millones de estructuras a escala.

**Breakthrough conceptual:** la información evolutiva no tiene que venir explícita en un alineamiento — puede estar **internalizada en un LLM** entrenado masivamente.

> **[IMAGEN SUGERIDA]:** diagrama comparativo: AF2 (secuencia + MSA → estructura) vs ESMFold (secuencia → LLM → estructura), con un cronómetro mostrando la diferencia de tiempo.

---

# AlphaFold 3 (2024) — generalización con difusión

AF2 predice estructuras de **proteínas solas**. Pero en biología real, una proteína casi nunca está sola: interactúa con drogas (ligandos pequeños), con ADN/ARN, con otras proteínas, con iones. Lo que importa clínicamente suele ser el **complejo**, no la proteína aislada.

AF3 (2024) generaliza el problema: una sola arquitectura predice estructuras de cualquier combinación de proteínas + ligandos + ácidos nucleicos + iones. El cambio técnico clave: el módulo final ya no es geométrico — es un **modelo de difusión** que genera coordenadas 3D iterativamente, partiendo de ruido.

**Breakthrough conceptual:** **el mismo paradigma de Stable Diffusion (Clase 9), aplicado a estructuras moleculares 3D**. La difusión resultó ser una arquitectura general para generar datos estructurados de alta dimensión, no solo imágenes. Cambia el dominio, no el método.

> **[IMAGEN SUGERIDA]:** secuencia de denoising — desde una nube de átomos al azar hasta un complejo proteína-ligando 3D limpio, en pasos sucesivos.

---

# Nobel de Química 2024

El Nobel de Química 2024 fue compartido entre:

- **Demis Hassabis y John Jumper** (DeepMind) — por AlphaFold.
- **David Baker** (University of Washington) — por diseño computacional de proteínas: dada una función deseada, generar una proteína nueva que la cumpla.

Es la **primera vez** que el Nobel premia un trabajo cuyo método principal es una red neuronal entrenada. Marca formalmente que la IA dejó de ser herramienta auxiliar para ser **el método** en problemas de biología estructural.

> **[IMAGEN SUGERIDA]:** foto oficial del Nobel 2024 con los tres premiados.

---

# Sección 3

## Impacto y recursos abiertos

---

# AlphaFold DB: 200 millones de estructuras, libres

DeepMind y EMBL-EBI corrieron AF2 sobre prácticamente **todas las proteínas conocidas en UniProt**. El resultado se llama **AlphaFold Protein Structure Database** y está abierto al público en `alphafold.ebi.ac.uk`.

| Antes (2020) | Después (AlphaFold DB) |
|---|---|
| ~200.000 estructuras experimentales en PDB | ~200.000.000 estructuras predichas |
| Décadas de trabajo de cristalografía | Predicciones en horas |
| Acceso restringido a proteínas "interesantes" | Cualquier proteína secuenciada en UniProt |

**Impacto inmediato:** investigadores en todo el mundo dejaron de tener que adivinar la estructura de la proteína que estudian — la buscan en la base y la usan como punto de partida.

> **[IMAGEN SUGERIDA]:** screenshot de la AlphaFold DB con una proteína consultada (vista 3D + nivel de confianza por color).

---

# Aplicaciones que ya están en producción

- **Drug discovery:** identificar bolsillos de unión (binding sites) en proteínas humanas y de patógenos, acelerar la búsqueda de fármacos candidatos.
- **Diseño de enzimas (Baker lab):** crear proteínas que no existen en la naturaleza, con función deseada — enzimas para degradar plásticos, vacunas estructuralmente diseñadas, sensores moleculares.
- **Anticuerpos terapéuticos:** modelar la interacción anticuerpo-antígeno antes de sintetizar nada en laboratorio.
- **Enfermedades raras:** explicar cómo una mutación específica desestabiliza la proteína de un paciente.

No reemplaza al experimento — todavía hay que validar en laboratorio. Pero **filtra y prioriza**: en vez de probar miles de candidatos a ciegas, se prueban decenas con justificación estructural.

---

# Limitaciones honestas

AlphaFold predice **una estructura estática promedio**. Eso deja afuera varias cosas que importan:

- **Dinámica conformacional.** Las proteínas reales se mueven, abren y cierran bolsillos, cambian de forma según con qué interactúan. AF da una foto, no un video.
- **Mutaciones puntuales.** El efecto fino de cambiar un solo aminoácido (típico en enfermedades genéticas) muchas veces queda por debajo del nivel de resolución del modelo.
- **Condiciones fisiológicas.** AlphaFold no sabe nada de pH, temperatura, concentración iónica, ni del entorno celular real.
- **Proteínas intrínsecamente desordenadas.** Hay proteínas que **no tienen** una estructura plegada estable — son desordenadas por diseño. AF no sabe representar eso bien.

**Conclusión clínica:** AlphaFold es un punto de partida fantástico, no una respuesta final. La validación experimental sigue siendo necesaria.

---

# Sección 4

## Cómo representamos moléculas

---

# Tres formas de representar la misma molécula

Antes de poder hacer IA con moléculas, hay que decidir cómo dárselas a la red neuronal. Hay tres representaciones estándar — cada una con sus ventajas:

| Representación | Qué es | Ejemplo (cafeína) |
|---|---|---|
| **SMILES** | String de texto que codifica átomos y enlaces siguiendo una gramática | `CN1C=NC2=C1C(=O)N(C(=O)N2C)C` |
| **Grafo molecular** | Átomos como nodos, enlaces como aristas (estructura, no texto) | Diagrama 2D con átomos y bonds |
| **Fingerprint** | Vector binario fijo (~2048 bits): 1 si la molécula contiene cierta subestructura | `[0,1,0,1,1,0,...,0,1]` |

La misma molécula, tres formas. Cada una sirve para tareas distintas.

> **[IMAGEN SUGERIDA]:** la molécula de cafeína mostrada en las tres representaciones lado a lado.

---

# Cuándo usar cada una

**SMILES** es legible y compacto — es el formato estándar para distribuir datos (ZINC, ChEMBL, PubChem). Como input para una red neuronal, sirve para **modelos secuenciales** (LSTM, transformers). Limitación: el mismo compuesto puede escribirse de varias formas (no es canónico por defecto).

**Grafos** capturan la estructura molecular tal como es: no hay ambigüedad de notación, las simetrías están explícitas. Es el input natural para **GNNs**, que veremos en la próxima sección. Es la representación correcta para predecir propiedades químicas.

**Fingerprints** son rápidos y fáciles de comparar (similitud de Tanimoto). Sirven para búsqueda rápida en bases de millones de moléculas (drug discovery clásico, antes de redes neuronales). Limitación: vector fijo y predefinido — no se adapta al problema.

**En la práctica de hoy**: vamos a usar **grafos** para predecir propiedades (Ejercicio 1) y **SMILES** como entrada/salida del modelo generativo (Ejercicio 2).

---

# Sección 5

## GNNs para predicción de propiedades

---

# Message passing: la idea central

Una **Graph Neural Network (GNN)** es una red que opera sobre grafos. La operación básica se llama **message passing** y es muy simple:

> Cada nodo (átomo) actualiza su representación combinando información de sus vecinos.

Después de **1 capa**, cada átomo "sabe" sobre sí mismo y sus vecinos directos. Después de **2 capas**, sobre sus vecinos de los vecinos. Después de **k capas**, sobre todo lo que está a distancia k en el grafo.

Al final, se agrega todo en un único vector (**pooling global**: promedio o suma sobre todos los nodos) y se pasa a una cabeza MLP que predice la propiedad final.

**Por qué funciona en moléculas:** las propiedades químicas dependen del entorno local (qué grupos funcionales hay, qué subestructuras), y eso es exactamente lo que el message passing captura.

> **[IMAGEN SUGERIDA]:** secuencia de 3 grafos mostrando cómo se propaga la información: capa 1 (nodo + vecinos), capa 2 (vecinos de vecinos), capa 3 (toda la molécula). Color de intensidad = info acumulada.

---

# GCN, GIN, MPNN — variantes del mismo patrón

Hay varias arquitecturas de GNN. Difieren en cómo combinan la información de los vecinos:

- **GCN** (Graph Convolutional Network, Kipf 2016) — promedio ponderado, simple y eficiente. La usamos en la práctica.
- **GIN** (Graph Isomorphism Network, Xu 2018) — suma + MLP, mayor poder expresivo, distingue grafos que GCN confunde.
- **MPNN** (Message Passing Neural Network, Gilmer 2017) — formulación general. Permite usar features de los enlaces, no solo de los nodos.

En este curso no vamos a entrar en las diferencias matemáticas — quedate con la intuición: **todas son la misma idea (message passing), con variantes en cómo se mezclan los mensajes**. GCN es la más simple, suficiente para nuestro problema.

---

# Aplicaciones y conexión con la práctica

Las GNNs sobre moléculas se usan industrialmente para predecir:

- **Toxicidad** (¿este compuesto es seguro?)
- **Solubilidad** (¿se disuelve en agua?)
- **ADMET** (absorción, distribución, metabolismo, excreción, toxicidad — el filtro clásico de drug discovery)
- **Binding affinity** (¿se une fuerte a esta proteína objetivo?)

**En la práctica de hoy** vamos a entrenar una GCN sobre el dataset **BBBP** (Blood-Brain Barrier Penetration): predecir si una molécula puede cruzar la barrera hematoencefálica. Es un problema crítico en el diseño de fármacos para el sistema nervioso central (Alzheimer, Parkinson, depresión, dolor crónico) — si la droga no cruza la BBB, no hay nada que hacer.

---

# Sección 6

## Generación de moléculas: VAE y difusión

---

# Por qué generar

Predecir propiedades de moléculas existentes (Sección anterior) es solo la mitad del problema. La otra mitad es **proponer moléculas nuevas** que cumplan propiedades deseadas.

El espacio de moléculas drug-like se estima en **~10⁶⁰** estructuras posibles. No se puede enumerar. La fuerza bruta no escala — necesitamos modelos generativos que aprendan la distribución de moléculas válidas y muestreen de ahí.

Dos paradigmas, separados por unos años:

- **VAE de SMILES** (2018) — el clásico de generación molecular.
- **Difusión** (2022 en adelante) — el paradigma actual, traído del mundo de imágenes.

En la práctica de hoy implementamos los dos y los comparamos directamente.

---

# VAE de SMILES — el paradigma clásico (2018)

Un **VAE** (Variational Autoencoder) aprende dos cosas en simultáneo sobre los SMILES de entrenamiento:

- Un **encoder** que mapea cada SMILES a un punto en un espacio latente continuo (vector de ~64 dimensiones).
- Un **decoder** que toma un punto del latente y reconstruye un SMILES.

Una vez entrenado, **muestreamos** moléculas nuevas: tomamos un vector al azar del latente (`z ~ N(0,I)`) y pasamos por el decoder. Si el VAE entrenó bien, esa muestra debería ser un SMILES válido y plausible.

**Problema clásico:** el espacio latente del VAE casi nunca se distribuye perfectamente como `N(0,I)`. Tiene huecos, modos, regiones vacías. Muestrear ciegamente de la normal cae muchas veces en zonas donde el decoder produce basura — SMILES sintácticamente inválidos o moléculas raras.

> **[IMAGEN SUGERIDA]:** esquema clásico del VAE — encoder (SMILES → z) + decoder (z → SMILES). Pequeña anotación de la pérdida (reconstrucción + KL hacia el prior).

---

# Difusión latente — el paradigma actual

La idea es la **misma que Stable Diffusion** (Clase 9): en vez de muestrear `z` ciegamente, entrenamos un **modelo de difusión sobre el espacio latente del VAE**.

El modelo de difusión aprende a generar **latentes que están en la distribución real de los datos**, no en `N(0,I)` ingenua. Cuando muestreamos con difusión y decodificamos, caemos en zonas que el decoder sabe manejar — y la validez sube.

Stable Diffusion hizo esto sobre imágenes: VAE de imágenes + difusión sobre el latente. **Acá hacemos exactamente lo mismo con un VAE de moléculas.** Cambia el dominio, no el paradigma.

**En la práctica de hoy**, este es el Ejercicio 2: comparar muestreo directo del VAE vs muestreo con difusión latente sobre el mismo VAE. Mismo decoder en los dos casos, distinta forma de elegir el `z`.

> **[IMAGEN SUGERIDA]:** dos pipelines superpuestos: (a) ruido N(0,I) → decoder VAE → SMILES (baseline); (b) ruido → modelo difusión → decoder VAE → SMILES (nuestro modelo).

---

# Showcase: lo que ya se está haciendo en producción

La difusión sobre estructuras moleculares no es solo un experimento académico — ya se usa en pipelines reales:

- **RFdiffusion (Baker lab, 2023)** — diseña **proteínas de novo** desde cero, con función deseada. Es uno de los métodos que llevó a Baker al Nobel 2024. Se usa para diseñar enzimas, vacunas, anticuerpos.
- **DiffDock (MIT, 2023)** — predice cómo se acopla un ligando (droga) a una proteína (docking molecular). Más rápido y preciso que los métodos clásicos.
- **AlphaFold 3 (2024)** — el módulo final es de difusión, predice estructuras de proteínas + ligandos + ADN/ARN.

**El patrón es claro:** difusión + representación adecuada del dominio = nuevo estándar para problemas estructurales en biología y química.

> **[IMAGEN SUGERIDA]:** tres mini-figuras: proteína de novo (RFdiffusion), complejo proteína-ligando (DiffDock), complejo multi-cadena (AF3).

---

# Sección 7

## Cierre, síntesis y horizontes

---

# El patrón común detrás de los casos exitosos

Todos los casos que vimos hoy —AlphaFold, ESMFold, AF3, RFdiffusion, DiffDock, GNNs sobre BBBP, difusión latente sobre moléculas— comparten la misma receta:

1. **Representación correcta del dominio.** Grafos para moléculas, MSA o LLM para proteínas, voxels para imágenes médicas, secuencias de tokens para ADN. La elección de cómo le damos los datos al modelo es la mitad del problema.
2. **Arquitectura escalable.** GNNs, transformers, modelos de difusión. Arquitecturas que aprovechan estructura del dominio y escalan con compute y datos.
3. **Datos masivos abiertos.** PDB, UniProt, ZINC, AlphaFold DB, ChEMBL. La parte que la academia y la industria llevan décadas construyendo.

Las tres juntas habilitaron el salto. Cuando un dominio nuevo cumple las tres, la IA generativa entra y cambia el juego.

---

# Limitaciones y horizonte

**Lo que no resuelve la IA por sí sola.** Los modelos generan candidatos —estructuras, moléculas, secuencias— pero la validación experimental sigue siendo necesaria. Predicción ≠ verdad biológica. Y los modelos heredan los sesgos de los datos: si una proteína es rara en PDB, la predicción será menos confiable.

**Otros dominios moviéndose al mismo ritmo.** No vimos hoy, pero parte del mismo movimiento:

- **Física aplicada:** GraphCast (Google, 2023) predice clima con precisión de modelos numéricos, 1000× más rápido. PINNs (Physics-Informed Neural Networks) para simulación.
- **Materiales:** GNoME (Google, 2023) descubrió 2.2 millones de cristales nuevos estables.
- **Single-cell genomics:** modelos tipo transformer sobre expresión génica para entender tipos celulares y enfermedades.

**La idea general que se llevan de esta clase:** la IA generativa dejó de ser un tema solo de lenguaje e imágenes. Cuando hay buena representación, buena arquitectura y datos abiertos, entra al dominio que sea — y suele cambiarlo. Biología, química, física, materiales: están todos en distintos puntos de la misma curva.

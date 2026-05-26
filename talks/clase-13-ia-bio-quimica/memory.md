# memory.md — clase-13-ia-bio-quimica

**Current step:** 7 — Learnings awaiting_presenter
**Awaiting:** 2026-05-26 — "Dos decisiones finales: (a) ¿Promover Talk a knowledge-library/? (b) ¿Render PPTX (Step 8)?"
**Topic:** Introducción al uso de IA en Biología y Química (Clase 13 del curso IA para Ingeniería Biomédica)
**Folder:** talks/clase-13-ia-bio-quimica/
**Started:** 2026-05-26

---

## Talk briefing

La idea de esta clase es introducir a los alumnos al uso de IA en Biología y Química

---

## 2026-05-26 — Step 1 (Frame)
- Status: complete
- Asks log:
  - 2026-05-26 — "¿De qué se trata esta clase? (free-text briefing)" → "La idea de esta clase es introducir a los alumnos al uso de IA en Biología y Química"
  - 2026-05-26 — "Folder name (kebab-case)" → "clase-13-ia-bio-quimica"
  - 2026-05-26 — "PPTX style" → "strict"
- What was decided: folder = `clase-13-ia-bio-quimica`; PPTX style = `strict` (clase recurrente de curso, uniformidad clase a clase); briefing minimalista — "introducir a los alumnos al uso de IA en Biología y Química".
- Key inputs: briefing del presenter; profile lleno con Subject = "IA para Ingeniería Biomédica. Universidad Austral, Facultad de Ingeniería", Presenter = "Marco Sanchez Sorondo y Paulo Veiga", consumo = clase presencial, audiencia = grado con Python/ML básico, duración = 120 min, lenguaje = Español por defecto.
- Files created/modified: config/profile.md (6 secciones completadas); talks/clase-13-ia-bio-quimica/{memory.md, research/{articles,llm-chats,web,corpus}/, images/, output/}
- Pending open questions: none

## 2026-05-26 — Step 2 (Collect)
- Status: complete
- Asks log:
  - 2026-05-26 — "¿Cómo querés traer las fuentes? (4 vías)" → "copiá los dos archivos de Clase 13"
  - 2026-05-26 — "¿Querés que haga exploración de fuentes asociadas útiles?" → "sí"
  - 2026-05-26 — "¿Qué fuentes adicionales traemos? (papers / clase 9 / imágenes / nada)" → "imágenes externas con URLs provistas"
  - 2026-05-26 — "URLs de imágenes pendientes (Nobel, AF DB, CASP, overlay 3D)" → URLs provistas; el overlay 3D fue completado por el agent al descubrir que vivía en la misma página naukas que el chart CASP14.
  - 2026-05-26 — "¿Bajamos los 7 papers troncales?" → "no"
  - 2026-05-26 — "¿Copiamos material de Clase 9?" → "no"
- What was decided: 6 fuentes en `research/articles/` — la teórica `.md`, el notebook `.ipynb` resuelto, y 4 imágenes (`nobel-2024-...jpg`, `alphafold-db-...webp`, `casp14-gdt-ts-progression.png`, `af2-vs-experimental-3d-overlay.png`). El overlay 3D fue un bonus encontrado por el agent. Papers troncales y material de Clase 9 quedan fuera por decisión explícita del presenter — el `.md` ya tiene los claims redactados con la profundidad deseada.
- Key inputs: 2 archivos copiados del directorio externo + 4 imágenes descargadas vía curl (URLs Infobae / alphafold.ebi.ac.uk / francis.naukas.com).
- Files created/modified: 6 archivos en `talks/clase-13-ia-bio-quimica/research/articles/`.
- Pending open questions: none

## 2026-05-26 — Step 3 (Corpus)
- Status: complete
- Asks log:
  - 2026-05-26 — "Phase 2 (transcripción de imágenes): Process now / Skip — text only / Defer" → "Process now (opción 1)"
- What was decided: Phase 1 produjo 6 corpus records con 4 image stubs (todos los image-type sources). Phase 2 transcribió las 4 imágenes — quedaron filled `Depiction` / `Why it matters` / `Transcribed text`. Las transcripciones también corrigieron 2 inexactitudes de Phase 1: la "foto" Nobel es en realidad una **ilustración oficial de Niklas Elmehed**, y el chart CASP cubre 2006→2020 (no 1994→2020). El record del overlay 3D agregó identificación de los dos targets: T1037/6vr4 (90.7 GDT) y T1049/6y4f (93.3 GDT).
- Key inputs: 6 fuentes en `research/articles/` + visión multimodal de las 4 imágenes.
- Files created/modified: 6 corpus records + 6 companion folders + 4 image bytes copiadas (`research/corpus/{AIG4B-Clase-13-IA-Bio-Quimica.md.md, AIG4B-Clase-13-IA-Bio-Quimica-Practica-Resuelta.ipynb.md, nobel-...md, alphafold-...md, casp14-...md, af2-...md}` + 6 carpetas companion).
- Pending open questions: none — todos los stubs `pending:` resueltos.

## 2026-05-26 — Step 4 (Draft)
- Status: awaiting_presenter
- Asks log:
  - 2026-05-26 — "Subtitle de la Clase 13 (per-Talk frontmatter, va en la portada bajo el Subject)" → "Clase 13 — Introducción a la IA en Biología y Química"
  - 2026-05-26 — "Fecha de la Clase 13 (per-Talk frontmatter)" → "27 de mayo de 2026"
  - 2026-05-26 — "Modo de Step 4: A (Interview) / B (Agent Draft) / C (Presenter Outline)" → "B (Agent Draft)"
  - 2026-05-26 — "Critical Q1: ¿La práctica corre en Colab o local?" → "Google Colab (GPU obligatoria; confirmado en cell 23 del notebook con la nota '~5-8 min con GPU, >1h en CPU')"
  - 2026-05-26 — "Critical Q2: ¿Versión sin resolver o resuelta?" → "Sin resolver — alumnos completan las celdas `=== SOLUCIÓN ===` y los bloques `<!-- SOLUCIÓN -->`"
  - 2026-05-26 — "Critical Q3: ¿Dataset de pre-entrenamiento del VAE?" → "ZINC 250k (subset 10k random, longitud 5-50) — confirmado por inspección directa de cell 19 del notebook; archivo del repo aspuru-guzik-group/chemical_vae"
  - 2026-05-26 — "¿Pasamos a Step 5 (Review)? — todas las critical questions resueltas, draft listo para feedback en draft.md" → "saltar review, polish (presenter declaró draft.md final sin feedback round)"

## 2026-05-26 — Step 5 (Review)
- Status: complete
- Asks log:
  - (sin rondas — presenter saltó Review directo a Polish; el draft pasó intacto)
- What was decided: Skip Review (Mode B draft + critical-Q resolution se aceptan tal cual; no feedback bullets autoreados, no rondas aplicadas).
- Key inputs: ninguno — paso vacío.
- Files created/modified: ninguno.
- Pending open questions: ninguno (los 3 originales se resolvieron en Step 4 antes del skip).

## 2026-05-26 — Step 5 (Review) — re-opened, additive change
- Status: complete
- Asks log:
  - 2026-05-26 — "Adición presenter: link distill.pub + diagrama abstracto de convolución parametrizada en sección GNNs" → "aplicado: nuevo slide 6.2 'Una convolución parametrizada' con ASCII abstracto (entrada → agregar → transformar W,b,σ → salida) + footer con link a distill.pub/2021/understanding-gnns; renumerado old 6.2 (GCN/GIN/MPNN) → 6.3, old 6.3 (Aplicaciones+BBBP) → 6.4."
- What was decided: cambio aditivo en `draft.md` — sección 6 (GNNs) crece de 3 a 4 slides. Total deck: 29 content + 2 conclusions = 31. La adición aprovecha la re-runnability de Step 6.
- Key inputs: solicitud directa del presenter; el link y el concepto vienen del presenter (distill.pub article — Daigavane, Ravindran, Aggarwal 2021).
- Files created/modified: `draft.md` editado (slide 6.2 nuevo + renumeración + Presenter feedback field agregado para schema compliance).
- Pending open questions: none.

## 2026-05-26 — Step 6 (Polish) — re-run tras adición
- Status: complete
- Asks log:
  - (sin asks — Polish corre end-to-end sin prompts)
- What was decided: `final.md` re-derivado de `draft.md` actualizado. **10 ASCII** ahora (era 9 + s6-2-1 nuevo); 9 idempotentes (sidecars unchanged, SVG/PNG existentes reutilizados), 1 nuevo (s6-2-1 `convolucion-parametrizada` clean after 1 revision — defecto `N(v)` label cross-fan-in corregido). 4 imágenes externas consolidadas (idempotente). 38 campos `Presenter feedback` strippeados de `final.md`. 0 `[open]` para rescatar.
- Key inputs: `draft.md` (intacto), corpus de imágenes en `research/corpus/`.
- Files created/modified:
  - `talks/clase-13-ia-bio-quimica/final.md` (873 líneas, derivado de draft)
  - `talks/clase-13-ia-bio-quimica/images/`: 9 SVGs + 9 PNGs + 9 .ascii sidecars + 4 imágenes externas (Nobel, AF DB, CASP14, AF2-overlay)
  - `talks/clase-13-ia-bio-quimica/images/.critique/`: 9 PNGs critique + 9 .md critique logs
- Pending open questions: ninguno.

## 2026-05-26 — Step 7 (Learnings)
- Status: awaiting_presenter
- Asks log:
  - 2026-05-26 — "Dos decisiones finales: (a) ¿Promover Talk a knowledge-library/? (b) ¿Render PPTX (Step 8)?" → pending
- What was decided: `feedback-backlog.md` está vacío (primera Talk del fork, sin rondas de feedback en esta sesión) → 0 patrones recurrentes para promover a `learnings.md`. Solo quedan las dos decisiones de cierre.
- Key inputs: `config/feedback-backlog.md` (vacío).
- Files created/modified: ninguno todavía.
- Pending open questions: <pending — depende de respuestas>
- What was decided: <pending>
- Key inputs: <pending>
- Files created/modified: <pending>
- Pending open questions: <pending>

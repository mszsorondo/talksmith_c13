# memory.md — clase-16-compliance-regulaciones-ia

**Current step:** 8 — Render PPTX in_progress
**Topic:** Compliance, regulaciones e infraestructura de IA aplicada a Ingeniería Biomédica
**Folder:** talks/clase-16-compliance-regulaciones-ia/
**Started:** 2026-06-16

---

## Talk briefing

Clase sobre compliance, regulaciones e infraestructura de IA aplicada a Ingeniería Biomédica.

Ángulo regulatorio/legal (HIPAA, Argentina) pero con mucha conciencia de infraestructura, proyectos.

Es teórica.

Al salir, los alumnos deben entender las implicancias y responsabilidades asociadas a desplegar sistemas informáticos y de IA en entornos biomédicos comunes.

---

## 2026-06-16 — Step 1 (Frame)
- Status: complete
- Asks log:
  - 2026-06-16 — "¿De qué va esta clase? (ángulo, tesis, formato, learning outcome)" → Ángulo regulatorio/legal (HIPAA, Argentina) con conciencia de infraestructura y proyectos; teórica; outcome = entender implicancias y responsabilidades de desplegar sistemas IT/IA en entornos biomédicos.
  - 2026-06-16 — "Nombre de carpeta + estilo PPTX" → clase-16-compliance-regulaciones-ia; strict.
- What was decided: Talk es la Clase 16 del curso, teórica, ángulo regulatorio/legal con foco en infraestructura. Carpeta `clase-16-compliance-regulaciones-ia`, estilo PPTX `strict`.
- Key inputs: Profile (Subject: IA para Ingeniería Biomédica, Austral). Briefing verbatim arriba.
- Files created/modified: memory.md; árbol de carpetas (research/{articles,llm-chats,web,corpus}, images/, output/).
- Pending open questions: none

## 2026-06-16 — Step 2 (Collect)
- Status: complete
- Asks log:
  - 2026-06-16 — "¿Cómo querés arrancar la recolección?" → exploremos (live exploration).
  - 2026-06-16 — "¿Capturo la exploración / seguimos / a Corpus?" → listo (capturar).
  - 2026-06-16 — "¿Traer fuentes oficiales / seguir explorando / a Corpus?" → traer fuentes oficiales (opción 1).
  - 2026-06-16 — "¿Confirmás las 5 URLs?" → confirmo.
- What was decided: Recolección por exploración en vivo (1 transcript) + 5 fuentes externas (1 oficial verbatim + 4 síntesis verificada porque los sitios gov bloquearon el fetch).
- Key inputs: Tesis y agenda candidata de 6 secciones; casos DeepMind/Royal Free e IDx-DR; eje hardware (nube/on-prem/edge) con IEC 60601/62304.
- Files created/modified:
  - research/llm-chats/explore-compliance-regulaciones-infra-2026-06-16.md
  - research/web/infoleg-ley-25326/ (oficial verbatim)
  - research/web/hhs-hipaa-deidentification/ (síntesis, needs_verification)
  - research/web/fda-samd/ (síntesis, needs_verification)
  - research/web/fda-idx-dr-clearance/ (síntesis, needs_verification)
  - research/web/ico-royal-free-deepmind/ (síntesis, needs_verification)
- Pending open questions: Cifras de las 4 fuentes-síntesis a confirmar contra texto oficial antes del slide final. Presenter hará un deep research externo para sumar más fuentes (se ingestarán y re-correrá Librarian si llegan).

## 2026-06-16 — Step 3 (Corpus)
- Status: complete
- Asks log:
  - 2026-06-16 — "¿Avanzo al Paso 3?" → si, actualiza memory y procede.
- What was decided: Librarian Phase 1 sobre las 6 fuentes. Sin imágenes → images_pending vacío, no se necesita Phase 2.
- Key inputs: 1 exploración (chat-export) + 5 web-captures. Fuente principal de estructura = la exploración.
- Files created/modified (research/corpus/):
  - explore-compliance-regulaciones-infra-2026-06-16.md.md (+ companion)
  - infoleg-ley-25326.web.md (texto oficial verbatim)
  - hhs-hipaa-deidentification.web.md (needs_verification)
  - fda-samd.web.md (needs_verification)
  - fda-idx-dr-clearance.web.md (needs_verification)
  - ico-royal-free-deepmind.web.md (needs_verification)
- Pending open questions: 4 records con needs_verification (cifras a confirmar contra texto oficial). Presenter trae deep research externo → ingestar + re-correr Librarian si llega antes del Draft.

## 2026-06-16 — Step 4 (Draft)
- Status: complete
- Asks log:
  - 2026-06-16 — "¿Esperás el deep research o arrancamos el Draft?" → pidió pre-draft resumido primero.
  - 2026-06-16 — Presenter pide agregar una SECCIÓN DEDICADA DE BUENAS PRÁCTICAS. → integrada en la estructura.
- What was decided: Pre-draft de 6 secciones presentado y validado vía exploración. Deep research externo (PDF, 24 págs.) llegó completo y se ingestó al corpus como fuente principal de contenido/cifras. Se agrega una sección de Buenas prácticas (checklist accionable por eje).
- Key inputs:
  - research/articles/Compliance de IA Biomédica.pdf + research/corpus/Compliance de IA Biomédica.pdf.md (fuente principal, ~96 fuentes citadas)
  - Resuelve los needs_verification previos; quedan 3 discrepancias menores a decidir en Draft (Art.21 vs 12; cifras IDx-DR; fechas "2026" vigentes vs propuestas).
- Files created/modified: research/corpus/Compliance de IA Biomédica.pdf.md; draft.md (Modo B — Agent Draft, 7 secciones + conclusiones, ~26 slides, 4 diagramas ASCII).
- Composer review (scope=full): 0 blockers, 2 majors (largo de títulos H1/H2 — aplicados vía Editor), 2 minors (split candidates 4.3 y 7.2 — monitorear en render).
- Pending open questions:
  - draft.md Open questions: fecha real de la clase; Art. 21 vs 12 (25.326); cifras IDx-DR; vigencia de fechas "2026"; slide 2.6 GDPR comprimible.
  - Minors diferidos: 5.3 (caminos+PCCP) y 8.2 (checklist denso) — partir solo si overflowan en render.
- 2026-06-17 — Presenter pidió: (1) hacer explícito el "¿anonimizar para qué?" en slide 2.2 [aplicado]; (2) agregar contenido de prompt security (https://aitutorial.dev/prompting/prompt-security) [ingestado + corpus record + nueva Sección 4 "Seguridad de prompts" con 2 slides + tabla de defensas; renumeradas secciones 5-8; ítem LLM agregado al checklist]. Deck 8 secciones.
- 2026-06-17 — Correcciones de español (chat): "brecha de/en salud" → "filtración de datos de salud" (×3); "equipo de stroke" → "equipo de guardia neurológica (de ACV)". Presenter: dejar "triage"/"backup".
- 2026-06-17 — Presenter pidió: (1) nueva slide de referencia 2.3 "Los 18 identificadores (Safe Harbor)" (tabla agrupada) [insertada; renumeradas slides 2.4-2.7]; (2) nueva slide 8.1 "Las dos reglas de oro" (NUNCA subir API keys a repos públicos / NUNCA subir estudios identificados a terceros sin compliance — ej. Hospital Austral) [insertada; renumeradas checklists 8.2/8.3]. Deck ahora 8 secciones, ~31 slides. También acortado título 5.1.

## 2026-06-17 — Step 5 (Review)
- Status: complete
- What was decided: Feedback dado por chat (anglicismos, "para qué anonimizar", 18 identificadores, reglas NUNCA, prompt security) — aplicado vía Editor directo. Sin bullets formales en draft.md → nada que estampar/espejar por skill. Presenter señaló "listo".
- Files created/modified: draft.md (rondas de edición).
- Pending open questions: las 6 de # Open questions.

## 2026-06-17 — Step 6 (Polish)
- Status: complete
- What was decided: cp draft.md→final.md; Illustrator renderizó 4 SVG (s1-2-1, s3-1-1, s5-2-1, s7-1-1) — todos clean (s3-1-1 en 2 iter). Editor: (a) 4 fences→SVG, (b) sin refs externas, (c) sin [open] que rescatar, (d) 41 campos Presenter feedback eliminados.
- Files created/modified: final.md; images/ (4× svg+png+ascii); images/.critique/*.
- Pending open questions: las 6 de # Open questions (no bloquean el deliverable).

## 2026-06-17 — Step 7 (Learnings)
- Status: complete
- What was decided: feedback-backlog.md vacío → ningún patrón recurre ≥3× → nada que promover a learnings.md. Decisiones del presenter: (1) NO promover a knowledge-library; (2) SÍ renderizar a PPTX (→ Step 8).
- Files created/modified: ninguno.
- Pending open questions: none.

## 2026-06-17 — Step 8 (Render PPTX)
- Status: awaiting_presenter (bloqueado por entorno)
- What was decided: Presenter pidió renderizar. Prereqs OK (final.md limpio, 4 SVG+PNG, base-template/spec strict presentes, style=strict). BLOQUEANTE: skill nativo `pptx` no está en el registro — sesión es Claude Code CLI, no Cowork. md-to-pptx no tiene fallback CLI.
- Files created/modified: ninguno (render no ejecutado).
- Pending open questions: Re-correr Paso 8 dentro de Claude Cowork: "renderizá talks/clase-16-compliance-regulaciones-ia/final.md a PPTX". Todo el material ya está en disco.

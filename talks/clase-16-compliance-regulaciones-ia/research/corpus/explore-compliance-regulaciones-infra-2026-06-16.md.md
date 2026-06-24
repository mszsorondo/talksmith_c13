---
source_file: explore-compliance-regulaciones-infra-2026-06-16.md
source_type: chat-export
ingested_at: 2026-06-16
---

# Exploración en vivo — Compliance, regulaciones e infraestructura de IA en Ingeniería Biomédica

## Provenance
- Original location: research/llm-chats/explore-compliance-regulaciones-infra-2026-06-16.md
- Format: live-exploration transcript (Paso 2 — Collect), verbatim
- Author / source: Presenter (Marco Sanchez Sorondo / Paulo Veiga) + Talksmith
- Date of original: 2026-06-16
- Nota: fuente PRINCIPAL de estructura — define tesis, agenda y decisiones de alcance.

## Key claims
- **Tesis acordada:** "Desplegar IA en salud no es un problema técnico que después tiene un trámite legal: la regulación define qué podés construir, con qué datos, y quién responde cuando falla. El ingeniero biomédico es responsable desde la primera línea de código."
- **Alcance decidido:** la clase cubre **el dato Y el dispositivo** (no uno solo). + sección dedicada de **hardware/infraestructura**. + dimensión **IEC 60601 / 62304**.
- **Arco narrativo = ciclo de vida de un sistema de IA biomédico:** (1) conseguir datos → dato/privacidad; (2) entrenar/construir → infraestructura; (3) desplegar en clínica → dispositivo; (4) operar/mantener → responsabilidad continua; (5) caso de cierre.
- **Formato:** teórica, ~120 min, español + términos técnicos en inglés. Audiencia: estudiantes de grado de Ing. Biomédica con Python/ML básico.
- **Casos elegidos:** cierre con **DeepMind / Royal Free** (recap de los 3 ejes); eje dispositivo con producto FDA-cleared real **IDx-DR**.
- **Outcome:** los alumnos entienden las implicancias y responsabilidades de desplegar sistemas IT/IA en entornos biomédicos comunes.

## Definitions and terminology
- **BAA (Business Associate Agreement):** contrato necesario para que un tercero (cloud, API) procese PHI legalmente bajo HIPAA. Sin él, mandar el dato ya es violación.
- **SaMD:** ¿cuándo el modelo "es" un dispositivo médico? Umbral "sugiere vs decide".
- **Shared responsibility model:** el cloud asegura la seguridad *de* la nube; el cliente, la seguridad *en* la nube. ~90% de los breaches son del lado del cliente.
- **Data residency / transferencia internacional:** el dato vive en un lugar físico con jurisdicción (p.ej. `us-east-1` = Virginia, ley de EE.UU.).
- **Tres capas de hardware:** nube (GPU alquilada) / on-prem (datacenter del hospital) / edge-embebido (el modelo dentro del aparato).
- **IEC 60601:** seguridad eléctrica de equipo médico. **IEC 62304:** ciclo de vida del software de dispositivo médico.

## Evidence and examples
- "Anonimizar" ≠ borrar el nombre → HIPAA define 18 identificadores; aún así hay riesgo de re-identificación.
- Patrón histórico de breaches HIPAA: durante años la mayor causa de multas no fueron hackers sino **laptops/discos sin encriptar perdidos o robados** → el hardware físico como vector de incumplimiento.
- Gap argentino: Ley 25.326 es de 2000 (pre-nube, pre-IA); ANMAT regula software médico pero con marco menos maduro que FDA; reforma de datos pendiente.

## Inconsistencies / open questions
- Cifras precisas a verificar antes del slide final: montos de multas HIPAA, fechas/cifras exactas de Royal Free, número de identificadores, artículos específicos de la 25.326. (Parcialmente resueltas por las fuentes web ingestadas — varias con `needs_verification: true`.)
- ANMAT: tratar como "existe, está menos maduro, acá está el riesgo" — no pretender precisión normativa fina por falta de fuente sólida.
- Presenter hará un **deep research externo** para sumar fuentes; se ingestarán y re-correrá Librarian si llegan.

## Images / diagrams
Tres diagramas ASCII generados durante la exploración (preservados en Raw):
1. Matriz "¿QUÉ se regula?" (dato vs dispositivo × USA/AR/EU + infraestructura).
2. Ciclo de vida del sistema de IA biomédico (4 etapas → responsabilidad legal).
3. "¿Dónde corre el sistema?" — 3 capas de hardware (nube/on-prem/edge) × mundo regulatorio.
4. Estructura candidata de 6 secciones (0–5).

## Raw / preserved excerpts

### Matriz — ¿QUÉ se regula?
```
                    ¿QUÉ se regula?
        ┌─────────────────────┬─────────────────────────┐
        │  EL DATO             │  EL DISPOSITIVO/MODELO   │
        │  (privacidad)        │  (seguridad/eficacia)    │
 USA    │  HIPAA              │  FDA (SaMD / AI-ML)      │
 AR     │  Ley 25.326 (PDP)   │  ANMAT (software médico) │
 EU     │  GDPR               │  MDR + EU AI Act         │
        └─────────────────────┴─────────────────────────┘
                                  +  INFRAESTRUCTURA
                            (cloud, on-prem, logs, acceso, BAA)
```

### Ciclo de vida → responsabilidad legal
```
  [1] Conseguir datos  → EL DATO (consentimiento, anonimización, HIPAA/25.326)
  [2] Entrenar/construir → INFRAESTRUCTURA (cloud vs on-prem, BAA, encriptación)
  [3] Desplegar en clínica → EL DISPOSITIVO (SaMD, FDA/ANMAT, riesgo)
  [4] Operar/mantener → RESPONSABILIDAD CONTINUA (drift, post-market, ¿quién responde?)
```

### Tres capas de hardware
```
  CAPA 3 — APARATO CLÍNICO (edge/embedded): hardware ES el dispositivo → IEC 60601/62304, failure físico
  CAPA 2 — SERVIDOR DEL HOSPITAL (on-prem): control físico, encriptación at-rest, dato no sale del edificio
  CAPA 1 — LA NUBE (GPU alquilada): data residency, BAA, shared responsibility, transferencia internacional
```

### Estructura candidata (6 secciones)
```
  0. Apertura — el shock ("tu modelo con AUC 0.95 ya es ilegal")
  1. EL DATO — privacidad (HIPAA/25.326, 18 identificadores, gap AR)
  2. LA INFRAESTRUCTURA — ¿dónde corre? (nube/on-prem/edge, BAA, IEC 60601/62304)
  3. EL DISPOSITIVO — seguridad/eficacia (SaMD, FDA/ANMAT, IDx-DR, sugiere vs decide)
  4. RESPONSABILIDAD CONTINUA (drift, post-market, quién responde)
  5. CASO DE CIERRE — DeepMind/Royal Free (recap vivo de los 3 ejes)
```

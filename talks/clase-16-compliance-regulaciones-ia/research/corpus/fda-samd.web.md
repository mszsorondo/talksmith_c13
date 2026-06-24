---
source_file: fda-samd (web capture)
source_type: web-capture
ingested_at: 2026-06-16
---

# FDA — Software as a Medical Device (SaMD) + IMDRF + PCCP

## Provenance
- Original location: research/web/fda-samd/ (page.md)
- Format: síntesis verificada de fuentes secundarias (página FDA dio timeout)
- Author / source: FDA / IMDRF — reconstruido de greenlight.guru, IntuitionLabs, RQM+
- Date of original: framework IMDRF adoptado por FDA; PCCP finalizado dic-2024
- ⚠️ `needs_verification: true`

## Key claims
- **SaMD:** software destinado a propósitos médicos que los cumple **sin ser parte del hardware** de un dispositivo médico (distinto de SiMD — *software in a medical device*).
- El riesgo de una SaMD se categoriza por el cruce de **dos dimensiones** (framework IMDRF):
  - **Estado de la condición de salud:** crítica / seria / no-seria.
  - **Significancia de la información para la decisión clínica:** tratar o diagnosticar / conducir el manejo clínico / informar el manejo clínico.
- Resultan **4 categorías (I–IV)**; I = menor riesgo (informa, condición no-seria), IV = mayor riesgo (trata/diagnostica, condición crítica). Mayor categoría → mayor exigencia (evidencia clínica, controles).
- Caminos regulatorios FDA: **510(k)** (equivalencia sustancial a un predicado), **De Novo** (novedoso, sin predicado, riesgo bajo/moderado), **PMA** (alto riesgo).
- **El problema del modelo que aprende:** un modelo de ML que se reentrena cambia su comportamiento → tensión con un marco diseñado para dispositivos estáticos.
- **PCCP (Predetermined Change Control Plan):** guía FDA finalizada en **diciembre 2024** para AI-enabled device software functions. Permite **pre-especificar** en la submission original qué modificaciones del algoritmo se anticipan y cómo se evaluarán, e implementarlas sin nueva solicitud si se sigue el protocolo aprobado.

## Definitions and terminology
- **SaMD vs SiMD:** SaMD es independiente del hardware; SiMD es parte/controla un aparato físico.
- **510(k) / De Novo / PMA:** los tres caminos de autorización FDA según riesgo.
- **PCCP:** plan pre-aprobado de cambios del algoritmo — clave para IA que aprende.
- **IMDRF:** International Medical Device Regulators Forum — armoniza criterios entre reguladores (FDA, EU, etc.).

## Evidence and examples
Matriz de categorización IMDRF (significancia × condición):

```
                        SIGNIFICANCIA DE LA INFORMACIÓN
                   Informa     Conduce     Trata/Diagnostica
  Crítica          II          III          IV  (mayor riesgo)
  Seria            I           II           III
  No-seria         I           I            II
```
- Caso límite "sugiere vs decide": un modelo que **informa** (categoría baja) vs uno que **trata/diagnostica** de forma autónoma (categoría alta) — el umbral define la carga regulatoria.

## Inconsistencies / open questions
- Detalle exacto de las 4 categorías IMDRF (definición textual de II y III) parcialmente reconstruido — verificar con la guía IMDRF/FDA.
- Relación FDA "AI/ML SaMD Action Plan" (2021) ↔ PCCP final (2024): confirmar cronología antes de citar fechas.

## Images / diagrams
(ninguna — matriz reconstruida arriba en texto)

## Raw / preserved excerpts
> "The IMDRF SaMD framework classifies SaMD into four risk categories based on two dimensions: the state of the healthcare situation or condition (critical, serious, or non-serious) and the significance of the SaMD's output to the healthcare decision (treat or diagnose, drive clinical management, or inform clinical management)." (síntesis verificada)

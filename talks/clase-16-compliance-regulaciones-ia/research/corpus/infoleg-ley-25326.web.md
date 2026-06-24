---
source_file: infoleg-ley-25326 (web capture)
source_type: web-capture
ingested_at: 2026-06-16
---

# Ley 25.326 — Protección de los Datos Personales (Argentina)

## Provenance
- Original location: research/web/infoleg-ley-25326/ (page.md, 619 líneas; original.html preservado)
- Format: html → markdown (Infoleg, texto oficial)
- Author / source: Congreso de la Nación Argentina · Infoleg (servicios.infoleg.gob.ar)
- Date of original: Sancionada 4 oct 2000; promulgada parcialmente 30 oct 2000
- Nota: texto OFICIAL verbatim (no es síntesis). Encoding con caracteres especiales degradados (`�`) en la captura, pero legible.

## Key claims
- **Objeto (Art. 1):** protección integral de datos personales en archivos/registros/bancos de datos, públicos o privados, para garantizar honor, intimidad y acceso a la información (anclado en art. 43 párr. 3 de la Constitución Nacional — hábeas data).
- **Dato sensible incluye salud (Art. 2):** "Datos sensibles: datos personales que revelan origen racial y étnico, opiniones políticas, convicciones religiosas, filosóficas o morales, afiliación sindical e **información referente a la salud** o a la vida sexual." → los datos de salud son legalmente datos sensibles en AR.
- **Disociación (Art. 2):** "Todo tratamiento de datos personales de manera que la información obtenida no pueda asociarse a persona determinada o determinable." → el equivalente argentino a la de-identificación.
- **Calidad de datos / minimización (Art. 4):** datos ciertos, adecuados, pertinentes y **no excesivos** respecto del fin; no usarse para fines distintos/incompatibles; destruirse cuando dejan de ser necesarios.
- **Consentimiento (Art. 5):** el tratamiento es ilícito sin consentimiento libre, expreso e informado, por escrito o medio equiparable. Excepciones: fuentes de acceso público irrestricto, función estatal/obligación legal, listados básicos, relación contractual/científica/profesional, entidades financieras.
- **Categoría de datos sensibles (Art. 7):** nadie puede ser obligado a dar datos sensibles; sólo se recolectan/tratan por razones de interés general autorizadas por ley, o con fines estadísticos/científicos **cuando no puedan identificarse los titulares**; prohibido formar archivos que revelen datos sensibles directa o indirectamente.
- **Datos de salud (Art. 8):** establecimientos sanitarios y profesionales de la salud **pueden** recolectar y tratar datos de salud de sus pacientes, respetando el secreto profesional.
- **Seguridad de los datos (Art. 9):** el responsable/usuario debe adoptar las medidas **técnicas y organizativas** necesarias para garantizar seguridad y confidencialidad, evitar adulteración/pérdida/consulta/tratamiento no autorizado, y detectar desviaciones — provengan de la acción humana o del **medio técnico utilizado**. Prohibido registrar datos en archivos que no reúnan condiciones técnicas de integridad y seguridad. → base legal del compliance de infraestructura.
- **Confidencialidad (Art. 10):** secreto profesional que subsiste tras finalizar la relación; relevable sólo por resolución judicial o razones de seguridad/salud pública.
- **Cesión (Art. 11):** datos sólo se ceden para fines relacionados con el interés legítimo y con consentimiento previo. Excepción para datos de salud por salud pública/emergencia/estudios epidemiológicos **preservando identidad mediante disociación**. El cesionario queda sujeto a las mismas obligaciones; el cedente responde **solidaria y conjuntamente**. → análogo conceptual al encadenamiento de responsabilidad (BAA).
- **Transferencia internacional (Art. 12):** **prohibida** la transferencia a países/organismos que no proporcionen niveles de protección **adecuados**. Excepciones: colaboración judicial, intercambio médico para tratamiento del afectado o investigación epidemiológica (con disociación), transferencias bancarias, tratados internacionales, cooperación de inteligencia. → núcleo del problema "el dato vive en us-east-1".
- **Derechos del titular (Arts. 13–16):** información, acceso (respuesta en 10 días corridos), rectificación, actualización, supresión, confidencialidad. Acción de hábeas data.
- **Sanciones (Art. 31):** sanciones administrativas (apercibimiento, suspensión, multa, clausura/cancelación del archivo). El Código Penal (incorporado por la ley) tipifica el acceso ilegítimo a bancos de datos personales.

## Definitions and terminology
- **Dato personal:** información de cualquier tipo referida a personas físicas o de existencia ideal determinadas o determinables.
- **Dato sensible:** incluye explícitamente la información referente a la salud.
- **Tratamiento de datos:** recolección, conservación, almacenamiento, modificación, evaluación, bloqueo, destrucción y cesión a terceros.
- **Responsable de archivo/banco de datos:** titular del archivo (≈ "data controller").
- **Disociación de datos:** anonimización — tratamiento que impide asociar la información a persona determinable.
- **Hábeas data:** acción constitucional de protección de datos personales (art. 43 CN).

## Evidence and examples
- La ley es de **2000**: pre-nube, pre-IA, pre-big-data. Marco de referencia para discutir el gap argentino frente a HIPAA (1996, pero con reglas técnicas más desarrolladas) y GDPR (2018).
- Autoridad de control: hoy la **AAIP** (Agencia de Acceso a la Información Pública) — sucesora de la antigua Dirección Nacional de Protección de Datos Personales. (No nombrada literalmente en el texto 2000; contexto institucional posterior.)

## Inconsistencies / open questions
- El texto capturado es el original de 2000; **existe un proyecto de reforma** de la ley de datos personales (mencionado en exploración) que conviene contrastar — la versión vigente "actualizada" puede tener modificaciones. Verificar estado de la reforma antes de afirmar el marco vigente exacto.
- AR no tiene (a 2026) una ley específica de IA; la regulación de IA en salud se apoya en esta ley + normativa ANMAT de dispositivos. Confirmar.

## Images / diagrams
(ninguna — fuente de texto)

## Raw / preserved excerpts
> **Art. 2 (Datos sensibles):** "Datos personales que revelan origen racial y étnico, opiniones políticas, convicciones religiosas, filosóficas o morales, afiliación sindical e información referente a la salud o a la vida sexual."

> **Art. 9.1 (Seguridad):** "El responsable o usuario del archivo de datos debe adoptar las medidas técnicas y organizativas que resulten necesarias para garantizar la seguridad y confidencialidad de los datos personales, de modo de evitar su adulteración, pérdida, consulta o tratamiento no autorizado, y que permitan detectar desviaciones, intencionales o no, de información, ya sea que los riesgos provengan de la acción humana o del medio técnico utilizado."

> **Art. 12.1 (Transferencia internacional):** "Es prohibida la transferencia de datos personales de cualquier tipo con países u organismos internacionales o supranacionales, que no proporcionen niveles de protección adecuados."

> **Art. 8 (Datos relativos a la salud):** "Los establecimientos sanitarios públicos o privados y los profesionales vinculados a las ciencias de la salud pueden recolectar y tratar los datos personales relativos a la salud física o mental de los pacientes... respetando los principios del secreto profesional."

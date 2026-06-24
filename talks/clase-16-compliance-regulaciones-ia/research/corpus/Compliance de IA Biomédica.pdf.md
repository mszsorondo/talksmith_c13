---
source_file: Compliance de IA Biomédica.pdf
source_type: article
ingested_at: 2026-06-16
---

# Regulación, Compliance e Infraestructura de IA en Entornos Biomédicos (deep research)

## Provenance
- Original location: research/articles/Compliance de IA Biomédica.pdf
- Format: pdf (24 págs.), reporte de deep research generado por IA externa siguiendo el prompt en research/deep-research-prompt.txt
- Author / source: deep research del presenter; ~96 fuentes primarias citadas (FDA, HHS, EUR-Lex, ICO, Infoleg, ANMAT, IMDRF, IEC, papers PMC)
- Date of original: 2026-06-16
- Nota: fuente PRINCIPAL de contenido y cifras. Supersede/confirma los 4 records con needs_verification. Estructura en 4 bloques + tabla comparativa, cada tema con "ficha técnica" (a fuente / b cifras / c cita textual / d relevancia para el ingeniero).

## Key claims

### Eje 1 — El dato (privacidad)
- **HIPAA:** clasifica info de salud como ePHI; covered entities + business associates → relación formalizada por **BAA**. De-identificación por **45 CFR §164.514**: Safe Harbor (18 identificadores) o Expert Determination.
- **Multas/breaches HIPAA reales:** Anthem USD 16M (2018, mayor sanción OCR histórica); ransomware **Change Healthcare** (feb-2024, grupo ALPHV/BlackCat): ~192,7M personas, rescate USD 22M, costos totales ~USD 2.457B (mayor brecha de salud de la historia de EE.UU.); Solara Medical Supplies USD 3M (2024); Gulf Coast Pain Management USD 1.19M. Factor común: ausencia de análisis de riesgos de seguridad.
- **HIPAA Security Rule — actualización 2026:** MFA obligatoria; encriptación AES-256 en reposo y TLS 1.2+ (preferencia 1.3) en tránsito pasa de "direccionable" a obligatoria; segmentación de red; inventario de activos + mapa de red auditado anualmente; SLA de desactivación de cuentas comprometidas (1 h) y planes de contingencia (24 h).
- **Argentina — Ley 25.326 (2000):** Art. 2 dato sensible incluye salud; Art. 4 inc. 3 no desviación de finalidad; Art. 9/10 seguridad y confidencialidad; Art. 11 cesión con consentimiento; **Art. 21 (NOTA: el PDF cita "Art. 21" para transferencia internacional; el texto oficial Infoleg lo ubica en Art. 12 — verificar numeración)**.
- **AAIP:** autoridad de aplicación. **Res. AAIP 161/2023** crea el "Programa de Transparencia y Protección de Datos Personales en el Uso de la IA". **Guía de Recomendaciones para una IA Responsable (oct-2024):** accountability, privacy by design, DPIA, calibración de calidad del dato, derecho a explicación.
- **Reforma de datos (Mensaje PEN 87/2023, en debate):** armoniza con GDPR para mantener estatus de "país adecuado" (ratificado por UE en ene-2024); multas proporcionales hasta 3% de facturación local anual; **sandboxes regulatorios** para IA < 5 años; gobernanza específica de IA en vigencia progresiva a 30 meses. (También: Expediente 6156-D-2024 — Registro Nacional de Sistemas de IA.)
- **GDPR (contraste):** Art. 9 datos de salud = categoría especial; excepciones Art. 9(2) (consentimiento explícito, medicina preventiva/diagnóstico Art. 9(2)(h), interés público salud Art. 9(2)(i)); transferencias Art. 44-49 (decisión de adecuación o SCC + TIA); multas hasta 20M EUR o 4% facturación global.

### Eje 2 — El dispositivo (SaMD)
- **FDA/IMDRF (Doc. N41):** SaMD = software de propósito médico que no es parte del hardware. 4 categorías de riesgo (I–IV) por cruce de **gravedad de la condición** (crítica/seria/no-seria) × **significancia de la información** (tratar-diagnosticar / dirigir manejo / informar manejo).
- **Caminos FDA:** 510(k) (equivalencia sustancial; mediana 151 días; ~96% de las autorizaciones de IA/ML); De Novo (novedoso sin predicado); PMA (Cat. IV/Clase III, ensayos clínicos prospectivos).
- **PCCP (Plan de Control de Cambios Predeterminado):** guía final FDA **3-dic-2024**, base legal **§515C FD&C Act (reforma FDORA 2022)**. Tres secciones obligatorias: Description of Modifications / Modification Protocol / Impact Assessment. Permite re-entrenamiento pre-aprobado sin nueva submission.
- **Estadística FDA:** >1.000 (algunas bases >1.400) dispositivos de IA/ML autorizados; ~96% vía 510(k); a fines de 2024, ≥53 dispositivos bajo esquema PCCP.
- **Argentina — ANMAT Disp. 9688/2019** (29-nov-2019, BO 3-dic-2019): Art. 26 software autónomo = "producto médico activo", inscripción obligatoria en **RPPTM**; **RESE** (Requisitos Esenciales de Seguridad y Eficacia, Disp. 4306/1999); gestión de riesgos **ISO 14971**; V&V por fase del ciclo de vida; 4 clases de riesgo. Colaboración IMDRF (mar-2026).
- **UE — MDR (2017/745) Regla 11:** software diagnóstico/monitoreo crítico → clases IIa/IIb/III. **EU AI Act (2024/1689) Art. 6(1):** IA médica con marcado CE de terceros = "alto riesgo"; obligatorio desde **2-ago-2027**.

### Eje 3 — Hardware e infraestructura
- **IEC 62304** (ciclo de vida del software de dispositivo médico): clases **A** (sin daño posible) / **B** (lesión no grave) / **C** (muerte o lesión grave). Aplica a SaMD y software embebido.
- **IEC 60601-1** (seguridad eléctrica + funcionamiento esencial): **Sección 14 = PEMS** (Sistemas Electromédicos Programables); exige especificación/diseño/V&V del subsistema programable, convergiendo con IEC 62304 cuando el software controla la seguridad básica.
- **Modelos de despliegue:** Cloud (escalable, latencia + transferencia internacional GDPR Art.44 / Ley 25.326 Art.21); On-prem (control directo, sin latencia de red, alto costo de mantenimiento); Edge/Embedded (GPU integrada, p.ej. ecógrafo en quirófano, mínima dependencia de red).
- **BAA en la nube:** AWS, GCP y Azure firman BAA **condicionado** a que el cliente configure encriptación (reposo + tránsito), active audit logging y use sólo servicios del catálogo "HIPAA-Eligible".
- **Patrón histórico de fugas:** >80% de las brechas en el portal OCR eran por intrusiones o **robo de dispositivos físicos sin encriptar** (laptops, discos, backups). Costo promedio de brecha en salud 2025: récord USD 7.42M (IBM). Encriptación at-rest pasa a obligatoria con la Security Rule 2026 (gracia 240 días).

### Eje 4 — Responsabilidad y caso de cierre
- **Distribución de responsabilidad:** Fabricante (diseño/validación del algoritmo, PMS para detectar Model Drift); Institución de salud (integración operativa, seguridad perimetral, capacitación, roles de acceso); Ingeniero de despliegue (config criptográfica, parches críticos en plazo — 15 días críticos / 30 días alta severidad por HIPAA 2026, registros de auditoría). Fuente: FDA Draft Guidance on Clinical Decision Support (CDS) Software 2022 + post-market surveillance MDR.
- **Caso Royal Free / DeepMind (Streams, 2017):** cronología 30-sep-2015 (ISA, 1,6M registros) → 18-nov-2015 (data streaming) → abr-2016 (FOI revela acuerdo) → may-2016 (ICO abre investigación) → feb-2017 (Streams en uso, Clase I MHRA) → 3-jul-2017 (resolución ICO, undertaking). Incumplió **DPA 1998** Principios 1 (base legal — "consentimiento implícito de cuidado directo" no cubre testeo), 3 (exceso/desproporción — 1,6M para detección de AKI), 6 (transparencia/opt-out), 7 (sin DPIA). **No hubo multa** (DPA 1998 pre-GDPR reservaba multas para dolo/daño directo; el Trust actuó de buena fe). Consecuencias: undertaking + auditoría independiente; intervención de la National Data Guardian (Fiona Caldicott); Streams pasó luego a Google Health.

## Definitions and terminology
- **ePHI / PHI:** información de salud (electrónica) individualmente identificable.
- **BAA:** Business Associate Agreement — contrato HIPAA con terceros que procesan PHI.
- **Safe Harbor / Expert Determination:** los dos métodos de de-identificación (45 CFR §164.514).
- **SaMD / SiMD:** software *as* a medical device (independiente del hardware) vs *in* a medical device.
- **PCCP:** Predetermined Change Control Plan — plan pre-aprobado de cambios del algoritmo de IA.
- **PEMS:** Programmable Electrical Medical System (IEC 60601-1 Sec. 14).
- **Model Drift:** degradación progresiva del desempeño del modelo por cambio en la distribución de datos de entrada.
- **PMS:** Post-Market Surveillance.
- **DPIA / PIA:** Data/Privacy Impact Assessment.
- **RPPTM / RESE:** Registro de Productores y Productos de Tecnología Médica / Requisitos Esenciales de Seguridad y Eficacia (ANMAT).

## Evidence and examples
- Cifras de casos FDA: **IDx-DR** (abr-2018, De Novo, DEN180007; estudio pivotal prospectivo 900 pac. diabéticos en 10 centros de atención primaria, 819 completaron; **sensibilidad 87,2% (IC95 81,8–91,2)**, **especificidad 90,7% (IC95 88,3–92,7)**, evaluabilidad 96,1%; umbral FDA ≥75% sens. / ≥77,5% esp.). **NOTA:** el press release suele citarse como 87,4%/89,5% — el PDF reporta 87,2%/90,7% del De Novo Summary; verificar/elegir la cifra a usar.
- **Viz LVO (ContaCT):** feb-2018, De Novo (DEN170073); estudio retrospectivo 2.544 pac. de 139 hospitales; sensibilidad 96,32% / especificidad 93,83%.
- **CINA LVO:** estudio McLouth et al. 2021, 378 escaneos; exactitud 98%, sens. 94,3%, esp. 97,4%.
- Tabla comparativa final USA/AR/UE por los 3 ejes (dato/dispositivo/hardware) — en Raw.

## Inconsistencies / open questions
- **Numeración Art. 21 vs Art. 12 (Ley 25.326, transferencia internacional):** el PDF dice Art. 21; el texto oficial Infoleg capturado lo ubica en Art. 12. Resolver antes del slide (posible diferencia entre texto original 2000 y texto ordenado/actualizado).
- **Cifras IDx-DR:** 87,2%/90,7% (De Novo Summary, en el PDF) vs 87,4%/89,5% (citado en press release / nuestra fuente fda-idx-dr). Elegir una y citar la fuente.
- **Fechas "2026":** varios items fechados 2026 (HIPAA Security Rule 2026, colaboración ANMAT-IMDRF mar-2026, dossier legislativo abr-2026). Hoy es jun-2026 — confirmar si son vigentes o aún propuestos antes de afirmar en clase.
- **EU AI Act:** obligatoriedad alto-riesgo desde 2-ago-2027 (futuro) — encuadrar como "entra en vigencia".

## Images / diagrams
(ninguna — el PDF es texto; tablas reproducidas en Raw)

## Raw / preserved excerpts

### Tabla comparativa (resumen de la §5 del PDF)
```
EJE          | USA (HIPAA/FDA)              | Argentina (Ley 25.326/ANMAT)      | UE (GDPR/MDR/AI Act)
-------------|-----------------------------|-----------------------------------|-----------------------------
Dato         | ePHI; BAA; Safe Harbor 18   | Dato sensible (Art.2); disociación| Cat. especial Art.9; anonim.
             | ID / Expert Det.; multas    | consentimiento; multas reforma    | irreversible; multas 20M/4%
             | (Anthem 16M, Change 2.457B) | hasta 3% facturación local        | global
Dispositivo  | IMDRF 4 cat.; 510(k)/DeNovo/| ANMAT Disp.9688/2019; RPPTM;      | MDR Regla 11 (IIa-III);
             | PMA; PCCP (dic-2024)        | RESE; sin PCCP formal             | AI Act Art.6(1) alto riesgo (2027)
Hardware     | IEC 62304 + 60601-1 (Sec.14)| IEC 62304/60601-1 vía RESE;       | IEC 62304/60601-1 armonizadas;
             | BAA HIPAA-Eligible; AES-256 | cloud si nivel adecuado/contrato; | soberanía de datos; AI Act Art.15
             | TLS1.3; MFA (2026)          | encriptación proporcional         | ciberseguridad
```

### Citas textuales clave (verbatim del PDF)
> Expert Determination (45 CFR §164.514): "Applying such principles and methods, determines that the risk is very small that the information could be used, alone or in combination with other reasonably available information, by an anticipated recipient to identify an individual."

> BAA AWS: "...compliance obligations are conditional on the in-scope services covered by the Addendum being configured correctly by the customer, that audit logging is enabled, and that all PHI placed into the AWS Cloud is encrypted."

> Ley 25.326 Art. 2 (dato sensible): "Datos personales que revelan origen racial y étnico, opiniones políticas, convicciones religiosas, filosóficas o morales, afiliación sindical e información referente a la salud o a la vida sexual."

> PCCP (ventaja, marco FDA): "...reduce the need for repeated approvals and decrease waiting times for approval decisions, thereby fostering innovation and improving patient access to advanced technologies."

> ICO sobre Royal Free: "The processing of patient records by DeepMind significantly differs from what data subjects might reasonably have expected to happen to their data when presenting at the Royal Free for treatment."

> OCR ante el Congreso: "...many data breaches could have been prevented through proactive compliance, rather than addressing security issues after exploitation."

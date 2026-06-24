---
source_file: hhs-hipaa-deidentification (web capture)
source_type: web-capture
ingested_at: 2026-06-16
---

# HIPAA — De-identification of Protected Health Information (45 CFR § 164.514)

## Provenance
- Original location: research/web/hhs-hipaa-deidentification/ (page.md)
- Format: síntesis verificada de fuentes secundarias (página oficial HHS dio HTTP 403)
- Author / source: U.S. Dept. of Health & Human Services (45 CFR § 164.514) — reconstruido de HIPAA Journal, Accountable, Censinet, ComplyDome
- Date of original: HIPAA Privacy Rule (regla de de-identificación vigente)
- ⚠️ `needs_verification: true` — confirmar contra texto oficial de HHS antes de citar literal.

## Key claims
- HIPAA permite que la PHI deje de ser PHI por **dos métodos** de de-identificación (45 CFR § 164.514).
- **Safe Harbor (§ 164.514(b)(2)):** remover **18 identificadores enumerados** Y no tener "conocimiento real" (*no actual knowledge*) de que la info restante podría identificar al individuo, sola o en combinación.
- **Expert Determination (§ 164.514(b)(1)):** experto calificado determina y documenta que el riesgo de re-identificación es "muy pequeño"; permite retener más detalle pero exige expertise y gobernanza continua.
- Una vez de-identificado, el dato **deja de ser PHI** y queda exento de las reglas de Privacy, Security y Breach Notification.
- Punto de enseñanza: "anonimizar" ≠ borrar el nombre. Aun sacando los 18, puede quedar riesgo de re-identificación por combinación de cuasi-identificadores.

## Definitions and terminology
- **PHI (Protected Health Information):** información de salud individualmente identificable manejada por una covered entity.
- **Covered entity:** prestadores, planes de salud, clearinghouses sujetos a HIPAA.
- **Business Associate:** tercero que procesa PHI por cuenta de una covered entity → requiere un **BAA (Business Associate Agreement)**.
- **Safe Harbor / Expert Determination:** los dos métodos de de-identificación.

## Evidence and examples
**Los 18 identificadores (Safe Harbor):**
1. Nombres
2. Subdivisiones geográficas menores a un estado (calle, ciudad, condado, ZIP con reglas especiales de población)
3. Fechas (excepto el año) ligadas al individuo: nacimiento, admisión, alta, fallecimiento; edades > 89
4. Teléfonos
5. Fax
6. Emails
7. SSN (Seguro Social)
8. Número de historia clínica
9. Número de beneficiario de plan de salud
10. Números de cuenta
11. Certificados/licencias
12. Identificadores de vehículo / patente
13. Identificadores de dispositivo y números de serie
14. URLs
15. IPs
16. Identificadores biométricos (huellas, voz)
17. Fotos de cara completa e imágenes comparables
18. Cualquier otro número/característica/código único de identificación

## Inconsistencies / open questions
- Cifra de multa máxima HIPAA y montos de penalidades no incluidos aquí — verificar con la fuente OCR/HHS antes de citar números de multas en slide.
- Safe Harbor exige reglas específicas para ZIP de 3 dígitos según población (>20.000) — detalle a confirmar.

## Images / diagrams
(ninguna)

## Raw / preserved excerpts
> "Under the safe harbor method, covered entities must remove all of a list of 18 enumerated identifiers and have no actual knowledge that the information remaining could be used, alone or in combination, to identify a subject of the information." (síntesis verificada de § 164.514(b)(2))

# HIPAA De-identification of Protected Health Information (45 CFR § 164.514)

> **Procedencia:** la página oficial de HHS (`hhs.gov/.../de-identification/index.html`) devolvió HTTP 403 al fetcher y timeout vía WebFetch. Este contenido es una **síntesis verificada de fuentes secundarias** (HIPAA Journal, Accountable, Censinet, ComplyDome) sobre el texto de 45 CFR § 164.514. Verificar contra el texto oficial de HHS antes de citar literal en slide final.

## Dos métodos de de-identificación (45 CFR § 164.514)

Bajo la HIPAA Privacy Rule, información de salud deja de ser PHI (Protected Health Information) si se de-identifica por uno de dos métodos:

### 1. Expert Determination — § 164.514(b)(1)
Un experto calificado (con conocimiento estadístico/científico apropiado) determina y **documenta** que el riesgo de re-identificación es "muy pequeño" (*very small*), solo o en combinación con otra información razonablemente disponible. Permite retener más detalle (p.ej. fechas a nivel mes, geografía regional) pero exige expertise, documentación y gobernanza continua.

### 2. Safe Harbor — § 164.514(b)(2)
Camino prescriptivo: remover los **18 identificadores enumerados** Y no tener conocimiento real (*no actual knowledge*) de que la información restante podría usarse, sola o en combinación, para identificar al individuo.

## Los 18 identificadores (Safe Harbor)

1. Nombres
2. Subdivisiones geográficas menores a un estado (calle, ciudad, condado, ZIP — el ZIP de 5 dígitos con reglas especiales de población)
3. Todos los elementos de fecha (excepto el año) directamente relacionados a un individuo: nacimiento, admisión, alta, fallecimiento; y todas las edades > 89 y fechas indicativas de esa edad
4. Números de teléfono
5. Números de fax
6. Direcciones de email
7. Números de Seguro Social (SSN)
8. Números de historia clínica (medical record numbers)
9. Números de beneficiario de plan de salud
10. Números de cuenta
11. Números de certificado/licencia
12. Identificadores de vehículo y números de serie (incluyendo patente)
13. Identificadores de dispositivo y números de serie
14. URLs web
15. Direcciones IP
16. Identificadores biométricos (huellas, voz)
17. Fotografías de cara completa e imágenes comparables
18. Cualquier otro número, característica o código único de identificación

## Consecuencia
Una vez que el dato cumple los requisitos de de-identificación, **deja de ser PHI** y queda exento de las reglas de Privacy, Security y Breach Notification de HIPAA.

## Punto de enseñanza clave
"Anonimizar" ≠ borrar el nombre. Safe Harbor exige sacar 18 categorías, y aún así puede quedar riesgo de re-identificación por combinación de cuasi-identificadores → de ahí la existencia del método Expert Determination y la cláusula de "no actual knowledge".

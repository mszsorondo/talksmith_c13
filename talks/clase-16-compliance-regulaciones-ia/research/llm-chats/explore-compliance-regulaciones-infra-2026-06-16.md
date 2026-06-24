---
source_type: live-exploration
started_at: 2026-06-16
ended_at: 2026-06-16
topic: Compliance, regulaciones e infraestructura de IA aplicada a Ingeniería Biomédica
---

# Exploración — Compliance, regulaciones e infraestructura de IA en Ingeniería Biomédica

Transcripción verbatim de la exploración en vivo (Paso 2 — Collect) entre el presenter y Talksmith. Sin parafraseo.

---

### Agent

Arranco poniendo el territorio sobre la mesa, porque "compliance + regulación + infra" en biomédica se cruza en una matriz que vale la pena ver antes de elegir el recorrido de la clase.

**El choque de fondo que vale como tesis candidata:** un estudiante de Ing. Biomédica va a construir o desplegar software que toca datos de salud y/o toma decisiones clínicas. En el momento en que ese software sale del notebook y entra a un hospital, deja de ser "un modelo con buen AUC" y pasa a ser **un dispositivo regulado que maneja datos sensibles de personas reales**. La clase es, básicamente, el shock de pasar del `model.fit()` al mundo donde un error es responsabilidad legal de alguien.

Lo desgloso en tres ejes que conviene no mezclar:

```
                    ¿QUÉ se regula?
        ┌─────────────────────┬─────────────────────────┐
        │  EL DATO             │  EL DISPOSITIVO/MODELO   │
        │  (privacidad)        │  (seguridad/eficacia)    │
        ├─────────────────────┼─────────────────────────┤
 USA    │  HIPAA              │  FDA (SaMD / AI-ML)      │
        │  (Privacy+Security) │  510(k), De Novo, PCCP   │
        ├─────────────────────┼─────────────────────────┤
 AR     │  Ley 25.326 (PDP)   │  ANMAT (Disp. software   │
        │  + AAIP             │  médico, IMDRF)          │
        ├─────────────────────┼─────────────────────────┤
 EU     │  GDPR               │  MDR + EU AI Act         │
 (ref)  │                     │  (high-risk)             │
        └─────────────────────┴─────────────────────────┘
                                        +  INFRAESTRUCTURA
                                  (cómo lo desplegás: cloud,
                                   on-prem, logs, acceso, BAA)
```

Acá ya hay una decisión de alcance que te quiero tirar como pregunta:

**¿La clase es "el dato" o "el dispositivo" o ambos?** Son responsabilidades muy distintas:
- **El dato** (HIPAA / Ley 25.326): quién puede ver qué, encriptación, consentimiento, breach notification, contratos con proveedores (BAA). Acá vive el 80% de lo que un ingeniero rompe sin darse cuenta.
- **El dispositivo** (FDA / ANMAT): si tu modelo "diagnostica" o "recomienda tratamiento", es un dispositivo médico y necesita aprobación regulatoria. Esto cambia radicalmente la responsabilidad.

Mi lectura: dado tu outcome ("implicancias y responsabilidades de desplegar"), el **eje del dato + la capa de infraestructura** es donde más se la juega un egresado, pero el eje del dispositivo es el que más los sorprende ("¿cómo que mi modelo es legalmente un dispositivo médico?").

Tres preguntas para calibrar el recorrido:

1. **¿Querés que la clase sea comparada (USA vs Argentina vs EU) o anclada en el caso argentino** con HIPAA/EU como contraste? Para alumnos que van a trabajar acá, anclar en AR y usar HIPAA como "el estándar de oro que todos copian" suele funcionar mejor.
2. **¿Entra el ángulo "dispositivo médico regulado"** (FDA/ANMAT, SaMD) o lo dejamos para otra clase y nos quedamos en datos+infra?
3. Cuando decís **"proyectos"** en el brief — ¿te referís a que quieras casos/ejemplos concretos de proyectos biomédicos reales para aterrizar cada regulación, o a responsabilidades en la *gestión de un proyecto* (roles, DPO, ciclo de vida)?

### Presenter

La clase es "el dato" Y "el dispositivo"

### Agent

Buenísimo — los dos ejes. Eso me da un arco natural, porque **el dato y el dispositivo se ordenan en el tiempo de vida de un sistema biomédico**, no son dos temas paralelos. Te muestro cómo lo encadenaría:

```
  CICLO DE VIDA DE UN SISTEMA DE IA BIOMÉDICO
  (y qué responsabilidad legal aparece en cada etapa)

  [1] Conseguir datos ──────► EL DATO
       de pacientes            · ¿consentimiento? ¿anonimización real?
                               · HIPAA (de-identification, 18 identifiers)
                               · Ley 25.326: dato sensible = salud
                               · AAIP, transferencia internacional
            │
            ▼
  [2] Entrenar / construir ──► INFRAESTRUCTURA
       el modelo               · ¿dónde viven los datos? cloud vs on-prem
                               · BAA con el proveedor (AWS/GCP firman)
                               · encriptación, control de acceso, logs/auditoría
            │
            ▼
  [3] Desplegar en clínica ──► EL DISPOSITIVO
       (toma/asiste decisión)  · ¿es Software as a Medical Device?
                               · FDA: 510(k)/De Novo/PCCP · ANMAT en AR
                               · clasificación de riesgo, evidencia clínica
            │
            ▼
  [4] Operar y mantener ─────► RESPONSABILIDAD CONTINUA
       en producción           · monitoreo, model drift, post-market
                               · breach notification, ¿quién responde?
```

Esto te resuelve el problema de "dos temas en una clase": **es un solo relato cronológico** donde el dato domina las etapas 1–2 y el dispositivo las 3–4, y la infraestructura es la capa transversal que sostiene todo.

La **tesis** que destila de acá podría ser algo como:

> *"Desplegar IA en salud no es un problema técnico que después tiene un trámite legal: la regulación define qué podés construir, con qué datos, y quién responde cuando falla. El ingeniero biomédico es responsable desde la primera línea de código."*

Un par de cosas potentes que conviene que la clase deje clavadas (te las tiro para validar):

- **"Anonimizado" no es lo que creen.** El estudiante promedio piensa que borrar el nombre = anonimizado. HIPAA define **18 identificadores** que hay que sacar (fechas, ZIP, etc.), y aún así hay riesgo de re-identificación. Esto es un golpe de realidad buenísimo para abrir.
- **El BAA (Business Associate Agreement).** Si usás una API de un tercero (OpenAI, un cloud) para procesar datos de pacientes, *necesitás un contrato específico* o estás violando HIPAA por el solo hecho de mandar el dato. Conecta directo con "infraestructura".
- **El umbral SaMD.** ¿Cuándo tu modelo deja de ser "una herramienta de apoyo" y se convierte en dispositivo médico que requiere aprobación? La FDA tiene una lógica de riesgo (qué tan crítica es la decisión × qué tan grave la condición). Casos límite: un modelo que "sugiere" vs uno que "decide".
- **El gap argentino.** La Ley 25.326 es de **2000** — pre-nube, pre-IA. ANMAT regula software médico pero el marco está mucho menos maduro que FDA. Hay un proyecto de reforma de datos personales y la pregunta abierta de cómo se regula IA en AR. Esto es honesto y relevante para ellos.

Dos preguntas para seguir afilando:

1. **¿Cerramos con algún caso real conocido** que haya pinchado en compliance? (p.ej. el deal de **DeepMind/Royal Free** en UK donde se compartieron 1.6M registros sin base legal adecuada — es el caso de enseñanza perfecto de "buen modelo, desastre legal"). ¿Querés uno USA, uno AR, o ambos?
2. Para el eje dispositivo — **¿metemos casos de productos FDA-cleared reales** (tipo IDx-DR, el primer diagnóstico autónomo aprobado de retinopatía diabética) para que vean que esto no es teórico?

### Presenter

1. si, cerramos con ese caso real
2. si
también quiero que hables sobre el hardware en donde se ejecutan los sistemas

### Agent

Perfecto — caso DeepMind/Royal Free para el cierre, productos FDA-cleared reales para el eje dispositivo. Y el hardware es justo la pata que faltaba para que "infraestructura" no quede abstracta. Acá hay mucho más de lo que parece, porque **en biomédica el hardware está regulado por partida doble**: como cómputo (dónde viven los datos) y como dispositivo físico (el aparato que toca al paciente).

Lo separo en tres capas porque mezclarlas confunde:

```
  ¿DÓNDE CORRE EL SISTEMA?  — tres capas de hardware, tres mundos regulatorios

  ┌──────────────────────────────────────────────────────────────┐
  │ CAPA 3 — EL APARATO CLÍNICO (embedded / edge)                  │
  │   el monitor, la bomba de infusión, el ecógrafo con IA         │
  │   · hardware ES el dispositivo médico → IEC 60601 (seguridad   │
  │     eléctrica), IEC 62304 (software de disp. médico)           │
  │   · failure mode = daño físico directo al paciente             │
  │   · tiempo real, sin red, certificación de hardware            │
  └──────────────────────────────────────────────────────────────┘
                              ▲
  ┌──────────────────────────────────────────────────────────────┐
  │ CAPA 2 — EL SERVIDOR DEL HOSPITAL (on-prem)                    │
  │   GPUs/servidores en el datacenter de la institución           │
  │   · control físico = el hospital responde por el acceso        │
  │   · encriptación at-rest, destrucción de discos, redundancia   │
  │   · ventaja compliance: el dato nunca sale del edificio        │
  └──────────────────────────────────────────────────────────────┘
                              ▲
  ┌──────────────────────────────────────────────────────────────┐
  │ CAPA 1 — LA NUBE (cloud / GPU alquilada)                       │
  │   AWS/GCP/Azure, una H100 que alquilás por hora                │
  │   · ¿dónde está físicamente el server? → data residency        │
  │   · BAA obligatorio · "shared responsibility model"            │
  │   · Ley 25.326: transferencia internacional de datos = problema│
  └──────────────────────────────────────────────────────────────┘
```

Los conceptos de hardware que vale la pena clavar, porque son contraintuitivos para alguien que viene de ML:

- **"El dato vive en un lugar físico, y ese lugar tiene jurisdicción."** Cuando alquilás una GPU en `us-east-1`, los datos de salud de un paciente argentino están en Virginia, bajo ley de EE.UU. La Ley 25.326 exige condiciones para la **transferencia internacional**. Esto es puro hardware → derecho.

- **Shared responsibility model.** AWS te asegura la seguridad *de* la nube (el datacenter, el hardware físico, el hypervisor); vos sos responsable de la seguridad *en* la nube (tu config, tus accesos, tu encriptación). El 90% de los breaches son del lado del cliente — un bucket S3 mal configurado, no un hackeo a Amazon. Buenísimo para responsabilizar al ingeniero.

- **On-prem vs cloud no es una decisión técnica, es una decisión de compliance y costo.** On-prem = control total + CAPEX + vos mantenés todo. Cloud = elasticidad + el proveedor firma el BAA + dependés de su config. Muchos hospitales eligen on-prem *por* regulación, no por performance.

- **Edge / embedded.** Cuando el modelo corre *dentro* del aparato (un marcapasos inteligente, un glucómetro con IA), el hardware **es** el dispositivo médico: certificación IEC 60601/62304, no podés "actualizar el modelo" sin re-validar, y el failure mode es físico e inmediato. Esto cierra el círculo con el eje dispositivo.

- **Secure enclaves / encriptación at-rest.** El disco donde se guardan los datos: si roban el server o un disco se da de baja, ¿el dato es legible? HIPAA Security Rule lo exige; la destrucción certificada de discos es parte del compliance.

Un caso de hardware que conecta perfecto: el famoso patrón de **breaches por discos/laptops robados** — durante años la mayor causa de multas HIPAA no fueron hackers, fueron *laptops sin encriptar perdidas* con datos de pacientes. El hardware físico como vector de incumplimiento.

Esto me arma una **cuarta dimensión transversal** al ciclo de vida que ya teníamos. Te propongo cómo encaja en la estructura:

- La capa hardware se puede dar como **una sección propia** ("¿dónde corre esto?") justo después de datos y antes/junto con dispositivo, o bien **entreverada** en cada etapa del ciclo de vida.

Dos preguntas:

1. **¿Hardware como sección dedicada** (un bloque claro "cloud vs on-prem vs edge") **o transversal** (lo voy tocando en cada etapa)? Para una clase teórica, una sección dedicada suele ser más clara.
2. ¿Querés que entre la dimensión **IEC 60601 / 62304** (normas de hardware/software de dispositivo médico) o eso ya es demasiado y lo mantenemos a nivel "existe y por qué importa"?

### Presenter

1. quiero que tenga una sección dedicada
2. también incluí la dimensión IEC 60601 / 62304

### Agent

Listo — sección de hardware dedicada, con IEC 60601/62304 adentro. Creo que ya tenemos el esqueleto completo. Te lo consolido como **agenda candidata** para que lo veas entero y digas si lo capturamos o seguimos afilando:

```
  ESTRUCTURA CANDIDATA — Clase 16 (teórica)

  0. Apertura — el shock                                        [hook]
     "tu modelo con AUC 0.95 ya es ilegal" — el salto del
     notebook al hospital. Tesis: la regulación define qué
     podés construir y quién responde.

  1. EL DATO — privacidad                                       [eje 1]
     · dato de salud = dato sensible (HIPAA / Ley 25.326)
     · "anonimizar" no es borrar el nombre (18 identificadores)
     · consentimiento, breach notification
     · gap AR: ley de 2000, AAIP, reforma pendiente

  2. LA INFRAESTRUCTURA — ¿dónde corre esto?                    [eje hardware]
     · 3 capas: nube / on-prem / edge-embebido
     · data residency + transferencia internacional (25.326)
     · BAA + shared responsibility model
     · encriptación at-rest, discos robados como vector
     · IEC 60601 (seguridad eléctrica) + IEC 62304 (software disp.)

  3. EL DISPOSITIVO — seguridad y eficacia                      [eje 2]
     · ¿cuándo tu modelo ES un dispositivo médico? (SaMD)
     · lógica de riesgo FDA · 510(k)/De Novo/PCCP
     · ANMAT en AR · casos reales FDA-cleared (IDx-DR)
     · "sugiere" vs "decide" — el umbral

  4. RESPONSABILIDAD CONTINUA                                   [síntesis]
     · monitoreo, model drift, post-market surveillance
     · ¿quién responde cuando falla? (ingeniero/hospital/fabricante)

  5. CASO DE CIERRE — DeepMind / Royal Free                     [aterrizaje]
     · 1.6M registros, buen modelo, desastre legal
     · qué se hizo mal en cada eje que vimos → recap vivo
```

Lo que me gusta de este arco: **el caso de cierre (5) funciona como recap** — podés volver a cada sección preguntando "¿dónde falló esto?" y el caso toca dato, infra y responsabilidad de golpe.

Un par de huecos honestos que conviene que sepas antes de capturar (los marco para que no se pierdan):

- **Datos/cifras concretas** (montos de multas HIPAA, fechas exactas del caso Royal Free, número de identificadores, artículos específicos de la 25.326): los tengo a nivel conceptual, pero conviene **verificar las cifras precisas** en fuentes oficiales antes del slide final.
- **ANMAT**: el marco argentino de software médico es real pero menos documentado que FDA — vale tratarlo como "existe, está menos maduro, acá está el riesgo" más que pretender precisión normativa fina.

### Presenter

listo

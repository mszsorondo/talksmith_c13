# FDA — Software as a Medical Device (SaMD)

> **Procedencia:** la página oficial de FDA dio timeout (fetcher y WebFetch). Síntesis verificada de fuentes secundarias (greenlight.guru, IntuitionLabs, RQM+) sobre el marco IMDRF adoptado por FDA. Verificar contra fda.gov antes de citar literal.

## Definición (IMDRF, adoptada por FDA)
**Software as a Medical Device (SaMD):** software destinado a ser usado para uno o más propósitos médicos, que cumple esos propósitos **sin ser parte del hardware de un dispositivo médico**. (Distinto de "Software in a Medical Device" — SiMD — que sí es parte/controla un aparato físico.)

## Las dos dimensiones del riesgo (framework IMDRF)
El riesgo de una SaMD se categoriza según el cruce de dos atributos:

**(A) Estado de la situación/condición de salud:**
- Crítica (*critical*)
- Seria (*serious*)
- No-seria (*non-serious*)

**(B) Significancia de la información provista por la SaMD a la decisión clínica:**
- Tratar o diagnosticar (*treat or diagnose*)
- Conducir el manejo clínico (*drive clinical management*)
- Informar el manejo clínico (*inform clinical management*)

## Las cuatro categorías de riesgo (I–IV)

```
                        SIGNIFICANCIA DE LA INFORMACIÓN
                   Informa     Conduce     Trata/Diagnostica
  Condición       manejo      manejo
  ──────────────────────────────────────────────────────────
  Crítica          II          III          IV  (mayor riesgo)
  Seria            I           II           III
  No-seria         I           I            II
```
- **Categoría I** — menor riesgo: informa manejo clínico de condición no-seria.
- **Categoría IV** — mayor riesgo: trata/diagnostica en condición crítica.

A mayor categoría, mayor exigencia regulatoria (evidencia clínica, controles).

## Caminos regulatorios FDA
- **510(k)** — equivalencia sustancial a un predicado ya autorizado.
- **De Novo** — para dispositivos novedosos de riesgo bajo/moderado sin predicado (clasificación).
- **PMA** (Premarket Approval) — alto riesgo.

## AI/ML y el problema del "modelo que aprende"
El desafío regulatorio: un modelo de ML que se reentrena cambia su comportamiento → ¿requiere nueva submission por cada update?

**PCCP (Predetermined Change Control Plan):** guía finalizada por FDA en **diciembre 2024** para AI-enabled device software functions. Permite al fabricante **pre-especificar** en la submission original qué modificaciones del algoritmo anticipa y cómo las va a evaluar, e implementarlas sin presentar una nueva solicitud, siempre que siga el protocolo aprobado. Resuelve el choque entre modelos que aprenden y un marco regulatorio diseñado para dispositivos estáticos.

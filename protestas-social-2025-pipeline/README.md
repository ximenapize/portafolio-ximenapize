# Ampliación de la Base de Protestas Sociales mediante Fuentes Digitales (2025)

## Contexto

Gestión de la base histórica de protestas sociales del Observatorio (1980–actualidad, ~25 700 registros). Inicialmente el proceso se hacía por recojo manual  mediante formularios y, por iniciativa propia, automatización del recojo para diarios digitales mediante crawling y scraping.

## Resumen

Diseño y ejecución de un pipeline de cinco fases para ampliar la base histórica de protestas sociales del Observatorio (1980–actualidad, ~25 700 registros) con eventos reportados en medios digitales durante 2025, integrando crawling propio, scraping de texto completo, clasificación asistida por IA y revisión manual.

**Pipeline:** crawling propio por diario → scraping con `trafilatura` → clasificación con Claude Haiku 4.5 contra taxonomías cerradas → revisión manual del equipo → deduplicación y fusión con la base impresa preexistente.

## Resultados

| Fase | Descripción | Resultado |
|---|---|---|
| 1. Crawling | Inventario de titulares por diario (La República, Expreso, El Comercio), filtrado por palabras clave | 595 artículos únicos (412 LR, 106 Expreso, 77 EC) |
| 2. Scraping | Extracción de texto completo con `trafilatura` | 493 artículos con texto útil — status 200 en el 100% de los casos útiles (356 LR, 88 Expreso, 49 EC) |
| 3. Clasificación IA | Claude Haiku 4.5 vía Batch API, contra taxonomías cerradas | 488 artículos clasificados como protesta (98.99%); 603 eventos individuales extraídos |
| 4. Revisión manual | Validación del equipo y desagregación geográfica | 601 filas finales |
| 5. Integración | Deduplicación y fusión con la base impresa preexistente | **720 eventos** en la base 2025 final — 449 con aporte exclusivo de fuentes digitales (62.4%) |

## Métricas de eficiencia

- Consumo de tokens: 2 943 174 input + 430 601 output
- Costo total de clasificación: **USD 5.10** (API estándar) — USD 2.55 con Batch API (–50%)
- Precisión de clasificación IA: 98.99% de los artículos correctamente identificados como evento de protesta

## Stack

Python (crawling propio, `requests`, `trafilatura` para scraping), Claude Haiku 4.5 (Anthropic Batch API) para clasificación de texto, hoja de cálculo compartida para revisión manual y control de calidad.

## Nota metodológica

El pipeline prioriza transparencia y replicabilidad: cada fase queda documentada con sus tasas de pérdida y criterios de filtro, y la clasificación automatizada se somete a revisión manual antes de integrarse a la base histórica, evitando que un evento quede contabilizado solo por criterio del modelo.

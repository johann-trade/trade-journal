Projekt: Trade Journal
==========================

Zielsetzung
-----------

> Das Projekt "Trade Journal"
> zielt darauf ab, eine webbasierte Plattform bereitzustellen,
> auf der Mitglieder ihre Handelsaktivitäten protokollieren, verfolgen und analysieren
> können. Die Plattform soll einfach und intuitiv zu bedienen sein, visuell ansprechend und
> übersichtlich gestaltet sein und umfangreiche Einblicke bieten, um die
> Handelsentscheidungen der Benutzer zu verbessern.

Anforderungen:

> 1. Eingabe von getätigten Orders auf Aktien
> 2. Übersicht aller getätigten Orders (History)
> 3. Anzeige abgeschlossener Trades
> 4. Anzeige offener Aktienpositionen
> 5. Auswertung von Trades
>    - Gewinn/Verlust pro Trade
>    - Wie lange lief der Trade
> 6. Eingabe des eingezahlten Kapitals ins Depot
> 7. Auswertung Depot
>    - Anzeige aktueller Depotwert
>    - Anzahl abgeschlossener Trades
>    - Trefferwahrscheinlichkeit (Anteil der Trades mit Gewinn zu Anzahl gesamter Trades)
>    - Profitfaktor (Gewinne/Verluste)
>    - Durchschnittsgewinn/Verlust
>    - Durchschnittliche Haltedauer
> 8. Eingabe von Learnings zu einem Trade (Notizfeld)
> 9. Eingabe eines Kommentars zu einer Order

Architektur & Technologie-Stack
-------------------------------

Überblick: TS/Node Monorepo mit pnpm/turborepo bestehend aus Frontend (TS/React) und Backend (TS/Node/FastApi). Docker compose für lolkale Entwicklung und Tests.

### Frontend: React/TypeScript

- Alternativ Vuejs, aber bislang wird bei PJM nur React verwendet, daher bietet es sich an in diesem Ökosystem zu bleiben.
- In der ersten Version kein Next.js (Kosten/Nutzen)
- UI-Bibliothek: Radix UI. Keine große Präferenz, jede andere UI-Bibliothek ist auch möglich.
- Translations über i18next
- Cache-Management über Tanstack Query (Cache over State)
- Kein State-Management bis es nicht nötig wird (dann ggf Zustand)
- Validierung: Zod
- Routing über Tanstack Router

### Backend: Node.js mit Fastify

- Alternativ Go oder Python/Pydantic/FastApi
- ORM: Sequelize
- Datenbank: PostgreSQL
- API-Schema: REST
- Authentifizierung und User Management über Auth0
- Ggf. Feature Flags über OpenFeature
- Automatische Api-Docks über Swagger/OpenApi

### CI/CD: GitHub Actions oder Gitlab CI

In meiner Erfahrung funktioniert beides relativ gleich gut. In zweiten Ausbauschritt wären automatische per-branch-Staging deployments und Continues Deployment von main in production sinnvoll.

### Testing: E2E-Tests mit Playwright und Codecept

Ich bevorzuge umfangreiche E2E- sowie API-Tests sowie Typechecking und Linting in der Pipelines über Unittests die mehr im Einzelfall nützlich sind (gern auch als doctests).

- E2E mit Playwright und ggf Codecept
- linting per eslint und tsc, formatting mit prettier

### Hosting

Unentschieden und für den Prototypen nicht entscheidend; evtl. Azure, Vercel oder AWS. Der Prototyp wird auf Hetzner gehostet.

## Grobe Aufwandschätzung (Arbeitspakete)

Die Aufwandschätzung ist in Stunden angegeben und umfasst die wichtigsten Arbeitspakete für die Implementierung des Trade Journals. Die Schätzung ist grob und kann je nach Komplexität und Anforderungen variieren.

| Arbeitspaket | Aufwand (Stunden) |
|--------------|------------------|
| [Initial Monorepo setup](https://github.com/johann-trade/trade-journal/issues/1) | 4 |
| [Intial layout + Design UI](https://github.com/johann-trade/trade-journal/issues/3) | 2 |
| [Order- Api](https://github.com/johann-trade/trade-journal/issues/2) | 2 |
| [Order UI](https://github.com/johann-trade/trade-journal/issues/4) | 2 |
| [Trades Api](https://github.com/johann-trade/trade-journal/issues/5) | 3 |
| [Trades UI](https://github.com/johann-trade/trade-journal/issues/8) | 2 |
| [Open Stock Api](https://github.com/johann-trade/trade-journal/issues/6) | 2 |
| [Open Stock UI](https://github.com/johann-trade/trade-journal/issues/9) | 3 |
| [Trade analytics api](https://github.com/johann-trade/trade-journal/issues/7) | 3 |
| [Trade analytics UI](https://github.com/johann-trade/trade-journal/issues/10) | 4 |
| [Depot API](https://github.com/johann-trade/trade-journal/issues/11) | 3 |
| [Depot UI](https://github.com/johann-trade/trade-journal/issues/12) | 3 |
| [Add notes to trades](https://github.com/johann-trade/trade-journal/issues/13) | 4 |
| [Add notes to order](https://github.com/johann-trade/trade-journal/issues/14) | 4 |

| **Gesamt** | **ca. 41 Stunden** |

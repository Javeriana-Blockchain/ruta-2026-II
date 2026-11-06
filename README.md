# Ruta JaveBlockchain 2026-II

Repositorio central del semillero de blockchain de la Pontificia Universidad Javeriana. Aquí viven las guías de cada semana, los recursos de estudio, las actas de office hours y, en `participantes/`, la ficha de cada persona de la ruta.

## Calendario

| Fecha | Sesión | Entrega previa (lunes 11:59 p. m.) |
|---|---|---|
| Vie 16 oct | S1 · Arranque y primera transacción | — |
| Vie 23 oct | S2 · Activos (Fundamentos) · Primer contrato Soroban (Builders) | PR #1: tu ficha en `participantes/` |
| Vie 30 oct | S3 · Wallets, anclas e integraciones (40 min; el taller se hace en casa) | PR #2 (por equipo) |
| Vie 6 nov | S4 · Taller integrador: reto sin IA, integración y prueba oral (135 min) | PR #3 (por equipo) |
| Vie 13 nov | S5 · Demo Day | PR #4 (por equipo) |

Office hours: todos los martes, virtual, 60 min (enlace en el grupo).

## Guías

- [Semana 1 · PR #1: tu ficha de participante](GUIA_PR1.md)
- [Semana 3 · Taller en casa de la sesión 3 y PR #3: tu app con wallet / contrato + frontend](GUIA_S3.md) ([PDF](GUIA_S3.pdf))
- [Semana 4 · PR #4: el proyecto listo para el Demo Day (README final, pitch, lista de verificación de la demo)](GUIA_S4.md) ([PDF](GUIA_S4.pdf))

## Recursos de estudio

**Base (todos)**
- [Stellar Docs → Learn → Fundamentals](https://developers.stellar.org/docs/learn/fundamentals): cuentas, activos, operaciones, transacciones, fees, consenso. Lectura obligatoria S1–S2.
- [Stellar Lab](https://lab.stellar.org): construir, firmar y enviar transacciones a mano en testnet.
- [stellar.expert (testnet)](https://stellar.expert/explorer/testnet): explorador.
- [Freighter](https://www.freighter.app): wallet de navegador.

**Builders**
- [Getting Started: Setup](https://developers.stellar.org/docs/build/smart-contracts/getting-started/setup) · Hello World · Deploy to Testnet.
- [Soroban Examples](https://github.com/stellar/soroban-examples): contratos de referencia.
- [Rust Book](https://doc.rust-lang.org/book/), caps. 1–6 y 10.

**Fundamentos**
- [Stellar SDK JavaScript](https://github.com/stellar/js-stellar-sdk) y [Freighter API](https://docs.freighter.app).
- [Anchors y SEPs](https://developers.stellar.org/docs/learn/fundamentals/anchors).
- [Stellar Quest](https://quest.stellar.org): retos gamificados.

**Programa**
- [Stellar Ambassador Program](https://communityfund.stellar.org/ambassadors) · [Stellar Community Fund](https://communityfund.stellar.org).

## Plantillas para los repos de equipo (desde la S2)

- `Javeriana-Blockchain/template-fundamentos`
- `Javeriana-Blockchain/template-builders`

## Starters por sesión (`starters/`)

Código que aparece después de que los repos de equipo ya existen. Cada equipo lo copia a su repo siguiendo la guía de la semana (Parte 0 de `GUIA_S3.md`).

| Carpeta | Ruta | Qué es |
|---|---|---|
| `starters/s3-fundamentos-app/` | Fundamentos | `jave-wallet-starter` v2: balances por activo, trustline y pago en cualquier activo con Freighter |
| `starters/s3-fundamentos-docs/` | Fundamentos | `PANTALLAS.md`: plantilla de las tres pantallas y la operación que dispara cada una |
| `starters/s3-builders-app/` | Builders | `jave-contract-starter`: frontend Vite + React que invoca tu contrato con `contract.Client.from` y firma con Freighter |
| `starters/s3-builders-docs/` | Builders | `DISENO_CONTRATO.md`: plantilla de una página para el diseño del contrato del Demo Day |
| `starters/ci-con-app.yml` | Builders | Workflow de CI que compila contratos y `app/` |
| `starters/GITIGNORE_APP.txt` | Todos | Líneas que faltan en el `.gitignore` de los repos creados antes de la S3 |

## Política de uso de IA

La IA está permitida y se enseña a usarla bien. Lo único prohibido es ocultarla: cada PR declara qué se generó con IA y qué se entendió y modificó. Ver `CONTRIBUTING.md`.

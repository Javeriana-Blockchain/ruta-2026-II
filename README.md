# Ruta JaveBlockchain 2026-II

Repositorio central del semillero de blockchain de la Pontificia Universidad Javeriana. Aquí viven las guías de cada semana, los recursos de estudio, las actas de office hours y, en `participantes/`, la ficha de cada persona de la ruta.

## Calendario

| Fecha | Sesión | Entrega previa (lunes 11:59 p. m.) |
|---|---|---|
| Vie 16 oct | S1 · Arranque y primera transacción | — |
| Vie 23 oct | S2 · Activos (Fundamentos) · Primer contrato Soroban (Builders) | PR #1: tu ficha en `participantes/` |
| Vie 30 oct | S3 · Wallets, anclas y dApp | PR #2 (por equipo) |
| Vie 6 nov | S4 · Taller integrador y reto sin IA | PR #3 (por equipo) |
| Vie 13 nov | S5 · Demo Day | PR #4 (por equipo) |

Office hours: todos los martes, virtual, 60 min (enlace en el grupo).

## Guías

- [Semana 1 · PR #1: tu ficha de participante](GUIA_PR1.md)

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

## Política de uso de IA

La IA está permitida y se enseña a usarla bien. Lo único prohibido es ocultarla: cada PR declara qué se generó con IA y qué se entendió y modificó. Ver `CONTRIBUTING.md`.

---

## Personal Notes (Andrés Chanchi)

> **Not mine, but useful:** the section above is the professor’s. Everything below is my own reference for setting up a fresh laptop and understanding the architecture. Not part of any PR.


### Fresh laptop setup (WSL2 / Ubuntu / Debian)

These are the commands I use to get a Stellar development environment ready from zero. Copy-paste friendly.

#### 0. System prerequisites

```bash
sudo apt update && sudo apt install -y build-essential curl git
```

`build-essential` is needed if `stellar-cli` has to be built from source or if any native Rust crate needs a C linker.

#### 1. Git identity + SSH commit signing (local only)

This laptop is shared, so I keep identity and signing keys at the **local** repo level, never global.

```bash
# Inside the cloned repo
git config --local user.name "Andres Chanchi"
git config --local user.email "4chanchi@gmail.com"
git config --local gpg.format ssh
git config --local user.signingkey /home/route/...pub
git config --local commit.gpgsign true
```


#### 2. Rust + WebAssembly target

Stellar contracts need **Rust ≥ 1.84.0** because `wasm32v1-none` is only available from that version onward. My 1.98.1 is fine.

```bash
# Install Rust via rustup if not present
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source "$HOME/.cargo/env"

# Add the only WASM target Soroban needs
rustup target add wasm32v1-none
rustup target list --installed
# Expected: wasm32-unknown-unknown, wasm32v1-none, x86_64-unknown-linux-gnu
```

#### 3. Stellar CLI

The official install script is the fastest path on Linux/WSL.

```bash
curl -fsSL https://github.com/stellar/stellar-cli/raw/main/install.sh | sh
# It installs to ~/.local/bin
export PATH="$HOME/.local/bin:$PATH"   # add to ~/.bashrc to persist

stellar --version
# Expected: stellar 28.1.0 (protocol 29 era)
```

If the script fails, the fallback is `cargo install --locked stellar-cli` (10–20 min compile), but the script is usually enough.

#### 4. Testnet key

```bash
stellar keys generate alice --network testnet --fund
stellar keys address alice
# → G... (56 chars)
```

`alice` lives in `~/.config/stellar/identity/alice.toml`. Never commit that file or the `S...` secret. I mean, .gitignore papu

- SEP = ERC
- CAP = EIP

---

### Stellar vs. EVM: Architecture notes for protocol engineers

These notes map what I already know to Stellar’s model.

#### 1. Consensus & finality

Stellar uses the **Stellar Consensus Protocol (SCP)**, a federated Byzantine agreement (FBA) system. There is no PoW or PoS. Each validator chooses its own **quorum slices**, prioritizing safety over liveness: the network can halt rather than accept an invalid ledger. The trade-off is explicit: Stellar is more federated than Ethereum (10 Tier-1 organizations, Nakamoto coefficient 3), but it gives 3–5s finality and predictable fees (base 100 stroops = 0.00001 XLM) with a VCG-style auction for surge pricing.

#### 2. Cryptography: Ed25519 and post-quantum plans

Native account signatures use **Ed25519** on the `edwards25519` curve. Public keys are 32 bytes, private keys 64 bytes. Unlike ECDSA on `secp256k1`, Ed25519 is deterministic and fast to verify, which matters in a concurrent runtime like Soroban. **BLS signatures** are not native for base accounts but are relevant for non-interactive aggregation (batching, agent micropayments). A **post-quantum plan (QPP)** exists to add ML-DSA/Dilithium signers to Soroban accounts around 2026–2027.

#### 3. Address format: StrKey, not 0x

Stellar addresses use **StrKey** (Base32) with a version byte, 32-byte payload, and CRC16 checksum → 56 characters. Prefix `G...` = account; `C...` = contract. The checksum catches typos before funds leave.

#### 4. Soroban runtime

Soroban compiles Rust to WASM. Key differences from Stylus:

- **Contract size limit:** 128 KB on mainnet (vs. 24 KB for EVM). No automatic fragmentation like Stylus; aim for 64 KB for efficiency.
- **Parallel execution (CAP-0063):** Each transaction declares a **footprint** (ledger keys it will read/write). Non-conflicting transactions run in parallel.
- **State model:** `Instance` (global config, loaded every call, 64 KiB limit), `Persistent` (critical data), `Temporary` (cheap, expiring).
- **Rent:** You pay for TTL, not a one-time storage slot. If TTL is not extended, temporary data is deleted and persistent data is archived.

#### 5. Account abstraction & auth

Soroban has native AA via `__check_auth`. When a contract calls `Address::require_auth`, the host invokes the account contract’s `__check_auth` to validate the authorization. **Protocol 27 / CAP-71** introduced **delegated authentication**, allowing an account to delegate its `__check_auth` logic to registered signers (modular multisig). There is no `msg.sender`; `require_auth()` is the explicit path.

#### 6. ZK primitives

**Protocol 25 (X-Ray)** added host functions for **BN254** (pairing-friendly curve) and **Poseidon/Poseidon2** (ZK-friendly hashes). Groth16 verification costs ~12M CPU instructions ≈ 1,100 stroops (fractions of a cent), well within the 100M-instruction transaction budget. The `stellar-zk` devkit supports **Groth16 (Circom)**, **UltraHonk (Noir)**, and **RISC Zero (Rust zkVM)**.

#### 7. Agent payments (x402)

The **x402** protocol turns HTTP `402 Payment Required` into a programmatic per-request payment mechanism for AI agents/APIs. On Stellar it uses **Soroban authorization entries** signed by the client and settled via a facilitator. BLS aggregation is a natural fit for high-frequency agent micropayment sessions, collapsing many interactions into a single on-chain signature.

#### 8. Ecosystem & institutional reality

Stellar hosts billions in tokenized RWAs (Franklin Templeton, Spiko). Payment rails include MoneyGram, BVNK (Mastercard), Tether (USDT0), and UN programs. **Chainlink** data feeds/streams are live on mainnet/testnet, but **CCIP is not deployed in production** yet (adapter code only). The SDF has a **$100M Soroban adoption fund** plus the **Stellar Community Fund (SCF)** with up to **$150k in XLM** per round.

#### 9. Resource optimization (gas vs. Soroban)

Soroban does not use abstract gas; it measures **CPU, memory, and I/O**.

- **Avoid:** storage reads/writes inside loops, large `Instance` data, unnecessary `clone()`.
- **Prefer:** accumulate changes in memory and write once, `Symbol` constants for storage keys, keepers to extend TTL, events for historical data instead of storage writes.

#### 10. Official links (pinned)

- Docs root: https://developers.stellar.org/docs
- Account abstraction & authorization: https://developers.stellar.org/docs/learn/fundamentals/contract-development/authorization#account-abstraction
- Delegated auth example (CAP-71): https://developers.stellar.org/docs/build/smart-contracts/example-contracts/delegate-auth
- ZK proofs: https://developers.stellar.org/docs/learn/fundamentals/contract-development/zk
- Agent payments (x402): https://developers.stellar.org/docs/build/agentic-payments/x402
- Agent payments (MPP): https://developers.stellar.org/docs/build/agentic-payments/mpp
- ZK devkit (`stellar-zk`): https://github.com/salazarsebas/stellar-zk

---

*Note to self: Stellar is not trying to replace EVM composability. It is a deterministic, highly concurrent, and predictable backend for real-world financial applications. The mental shift is from “gas” to measured resources and from “msg.sender” to explicit `require_auth`.*

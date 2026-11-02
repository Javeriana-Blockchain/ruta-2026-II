# André Landinez

| Campo | Valor |
|---|---|
| Usuario de GitHub | @andreMD287 |
| Carrera y semestre | Ingeniería de Sistemas, 9.º |
| Nivel | Builders |
| Dirección pública de testnet | `GAOKEU3JCLOTL3DY55HRKFYQJJDFFAR5CFSMJUHFAU42KPB5IKOVAUZ6` |
| Hash de mi primera transacción | `a271d654f7f37ad9684484a43fbbda2780913c3e824832b89a0341c68017a57c` |
| Enlace en el explorador | https://stellar.expert/explorer/testnet/tx/a271d654f7f37ad9684484a43fbbda2780913c3e824832b89a0341c68017a57c |

## Mi primera transacción (máx. 150 palabras, en mis palabras)

La hice con `stellar-cli` desde mi llave `alice`, no con Freighter. El comando armó una transacción con una sola operación de pago: 10 XLM desde mi cuenta `alice` hacia otra cuenta mía de testnet (`GCSB…MULF`). Incluyó mi cuenta como origen, el siguiente número de secuencia y la comisión. La firmó con mi llave secreta, que queda guardada en mi computador y no viaja: a la red solo se envía la transacción ya firmada, y cualquiera puede comprobar la firma con mi llave pública. El fee lo pagó mi cuenta, por ser la de origen: 100 stroops (0,00001 XLM). Comprobé que ocurrió consultando el hash en la red de pruebas: quedó exitosa en el ledger 5419050, con una operación de 10 XLM y fee de 100 stroops.

## Para armar equipos (se usa el viernes 23)

| Campo | Valor |
|---|---|
| Qué sé hacer | Contratos en Soroban/Rust (escribir, probar y desplegar en testnet con stellar-cli y Caatinga); desarrollo de sistemas. |
| Qué quiero aprender en la ruta | A conectar los contratos con un frontend y con wallets, y a diseñar controles de transparencia confiables. |
| Un problema que me gustaría resolver | Que las donaciones para fauna rescatada del tráfico ilegal se puedan rastrear: qué se recibió, en qué se gastó y qué evidencia lo respalda (proyecto Raíz Silvestre). |
| Ya tengo con quién hacer equipo | sí: @duraznito16 |

## Solo Builders: entorno

```
$ rustc --version
rustc 1.93.1 (01f6ddf75 2026-02-11)

$ stellar --version
stellar 23.1.4 (4b99a259b43aef27ca0ca07134ffe293b3f748bc)
stellar-xdr 23.0.0 (e83a6337204ecfdb0ac0d44ffb857130c1249b1b)
xdr curr (4b7a2ef7931ab2ca2499be68d849f38190b443ca)

$ stellar keys address alice
GAOKEU3JCLOTL3DY55HRKFYQJJDFFAR5CFSMJUHFAU42KPB5IKOVAUZ6
```

cargo test: 2 passed

## Declaración de uso de IA para este archivo

Usé IA (Claude Code) para clonar el repositorio, enviar la transacción de 10 XLM con stellar-cli, verificar el resultado en la red y redactar un borrador de la explicación y de esta ficha. Lo que quedó escrito sobre mi transacción corresponde a datos reales que verifiqué en testnet.

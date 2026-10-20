# Andrés Chanchi

| Campo | Valor |
|---|---|
| Usuario de GitHub | @andreschanchi |
| Carrera y semestre | Ex-estudiante de Matemáticas (Universidad Distrital) · Actualmente autodidacta |
| Nivel | Builders |
| Dirección pública de testnet | GCFLQXMZWK2QSJYCPDAAOTWLQNVKLM6RJXWJDHYZSIF2SQJLUSNDV5QP |
| Hash de mi primera transacción | 57b74a61f71ae38a9c9dd4762f68a619654360db23827792cef5fcfa990a6b10 |
| Enlace en el explorador | https://stellar.expert/explorer/testnet/tx/57b74a61f71ae38a9c9dd4762f68a619654360db23827792cef5fcfa990a6b10 |

## Mi primera transacción

Ejecuté `stellar tx new payment` desde `alice` hacia mi wallet móvil, con `--amount 100000000` (100 millones de stroops = 10 XLM, porque 1 XLM = 10,000,000 stroops). Antes había probado con `--amount 10`, pero eso envió solo 10 stroops (0.000001 XLM); lo detecté al comparar el monto en el explorador. La transacción se firmó localmente con la llave privada de `alice` —la firma aparece en el detalle del explorer— y esa llave nunca salió del equipo. El fee de red (0.00001 XLM) lo pagó la cuenta origen `alice`. Verifiqué el resultado en Stellar Expert: estado `Successful`, ledger 5281065, y el detalle confirma `sent 10 XLM` desde `GCFL…V5QP` hacia `GCSI…VVDQ`.

## Para armar equipos

| Campo | Valor |
|---|---|
| Qué sé hacer | Rust básico, Git, scripting y muchas ganas de aprender |
| Qué quiero aprender en la ruta | Habilidades blandas, trabajo en equipo, ejecución de producto y aprender a comunicar y vender una idea (producto y negocio) |
| Un problema que me gustaría resolver | En Bogotá, muchos jóvenes y trabajadores independientes no pueden acceder a vivienda propia ni construir historial crediticio, mientras los propietarios tienen su capital atrapado en inmuebles poco líquidos. Quiero explorar cómo tokenizar contratos de arriendo (RWA) para dar liquidez a los propietarios y permitir que los inquilinos construyan historial, usando pagos programables en Stellar. |
| Ya tengo con quién hacer equipo | no |

## Solo Builders: entorno

```text
$ rustc --version
rustc 1.98.1 (48a229cea 2026-09-01)

$ stellar --version
stellar 28.1.0 (c0f4d0da891bbf214c08b8c5035ae6db80e9a3bd)
stellar-xdr 28.0.0 (d0f1330e43c3a2c0c616da30698b24140d4eea72)
xdr (9c9c145953e80990d6ff1ae3a6a973a0ce6d0694)

$ stellar keys address alice
GCFLQXMZWK2QSJYCPDAAOTWLQNVKLM6RJXWJDHYZSIF2SQJLUSNDV5QP
```

`cargo test: 2 passed`

## Declaración de uso de IA para este archivo

Usé IA (DeepSeek) para redactar el borrador del párrafo y verificar sintaxis de comandos. Los comandos los ejecuté, verifiqué y ajusté yo mismo (incluida la corrección de `--amount 10` a `--amount 100000000` al entender stroops); el hash, la transacción y los enlaces son reales y verificables en el explorador.

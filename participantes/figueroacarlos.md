# Carlos Andrés Figueroa Vega

| Campo | Valor |
|---|---|
| Usuario de GitHub | @FigueroaCarlos |
| Carrera y semestre | Ingeniería de Sistemas, 4.º |
| Nivel | Fundamentos |
| Dirección pública de testnet | `G<55 caracteres más>` |
| Hash de mi primera transacción | `<64 caracteres hexadecimales>` |
| Enlace en el explorador | https://stellar.expert/explorer/testnet/tx/<hash> |

## Mi primera transacción (máx. 150 palabras, en mis palabras)

Cuando presioné *Send*, Freighter armó una transacción con mi cuenta como origen, el siguiente número de secuencia de mi cuenta, un fee máximo y una sola operación *Payment* de 10 XLM (el activo nativo) hacia la dirección destino, todo marcado para la red testnet. Luego la firmó con mi llave secreta (la que empieza por S), que Freighter guarda cifrada dentro de la extensión: la firma se calcula ahí mismo y a la red solo viaja la transacción firmada, nunca la llave. Con mi llave pública (G…) cualquier nodo puede comprobar que la firma es mía sin conocer la secreta. El fee lo pagó mi cuenta, no quien recibió: 0,00001 XLM (100 stroops). Para verificarla busqué el hash en stellar.expert/explorer/testnet: aparece como exitosa, con el ledger en que quedó incluida, y mi saldo bajó 10,00001 XLM.

## Para armar equipos (se usa el viernes 23)

| Campo | Valor |
|---|---|
| Qué sé hacer | <p. ej. React, Python, diseño en Figma, nada todavía y con ganas> |
| Qué quiero aprender en la ruta | <una frase> |
| Un problema que me gustaría resolver | <una frase; puede ser de la universidad, el barrio, la familia> |
| Ya tengo con quién hacer equipo | <no / sí: @usuario1, @usuario2> |

## Solo Builders: entorno

No aplica: estoy en nivel Fundamentos.

## Declaración de uso de IA para este archivo

Usé IA (Claude Code) para preparar el repositorio (fork, rama y copia de la plantilla) y para redactar el párrafo «Mi primera transacción» con los valores típicos de testnet; todavía no los he comparado con mi transacción. Lo revisé y puedo explicar cada parte.

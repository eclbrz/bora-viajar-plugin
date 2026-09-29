---
name: sugerir-reservas
description: Analisa o roteiro de uma viagem do Bora Viajar e aponta o que ainda falta reservar (hospedagem por noite, transfers, restaurantes e ingressos que pedem reserva). Use quando o usuário perguntar "o que falta reservar?", "quais reservas eu preciso fazer?" ou pedir para completar as reservas de uma viagem.
---

# Sugerir reservas

Encontra as lacunas de reserva de uma viagem existente.

## Passos

1. Identifique a viagem: se o usuário não passou o `tripId`, chame `listar_viagens` e peça para escolher.
2. Leia a viagem com o resource `viagem://{tripId}` (markdown com roteiro, reservas e pessoas) ou, se o resource não estiver disponível, com a tool `get_viagem`.
3. Aponte o que falta reservar:
   - hospedagem por noite (noites sem `stay` cobrindo);
   - transfers entre cidades e do/para aeroportos;
   - restaurantes que pedem reserva;
   - ingressos e passeios com fila ou lotação.
4. Ofereça adicionar cada sugestão via `criar_reserva` (avulsa) ou `importar_roteiro` com `tripId` (várias de uma vez, upsert por `externalId`).

## Regras

- Não invente confirmações: reservas novas entram como `aPesquisar`.
- Só grave depois de o usuário confirmar quais sugestões quer.
- Reservas exigem papel de planner ou assessor na viagem; se a tool recusar, avise o usuário.

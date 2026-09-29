---
name: planejar-viagem
description: Monta um roteiro completo dia a dia para um destino e grava tudo de uma vez no Bora Viajar com importar_roteiro. Use quando o usuário quiser planejar, montar ou criar uma viagem nova ("planeja 5 dias em Lisboa", "monta um roteiro pra Gramado com as crianças", "quero viajar pra…") ou importar um roteiro que já tem, mesmo sem citar o Bora Viajar.
---

# Planejar viagem

Monta um roteiro dia a dia para um destino e grava no Bora Viajar de uma vez, pela tool `importar_roteiro` do MCP `bora-viajar`.

## Entrada

Pergunte só o que faltar, uma coisa de cada vez:

- **destino** (cidade/região, ex.: Lisboa);
- **duração** em dias;
- **perfil**: família com crianças, casal, mochilão, etc.

## Passos

1. Confirme com o usuário as **datas reais** (yyyy-mm-dd) e o **fuso IANA do destino** (ex.: `Europe/Lisbon`). Não grave sem isso.
2. Monte o roteiro dia a dia: atividades, refeições e deslocamentos, com horário (hh:mm) e **local geocodável** (nome do lugar + cidade) em cada item. Tipos de item: `activity`, `meal`, `transfer`, `free`, `note`.
3. Sugira reservas (voo, hospedagem, passeios, restaurantes) com status `aPesquisar`. Tipos de reserva: `flight`, `train`, `bus`, `boat`, `stay`, `car`, `restaurant`, `tour`, `other`. Defina também o motivo/ocasião adequado da viagem.
4. Mostre o resumo ao usuário e peça confirmação.
5. Grave tudo com **uma única chamada** a `importar_roteiro`, com `itinerary = { trip, days, reservations }`. Sem `tripId` cria uma viagem nova; com `tripId` faz upsert idempotente por `externalId` (use `externalId` estável nos itens/reservas se for possível reimportar depois).

## Regras

- Nunca invente confirmações: reservas novas entram sempre como `aPesquisar`.
- Criar viagem exige o papel de criador no app; se a tool recusar, explique ao usuário em vez de tentar contornar.
- Depois de gravar, informe o `tripId` retornado e ofereça `revisar-roteiro` ou `sugerir-reservas`.

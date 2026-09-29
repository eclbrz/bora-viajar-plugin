---
name: registrar-voos
description: Converte um print, PDF, e-mail ou texto de reserva aérea (localizador/PNR, trechos, passageiros, assentos) em voos estruturados no Bora Viajar com registrar_voos. Use quando o usuário colar ou anexar uma passagem, cartão de embarque, confirmação de voo ou disser "registra esses voos", mesmo sem citar a tool.
---

# Registrar voos

Transforma uma reserva aérea (imagem, PDF ou texto) no payload da tool `registrar_voos`, que cria **1 reserva por trecho** e o assento por passageiro. É **idempotente** por `locator + voo + dia`: rodar de novo atualiza em vez de duplicar.

## Passos

1. Identifique a viagem de destino (`listar_viagens`; `tripId` obrigatório). Para ligar passageiros a pessoas, chame `listar_membros` e case cada nome com o `memberId`.
2. Leia o anexo/texto e extraia, sem inventar nada que não esteja lá:
   - `locator`: código da reserva (PNR);
   - `passengers[]`: `{ key, memberId?, name }`, com `key` curta e estável (ex.: `edu`, `ana`), usada nos assentos. Infante é um membro sem assento;
   - `segments[]`, um por trecho:
     - `flightNo`, `date` (yyyy-mm-dd, **dia local da partida**), `marketingCarrier?`, `operatingCarrier?`, `cabin?`, `fareFamily?`, `aircraft?`, `durationMin?`, `status?`;
     - `origin`: `{ code, city?, tz, time (hh:mm), terminal? }`;
     - `dest`: `{ code, city?, tz, time (hh:mm), terminal?, arrivalDayOffset? }`. Use `arrivalDayOffset` (ex.: 1) quando chega no dia seguinte;
     - `seats[]`: `{ pax: <key>, seat?, baggage?, ticketStatus? }`.
3. Os horários são da **parede local** de cada aeroporto e `tz` é o fuso IANA (ex.: `America/Sao_Paulo`, `Europe/Lisbon`). Não converta para UTC.
4. Monte o payload `{ locator, passengers, segments, criarItens? }`. Use `criarItens: true` se o usuário quiser também os itens vinculados no roteiro (padrão: false).
5. **Mostre uma tabela de conferência** (trecho, horário local, passageiros e assentos) e peça confirmação. Se algo estiver ilegível ou ambíguo, pergunte em vez de chutar.
6. Chame `registrar_voos` com o `tripId` e o payload.

## Regras

- Não chute assento, horário ou fuso. Campo ausente fica ausente.
- Franquia de bagagem (kg/peças) é manual: se o usuário informar, ajuste depois com `editar_reserva` (`flight.baggageAllowance`).
- Exige papel de planner ou assessor na viagem; se recusar, avise o usuário.
- Depois de registrar, ofereça `sugerir-bagagem` (a franquia alimenta o aviso de excesso na mala).

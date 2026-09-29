---
name: revisar-roteiro
description: Revisa criticamente o roteiro de uma viagem do Bora Viajar (ritmo dos dias, deslocamentos ilógicos, horários conflitantes, pontas soltas) e propõe correções concretas. Use quando o usuário pedir para revisar, criticar, checar ou melhorar um roteiro/itinerário.
---

# Revisar roteiro

Faz uma revisão crítica do roteiro e propõe correções, sem aplicar nada sem confirmação.

## Passos

1. Identifique a viagem: sem `tripId`, chame `listar_viagens` e peça para escolher.
2. Leia o resource `viagem://{tripId}` (ou a tool `get_viagem`).
3. Avalie:
   - dias cheios demais ou ociosos;
   - deslocamentos ilógicos (zigue-zague geográfico);
   - horários conflitantes;
   - refeições e atrações que pedem reserva e ainda estão `aPesquisar`;
   - pontas soltas: item sem horário, pin faltando ou claramente errado, reserva no dia errado.
4. Liste os problemas **em ordem de impacto**. Para cada um, proponha a correção concreta e a tool que a aplicaria: `editar_item`, `mover_item`, `editar_reserva`, `remover_item`.
5. Aplique **só o que o usuário confirmar**.

## Regras

- Nunca aplique alterações sem confirmação explícita.
- `remover_item` e `remover_reserva` apagam de vez: peça confirmação item a item.

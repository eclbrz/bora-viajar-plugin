---
name: otimizar-dia
description: Otimiza a ordem das paradas e os deslocamentos de um único dia de uma viagem do Bora Viajar, agrupando por região e encaixando refeições. Use quando o usuário quiser reorganizar, encurtar deslocamentos ou "arrumar" um dia específico do roteiro.
---

# Otimizar dia

Reordena um único dia para reduzir deslocamento e encaixar as refeições.

## Passos

1. Descubra a viagem (`listar_viagens` se faltar o `tripId`) e o **dia** (yyyy-mm-dd); pergunte se não foi dito.
2. Leia o resource `viagem://{tripId}` (ou `get_viagem`) e foque no dia escolhido.
3. Reordene as paradas para minimizar deslocamento (agrupando por bairro/região), encaixe as refeições em horários coerentes, sinalize transfers apertados e buracos no dia.
4. Proponha a nova ordem com horários e mostre o que muda em relação ao atual.
5. Depois da confirmação, aplique com `mover_item` e `editar_item`.

## Regras

- Respeite janelas fixas: reservas com hora marcada, e soneca de criança se constar nas notas.
- Nunca aplique sem confirmação.

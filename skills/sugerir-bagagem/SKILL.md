---
name: sugerir-bagagem
description: Monta a mala recomendada de um viajante do Bora Viajar a partir do clima, roteiro, duração e perfil, e grava com gerar_bagagem. Use quando o usuário pedir para montar, sugerir ou revisar a mala/bagagem, "o que levar" ou lista de itens de uma viagem.
---

# Sugerir bagagem

Você monta a lista; a tool `gerar_bagagem` só **materializa** (não chama nenhum LLM).

## Passos

1. Identifique a viagem (`listar_viagens` se faltar) e chame `listar_membros` para saber de quem é a mala e obter o `memberId`.
2. Leia o resource `viagem://{tripId}` (destinos, datas, duração, atividades) e `get_perfil` (estilo de mala, hábitos/kits, tamanhos, idade e necessidades especiais). Se o perfil estiver vazio, sugira antes a skill `anamnese-viajante`.
3. Monte a lista item a item:
   - `recommended` coerente com a **duração**, o **clima do período** e as **atividades**;
   - **escalado pelo estilo**: enxuto, equilibrado ou conservador;
   - se a viagem cobre trechos com climas diferentes, preencha `segment` por trecho.
4. Mostre o resumo e peça confirmação.
5. Grave com **uma chamada** a `gerar_bagagem` (`tripId`, `memberId`, `items`).

## Regras

- O merge é **não destrutivo**: re-rodar atualiza só o `recommended`, sem apagar `planned`/`owned`/`acquire`/`packed` que a pessoa já ajustou. Idempotente por nome + categoria.
- Para ajustes pontuais de um item, use `editar_item_bagagem`.
- Participante só grava a própria mala; o planner grava qualquer uma. Se a tool recusar, explique.

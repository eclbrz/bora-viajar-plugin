---
name: anamnese-viajante
description: Conduz uma entrevista curta e conversacional (anamnese) para montar o perfil de um viajante do Bora Viajar (estilo de mala, tamanhos, hábitos, nascimento, necessidades especiais) e grava com salvar_perfil. Use quando o usuário quiser criar ou atualizar o perfil de uma pessoa da viagem, ou antes de montar a mala.
---

# Anamnese do viajante

É uma **conversa, não um formulário**: uma pergunta de cada vez, em linguagem natural, seja breve.

## Passos

1. Identifique a viagem (`listar_viagens` se faltar o `tripId`) e chame `listar_membros` para ver as pessoas e casar o nome com o `memberId`. Se o usuário não disse de quem é o perfil, pergunte.
2. Leia o que já existe com `get_perfil` e **não repergunte** o que está preenchido.
3. Levante, conversando:
   - **estilo de mala**: enxuto (leva o mínimo), equilibrado (padrão) ou conservador (leva com folga);
   - **tamanhos**: roupa e calçado;
   - **hábitos e atividades** que pesam na mala (fotografia, surf, ski, corrida, trabalho…); viram "kits";
   - **data de nascimento** (yyyy-mm-dd), que define se é menor de idade;
   - **necessidades especiais** (remédio de uso contínuo, bombinha, fralda, dieta…): dado **sensível**.
4. Se a pessoa for **menor de idade**, o perfil só pode ser gravado pelo **responsável**: confirme o `responsibleMemberId` (o memberId do responsável em `listar_membros`, em geral quem está conversando). O servidor recusa se quem grava não for o responsável nem o planner.
5. No fim, confirme o resumo e grave de uma vez com `salvar_perfil` (memberId + campos). As necessidades especiais vão no parâmetro `specialNeeds` (gravado no perfil privado). Para ajustar um campo depois, use `editar_perfil`.

## Regras

- Não invente dados: grave só o que o usuário disser.
- Trate `specialNeeds` como sensível: não repita em outros contextos nem em resumos desnecessários.
- Ao terminar, ofereça a skill `sugerir-bagagem`.

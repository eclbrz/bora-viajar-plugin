---
name: checklist-pre-viagem
description: Gera um checklist de véspera específico para uma viagem do Bora Viajar (reservas a confirmar, documentos, check-ins, câmbio e o que levar por clima). Use quando o usuário disser que vai viajar em breve, pedir "checklist", "o que falta antes de viajar" ou "preparar a viagem".
---

# Checklist pré-viagem

Monta um checklist de pré-viagem **específico para esta viagem**, não genérico.

## Passos

1. Identifique a viagem (`listar_viagens` se faltar o `tripId`).
2. Leia o resource `viagem://{tripId}` (ou `get_viagem`).
3. Cubra:
   - reservas ainda `aPesquisar` ou `reservado` que precisam virar `pago` / `confirmado`;
   - documentos: validade de passaporte e visto, se for viagem internacional;
   - check-in online de voos e hotéis;
   - câmbio e meios de pagamento;
   - o que levar na mala considerando datas e destino (estação e clima provável).
4. Ofereça atualizar status pelas tools `set_status_reserva` / `editar_reserva`, e sugira a skill `sugerir-bagagem` para montar a mala.

## Regras

- Baseie-se nos dados reais da viagem (datas, destino, reservas). Sem dado, pergunte.
- Só altere status depois de o usuário confirmar.

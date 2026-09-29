---
name: onboarding-bora-viajar
description: Onboarding do Bora Viajar. Verifica se o MCP bora-viajar está conectado (senão guia a autenticação pelo /mcp), lista as viagens do usuário e ajuda a escolher o primeiro fluxo (planejar viagem, importar roteiro, registrar voos, montar a mala). Use quando o usuário acabou de instalar o plugin, pedir "começar com o Bora Viajar", "conectar o Bora Viajar" ou não souber por onde começar.
---

# Onboarding do Bora Viajar

Guia o primeiro uso, de forma curta e prática.

## Passos

1. **Conexão.** Tente chamar `listar_viagens` do MCP `bora-viajar`.
   - Se as tools do `bora-viajar` não existem ou pedem autenticação: guie o usuário a rodar `/mcp`, escolher `bora-viajar`, autenticar (login com a conta Google) e, se preciso, recarregar com `/reload-plugins` ou reiniciar a sessão.
   - Se o servidor não aparece no `/mcp`: peça para conferir se o plugin está instalado e habilitado (`/plugin marketplace add eclbrz/bora-viajar-plugin`, depois `/plugin install bora-viajar@bora-viajar`). Como último recurso, adicionar manualmente: `claude mcp add --transport http bora-viajar https://viagens-mcp-286754895635.southamerica-east1.run.app/mcp` e depois autenticar pelo `/mcp`.
   - No claude.ai / app: Customize → Connectors → Add custom connector → colar a mesma URL → login Google.
2. **Viagens.** Com o MCP conectado, chame `listar_viagens` e resuma em poucas linhas (nome, destino, datas). Se não houver nenhuma, diga isso sem alarde.
3. **Primeiro fluxo.** Pergunte o que o usuário quer fazer e conduza com a skill certa:
   - planejar uma viagem nova: `planejar-viagem`;
   - importar/gravar um roteiro que ele já tem (texto, planilha, conversa): `planejar-viagem` (grava com `importar_roteiro`);
   - registrar voos de um print/PDF: `registrar-voos`;
   - montar a mala: `anamnese-viajante` e depois `sugerir-bagagem`;
   - com viagem existente: `revisar-roteiro`, `sugerir-reservas`, `otimizar-dia`, `checklist-pre-viagem`.
4. Faça o primeiro passo junto com o usuário usando o MCP, sem só descrever.

## Regras

- Nunca peça senha, token ou código de autorização no chat: a autenticação acontece no navegador, pelo `/mcp`.
- Se `criar_viagem`/`importar_roteiro` recusar por permissão, explique que criar viagem exige o papel de criador no app.

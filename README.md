# Bora Viajar — plugin Claude Code

Plugin do **Bora Viajar**, o app de viagens da família (roteiro, reservas, voos, perfil de viajante e mala). Ele registra o servidor MCP do Bora Viajar e traz skills que conduzem os fluxos principais em português.

O repositório não contém segredo nenhum: só a URL pública do MCP e as skills. O acesso aos seus dados exige entrar no Bora Viajar (Google ou e-mail e senha) e autorizar a conexão no primeiro uso (OAuth).

## Como conectar

### Claude Code (via plugin)

```
/plugin marketplace add eclbrz/bora-viajar-plugin
/plugin install bora-viajar@bora-viajar
```

O plugin registra o servidor MCP `bora-viajar` sozinho. No primeiro uso, rode `/mcp`, escolha `bora-viajar` e entre no Bora Viajar (Google ou e-mail e senha) e toque em **Permitir**.

Se o servidor não aparecer, adicione manualmente:

```
claude mcp add --transport http bora-viajar https://mcp.boraviajar.app/mcp
```

### claude.ai / app do Claude

Customize → Connectors → Add custom connector → cole a URL abaixo → entre no Bora Viajar e toque em **Permitir**.

```
https://mcp.boraviajar.app/mcp
```

(No claude.ai só o conector MCP é registrado; as skills abaixo são do Claude Code.)

## Skills

Depois de instaladas, ficam disponíveis como `/bora-viajar:<skill>` e disparam sozinhas pela descrição.

| Skill | O que faz |
|---|---|
| `onboarding-bora-viajar` | Confere a conexão do MCP, lista suas viagens e ajuda a escolher o primeiro fluxo |
| `planejar-viagem` | Monta um roteiro dia a dia e grava de uma vez (`importar_roteiro`) |
| `sugerir-reservas` | Aponta o que falta reservar no roteiro |
| `revisar-roteiro` | Revisão crítica do roteiro (ritmo, deslocamentos, pontas soltas) |
| `otimizar-dia` | Reordena as paradas de um dia para reduzir deslocamento |
| `checklist-pre-viagem` | Checklist de véspera específico da viagem |
| `anamnese-viajante` | Entrevista guiada para o perfil do viajante (`salvar_perfil`) |
| `sugerir-bagagem` | Monta a mala por clima, roteiro, duração e perfil (`gerar_bagagem`) |
| `registrar-voos` | Print/PDF de reserva aérea vira voos estruturados (`registrar_voos`) |

## Prompt de onboarding

Cole no Claude Code para ele instalar, conectar e conduzir o primeiro uso:

```
Conecte o Bora Viajar ao Claude Code e me faça o onboarding.

Primeiro, verifique se o plugin oficial Bora Viajar (https://github.com/eclbrz/bora-viajar-plugin) está instalado e habilitado. Se faltar, me guie pelos comandos:
/plugin marketplace add eclbrz/bora-viajar-plugin
/plugin install bora-viajar@bora-viajar
Abrir ou ler o repositório não conta como instalar. Se precisar recarregar o plugin ou reiniciar a sessão, me guie nisso antes de seguir.

O plugin registra o servidor MCP do Bora Viajar sozinho. Se não estiver conectado, me ajude a autenticar pelo /mcp (login no Bora Viajar). Se o servidor não aparecer, me guie a adicionar https://mcp.boraviajar.app/mcp manualmente e entrar com minha conta do Bora Viajar.

Por fim, confirme que as skills do Bora Viajar estão habilitadas, liste minhas viagens e me ajude a escolher a primeira coisa: planejar uma viagem nova, importar um roteiro, registrar voos de um print ou montar a mala — e use o MCP do Bora Viajar pra fazer junto comigo.
```

## Estrutura

```
.claude-plugin/marketplace.json   marketplace "bora-viajar" (1 plugin, source ./)
.claude-plugin/plugin.json        manifesto do plugin
.mcp.json                         servidor MCP remoto (HTTP + OAuth)
skills/<nome>/SKILL.md            9 skills
```

## Licença

MIT

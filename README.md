# claude-mural

Plugin do Claude Code com a skill **mural**: cada projeto ganha um quadro (artefato privado no claude.ai, estilo Miro) onde as sessões deixam perguntas (P), alinhamentos (A), pendências (T) e aprovações visuais (V). Você responde clicando, quando puder; o chat fica para conversa.

## Requisitos
- Claude Code com **Artifacts** e as capacidades `db` e `user` do artefato (sem elas o mural não guarda respostas).
- Acesso a este repositório (é privado): o git da máquina precisa estar logado no GitHub.

## Instalar
No Claude Code (depois, chame com `/mural:start`):
```
/plugin marketplace add SilRodrigo/claude-mural
/plugin install mural@claude-mural
```
Ou, sem os comandos, no `~/.claude/settings.json`:
```json
{
  "extraKnownMarketplaces": {
    "claude-mural": { "source": { "source": "github", "repo": "SilRodrigo/claude-mural" } }
  },
  "enabledPlugins": { "mural@claude-mural": true }
}
```

## Atualizar
```
/plugin marketplace update claude-mural
```
Atualizar o plugin não muda os murais já publicados. A skill compara a versão do mural com a do modelo e oferece atualizar cada um.

## Usar
- "cria um mural pra este projeto" → a sessão publica o mural e guarda o link na memória do projeto.
- As sessões abrem cards e avisam com uma linha no chat ("abri a P-03 no mural").
- Depois de responder, use **Copiar aviso** no card e cole no chat da sessão.

## Usar o mural de outra pessoa
1. O dono compartilha a página do mural com você, pelo menu Compartilhar, com acesso de edição.
2. O dono convida você neste repositório (é privado), e você instala o plugin.
3. No seu projeto, rode `/mural:start` e cole o link do mural. A sessão guarda o link na memória do projeto.

## Estrutura
```
.claude-plugin/marketplace.json
plugins/mural/.claude-plugin/plugin.json
plugins/mural/skills/start/SKILL.md          ← protocolo
plugins/mural/skills/start/modelo-mural.html ← página do mural
```
Ao mudar o modelo, suba `mural-versao` (no HTML) e `version` (no `plugin.json`) juntas.

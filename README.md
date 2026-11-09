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

### Extensão do VS Code
Lá o `/plugin` não existe. Use o `settings.json` acima, mas confira depois: o Claude Code clona o marketplace e registra a instalação, mas pode não criar a pasta do plugin, e aí a skill não carrega. Se `~/.claude/plugins/cache/claude-mural/mural/<versão>` não existir, copie à mão e dê **Reload Window**:
```bash
mkdir -p ~/.claude/plugins/cache/claude-mural/mural
cp -r ~/.claude/plugins/marketplaces/claude-mural/plugins/mural ~/.claude/plugins/cache/claude-mural/mural/<versão>
```
`<versão>` é a `version` de `plugins/mural/.claude-plugin/plugin.json`. A cada versão nova, refaça a cópia (depois de atualizar o marketplace).

## Atualizar
```
/plugin marketplace update claude-mural
```
Atualizar o plugin não muda os murais já publicados. A skill compara a versão do mural com a do modelo e oferece atualizar cada um.

## Usar
- "cria um mural pra este projeto" → a sessão publica o mural e guarda o link na memória do projeto.
- As sessões abrem cards e avisam com uma linha no chat ("abri a P-03 no mural").
- Depois de responder, use **Copiar aviso** no card e cole no chat da sessão.
- Para juntar tópicos já alinhados, **grampeie** os cards: solte um em cima do outro, ou selecione vários (bolinha no card ou Ctrl+clique) e clique em **Grampear**. A pilha pode ganhar um nome e ser arquivada inteira de uma vez.
- O botão **Tema** no topo troca entre automático (segue o claude.ai), claro e escuro.

## Estrutura
```
.claude-plugin/marketplace.json
plugins/mural/.claude-plugin/plugin.json
plugins/mural/skills/start/SKILL.md          ← protocolo
plugins/mural/skills/start/modelo-mural.html ← página do mural
```
Ao mudar o modelo, suba `mural-versao` (no HTML) e `version` (no `plugin.json`) juntas.

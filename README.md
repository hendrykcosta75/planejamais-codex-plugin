# Plugin ChatGPT/Codex — Planeja+

Plugin público (Agent Plugins) do conector MCP do **Planeja+** para ChatGPT e
Codex. Este repositório é apenas o pacote de distribuição; o produto Planeja+
não é aberto e vive em outro repositório.

## O que o plugin instala

- Servidor MCP remoto `planejamais` (`https://planejamais.planejareconsultoria.com.br/api/mcp`) em
  `mcp.json`, com OAuth 2.1 (Dynamic Client Registration + PKCE) conduzido pelo
  cliente.
- Skill `planejamais` com os fluxos de uso, o cuidado com `companyId` e as
  regras de confirmação para ações destrutivas.
- Metadados de listagem em `extensions.com.openai.interface` (nome, descrição,
  categoria, prompts e logo).

Nenhum token manual é necessário: na primeira chamada o cliente abre o navegador
para autorizar, e o token pode ser removido depois em
`https://planejamais.com.br/mcp`.

## Instalação para teste

Com o Codex CLI:

```bash
codex plugin marketplace add hendrykcosta75/planejamais-codex-plugin
```

Depois, no app do ChatGPT/Codex, abra o Plugins Directory, escolha o marketplace
`Planeja+` e instale o plugin. Em modo de desenvolvimento no ChatGPT
(Settings → Apps & Connectors → Developer mode), o mesmo conector pode ser
adicionado só com a URL acima para testar o OAuth.

## Publicação no diretório

A submissão é feita no portal de plugins da OpenAI
(`https://platform.openai.com/plugins`) na opção **With MCP**, usando a URL
universal do servidor. Requisitos e materiais (identidade verificada, prompts,
casos de teste, verificação de domínio em
`/.well-known/openai-apps-challenge`, annotations por tool) estão detalhados no
guia do produto.

## Manutenção

- A URL de produção é `https://planejamais.planejareconsultoria.com.br/api/mcp`.
  Se o app mudar de domínio, atualize `plugins/planejamais/mcp.json` e suba a versão.
- Ao publicar uma nova versão, incremente `version` em
  `plugins/planejamais/plugin.json`.
- `termsOfServiceURL` será adicionado ao manifesto quando a página pública de
  termos existir.

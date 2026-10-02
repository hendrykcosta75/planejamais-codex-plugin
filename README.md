# Plugin ChatGPT/Codex — Planeja+

Pacote Agent Plugins do conector MCP do **Planeja+** para ChatGPT e Codex.
A disponibilização no catálogo público ainda aguarda aprovação e publicação
pela OpenAI. Este repositório é apenas o pacote de distribuição; o produto
Planeja+ é mantido em outro repositório.

## Conectar sua própria conta

Após aprovação e publicação no catálogo da OpenAI:

1. Abra Plugins no ChatGPT ou Codex e procure **Planeja+**.
2. Instale o plugin e selecione **Conectar**.
3. Entre com sua própria conta do Planeja+ e autorize a conexão.
4. Escolha a empresa que deseja consultar ou atualizar.

É necessário ter uma conta no Planeja+. A integração acessa os dados das
empresas permitidas para essa conta e respeita suas permissões.

## O que o plugin instala

- Servidor MCP remoto `planejamais` (`https://planejamais.planejareconsultoria.com.br/api/mcp`) em
  `mcp.json`, com OAuth 2.1 (Dynamic Client Registration + PKCE) conduzido pelo
  cliente.
- Skill `planejamais` com os fluxos de uso, o cuidado com `companyId` e as
  regras de confirmação para ações destrutivas.
- Metadados de listagem em `extensions.com.openai.interface` (nome, descrição,
  categoria, prompts e logo).

O cliente conduz a autorização OAuth pelo navegador, sem token manual.
As autorizações podem ser revogadas na
[página MCP do Planeja+](https://planejamais.planejareconsultoria.com.br/mcp).

## Links oficiais

- [Integração Planeja+](https://planejamais.planejareconsultoria.com.br/integracoes/planejamais)
- [Suporte](https://planejamais.planejareconsultoria.com.br/integracoes/planejamais/suporte)
- [Privacidade](https://planejamais.planejareconsultoria.com.br/integracoes/planejamais/privacidade)
- [Termos de uso](https://planejamais.planejareconsultoria.com.br/integracoes/planejamais/termos)

O mesmo texto da política está disponível em [docs/privacidade.md](docs/privacidade.md).
O pacote 1.0.5 aponta para esse espelho público como URL de privacidade,
permitindo a consulta automatizada sem autenticação. A página oficial acima
continua disponível no site.

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
- Mantenha os links oficiais e os assets referenciados no manifesto atualizados.

---
name: planejamais
description: Consulta e atualiza o Planeja+ (planejamento estratégico, perspectivas, objetivos, iniciativas, etapas, quadros de tarefas, checklists, reuniões, eventos, relatórios e tickets) via MCP. Use quando o usuário pedir para ver o planejamento da empresa, acompanhar iniciativas ou tarefas, criar ou mover tarefas, agendar eventos ou reuniões, gerar relatórios ou abrir tickets.
---

# Planeja+

O servidor MCP `planejamais` expõe os dados e ações do Planeja+ respeitando o
papel do usuário em cada empresa (`proprietário`, `gerente`, `colaborador` ou
`observador`). Ações destrutivas pedem confirmação e podem ser recusadas pelo
backend mesmo que a ferramenta apareça na lista.

## Como usar

1. Comece por `list_my_companies` para descobrir o `id` e o papel do usuário em
   cada empresa. Sempre passe `companyId` nas chamadas seguintes — se você
   omitir, o servidor assume a empresa ativa mais antiga, que pode não ser a que
   o usuário mencionou.
2. Prefira as ferramentas de leitura para responder perguntas (`list_*`,
   `get_*`) e só use as de escrita quando o usuário pedir a mudança.
3. Antes de executar ferramentas marcadas como destrutivas (`delete_*`,
   `remove_*`, `end_meeting`, `set_company_user_status` etc.), confirme com o
   usuário o que será removido e o efeito esperado. Nunca encadeie várias ações
   destrutivas sem confirmação explícita.
4. Datas e valores seguem o formato aceito pela ferramenta; confirme o `id`
   correto antes de criar, mover ou atualizar itens (use as listagens para
   obtê-lo).

## Fluxos típicos

- Revisão semanal: `list_planejamentos` → `list_iniciativas` → `get_iniciativa`
  → `list_etapas` para resumir status, responsáveis e riscos.
- Organização do dia: `list_tasks` (por quadro ou responsável) →
  `move_task`/`update_task` → `add_checklist_item` para próximos passos.
- Reunião: `create_meeting` para agendar e `list_meetings` para acompanhar;
  use `create_event` para compromissos simples da agenda.
- Relatórios: `get_relatorio_geral` resume a empresa escolhida; passe `companyId`
  e, se necessário, `dateRange` com `startDate` e `endDate`. Para recorte de um
  planejamento, use `get_relatorio_por_perspectiva` com `planejamentoId`;
  `get_relatorio_por_usuario` aceita `targetUserId` para recortes por usuário.
- Suporte: `list_my_tickets` e `create_ticket` para registrar pedidos.

## Efeitos das ações

- `create_event` sempre inclui o usuário que cria o evento como participante.
  Uma lista `participantIds` vazia significa sem outros convidados.
- Comentários de iniciativas e tarefas, itens de checklist e alterações de
  descrições de tarefas/iniciativas podem enviar notificações e emails aos
  membros mencionados no texto. Confirme os destinatários e o texto antes de
  executar uma ação que enviará essas mensagens.
- Convites por email, remoção de membros, troca de papel, inativação e
  substituição dos membros de um planejamento afetam acesso ou enviam mensagens.
  Verifique o alvo e o efeito solicitados antes de executar.

## Autenticação

O cliente compatível conduz o OAuth na primeira chamada e abre o navegador para o
usuário autorizar. Se o servidor aparecer desconectado, oriente o usuário a reconectar o Planeja+
pelo gerenciamento de plugins/conexões do cliente e concluir a autorização OAuth. As autorizações podem ser revogadas
na página MCP do Planeja+. Se o cliente não conseguir renovar a sessão,
conclua a reconexão pelo gerenciamento de plugins/conexões.

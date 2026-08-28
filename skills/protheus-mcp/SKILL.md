---
name: protheus-mcp
description: Consulta o ERP TOTVS Protheus da empresa via MCP, em leitura: filiais e empresas, clientes e fornecedores, produtos e saldo em estoque, tabelas de preço, vendas e pedidos do varejo, totais de notas fiscais, ordens de produção e compras do MRP, centros de custo, comissões e limite de crédito. Use quando o usuário perguntar sobre dados do Protheus, do ERP da TOTVS, estoque, pedidos, faturamento, produção ou cadastro de clientes e fornecedores. Comece pelo diagnóstico quando não souber quais APIs aquela instalação responde, e use a tool curinga de rota REST para endpoints customizados.
---

# TOTVS Protheus — REST API skill

Você tem acesso à **TOTVS Protheus** REST API na MCP.AI.

> Converse com o **TOTVS Protheus** da sua empresa a partir do Claude, do ChatGPT ou de qualquer cliente MCP. Roda sobre a **API REST oficial da TOTVS**, contra a **sua própria instalação**: você informa a URL do serviço REST, o usuário e a senha do Protheus, e nada trafega por um intermediário do ERP. Diferente dos MCPs de Protheus que já existem, que são ferramentas de desenvolvimento (compilar AdvPL, buscar no TDN), este lê **dado de negócio**: filiais, clientes e fornecedores, produtos, estoque, tabelas de preço, vendas e pedidos, notas, ordens de produção e compras do MRP. Somente leitura. **Não afiliado à TOTVS.**

## Base URL

```
https://api.mcp.ai/api/protheus
```

Todo endpoint é um **POST** na Base URL + o path abaixo. Os parâmetros vão no corpo JSON.

## Autenticação

Inclua em toda request:

```
Authorization: Bearer sk_live_...
Content-Type: application/json
```

> Gere sua chave em **https://app.mcp.ai/settings/api-keys** (workspace API key `sk_live_…`, não expira, revogável). Uma única chave serve pra todos os seus MCPs.

## Formato de resposta

```json
{ "ok": true, "tool": "<tool_id>", "result": <payload> }
```

## Exemplo cURL

```bash
curl -X POST https://api.mcp.ai/api/protheus/api \
  -H "Authorization: Bearer sk_live_..." \
  -H "Content-Type: application/json" \
  -d '{"path":"..."}'
```

## Reportar problemas

Se um endpoint retornar erro, vazio ou dado inesperado, reporte (não desista calado): **POST /api/protheus/report** com `{ "message": "...", "context"?: "...", "conversation"?: [...] }`. Isso notifica o time da MCP.AI.

## Endpoints (26)

#### `protheus_api`

Faz um GET em qualquer rota REST da instalação Protheus conectada. _(POST /api/protheus/api)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `path` | string | Sim | Caminho completo da rota, começando com barra (ex.: /api/crm/v1/customerVendor). Não inclua o host: ele vem da conexão. |
| `page` | integer | Não | Página da coleção (parâmetro `page` da TOTVS). |
| `page_size` | integer | Não | Itens por página (parâmetro `pageSize` da TOTVS). Comece baixo: é o ERP de produção do cliente. |
| `order` | string | Não | Ordenação da coleção (parâmetro `order` da TOTVS). |
| `fields` | string | Não | Lista de campos a retornar, separados por vírgula (parâmetro `fields`). Use para reduzir o payload. |
| `filter` | string | Não | Filtro simples da coleção (parâmetro `filter` da TOTVS). |
| `expand` | string | Não | Campos expandidos (parâmetro `expand` da TOTVS). |
| `sql_filter` | string | Não | Filtro avançado com sintaxe básica de SQL (parâmetro `$filter`). Nem toda API do Protheus aceita. |
| `params` | object | Não | Parâmetros extras específicos da API, em query (ex.: { branchId: '01', product: 'PA001' }). Passados como vieram. |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |

#### `protheus_catalogo`

Consulta o catálogo das 125 APIs REST oficiais da linha Protheus (id, título, módulo e rotas de leitura), extraído da documentação pública da TOTVS. _(POST /api/protheus/catalogo)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `termo` | string | Não | Busca por nome, título, descrição ou módulo (ex.: 'estoque', 'pedido'). |
| `segmento` | string | Não | Filtra por segmento TOTVS (ex.: 'Manufatura', 'Varejo', 'Serviços', 'Backoffice'). |
| `limit` | integer | Não | Máximo de resultados (default 40, teto 125). |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |

#### `protheus_centros_custo`

Lista os centros de custo da contabilidade, ou consulta um pelo id interno. _(POST /api/protheus/centros/custo)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `id` | string | Não | Id interno do centro de custo. Sem ele, lista a coleção. |
| `page` | integer | Não | Página da coleção (parâmetro `page` da TOTVS). |
| `page_size` | integer | Não | Itens por página (parâmetro `pageSize` da TOTVS). Comece baixo: é o ERP de produção do cliente. |
| `order` | string | Não | Ordenação da coleção (parâmetro `order` da TOTVS). |
| `fields` | string | Não | Lista de campos a retornar, separados por vírgula (parâmetro `fields`). Use para reduzir o payload. |
| `filter` | string | Não | Filtro simples da coleção (parâmetro `filter` da TOTVS). |
| `expand` | string | Não | Campos expandidos (parâmetro `expand` da TOTVS). |
| `sql_filter` | string | Não | Filtro avançado com sintaxe básica de SQL (parâmetro `$filter`). Nem toda API do Protheus aceita. |
| `params` | object | Não | Parâmetros extras específicos da API, em query (ex.: { branchId: '01', product: 'PA001' }). Passados como vieram. |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |
| `ids` | string[] | Não | Bulk mode: multiple values for id |

#### `protheus_clientes_fornecedores`

Consulta o cadastro de clientes e fornecedores (API CustomerVendor). _(POST /api/protheus/clientes/fornecedores)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `tipo` | string | Não | Tipo da entidade na rota da TOTVS (entityType), que separa cliente de fornecedor nesta instalação. |
| `id` | string | Não | Código do cliente ou fornecedor. Exige `tipo`. |
| `page` | integer | Não | Página da coleção (parâmetro `page` da TOTVS). |
| `page_size` | integer | Não | Itens por página (parâmetro `pageSize` da TOTVS). Comece baixo: é o ERP de produção do cliente. |
| `order` | string | Não | Ordenação da coleção (parâmetro `order` da TOTVS). |
| `fields` | string | Não | Lista de campos a retornar, separados por vírgula (parâmetro `fields`). Use para reduzir o payload. |
| `filter` | string | Não | Filtro simples da coleção (parâmetro `filter` da TOTVS). |
| `expand` | string | Não | Campos expandidos (parâmetro `expand` da TOTVS). |
| `sql_filter` | string | Não | Filtro avançado com sintaxe básica de SQL (parâmetro `$filter`). Nem toda API do Protheus aceita. |
| `params` | object | Não | Parâmetros extras específicos da API, em query (ex.: { branchId: '01', product: 'PA001' }). Passados como vieram. |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |
| `ids` | string[] | Não | Bulk mode: multiple values for id |

#### `protheus_comissoes`

Consulta as comissões de venda, ou uma comissão pelo id interno. _(POST /api/protheus/comissoes)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `id` | string | Não | Id interno da comissão. Sem ele, lista a coleção. |
| `page` | integer | Não | Página da coleção (parâmetro `page` da TOTVS). |
| `page_size` | integer | Não | Itens por página (parâmetro `pageSize` da TOTVS). Comece baixo: é o ERP de produção do cliente. |
| `order` | string | Não | Ordenação da coleção (parâmetro `order` da TOTVS). |
| `fields` | string | Não | Lista de campos a retornar, separados por vírgula (parâmetro `fields`). Use para reduzir o payload. |
| `filter` | string | Não | Filtro simples da coleção (parâmetro `filter` da TOTVS). |
| `expand` | string | Não | Campos expandidos (parâmetro `expand` da TOTVS). |
| `sql_filter` | string | Não | Filtro avançado com sintaxe básica de SQL (parâmetro `$filter`). Nem toda API do Protheus aceita. |
| `params` | object | Não | Parâmetros extras específicos da API, em query (ex.: { branchId: '01', product: 'PA001' }). Passados como vieram. |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |
| `ids` | string[] | Não | Bulk mode: multiple values for id |

#### `protheus_compras_mrp`

Consulta os pedidos de compra ou as solicitações de compra do MRP. _(POST /api/protheus/compras/mrp)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `tipo` | string | Não | Pedido de compra (default) ou solicitação de compra. (pedido, solicitacao) |
| `branch_id` | string | Não | Código da filial. Junto com `codigo`, consulta um registro específico. |
| `codigo` | string | Não | Código do pedido ou da solicitação. Exige `branch_id`. |
| `page` | integer | Não | Página da coleção (parâmetro `page` da TOTVS). |
| `page_size` | integer | Não | Itens por página (parâmetro `pageSize` da TOTVS). Comece baixo: é o ERP de produção do cliente. |
| `order` | string | Não | Ordenação da coleção (parâmetro `order` da TOTVS). |
| `fields` | string | Não | Lista de campos a retornar, separados por vírgula (parâmetro `fields`). Use para reduzir o payload. |
| `filter` | string | Não | Filtro simples da coleção (parâmetro `filter` da TOTVS). |
| `expand` | string | Não | Campos expandidos (parâmetro `expand` da TOTVS). |
| `sql_filter` | string | Não | Filtro avançado com sintaxe básica de SQL (parâmetro `$filter`). Nem toda API do Protheus aceita. |
| `params` | object | Não | Parâmetros extras específicos da API, em query (ex.: { branchId: '01', product: 'PA001' }). Passados como vieram. |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |
| `branch_ids` | string[] | Não | Bulk mode: multiple values for branch_id |

#### `protheus_condicoes_pagamento`

Lista as condições de pagamento cadastradas, ou consulta uma pelo id interno. _(POST /api/protheus/condicoes/pagamento)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `id` | string | Não | Id interno da condição. Sem ele, lista a coleção. |
| `page` | integer | Não | Página da coleção (parâmetro `page` da TOTVS). |
| `page_size` | integer | Não | Itens por página (parâmetro `pageSize` da TOTVS). Comece baixo: é o ERP de produção do cliente. |
| `order` | string | Não | Ordenação da coleção (parâmetro `order` da TOTVS). |
| `fields` | string | Não | Lista de campos a retornar, separados por vírgula (parâmetro `fields`). Use para reduzir o payload. |
| `filter` | string | Não | Filtro simples da coleção (parâmetro `filter` da TOTVS). |
| `expand` | string | Não | Campos expandidos (parâmetro `expand` da TOTVS). |
| `sql_filter` | string | Não | Filtro avançado com sintaxe básica de SQL (parâmetro `$filter`). Nem toda API do Protheus aceita. |
| `params` | object | Não | Parâmetros extras específicos da API, em query (ex.: { branchId: '01', product: 'PA001' }). Passados como vieram. |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |
| `ids` | string[] | Não | Bulk mode: multiple values for id |

#### `protheus_contatos`

Lista os contatos do CRM, ou consulta um contato por id. _(POST /api/protheus/contatos)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `id` | string | Não | Id do contato. Sem ele, lista a coleção. |
| `page` | integer | Não | Página da coleção (parâmetro `page` da TOTVS). |
| `page_size` | integer | Não | Itens por página (parâmetro `pageSize` da TOTVS). Comece baixo: é o ERP de produção do cliente. |
| `order` | string | Não | Ordenação da coleção (parâmetro `order` da TOTVS). |
| `fields` | string | Não | Lista de campos a retornar, separados por vírgula (parâmetro `fields`). Use para reduzir o payload. |
| `filter` | string | Não | Filtro simples da coleção (parâmetro `filter` da TOTVS). |
| `expand` | string | Não | Campos expandidos (parâmetro `expand` da TOTVS). |
| `sql_filter` | string | Não | Filtro avançado com sintaxe básica de SQL (parâmetro `$filter`). Nem toda API do Protheus aceita. |
| `params` | object | Não | Parâmetros extras específicos da API, em query (ex.: { branchId: '01', product: 'PA001' }). Passados como vieram. |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |
| `ids` | string[] | Não | Bulk mode: multiple values for id |

#### `protheus_diagnostico`

Descobre quais APIs REST esta instalação Protheus realmente responde. _(POST /api/protheus/diagnostico)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `termo` | string | Não | Sonda só as APIs cujo nome, título ou módulo casem com o termo (ex.: 'retail', 'mrp', 'crm'). |
| `limit` | integer | Não | Máximo de APIs a sondar (default 25, teto 60). Cada sondagem é uma chamada ao ERP do cliente. |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |

#### `protheus_estoque`

Consulta o saldo em estoque. Escolha a fonte: varejo (saldo em estoque do varejo) ou mrp (estoque do MRP, com armazém, lote e saldos bloqueado, consignado e em controle de qualidade). São módulos dist _(POST /api/protheus/estoque)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `fonte` | string | Não | De onde ler o saldo: varejo (default) ou mrp. (varejo, mrp) |
| `page` | integer | Não | Página da coleção (parâmetro `page` da TOTVS). |
| `page_size` | integer | Não | Itens por página (parâmetro `pageSize` da TOTVS). Comece baixo: é o ERP de produção do cliente. |
| `order` | string | Não | Ordenação da coleção (parâmetro `order` da TOTVS). |
| `fields` | string | Não | Lista de campos a retornar, separados por vírgula (parâmetro `fields`). Use para reduzir o payload. |
| `filter` | string | Não | Filtro simples da coleção (parâmetro `filter` da TOTVS). |
| `expand` | string | Não | Campos expandidos (parâmetro `expand` da TOTVS). |
| `sql_filter` | string | Não | Filtro avançado com sintaxe básica de SQL (parâmetro `$filter`). Nem toda API do Protheus aceita. |
| `params` | object | Não | Parâmetros extras específicos da API, em query (ex.: { branchId: '01', product: 'PA001' }). Passados como vieram. |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |

#### `protheus_filiais`

Lista as empresas e filiais do grupo (API TSIBranches). _(POST /api/protheus/filiais)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `page` | integer | Não | Página da coleção (parâmetro `page` da TOTVS). |
| `page_size` | integer | Não | Itens por página (parâmetro `pageSize` da TOTVS). Comece baixo: é o ERP de produção do cliente. |
| `order` | string | Não | Ordenação da coleção (parâmetro `order` da TOTVS). |
| `fields` | string | Não | Lista de campos a retornar, separados por vírgula (parâmetro `fields`). Use para reduzir o payload. |
| `filter` | string | Não | Filtro simples da coleção (parâmetro `filter` da TOTVS). |
| `expand` | string | Não | Campos expandidos (parâmetro `expand` da TOTVS). |
| `sql_filter` | string | Não | Filtro avançado com sintaxe básica de SQL (parâmetro `$filter`). Nem toda API do Protheus aceita. |
| `params` | object | Não | Parâmetros extras específicos da API, em query (ex.: { branchId: '01', product: 'PA001' }). Passados como vieram. |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |

#### `protheus_limite_credito`

Consulta o limite de crédito dos clientes. _(POST /api/protheus/limite/credito)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `cliente_id` | string | Não | Id interno do cliente. Sem ele, lista a coleção. |
| `page` | integer | Não | Página da coleção (parâmetro `page` da TOTVS). |
| `page_size` | integer | Não | Itens por página (parâmetro `pageSize` da TOTVS). Comece baixo: é o ERP de produção do cliente. |
| `order` | string | Não | Ordenação da coleção (parâmetro `order` da TOTVS). |
| `fields` | string | Não | Lista de campos a retornar, separados por vírgula (parâmetro `fields`). Use para reduzir o payload. |
| `filter` | string | Não | Filtro simples da coleção (parâmetro `filter` da TOTVS). |
| `expand` | string | Não | Campos expandidos (parâmetro `expand` da TOTVS). |
| `sql_filter` | string | Não | Filtro avançado com sintaxe básica de SQL (parâmetro `$filter`). Nem toda API do Protheus aceita. |
| `params` | object | Não | Parâmetros extras específicos da API, em query (ex.: { branchId: '01', product: 'PA001' }). Passados como vieram. |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |
| `cliente_ids` | string[] | Não | Bulk mode: multiple values for cliente_id |

#### `protheus_list_accounts`

Lista as instalações Protheus conectadas a este install, com id e label (host/usuário). _(POST /api/protheus/list/accounts)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |

#### `protheus_modulos`

Lista os módulos do sistema Protheus nesta instalação. _(POST /api/protheus/modulos)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `page` | integer | Não | Página da coleção (parâmetro `page` da TOTVS). |
| `page_size` | integer | Não | Itens por página (parâmetro `pageSize` da TOTVS). Comece baixo: é o ERP de produção do cliente. |
| `order` | string | Não | Ordenação da coleção (parâmetro `order` da TOTVS). |
| `fields` | string | Não | Lista de campos a retornar, separados por vírgula (parâmetro `fields`). Use para reduzir o payload. |
| `filter` | string | Não | Filtro simples da coleção (parâmetro `filter` da TOTVS). |
| `expand` | string | Não | Campos expandidos (parâmetro `expand` da TOTVS). |
| `sql_filter` | string | Não | Filtro avançado com sintaxe básica de SQL (parâmetro `$filter`). Nem toda API do Protheus aceita. |
| `params` | object | Não | Parâmetros extras específicos da API, em query (ex.: { branchId: '01', product: 'PA001' }). Passados como vieram. |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |

#### `protheus_notas_totais`

Consulta os totais de notas fiscais de saída ou de entrada do varejo, incluindo a visão de notas canceladas. _(POST /api/protheus/notas/totais)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `tipo` | string | Não | Notas de saída (default) ou de entrada. (saida, entrada) |
| `canceladas` | boolean | Não | Com true, retorna a visão de notas canceladas. |
| `page` | integer | Não | Página da coleção (parâmetro `page` da TOTVS). |
| `page_size` | integer | Não | Itens por página (parâmetro `pageSize` da TOTVS). Comece baixo: é o ERP de produção do cliente. |
| `order` | string | Não | Ordenação da coleção (parâmetro `order` da TOTVS). |
| `fields` | string | Não | Lista de campos a retornar, separados por vírgula (parâmetro `fields`). Use para reduzir o payload. |
| `filter` | string | Não | Filtro simples da coleção (parâmetro `filter` da TOTVS). |
| `expand` | string | Não | Campos expandidos (parâmetro `expand` da TOTVS). |
| `sql_filter` | string | Não | Filtro avançado com sintaxe básica de SQL (parâmetro `$filter`). Nem toda API do Protheus aceita. |
| `params` | object | Não | Parâmetros extras específicos da API, em query (ex.: { branchId: '01', product: 'PA001' }). Passados como vieram. |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |

#### `protheus_oportunidades`

Lista as oportunidades comerciais do CRM, ou consulta uma oportunidade pelo id interno. _(POST /api/protheus/oportunidades)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `id` | string | Não | Id interno da oportunidade. Sem ele, lista a coleção. |
| `page` | integer | Não | Página da coleção (parâmetro `page` da TOTVS). |
| `page_size` | integer | Não | Itens por página (parâmetro `pageSize` da TOTVS). Comece baixo: é o ERP de produção do cliente. |
| `order` | string | Não | Ordenação da coleção (parâmetro `order` da TOTVS). |
| `fields` | string | Não | Lista de campos a retornar, separados por vírgula (parâmetro `fields`). Use para reduzir o payload. |
| `filter` | string | Não | Filtro simples da coleção (parâmetro `filter` da TOTVS). |
| `expand` | string | Não | Campos expandidos (parâmetro `expand` da TOTVS). |
| `sql_filter` | string | Não | Filtro avançado com sintaxe básica de SQL (parâmetro `$filter`). Nem toda API do Protheus aceita. |
| `params` | object | Não | Parâmetros extras específicos da API, em query (ex.: { branchId: '01', product: 'PA001' }). Passados como vieram. |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |
| `ids` | string[] | Não | Bulk mode: multiple values for id |

#### `protheus_ordens_producao`

Consulta as ordens de produção do MRP. _(POST /api/protheus/ordens/producao)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `branch_id` | string | Não | Código da filial. Junto com `codigo`, consulta uma ordem específica. |
| `codigo` | string | Não | Código da ordem de produção. Exige `branch_id`. |
| `page` | integer | Não | Página da coleção (parâmetro `page` da TOTVS). |
| `page_size` | integer | Não | Itens por página (parâmetro `pageSize` da TOTVS). Comece baixo: é o ERP de produção do cliente. |
| `order` | string | Não | Ordenação da coleção (parâmetro `order` da TOTVS). |
| `fields` | string | Não | Lista de campos a retornar, separados por vírgula (parâmetro `fields`). Use para reduzir o payload. |
| `filter` | string | Não | Filtro simples da coleção (parâmetro `filter` da TOTVS). |
| `expand` | string | Não | Campos expandidos (parâmetro `expand` da TOTVS). |
| `sql_filter` | string | Não | Filtro avançado com sintaxe básica de SQL (parâmetro `$filter`). Nem toda API do Protheus aceita. |
| `params` | object | Não | Parâmetros extras específicos da API, em query (ex.: { branchId: '01', product: 'PA001' }). Passados como vieram. |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |
| `branch_ids` | string[] | Não | Bulk mode: multiple values for branch_id |

#### `protheus_parametros`

Consulta os parâmetros de sistema do Protheus. _(POST /api/protheus/parametros)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `page` | integer | Não | Página da coleção (parâmetro `page` da TOTVS). |
| `page_size` | integer | Não | Itens por página (parâmetro `pageSize` da TOTVS). Comece baixo: é o ERP de produção do cliente. |
| `order` | string | Não | Ordenação da coleção (parâmetro `order` da TOTVS). |
| `fields` | string | Não | Lista de campos a retornar, separados por vírgula (parâmetro `fields`). Use para reduzir o payload. |
| `filter` | string | Não | Filtro simples da coleção (parâmetro `filter` da TOTVS). |
| `expand` | string | Não | Campos expandidos (parâmetro `expand` da TOTVS). |
| `sql_filter` | string | Não | Filtro avançado com sintaxe básica de SQL (parâmetro `$filter`). Nem toda API do Protheus aceita. |
| `params` | object | Não | Parâmetros extras específicos da API, em query (ex.: { branchId: '01', product: 'PA001' }). Passados como vieram. |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |

#### `protheus_pedidos_varejo`

Lista os pedidos de venda do varejo. _(POST /api/protheus/pedidos/varejo)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `id` | string | Não | Id interno do pedido. Com ele, retorna os itens do pedido. |
| `page` | integer | Não | Página da coleção (parâmetro `page` da TOTVS). |
| `page_size` | integer | Não | Itens por página (parâmetro `pageSize` da TOTVS). Comece baixo: é o ERP de produção do cliente. |
| `order` | string | Não | Ordenação da coleção (parâmetro `order` da TOTVS). |
| `fields` | string | Não | Lista de campos a retornar, separados por vírgula (parâmetro `fields`). Use para reduzir o payload. |
| `filter` | string | Não | Filtro simples da coleção (parâmetro `filter` da TOTVS). |
| `expand` | string | Não | Campos expandidos (parâmetro `expand` da TOTVS). |
| `sql_filter` | string | Não | Filtro avançado com sintaxe básica de SQL (parâmetro `$filter`). Nem toda API do Protheus aceita. |
| `params` | object | Não | Parâmetros extras específicos da API, em query (ex.: { branchId: '01', product: 'PA001' }). Passados como vieram. |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |
| `ids` | string[] | Não | Bulk mode: multiple values for id |

#### `protheus_produtos`

Consulta o cadastro de produtos. _(POST /api/protheus/produtos)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `fonte` | string | Não | De onde ler o produto: varejo (default) ou mrp. (varejo, mrp) |
| `page` | integer | Não | Página da coleção (parâmetro `page` da TOTVS). |
| `page_size` | integer | Não | Itens por página (parâmetro `pageSize` da TOTVS). Comece baixo: é o ERP de produção do cliente. |
| `order` | string | Não | Ordenação da coleção (parâmetro `order` da TOTVS). |
| `fields` | string | Não | Lista de campos a retornar, separados por vírgula (parâmetro `fields`). Use para reduzir o payload. |
| `filter` | string | Não | Filtro simples da coleção (parâmetro `filter` da TOTVS). |
| `expand` | string | Não | Campos expandidos (parâmetro `expand` da TOTVS). |
| `sql_filter` | string | Não | Filtro avançado com sintaxe básica de SQL (parâmetro `$filter`). Nem toda API do Protheus aceita. |
| `params` | object | Não | Parâmetros extras específicos da API, em query (ex.: { branchId: '01', product: 'PA001' }). Passados como vieram. |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |

#### `protheus_propostas_comerciais`

Lista as propostas comerciais de uma oportunidade, ou consulta uma proposta específica. _(POST /api/protheus/propostas/comerciais)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `oportunidade_id` | string | Sim | Id interno da oportunidade dona das propostas. Veja protheus_oportunidades. |
| `id` | string | Não | Id interno da proposta. Sem ele, lista as propostas da oportunidade. |
| `page` | integer | Não | Página da coleção (parâmetro `page` da TOTVS). |
| `page_size` | integer | Não | Itens por página (parâmetro `pageSize` da TOTVS). Comece baixo: é o ERP de produção do cliente. |
| `order` | string | Não | Ordenação da coleção (parâmetro `order` da TOTVS). |
| `fields` | string | Não | Lista de campos a retornar, separados por vírgula (parâmetro `fields`). Use para reduzir o payload. |
| `filter` | string | Não | Filtro simples da coleção (parâmetro `filter` da TOTVS). |
| `expand` | string | Não | Campos expandidos (parâmetro `expand` da TOTVS). |
| `sql_filter` | string | Não | Filtro avançado com sintaxe básica de SQL (parâmetro `$filter`). Nem toda API do Protheus aceita. |
| `params` | object | Não | Parâmetros extras específicos da API, em query (ex.: { branchId: '01', product: 'PA001' }). Passados como vieram. |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |
| `oportunidade_ids` | string[] | Não | Bulk mode: multiple values for oportunidade_id |
| `ids` | string[] | Não | Bulk mode: multiple values for id |

#### `protheus_tabela_precos`

Consulta as tabelas de preço. Sem argumentos lista os cabeçalhos; com `codigo` traz uma tabela; com `codigo` e `itens` traz os itens e preços dela. _(POST /api/protheus/tabela/precos)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `codigo` | string | Não | Código da tabela de preços. |
| `itens` | boolean | Não | Com true e `codigo`, retorna os itens da tabela em vez do cabeçalho. |
| `page` | integer | Não | Página da coleção (parâmetro `page` da TOTVS). |
| `page_size` | integer | Não | Itens por página (parâmetro `pageSize` da TOTVS). Comece baixo: é o ERP de produção do cliente. |
| `order` | string | Não | Ordenação da coleção (parâmetro `order` da TOTVS). |
| `fields` | string | Não | Lista de campos a retornar, separados por vírgula (parâmetro `fields`). Use para reduzir o payload. |
| `filter` | string | Não | Filtro simples da coleção (parâmetro `filter` da TOTVS). |
| `expand` | string | Não | Campos expandidos (parâmetro `expand` da TOTVS). |
| `sql_filter` | string | Não | Filtro avançado com sintaxe básica de SQL (parâmetro `$filter`). Nem toda API do Protheus aceita. |
| `params` | object | Não | Parâmetros extras específicos da API, em query (ex.: { branchId: '01', product: 'PA001' }). Passados como vieram. |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |

#### `protheus_transportadoras`

Lista as transportadoras cadastradas, ou consulta uma pelo id interno. _(POST /api/protheus/transportadoras)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `id` | string | Não | Id interno da transportadora. Sem ele, lista a coleção. |
| `page` | integer | Não | Página da coleção (parâmetro `page` da TOTVS). |
| `page_size` | integer | Não | Itens por página (parâmetro `pageSize` da TOTVS). Comece baixo: é o ERP de produção do cliente. |
| `order` | string | Não | Ordenação da coleção (parâmetro `order` da TOTVS). |
| `fields` | string | Não | Lista de campos a retornar, separados por vírgula (parâmetro `fields`). Use para reduzir o payload. |
| `filter` | string | Não | Filtro simples da coleção (parâmetro `filter` da TOTVS). |
| `expand` | string | Não | Campos expandidos (parâmetro `expand` da TOTVS). |
| `sql_filter` | string | Não | Filtro avançado com sintaxe básica de SQL (parâmetro `$filter`). Nem toda API do Protheus aceita. |
| `params` | object | Não | Parâmetros extras específicos da API, em query (ex.: { branchId: '01', product: 'PA001' }). Passados como vieram. |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |
| `ids` | string[] | Não | Bulk mode: multiple values for id |

#### `protheus_usuarios`

Lista os usuários do Protheus, ou consulta um usuário por id. _(POST /api/protheus/usuarios)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `id` | string | Não | Id do usuário. Sem ele, lista a coleção. |
| `page` | integer | Não | Página da coleção (parâmetro `page` da TOTVS). |
| `page_size` | integer | Não | Itens por página (parâmetro `pageSize` da TOTVS). Comece baixo: é o ERP de produção do cliente. |
| `order` | string | Não | Ordenação da coleção (parâmetro `order` da TOTVS). |
| `fields` | string | Não | Lista de campos a retornar, separados por vírgula (parâmetro `fields`). Use para reduzir o payload. |
| `filter` | string | Não | Filtro simples da coleção (parâmetro `filter` da TOTVS). |
| `expand` | string | Não | Campos expandidos (parâmetro `expand` da TOTVS). |
| `sql_filter` | string | Não | Filtro avançado com sintaxe básica de SQL (parâmetro `$filter`). Nem toda API do Protheus aceita. |
| `params` | object | Não | Parâmetros extras específicos da API, em query (ex.: { branchId: '01', product: 'PA001' }). Passados como vieram. |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |
| `ids` | string[] | Não | Bulk mode: multiple values for id |

#### `protheus_vendas_varejo`

Consulta as vendas do varejo, ou uma venda pelo id interno. _(POST /api/protheus/vendas/varejo)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `id` | string | Não | Id interno da venda. Sem ele, lista a coleção. |
| `page` | integer | Não | Página da coleção (parâmetro `page` da TOTVS). |
| `page_size` | integer | Não | Itens por página (parâmetro `pageSize` da TOTVS). Comece baixo: é o ERP de produção do cliente. |
| `order` | string | Não | Ordenação da coleção (parâmetro `order` da TOTVS). |
| `fields` | string | Não | Lista de campos a retornar, separados por vírgula (parâmetro `fields`). Use para reduzir o payload. |
| `filter` | string | Não | Filtro simples da coleção (parâmetro `filter` da TOTVS). |
| `expand` | string | Não | Campos expandidos (parâmetro `expand` da TOTVS). |
| `sql_filter` | string | Não | Filtro avançado com sintaxe básica de SQL (parâmetro `$filter`). Nem toda API do Protheus aceita. |
| `params` | object | Não | Parâmetros extras específicos da API, em query (ex.: { branchId: '01', product: 'PA001' }). Passados como vieram. |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |
| `ids` | string[] | Não | Bulk mode: multiple values for id |

#### `protheus_vendedores`

Lista os vendedores cadastrados, ou consulta um vendedor pelo código. _(POST /api/protheus/vendedores)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `id` | string | Não | Código do vendedor. Sem ele, lista a coleção. |
| `page` | integer | Não | Página da coleção (parâmetro `page` da TOTVS). |
| `page_size` | integer | Não | Itens por página (parâmetro `pageSize` da TOTVS). Comece baixo: é o ERP de produção do cliente. |
| `order` | string | Não | Ordenação da coleção (parâmetro `order` da TOTVS). |
| `fields` | string | Não | Lista de campos a retornar, separados por vírgula (parâmetro `fields`). Use para reduzir o payload. |
| `filter` | string | Não | Filtro simples da coleção (parâmetro `filter` da TOTVS). |
| `expand` | string | Não | Campos expandidos (parâmetro `expand` da TOTVS). |
| `sql_filter` | string | Não | Filtro avançado com sintaxe básica de SQL (parâmetro `$filter`). Nem toda API do Protheus aceita. |
| `params` | object | Não | Parâmetros extras específicos da API, em query (ex.: { branchId: '01', product: 'PA001' }). Passados como vieram. |
| `account` | string | Não | Quando há múltiplas instalações Protheus conectadas: id/label da conexão. Veja protheus_list_accounts. |
| `ids` | string[] | Não | Bulk mode: multiple values for id |

---

Este MCP também funciona via **conexão MCP** (Claude / Cursor) em `https://api.mcp.ai/p_protheus` — veja o [README](../../README.md). A skill acima é pra consumir a **REST API** direto (agente próprio / código).

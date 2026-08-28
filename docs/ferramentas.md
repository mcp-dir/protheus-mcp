# Ferramentas

TOTVS Protheus expõe 26 ferramentas (todas somente leitura).

### 1. `protheus_list_accounts`
**Input**: `account` (opcional)

Lista as instalações Protheus conectadas a este install, com id e label (host/usuário).

### 2. `protheus_diagnostico`
**Input**: `termo` (opcional), `limit` (opcional), `account` (opcional)

Descobre quais APIs REST esta instalação Protheus realmente responde.

### 3. `protheus_catalogo`
**Input**: `termo` (opcional), `segmento` (opcional), `limit` (opcional), `account` (opcional)

Consulta o catálogo das 125 APIs REST oficiais da linha Protheus (id, título, módulo e rotas de leitura), extraído da documentação pública da TOTVS.

### 4. `protheus_api`
**Input**: `path`, `page` (opcional), `page_size` (opcional), `order` (opcional), `fields` (opcional), `filter` (opcional), `expand` (opcional), `sql_filter` (opcional), `params` (opcional), `account` (opcional)

Faz um GET em qualquer rota REST da instalação Protheus conectada.

### 5. `protheus_filiais`
**Input**: `page` (opcional), `page_size` (opcional), `order` (opcional), `fields` (opcional), `filter` (opcional), `expand` (opcional), `sql_filter` (opcional), `params` (opcional), `account` (opcional)

Lista as empresas e filiais do grupo (API TSIBranches).

### 6. `protheus_modulos`
**Input**: `page` (opcional), `page_size` (opcional), `order` (opcional), `fields` (opcional), `filter` (opcional), `expand` (opcional), `sql_filter` (opcional), `params` (opcional), `account` (opcional)

Lista os módulos do sistema Protheus nesta instalação.

### 7. `protheus_parametros`
**Input**: `page` (opcional), `page_size` (opcional), `order` (opcional), `fields` (opcional), `filter` (opcional), `expand` (opcional), `sql_filter` (opcional), `params` (opcional), `account` (opcional)

Consulta os parâmetros de sistema do Protheus.

### 8. `protheus_usuarios`
**Input**: `id` (opcional), `page` (opcional), `page_size` (opcional), `order` (opcional), `fields` (opcional), `filter` (opcional), `expand` (opcional), `sql_filter` (opcional), `params` (opcional), `account` (opcional), `ids` (opcional)

Lista os usuários do Protheus, ou consulta um usuário por id.

### 9. `protheus_clientes_fornecedores`
**Input**: `tipo` (opcional), `id` (opcional), `page` (opcional), `page_size` (opcional), `order` (opcional), `fields` (opcional), `filter` (opcional), `expand` (opcional), `sql_filter` (opcional), `params` (opcional), `account` (opcional), `ids` (opcional)

Consulta o cadastro de clientes e fornecedores (API CustomerVendor).

### 10. `protheus_contatos`
**Input**: `id` (opcional), `page` (opcional), `page_size` (opcional), `order` (opcional), `fields` (opcional), `filter` (opcional), `expand` (opcional), `sql_filter` (opcional), `params` (opcional), `account` (opcional), `ids` (opcional)

Lista os contatos do CRM, ou consulta um contato por id.

### 11. `protheus_vendedores`
**Input**: `id` (opcional), `page` (opcional), `page_size` (opcional), `order` (opcional), `fields` (opcional), `filter` (opcional), `expand` (opcional), `sql_filter` (opcional), `params` (opcional), `account` (opcional), `ids` (opcional)

Lista os vendedores cadastrados, ou consulta um vendedor pelo código.

### 12. `protheus_oportunidades`
**Input**: `id` (opcional), `page` (opcional), `page_size` (opcional), `order` (opcional), `fields` (opcional), `filter` (opcional), `expand` (opcional), `sql_filter` (opcional), `params` (opcional), `account` (opcional), `ids` (opcional)

Lista as oportunidades comerciais do CRM, ou consulta uma oportunidade pelo id interno.

### 13. `protheus_propostas_comerciais`
**Input**: `oportunidade_id`, `id` (opcional), `page` (opcional), `page_size` (opcional), `order` (opcional), `fields` (opcional), `filter` (opcional), `expand` (opcional), `sql_filter` (opcional), `params` (opcional), `account` (opcional), `oportunidade_ids` (opcional), `ids` (opcional)

Lista as propostas comerciais de uma oportunidade, ou consulta uma proposta específica.

### 14. `protheus_tabela_precos`
**Input**: `codigo` (opcional), `itens` (opcional), `page` (opcional), `page_size` (opcional), `order` (opcional), `fields` (opcional), `filter` (opcional), `expand` (opcional), `sql_filter` (opcional), `params` (opcional), `account` (opcional)

Consulta as tabelas de preço. Sem argumentos lista os cabeçalhos; com `codigo` traz uma tabela; com `codigo` e `itens` traz os itens e preços dela.

### 15. `protheus_condicoes_pagamento`
**Input**: `id` (opcional), `page` (opcional), `page_size` (opcional), `order` (opcional), `fields` (opcional), `filter` (opcional), `expand` (opcional), `sql_filter` (opcional), `params` (opcional), `account` (opcional), `ids` (opcional)

Lista as condições de pagamento cadastradas, ou consulta uma pelo id interno.

### 16. `protheus_limite_credito`
**Input**: `cliente_id` (opcional), `page` (opcional), `page_size` (opcional), `order` (opcional), `fields` (opcional), `filter` (opcional), `expand` (opcional), `sql_filter` (opcional), `params` (opcional), `account` (opcional), `cliente_ids` (opcional)

Consulta o limite de crédito dos clientes.

### 17. `protheus_comissoes`
**Input**: `id` (opcional), `page` (opcional), `page_size` (opcional), `order` (opcional), `fields` (opcional), `filter` (opcional), `expand` (opcional), `sql_filter` (opcional), `params` (opcional), `account` (opcional), `ids` (opcional)

Consulta as comissões de venda, ou uma comissão pelo id interno.

### 18. `protheus_transportadoras`
**Input**: `id` (opcional), `page` (opcional), `page_size` (opcional), `order` (opcional), `fields` (opcional), `filter` (opcional), `expand` (opcional), `sql_filter` (opcional), `params` (opcional), `account` (opcional), `ids` (opcional)

Lista as transportadoras cadastradas, ou consulta uma pelo id interno.

### 19. `protheus_centros_custo`
**Input**: `id` (opcional), `page` (opcional), `page_size` (opcional), `order` (opcional), `fields` (opcional), `filter` (opcional), `expand` (opcional), `sql_filter` (opcional), `params` (opcional), `account` (opcional), `ids` (opcional)

Lista os centros de custo da contabilidade, ou consulta um pelo id interno.

### 20. `protheus_produtos`
**Input**: `fonte` (opcional), `page` (opcional), `page_size` (opcional), `order` (opcional), `fields` (opcional), `filter` (opcional), `expand` (opcional), `sql_filter` (opcional), `params` (opcional), `account` (opcional)

Consulta o cadastro de produtos.

### 21. `protheus_estoque`
**Input**: `fonte` (opcional), `page` (opcional), `page_size` (opcional), `order` (opcional), `fields` (opcional), `filter` (opcional), `expand` (opcional), `sql_filter` (opcional), `params` (opcional), `account` (opcional)

Consulta o saldo em estoque. Escolha a fonte: varejo (saldo em estoque do varejo) ou mrp (estoque do MRP, com armazém, lote e saldos bloqueado, consignado e em controle de qualidade). São módulos distintos e podem div…

### 22. `protheus_vendas_varejo`
**Input**: `id` (opcional), `page` (opcional), `page_size` (opcional), `order` (opcional), `fields` (opcional), `filter` (opcional), `expand` (opcional), `sql_filter` (opcional), `params` (opcional), `account` (opcional), `ids` (opcional)

Consulta as vendas do varejo, ou uma venda pelo id interno.

### 23. `protheus_pedidos_varejo`
**Input**: `id` (opcional), `page` (opcional), `page_size` (opcional), `order` (opcional), `fields` (opcional), `filter` (opcional), `expand` (opcional), `sql_filter` (opcional), `params` (opcional), `account` (opcional), `ids` (opcional)

Lista os pedidos de venda do varejo.

### 24. `protheus_notas_totais`
**Input**: `tipo` (opcional), `canceladas` (opcional), `page` (opcional), `page_size` (opcional), `order` (opcional), `fields` (opcional), `filter` (opcional), `expand` (opcional), `sql_filter` (opcional), `params` (opcional), `account` (opcional)

Consulta os totais de notas fiscais de saída ou de entrada do varejo, incluindo a visão de notas canceladas.

### 25. `protheus_ordens_producao`
**Input**: `branch_id` (opcional), `codigo` (opcional), `page` (opcional), `page_size` (opcional), `order` (opcional), `fields` (opcional), `filter` (opcional), `expand` (opcional), `sql_filter` (opcional), `params` (opcional), `account` (opcional), `branch_ids` (opcional)

Consulta as ordens de produção do MRP.

### 26. `protheus_compras_mrp`
**Input**: `tipo` (opcional), `branch_id` (opcional), `codigo` (opcional), `page` (opcional), `page_size` (opcional), `order` (opcional), `fields` (opcional), `filter` (opcional), `expand` (opcional), `sql_filter` (opcional), `params` (opcional), `account` (opcional), `branch_ids` (opcional)

Consulta os pedidos de compra ou as solicitações de compra do MRP.

## Prompts de exemplo

```
Quais APIs do Protheus a minha instalação responde?
Liste as filiais do grupo com os códigos de empresa
Qual o saldo em estoque dos produtos hoje?
Mostre a tabela de preços 001 com os itens
Quais ordens de produção estão previstas para esta semana?
Quanto de limite de crédito o cliente X tem?
```

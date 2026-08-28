# TOTVS Protheus

### MCP para TOTVS Protheus, o seu ERP respondendo em linguagem natural

Converse com o **TOTVS Protheus** da sua empresa a partir do Claude, do ChatGPT ou de qualquer cliente MCP. Roda sobre a **API REST oficial da TOTVS**, contra a **sua própria instalação**: você informa a URL do serviço REST, o usuário e a senha do Protheus, e nada trafega por um intermediário do ERP. Diferente dos MCPs de Protheus que já existem, que são ferramentas de desenvolvimento (compilar AdvPL, buscar no TDN), este lê **dado de negócio**: filiais, clientes e fornecedores, produtos, estoque, tabelas de preço, vendas e pedidos, notas, ordens de produção e compras do MRP. Somente leitura. **Não afiliado à TOTVS.**

- 🏢 **O seu Protheus, não um intermediário** — conecta na instalação da sua empresa pela API REST oficial da TOTVS
- 🔎 **Descobre o que a SUA instalação responde** — cada Protheus publica um conjunto diferente de APIs, e o diagnóstico mapeia isso em uma pergunta
- 📦 **Dado de negócio, não ferramenta de dev** — filiais, clientes e fornecedores, produtos, estoque, tabelas de preço, vendas, pedidos, notas, ordens de produção e compras do MRP
- 🧩 **Chama qualquer rota REST**, inclusive os endpoints customizados que a sua empresa criou no Protheus
- 🔒 **Somente leitura** — a versão 1 só consulta, nunca grava no ERP
- 💬 **Funciona com qualquer cliente MCP**: Claude Desktop, ChatGPT, Cursor, VS Code, Cline, Continue

[English version](README.md) · [Documentação completa](docs/) · [Skill pra agentes](skills/)

---

## Instalar em 1 clique

### Claude (Web e Desktop)

A Anthropic unificou a instalação de MCPs em `claude.ai/customize/connectors`. **O mesmo link serve pra Claude Web e Claude Desktop** (basta estar logado):

[➕ Abrir no Claude e conectar](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

**Manual** (se o deeplink não abrir): [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Adicionar conector personalizado** → cole **Nome** `TOTVS Protheus` e **URL** `https://api.mcp.ai/p_protheus`.

### Cursor

[➕ Instalar TOTVS Protheus no Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=protheus&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9wcm90aGV1cyJ9)

### VS Code (Copilot Chat)

[➕ Instalar TOTVS Protheus no VS Code](vscode:mcp/install?name=protheus&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_protheus%22%7D)

### ChatGPT, Manus, OpenClaw e mais 40+ clientes

Funciona em qualquer cliente MCP que suporte **MCP over HTTP**. A URL do servidor é sempre:

```
https://api.mcp.ai/p_protheus
```

Detalhes por cliente: [INSTALL.md](INSTALL.md).

---

## Exemplos de uso

```
Quais APIs do Protheus a minha instalação responde?
Liste as filiais do grupo com os códigos de empresa
Qual o saldo em estoque dos produtos hoje?
Mostre a tabela de preços 001 com os itens
Quais ordens de produção estão previstas para esta semana?
Quanto de limite de crédito o cliente X tem?
```

---

## 26 ferramentas disponíveis

| Tool | Descrição |
|---|---|
| `protheus_list_accounts` | Lista as instalações Protheus conectadas a este install, com id e label (host/usuário). |
| `protheus_diagnostico` | Descobre quais APIs REST esta instalação Protheus realmente responde. |
| `protheus_catalogo` | Consulta o catálogo das 125 APIs REST oficiais da linha Protheus (id, título, módulo e rotas de leitura), extraído da documentação pública da TOTVS. |
| `protheus_api` | Faz um GET em qualquer rota REST da instalação Protheus conectada. |
| `protheus_filiais` | Lista as empresas e filiais do grupo (API TSIBranches). |
| `protheus_modulos` | Lista os módulos do sistema Protheus nesta instalação. |
| `protheus_parametros` | Consulta os parâmetros de sistema do Protheus. |
| `protheus_usuarios` | Lista os usuários do Protheus, ou consulta um usuário por id. |
| `protheus_clientes_fornecedores` | Consulta o cadastro de clientes e fornecedores (API CustomerVendor). |
| `protheus_contatos` | Lista os contatos do CRM, ou consulta um contato por id. |
| `protheus_vendedores` | Lista os vendedores cadastrados, ou consulta um vendedor pelo código. |
| `protheus_oportunidades` | Lista as oportunidades comerciais do CRM, ou consulta uma oportunidade pelo id interno. |
| `protheus_propostas_comerciais` | Lista as propostas comerciais de uma oportunidade, ou consulta uma proposta específica. |
| `protheus_tabela_precos` | Consulta as tabelas de preço. Sem argumentos lista os cabeçalhos; com `codigo` traz uma tabela; com `codigo` e `itens` traz os itens e preços dela. |
| `protheus_condicoes_pagamento` | Lista as condições de pagamento cadastradas, ou consulta uma pelo id interno. |
| `protheus_limite_credito` | Consulta o limite de crédito dos clientes. |
| `protheus_comissoes` | Consulta as comissões de venda, ou uma comissão pelo id interno. |
| `protheus_transportadoras` | Lista as transportadoras cadastradas, ou consulta uma pelo id interno. |
| `protheus_centros_custo` | Lista os centros de custo da contabilidade, ou consulta um pelo id interno. |
| `protheus_produtos` | Consulta o cadastro de produtos. |
| `protheus_estoque` | Consulta o saldo em estoque. Escolha a fonte: varejo (saldo em estoque do varejo) ou mrp (estoque do MRP, com armazém, lote e saldos bloqueado, consignado e em controle de qualidade). São módulos distintos e podem div… |
| `protheus_vendas_varejo` | Consulta as vendas do varejo, ou uma venda pelo id interno. |
| `protheus_pedidos_varejo` | Lista os pedidos de venda do varejo. |
| `protheus_notas_totais` | Consulta os totais de notas fiscais de saída ou de entrada do varejo, incluindo a visão de notas canceladas. |
| `protheus_ordens_producao` | Consulta as ordens de produção do MRP. |
| `protheus_compras_mrp` | Consulta os pedidos de compra ou as solicitações de compra do MRP. |

Detalhe de cada tool: [docs/ferramentas.md](docs/ferramentas.md)


---

## O que dá para perguntar

| Área | Cobertura |
|---|---|
| **Descoberta** | Filiais e empresas do grupo, módulos do sistema, parâmetros, usuários |
| **Cadastros** | Clientes e fornecedores, contatos, vendedores, transportadoras, centros de custo |
| **Comercial** | Oportunidades, propostas comerciais, tabelas de preço, condições de pagamento, comissões, limite de crédito |
| **Produtos e estoque** | Produtos e saldo em estoque, nas duas fontes (varejo e MRP) |
| **Vendas** | Vendas e pedidos do varejo, totais de notas fiscais de entrada e de saída |
| **Manufatura** | Ordens de produção, pedidos e solicitações de compra do MRP |
| **Curinga** | Qualquer rota REST da sua instalação, incluindo endpoints customizados |

### Antes de conectar, um aviso honesto

O Protheus **não é um SaaS com um endereço único**: cada empresa roda a própria
instalação. Duas consequências práticas:

1. **O serviço REST precisa estar publicado.** O seu time de TI habilita o REST no
   `appserver.ini`, aloca as threads (que consomem licença) e libera a porta. Sem
   isso não há o que conectar, com nenhuma ferramenta.
2. **Cada instalação responde a um subconjunto das APIs.** A TOTVS publica 125 APIs
   para a linha Protheus, mas o que a sua responde depende da versão da LIB, dos
   módulos licenciados e das customizações. Por isso a primeira pergunta a fazer é
   o **diagnóstico**: ele sonda a sua instalação e devolve, API por API, o que está
   disponível, o que não existe aí e o que o seu usuário não tem permissão de ver.

---

## Preços

Planos a partir do tier grátis. Veja [docs/precos.md](docs/precos.md).

---

## Privacidade & LGPD

- **Somente leitura**, nenhuma ferramenta altera dados na origem.
- **Sub-processadores**: TOTVS, o LLM host que você escolher (Claude, ChatGPT, Cursor, agente próprio). Lista completa em [docs/privacidade-lgpd.md](docs/privacidade-lgpd.md).
- Os dados retornados pelas tools são enviados ao **LLM host que você escolher**, sub-processador fora do nosso controle. Recomendamos planos com opt-out de treinamento.

---

## Perguntas frequentes

**É o MCP oficial da TOTVS?**
Não. Este é um MCP **independente**, que fala com a API REST oficial do Protheus da sua própria empresa usando as suas credenciais. **Não é afiliado à TOTVS** e não implica parceria. TOTVS e Protheus são marcas da TOTVS S.A., citadas aqui de forma nominativa.

**Que dados vocês acessam?**
Só os que o **seu usuário do Protheus** já pode ver, e só em leitura. A versão 1 faz exclusivamente requisições GET: não cria pedido, não baixa título, não grava nada no ERP.

**Preciso liberar meu Protheus na internet?**
O serviço REST precisa estar acessível para a nossa plataforma. Isso normalmente é feito publicando o endpoint com HTTPS e restringindo o acesso por IP ou por VPN, junto do seu time de TI. Se hoje o REST não está no ar, esse é o primeiro passo, e vale para qualquer integração, não só para a nossa.

**Por que uma pergunta funciona e outra diz que a rota não existe?**
Porque a API é a mesma, mas a implantação é sua. A TOTVS publica o contrato de 125 APIs para a linha Protheus; a sua instalação responde às que a versão da LIB e os módulos licenciados habilitam. Quando uma rota não existe aí, a resposta diz exatamente isso, em vez de fingir que não há registros. Rode o diagnóstico para ver o mapa completo da sua instalação.

**E os endpoints que a minha empresa criou no Protheus?**
Funcionam. Existe uma ferramenta curinga que chama qualquer rota REST da sua instalação, então as APIs MVC customizadas da sua casa entram sem a gente precisar publicar nada novo.

**Onde ficam a minha senha e a URL do meu ERP?**
Cifradas, e usadas só para pedir o token na API oAuth2 da sua própria instalação. O token de acesso do Protheus é transitório (expira em uma hora) e não é armazenado.

**Meu usuário tem autenticação de dois fatores. Funciona?**
Ainda não. Use um usuário de integração sem segundo fator, com permissão apenas para o que você quer expor. É também a prática recomendada por outro motivo: o acesso fica auditável e limitado no próprio Protheus.

**Serve para Datasul, RM ou Logix?**
Não. Este MCP é da linha **Protheus**. As outras linhas TOTVS têm APIs próprias e ficariam num MCP separado.


---

## Suporte

- 📧 [protheus@mcp.ai](mailto:protheus@mcp.ai)
- 🐛 [GitHub Issues](https://github.com/mcp-dir/protheus-mcp/issues)
- 📄 [docs/](docs/)

---

## Licença

MIT — veja [LICENSE](LICENSE). O servidor MCP em `api.mcp.ai/p_protheus` é proprietário (hosted); este repositório (manifestos, docs, skills) é MIT.

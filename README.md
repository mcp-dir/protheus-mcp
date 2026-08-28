# TOTVS Protheus

### TOTVS Protheus MCP, your ERP answering in plain language

Talk to your company's **TOTVS Protheus** ERP from Claude, ChatGPT or any MCP client. It runs on the **official TOTVS REST API**, against **your own installation**: you provide the REST service URL and your Protheus user and password, and nothing goes through an ERP middleman. Unlike the Protheus MCPs that already exist, which are developer tools (compiling AdvPL, searching the TDN), this one reads **business data**: branches, customers and vendors, products, stock, price lists, sales and orders, invoice totals, production orders and MRP purchasing. Read-only. **Not affiliated with TOTVS.**

- 🏢 **Your Protheus, not a middleman** — connects to your company's installation through the official TOTVS REST API
- 🔎 **Finds out what YOUR installation answers** — every Protheus publishes a different set of APIs, and the diagnostic maps it in one question
- 📦 **Business data, not a dev tool** — branches, customers and vendors, products, stock, price lists, sales, orders, invoice totals, production orders and MRP purchasing
- 🧩 **Calls any REST route**, including the custom endpoints your company built in Protheus
- 🔒 **Read-only** — v1 only queries, it never writes to the ERP
- 💬 **Works with any MCP client**: Claude Desktop, ChatGPT, Cursor, VS Code, Cline, Continue

[Versão em português](README.pt.md) · [Full docs (PT-BR)](docs/) · [Agent skill](skills/)

---

## One-click install

### Claude (Web and Desktop)

Anthropic unified MCP installation at `claude.ai/customize/connectors`. **The same link works for Claude Web and Claude Desktop** (just be logged in):

[➕ Open in Claude and connect](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

**Manual** (if the deeplink does not open): [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Add custom connector** → paste **Name** `TOTVS Protheus` and **URL** `https://api.mcp.ai/p_protheus`.

### Cursor

[➕ Install TOTVS Protheus in Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=protheus&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9wcm90aGV1cyJ9)

### VS Code (Copilot Chat)

[➕ Install TOTVS Protheus in VS Code](vscode:mcp/install?name=protheus&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_protheus%22%7D)

### ChatGPT, Manus, OpenClaw and 40+ other clients

Works with any MCP client that speaks **MCP over HTTP**. The server URL is always:

```
https://api.mcp.ai/p_protheus
```

Per-client details: [INSTALL.md](INSTALL.md).

---

## Example prompts

```
Which Protheus APIs does my installation answer?
List the group's branches with their company codes
What is today's stock balance by product?
Show price list 001 with its items
Which production orders are scheduled for this week?
What is customer X's credit limit?
```

---

## 26 tools available

| Tool | Description |
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

Details for each tool: [docs/ferramentas.md](docs/ferramentas.md) (PT-BR)


---

## What you can ask

| Area | Coverage |
|---|---|
| **Discovery** | Group branches and companies, system modules, parameters, users |
| **Master data** | Customers and vendors, contacts, sales reps, carriers, cost centers |
| **Commercial** | Opportunities, commercial proposals, price lists, payment terms, commissions, credit limits |
| **Products and stock** | Products and stock balance, from both sources (retail and MRP) |
| **Sales** | Retail sales and orders, inbound and outbound invoice totals |
| **Manufacturing** | Production orders, MRP purchase orders and requests |
| **Wildcard** | Any REST route on your installation, including custom endpoints |

### An honest note before you connect

Protheus is **not a SaaS with a single address**: every company runs its own
installation. Two practical consequences:

1. **The REST service has to be published.** Your IT team enables REST in
   `appserver.ini`, allocates the threads (which consume licenses) and opens the
   port. Without that there is nothing to connect to, with any tool.
2. **Each installation answers a subset of the APIs.** TOTVS publishes 125 APIs for
   the Protheus line, but what yours answers depends on the LIB version, the
   licensed modules and your customizations. That is why the first question to ask
   is the **diagnostic**: it probes your installation and reports, API by API,
   what is available, what does not exist there, and what your user cannot see.

---

## Pricing

Plans start at a free tier. See [docs/precos.md](docs/precos.md) (PT-BR).

---

## Privacy & data protection

- **Read-only**, no tool changes data at the source.
- **Sub-processors**: TOTVS, the LLM host you choose (Claude, ChatGPT, Cursor, your own agent). Full list in [docs/privacidade-lgpd.md](docs/privacidade-lgpd.md).
- Data returned by the tools is sent to **the LLM host you choose**, a sub-processor outside our control. We recommend plans with training opt-out.

---

## FAQ

**Is this the official TOTVS MCP?**
No. This is an **independent** MCP that talks to your own company's official Protheus REST API using your credentials. It is **not affiliated with TOTVS** and implies no partnership. TOTVS and Protheus are trademarks of TOTVS S.A., referenced here nominatively.

**What data do you access?**
Only what **your Protheus user** can already see, and only for reading. v1 issues GET requests exclusively: it creates no orders, settles no invoices, and writes nothing to the ERP.

**Do I have to expose my Protheus to the internet?**
The REST service must be reachable by our platform. That is usually done by publishing the endpoint over HTTPS and restricting access by IP or VPN, together with your IT team. If REST is not up today, that is step one, and it applies to any integration, not just ours.

**Why does one question work and another says the route does not exist?**
Because the API is shared but the deployment is yours. TOTVS publishes the contract for 125 Protheus-line APIs; your installation answers the ones your LIB version and licensed modules enable. When a route does not exist there, the answer says exactly that instead of pretending there are no records. Run the diagnostic to see the full map of your installation.

**What about the endpoints my company built in Protheus?**
They work. There is a wildcard tool that calls any REST route on your installation, so your in-house custom MVC APIs are reachable without us shipping anything new.

**Where do my password and ERP URL live?**
Encrypted, and used only to request the token from your own installation's oAuth2 API. The Protheus access token is transient (it expires in an hour) and is not stored.

**My user has two-factor authentication. Does it work?**
Not yet. Use an integration user without a second factor, permissioned only for what you want to expose. That is the recommended practice anyway: access stays auditable and scoped inside Protheus itself.

**Does it work for Datasul, RM or Logix?**
No. This MCP targets the **Protheus** line. The other TOTVS lines have their own APIs and would be a separate MCP.


---

## Support

- 📧 [protheus@mcp.ai](mailto:protheus@mcp.ai)
- 🐛 [GitHub Issues](https://github.com/mcp-dir/protheus-mcp/issues)
- 📄 [docs/](docs/)

---

## License

MIT — see [LICENSE](LICENSE). The MCP server at `api.mcp.ai/p_protheus` is proprietary (hosted); this repo (manifests, docs, skills) is MIT.

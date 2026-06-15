# Registro de Mudanças — JS Imports Cell

> Arquivo de controle de versões do prompt do agente JS Imports Cell (WhatsApp / JSON n8n).
> **Regra:** nunca modificar o arquivo de versão anterior. Cada mudança gera um novo arquivo versionado.

---

## Mudança #1 — Versão inicial do prompt

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.0
**Solicitante:** Cliente

### Problema identificado
Projeto novo **JS Imports Cell** sem estrutura de versionamento no repositório M4IA. Necessidade de registrar o prompt original (referência interna v0.0 — base `Prompt/Padrao.md` + `formulario.csv` 07/05/2026) antes de aplicar ajustes solicitados pelo cliente.

### Solução
Criação da pasta do projeto com:
- `Prompt Original.md` — snapshot imutável do prompt recebido do cliente
- `JS Imports Cell.md` — arquivo de trabalho (versão atual)
- `JS Imports Cell_v1.0.0.md` — primeira versão versionada (padrão M4IA; equivalente à v0.0 do cliente)

### Arquivos afetados
- `Prompt Original.md` (criado)
- `JS Imports Cell.md` (criado)
- `JS Imports Cell_v1.0.0.md` (criado a partir do prompt original)
- `CAMBIOS_PROMPT.md` (criado)

### Validação
✅ Prompt original preservado integralmente em `Prompt Original.md`
✅ Versão inicial v1.0.0 criada e registrada
✅ Estrutura alinhada ao padrão M4IA (versionamento + CAMBIOS_PROMPT.md)
✅ Conteúdo inclui persona, ESTOQUE/TAXAS_MAQ, parcelamento (6x celular / 3x acessório / boleto 18x), JSON de saída e redirecionamentos `js_imports`

### Impacto
- **Padroniza:** Controle de versões para o projeto JS Imports Cell
- **Previne:** Perda do prompt base ao aplicar futuras modificações
- **Melhora:** Rastreabilidade de cada ajuste solicitado pelo cliente

---

## Mudança #2 — Abordagem natural do parcelamento no boleto

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.1
**Solicitante:** Cliente

### Problema identificado
A IA respondia de forma robotizada e extensa quando o cliente perguntava sobre requisitos ou parcelamento (ex.: "Quais os requisitos para parcelamento?"). Antecipava cartão de crédito, documentação, retirada do aparelho e informações técnicas juntas, deixando a conversa pesada. A explicação do boleto ficava confusa e pouco fluida para leads vindos do anúncio.

### Solução
Nova seção **PARCELAMENTO NO BOLETO — FLUXO NATURAL** com passos 1–3:
- **Passo 1:** explicação comercial leve (CPF, entrada, mensal vs 14 dias) — sem cartão, documentos ou retirada
- **Passo 2a:** parcelas mensais → copy com link de pré-análise (`https://analisejsimportscell.lovable.app/f/cadastroanalisejsimportscell`) — IA permanece em `js_imports`
- **Passo 2b:** parcelas a cada 14 dias → handoff `venda`
- **Passo 3:** cliente finalizou pré-análise mensal → handoff `venda`

Ajustes complementares em abertura, consulta genérica, formas de pagamento, objeções, redirecionamentos, exemplos JSON e checklist.

### Arquivos afetados
- `JS Imports Cell_v1.0.1.md` (criado a partir de v1.0.0)
- `JS Imports Cell.md` (atualizado)

### Validação
✅ Fluxo passo 1 alinhado ao copy comercial aprovado pelo cliente
✅ Passo 2a com link exato e trava de segurança só na etapa mensal
✅ Cartão e documentação restritos a pedido do cliente ou etapa humana
✅ Tabela de redirecionamentos atualizada (js_imports nos passos 1 e 2a)
✅ Exemplos JSON para requisitos, mensal e 14 dias

### Impacto
- **Corrige:** Respostas robotizadas e excesso de informação no início sobre boleto
- **Melhora:** Conversa mais leve, comercial e alinhada ao funil da loja
- **Previne:** Handoff prematuro e menção de cartão/retirada antes da hora

---

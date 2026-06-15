# Registro de Mudanças — Go Tech

> Arquivo de controle de versões do prompt da assistente virtual Maia (Gotech — Santa Maria e Uruguaiana).
> **Regra:** nunca modificar o arquivo de versão anterior. Cada mudança gera um novo arquivo versionado.

---

## Mudança #1 — Versão inicial do prompt

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.0
**Solicitante:** Cliente

### Problema identificado
Projeto novo sem estrutura de versionamento. Necessidade de registrar o prompt original da assistente Maia antes de aplicar ajustes solicitados pelo cliente.

### Solução
Criação da pasta do projeto com:
- `Prompt Original.md` — snapshot imutável do prompt recebido do cliente
- `Go Tech.md` — arquivo de trabalho (versão atual)
- `Go Tech_v1.0.0.md` — primeira versão versionada

### Arquivos afetados
- `Prompt Original.md` (criado)
- `Go Tech.md` (criado)
- `Go Tech_v1.0.0.md` (criado a partir do prompt original)

### Validação
✅ Prompt original preservado integralmente em `Prompt Original.md`
✅ Versão inicial v1.0.0 criada e registrada
✅ Estrutura alinhada ao padrão M4IA (versionamento + CAMBIOS_PROMPT.md)

### Impacto
- **Padroniza:** Controle de versões para o projeto Go Tech
- **Previne:** Perda do prompt base ao aplicar futuras modificações
- **Melhora:** Rastreabilidade de cada ajuste solicitado pelo cliente

---

## Mudança #2 — Qualificação financeira antes de ofertar iPhone (boleto/financiamento)

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.1
**Solicitante:** Cliente

### Problema identificado
Quando o lead mencionava boleto ou financiamento, a Maia perguntava qual iPhone ou oferecia modelos antes de qualificar a situação financeira (nome limpo vs negativado). Isso gerava expectativa de aprovação indevida. Em perfis negativados sem alternativas (RGE, familiar, CLT), a IA insistia em iPhone em vez de direcionar para Android.

**Caso real (Rogério):** cliente pediu boleto → IA perguntou "Qual iPhone você tá procurando?" e, ao pedir Android, sugeriu iPhone equivalente.

### Solução
Inserida seção **`### ⚠️ QUALIFICAÇÃO FINANCEIRA — BOLETO / FINANCIAMENTO ⚠️`** em `## IDENTIFICAÇÃO DO INTERESSE`, com fluxo em 6 passos:
1. Perguntar nome limpo ou negativado
2A. Nome limpo → financeiras parceiras → seguir qualificação iPhone
2B. Negativado → explicar restrição iPhone → perguntar RGE
3. RGE sim → iPhone | RGE não → perguntar CLT/desconto em folha
4. CLT sim → iPhone | CLT não → PASSO 5
5. Direcionar para Android (consultar `ESTOQUE` ou setor responsável)
6. Regra para pedido explícito de Android

Ajustes pontuais (sem alterar tools, variáveis JSON ou formato de saída):
- **Regras de Qualificação** — bloqueio de pergunta de modelo enquanto qualificação financeira pendente
- **Fluxo de Qualificação** — novo passo **1.5** obrigatório antes do passo MODELO
- **IDENTIFICAÇÃO DA LOJA** — exceção de escopo para Android em perfil com restrição via boleto
- Exemplo do erro Rogério documentado na seção

### Arquivos afetados
- `Go Tech_v1.0.1.md` (criado a partir de v1.0.0)
- `Go Tech.md` (arquivo de trabalho atualizado)

### Validação
✅ Gatilhos boleto/financiamento mapeados
✅ Pergunta canônica de nome limpo/negativado definida
✅ Ramificações nome limpo, negativado + RGE, negativado + CLT, Android
✅ Tools (`ESTOQUE`), variáveis e JSON de saída preservados
✅ v1.0.0 preservado intacto

### Impacto
- **Previne:** Oferta prematura de iPhone sem qualificação financeira
- **Melhora:** Assertividade da oferta conforme perfil (iPhone vs Android)
- **Corrige:** Fluxo do caso boleto + Android observado no atendimento

---

## Mudança #3 — Qualificação financeira universal (antes de qualquer oferta de iPhone)

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.2
**Solicitante:** Cliente

### Problema identificado
A qualificação financeira (v1.0.1) só era acionada quando o cliente mencionava boleto/financiamento. Em consultas comerciais normais (ex.: "que iPhones 15 vocês tem?"), a Maia ia direto para novo/seminovo, orçamento com preço/cores/bateria e pergunta de cor — sem perguntar se o nome está limpo ou negativado.

**Caso real (Jairo):** após nome e cidade, cliente perguntou iPhone 15 → IA perguntou novo/seminovo → entregou orçamento R$ 4.297 + cores/bateria → "Qual cor você prefere?" sem qualificação financeira.

### Solução
Seção renomeada e ampliada para **`QUALIFICAÇÃO FINANCEIRA — OBRIGATÓRIA ANTES DE OFERECER iPhone`**:
- Aplica a **toda** consulta comercial de iPhone após o nome ser conhecido (não só boleto)
- Bloqueio explícito de novo/seminovo, cor, `ESTOQUE` e orçamento enquanto pendente
- PASSO 2A atualizado com texto do cliente ("Vou te mostrar algumas opções de iPhone...")
- PASSO 2B unificado com pergunta RGE + menção CLT (texto canônico do cliente)
- Modelo informado antes da qualificação fica **guardado** e retomado depois
- Exemplo **Jairo** documentado; passo **−1** em **ORÇAMENTOS - REGRA CRÍTICA NÚMERO 1**
- **Fluxo de Qualificação** passo 1.5 generalizado para todo interesse comercial

### Arquivos afetados
- `Go Tech_v1.0.2.md` (criado a partir de v1.0.1)
- `Go Tech.md` (arquivo de trabalho atualizado)

### Validação
✅ Pergunta obrigatória antes de novo/seminovo ou orçamento
✅ Ramificações nome limpo / negativado / Android preservadas
✅ Tools, JSON e variáveis dinâmicas intactos
✅ v1.0.1 preservado intacto

### Impacto
- **Previne:** Oferta prematura mesmo sem menção a boleto (caso Jairo)
- **Corrige:** Qualificação financeira como gate universal da venda iPhone

---

## Mudança #4 — Método de pagamento antes da qualificação de crédito

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.3
**Solicitante:** Cliente

### Problema identificado
Na v1.0.2, ao cliente perguntar modelos (caso Jairo), a Maia pulava direto para a pergunta de nome limpo/negativado — sem antes identificar o **método de pagamento**. Faltava saber se seria à vista, cartão, boleto ou financiamento antes de qualificar crédito ou apresentar opções.

### Solução
Seção renomeada para **`QUALIFICAÇÃO COMERCIAL — ANTES DE OFERECER iPhone`** com fluxo em **dois passos**:
1. **PASSO 1** — Método de pagamento (sempre primeiro): "Qual seria seu método de pagamento? À vista, parcelado, boleto, financiamento etc?"
2. **PASSO 2** — Situação do nome — **somente** se boleto, financiamento ou parcelamento via boleto

Novidades:
- **PASSO 1B** — Ramificação: à vista/cartão → fluxo iPhone direto; boleto/financiamento → PASSO 2
- **PASSO 1C** — Cliente insiste em ver modelos sem informar pagamento → explica importância e repete pergunta
- Esclarecimento quando cliente diz só "parcelado" (cartão vs boleto)
- Exemplo Jairo atualizado: erro ao perguntar crédito antes do método de pagamento
- Passos de crédito renumerados (3A, 3B, 4, 5, 6)

### Arquivos afetados
- `Go Tech_v1.0.3.md` (criado a partir de v1.0.2)
- `Go Tech.md` (arquivo de trabalho atualizado)

### Validação
✅ Método de pagamento perguntado antes de nome limpo/negativado
✅ Qualificação de crédito só após boleto/financiamento
✅ Tratamento de cliente que insiste em ver modelos
✅ Ramificações nome limpo / negativado / Android preservadas
✅ v1.0.2 preservado intacto

### Impacto
- **Corrige:** Ordem correta de qualificação (pagamento → crédito → oferta)
- **Melhora:** Experiência para clientes à vista/cartão (sem pergunta desnecessária de crédito)

---

## Mudança #5 — Reforço redirecionamento Android (negativado sem RGE/CLT)

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.3
**Solicitante:** Cliente

### Problema identificado
O fluxo Android para cliente negativado **sem** conta RGE e **sem** desconto em folha (CLT) existia no PASSO 5, mas não estava suficientemente explícito — faltava deixar claro que, ao negar as alternativas, a IA **deve** direcionar imediatamente para Android com a mensagem canônica, sem insistir em iPhone.

### Solução
- **PASSO 4** expandido: sequência RGE → CLT → Android; proibições explícitas após negativa
- **PASSO 5** reforçado: critérios de acionamento obrigatório, mensagem exata do cliente, qualificação concluída para Android, lista de proibições
- Novo exemplo de erro: negativado sem RGE e sem CLT → redirecionamento Android (não oferecer iPhone)

### Arquivos afetados
- `Go Tech_v1.0.3.md` (atualizado)
- `Go Tech.md` (sincronizado)

### Validação
✅ Negativa às alternativas dispara PASSO 5 imediatamente
✅ Mensagem Android canônica documentada
✅ Proibição de insistir em iPhone após negativa

### Impacto
- **Corrige:** Redirecionamento Android quando negativado não possui RGE nem CLT
- **Previne:** Oferta de iPhone após esgotar alternativas de aprovação

---

# Registro de Mudanças — Francivaldo Phones

> Arquivo de controle de versões do prompt de atendimento Maria (Francivaldo Phones — Boleto/Financiamento).
> **Regra:** nunca modificar o arquivo de versão anterior. Cada mudança gera um novo arquivo versionado.

---

## Mudança #1 — Versão inicial do prompt

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.0
**Solicitante:** Cliente

### Problema identificado
Projeto novo sem estrutura de versionamento. Necessidade de registrar o prompt original do agente de processamento de consultas de estoque antes de aplicar ajustes solicitados pelo cliente.

### Solução
Criação da pasta do projeto com:
- `Prompt Original.md` — snapshot imutável do prompt recebido do cliente
- `Francivaldo Phones.md` — arquivo de trabalho (versão atual)
- `Francivaldo Phones_v1.0.0.md` — primeira versão versionada

### Arquivos afetados
- `Prompt Original.md` (criado)
- `Francivaldo Phones.md` (criado)
- `Francivaldo Phones_v1.0.0.md` (criado a partir do prompt original)

### Validação
✅ Prompt original preservado integralmente em `Prompt Original.md`
✅ Versão inicial v1.0.0 criada e registrada
✅ Estrutura alinhada ao padrão M4IA (versionamento + CAMBIOS_PROMPT.md)

### Impacto
- **Padroniza:** Controle de versões para o projeto Francivaldo Phones
- **Previne:** Perda do prompt base ao aplicar futuras modificações
- **Melhora:** Rastreabilidade de cada ajuste solicitado pelo cliente

---

## Mudança #2 — Identificação da loja (endereço e horário)

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.1
**Solicitante:** Cliente

### Problema identificado
O prompt não continha endereço nem horário de funcionamento da Francivaldo Phones em Oeiras, informações necessárias para orientar clientes sobre retirada na loja.

### Solução
Adicionada seção **Identificação da Loja — Francivaldo Phones** após **Sua Função**, com:
- Endereço: Praça Visconde da Parnaíba, nº 49, Centro de Oeiras
- Horário: Seg a sex 7h40–17h40 | Sáb e feriados 8h–12h40
- Modelo de referência para convite de retirada na loja (texto fornecido pelo cliente)

Atualizada seção **INFORMAÇÕES ADICIONAIS** no final do prompt com os mesmos dados da loja.

### Arquivos afetados
- `Francivaldo Phones_v1.0.1.md` (criado a partir de v1.0.0)
- `Francivaldo Phones.md` (arquivo de trabalho atualizado)

### Validação
✅ Endereço e horário inseridos conforme texto do cliente
✅ Modelo de mensagem de convite para retirada registrado como referência
✅ v1.0.0 preservado intacto

### Impacto
- **Padroniza:** Dados oficiais da loja no prompt
- **Melhora:** Base para orientar clientes sobre visita e retirada na loja

---

## Mudança #3 — Resposta padronizada ao interesse em boleto

**Data:** 19/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.2
**Solicitante:** Cliente

### Problema identificado
Quando o cliente mencionava boleto ou dizia que queria comprar no boleto, a IA respondia com texto resumido e em balões separados (ex.: "No boleto a gente trabalha com Android lacrado... em até 18x com entrada" + "Qual aparelho tu tá querendo?"), em vez do modelo oficial solicitado pelo cliente.

### Solução
Adicionado em **Identificação da Loja — Francivaldo Phones** o bloco **Modelo de referência — interesse em boleto**, com gatilhos, regra de uso exato do texto e mensagem obrigatória fornecida pelo cliente (Android novos e lacrados Samsung/Motorola/Realme/Xiaomi, até 18x, entrada facilitada e pergunta pelo modelo).

### Arquivos afetados
- `Francivaldo Phones_v1.0.2.md` (criado a partir de v1.0.1)
- `Francivaldo Phones.md` (arquivo de trabalho atualizado)

### Validação
✅ Modelo de mensagem cadastrado conforme texto do cliente
✅ Gatilhos de boleto documentados na seção de identificação da loja
✅ Regra proíbe resumir ou fragmentar a resposta em balões com redação diferente
✅ v1.0.1 preservado intacto

### Impacto
- **Padroniza:** Resposta única e oficial quando o cliente pergunta ou declara compra no boleto
- **Corrige:** Comportamento observado no atendimento (texto antigo em dois balões)
- **Melhora:** Clareza sobre marcas, parcelamento e próximo passo (modelo de interesse)

---

## Mudança #4 — Novo prompt Maria (atendimento humanizado)

**Data:** 23/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v2.0.0
**Solicitante:** Cliente

### Problema identificado
O prompt anterior (v1.0.x) era um **agente de processamento de consultas de estoque** (extração de query JSON para busca no banco). O cliente passou a usar a Francivaldo Phones com o fluxo de **atendimento virtual Maria** (qualificação, ESTOQUE, boleto/financiamento, links PayJoy/CLT, redirecionamento OFJ), alinhado ao padrão humanizado de outras lojas.

### Solução
Substituição completa do conteúdo do prompt por **Prompt de Atendimento — Maria | Francivaldo Phones (Boleto/Financiamento) — Versão Humanizada**, incluindo:
- Persona Maria, tom regional Piauí, fluxo Passos 1–7
- Tool `ESTOQUE`, card de orçamento, CTA obrigatório, quatro formas de pagamento
- Links PayJoy e CLT/consignado **sem** consulta de CPF no chat
- Políticas de seminovo (só iPhone), iPhone lacrado descontinuado, boleto Android
- Fichas de produtos complementares, assistência, redirecionamentos (`francivaldo-phones`, `varejo`, `gerente`, `atacado`, `tecnico`, `garantias`)
- Formato de saída JSON com exemplos

Versões v1.0.0–v1.0.2 e `Prompt Original.md` **preservados** como histórico do agente de estoque.

### Arquivos afetados
- `Francivaldo Phones_v2.0.0.md` (criado — novo prompt Maria)
- `Francivaldo Phones.md` (arquivo de trabalho atualizado)

### Validação
✅ Prompt Maria registrado integralmente em v2.0.0
✅ Arquivo de trabalho sincronizado com a versão versionada
✅ Versões anteriores (v1.0.x) mantidas intactas
✅ Entrada registrada em CAMBIOS_PROMPT.md

### Impacto
- **Substitui:** Agente de estoque pelo atendimento comercial humanizado Maria
- **Padroniza:** Fluxo OFJ, ESTOQUE-first, sem formulário de consulta de CPF
- **Melhora:** Qualificação (modelo → pagamento → orçamento), links de financiamento e handoff por departamento

---

## Mudança #5 — Resposta padronizada ao interesse em boleto (prompt Maria)

**Data:** 23/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v2.0.1
**Solicitante:** Cliente

### Problema identificado
No prompt Maria (v2.0.0), quando o cliente mencionava boleto ou dizia que queria comprar no boleto, a IA podia responder com texto resumido e em balões separados (ex.: "No boleto a gente trabalha com Android lacrado... em até 18x com entrada" + "Qual aparelho tu tá querendo?"), em vez do modelo oficial já validado na Mudança #3 (v1.0.2).

### Solução
- Adicionado em **Identificação da Loja** o bloco **Modelo de referência — interesse em boleto**, com gatilhos, regra de uso do texto exato e mensagem obrigatória (Android novos e lacrados Samsung/Motorola/Realme/Xiaomi, até 18x, entrada facilitada e pergunta pelo modelo).
- Adicionado em **Cenários Especiais** o cenário **Cliente pergunta ou declara interesse em boleto**, apontando para o modelo e proibindo fragmentar com redação diferente.

### Arquivos afetados
- `Francivaldo Phones_v2.0.1.md` (criado a partir de v2.0.0)
- `Francivaldo Phones.md` (arquivo de trabalho atualizado)

### Validação
✅ Modelo de mensagem cadastrado conforme Mudança #3
✅ Gatilhos de boleto documentados na seção de identificação da loja
✅ Cenário especial reforça proibição de resumir ou fragmentar a resposta
✅ v2.0.0 preservado intacto

### Impacto
- **Padroniza:** Resposta única e oficial quando o cliente pergunta ou declara compra no boleto
- **Corrige:** Comportamento observado no atendimento (texto antigo em dois balões)
- **Melhora:** Clareza sobre marcas, parcelamento e próximo passo (modelo de interesse)

---

## Mudança #6 — Pergunta oficial pelo modelo de interesse

**Data:** 23/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v2.0.2
**Solicitante:** Cliente

### Problema identificado
A IA respondia com variações como *"Qual aparelho tu tá querendo?"* ou *"Qual aparelho você está buscando?"* ao perguntar o modelo, em vez do texto oficial solicitado pelo cliente.

### Solução
- Substituída a pergunta pelo modelo em **Passo 2**, **apresentação comercial**, **Primeira Mensagem** e **exemplos JSON** por: **"Qual modelo de celular você tem interesse em?"**
- Adicionado bloco **Texto oficial da pergunta pelo modelo** com lista **PROIBIDO** (*"Qual aparelho tu tá querendo?"*, etc.)
- Regra explícita de usar sempre o texto oficial na qualificação de modelo (exceto no **Modelo de referência — interesse em boleto**, que mantém redação fixa própria)

### Arquivos afetados
- `Francivaldo Phones_v2.0.2.md` (criado a partir de v2.0.1)
- `Francivaldo Phones.md` (arquivo de trabalho atualizado)

### Validação
✅ Texto oficial cadastrado em Passo 2, abertura comercial e exemplos JSON
✅ Variações proibidas documentadas (tu tá querendo / aparelho)
✅ v2.0.1 preservado intacto

### Impacto
- **Padroniza:** Pergunta única pelo modelo conforme ficha do cliente
- **Corrige:** Resposta regional/informal "qual aparelho tu tá querendo?"
- **Melhora:** Clareza na qualificação do interesse (modelo de celular)

---

## Mudança #7 — Pergunta oficial pelo valor de entrada (Passo 4)

**Data:** 23/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v2.0.3
**Solicitante:** Cliente

### Problema identificado
No ramo **boleto** (Passo 4), a IA respondia *"Quanto tu pretende dar de entrada?"* em tom regional, em vez do texto oficial solicitado pelo cliente.

### Solução
- Substituído o **texto-base** do **Passo 4** por: **"[NOME], qual valor você pretende dar de entrada?"**
- Adicionado bloco **Texto oficial da pergunta de entrada** com lista **PROIBIDO** (*"Quanto tu pretende dar de entrada?"*, etc.)
- Regra de usar **você** + **qual valor** nesta pergunta (sem **tu/quanto**), alinhada em troca como entrada, simulação na loja e exemplo **3b** (ERRADO)

### Arquivos afetados
- `Francivaldo Phones_v2.0.3.md` (criado a partir de v2.0.2)
- `Francivaldo Phones.md` (arquivo de trabalho atualizado)

### Validação
✅ Texto oficial cadastrado no Passo 4 (somente boleto)
✅ Variações proibidas documentadas (tu/quanto)
✅ v2.0.2 preservado intacto

### Impacto
- **Padroniza:** Pergunta de entrada conforme ficha do cliente
- **Corrige:** "Quanto tu pretende dar de entrada?"
- **Melhora:** Qualificação de entrada no financiamento com linguagem consistente

---

## Mudança #8 — Reforço Passo 4 entrada (caso real John Jairo)

**Data:** 24/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v2.0.4
**Solicitante:** Cliente

### Problema identificado
Apesar do texto oficial na v2.0.3, em atendimento real (cliente John Jairo escolheu **boleto** após recomendação Xiaomi) a IA respondeu *"John Jairo, quanto tu pretende dar de entrada?"* em vez de *"John Jairo, qual valor você pretende dar de entrada?"*. O rótulo **tom regional** no Passo 4 conflitava com a regra de **você/qual valor**, e faltava exemplo JSON do ramo boleto → Passo 4.

### Solução
- **Passo 4:** bloco **REGRA CRÍTICA — PERGUNTA DE ENTRADA (TEXTO FIXO)** com caso real ERRADO vs texto exato
- Rótulo do texto-base alterado para **cópia exata, sem regionalismo tu/quanto**
- Tabela do **Passo 3** (ramo boleto) cita o texto exato obrigatório
- **Regras Específicas** e **checklist JSON** reforçam Passo 4
- **Exemplo 3f** (John Jairo + boleto → Passo 4) com JSON correto e ERRADO explícito

### Arquivos afetados
- `Francivaldo Phones_v2.0.4.md` (criado a partir de v2.0.3)
- `Francivaldo Phones.md` (arquivo de trabalho atualizado)

### Validação
✅ Caso real documentado como ERRADO no prompt
✅ Exemplo JSON 3f espelha fluxo boleto → pergunta de entrada
✅ v2.0.3 preservado intacto

### Impacto
- **Corrige:** IA usando tu/quanto no Passo 4 após escolha de boleto
- **Reforça:** Exceção ao tom regional só na pergunta de entrada
- **Melhora:** Adesão ao texto fixo sem alterar resto do fluxo

---

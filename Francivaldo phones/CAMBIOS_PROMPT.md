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

## Mudança #9 — Requisitos de documentação para análise no boleto (fluxo + FAQ)

**Data:** 23/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v2.0.5
**Solicitante:** Cliente

### Problema identificado
Quando o cliente confirmava compra via boleto ou perguntava sobre documentação, requisitos ou análise do boleto, a IA não informava de forma padronizada o que é necessário para prosseguir com a análise (RG legível, chip ativo, titular presente na loja).

### Solução
- Criado bloco **Requisitos para análise no boleto (documentação)** em **Financiamento no boleto** (Informações da Loja) com os três itens oficiais e texto de referência.
- **Passo 4** atualizado: após a pergunta de entrada (balão 1), **balão 2 obrigatório** com os requisitos quando o cliente confirmou compra via boleto.
- Novo cenário **Cliente pergunta documentos, requisitos ou análise no boleto (FAQ)** em Cenários Especiais — mesma ficha para perguntas sobre documentação, requisitos, aprovação ou análise.
- Reforço em **Regras Específicas**, checklist JSON e exemplos **3f** (fluxo) e **3g** (FAQ).

### Arquivos afetados
- `Francivaldo Phones_v2.0.5.md` (criado a partir de v2.0.4)
- `Francivaldo Phones.md` (arquivo de trabalho atualizado)

### Validação
✅ Fluxo boleto (Passo 4) exige segundo balão com RG, chip ativo e titular na loja
✅ FAQ global responde com os mesmos três requisitos e explicação de agilizar análise
✅ v2.0.4 preservado intacto

### Impacto
- **Padroniza:** Informação de documentação/requisitos no boleto em todo o atendimento
- **Melhora:** Cliente sabe o que levar antes da análise e visita à loja
- **Previne:** Respostas vagas ou redirecionamento ao vendedor sem listar requisitos

---

## Mudança #10 — Resposta combinada boleto (política + link PayJoy + requisitos)

**Data:** 23/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v2.0.6
**Solicitante:** Cliente

### Problema identificado
Caso real (Francisco): cliente perguntou *"O que é necessário para comprar no boleto?"* e a IA respondeu com política (Android, entrada, 18x) + link PayJoy, mas **sem** os requisitos de documentação. O cliente precisou insistir: *"Isso eu já sei. Qual documento é necessário?"*

### Solução
- Criado bloco **Resposta combinada — boleto PayJoy (política + link + requisitos)** em **Financiamento no boleto** — **3 balões obrigatórios** no mesmo turno quando o assunto for necessários/documentos/compra no boleto ou envio do link PayJoy.
- Cenário FAQ atualizado: **não** enviar só requisitos nem só política+link.
- **Passo 6** (regras dos links), **Cliente negativado**, checklist JSON, exceção de balões e exemplos **3g** (Francisco), **3h** (reforço) e **7** atualizados.

### Arquivos afetados
- `Francivaldo Phones_v2.0.6.md` (criado a partir de v2.0.5)
- `Francivaldo Phones.md` (arquivo de trabalho atualizado)

### Validação
✅ Pergunta *"o que é necessário para comprar no boleto?"* exige política + link + RG/chip/titular
✅ Caso real documentado como ERRADO (só 2 balões sem requisitos)
✅ v2.0.5 preservado intacto

### Impacto
- **Corrige:** Cliente não precisa perguntar documento em mensagem separada
- **Padroniza:** Link PayJoy sempre acompanhado dos requisitos oficiais
- **Melhora:** Resposta completa em um único turno

---

## Mudança #11 — CTA boleto/financiamento (link vs loja)

**Data:** 25/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v2.0.7
**Solicitante:** Cliente

### Problema identificado
Após orçamento no ramo boleto/financiamento, a IA improvisava comunicação formal (*"Você prefere fazer a análise pelo link ou passar na loja?"*), separava pitch de loja em balões extras e fechava com tagline corporativa (*"Francivaldo Phones — estamos à disposição..."*), fora do tom regional da Maria e sem orientar claramente o próximo passo (link PayJoy vs convite à loja).

### Solução
- **CTA obrigatório após orçamento:** texto oficial **CTA boleto/financiamento** (link vs loja + benefício da visita presencial) e variação curta; regras de ramificação (link → Passo 6 / Resposta combinada PayJoy; loja → Passo 5).
- Proibição de fechamento corporativo, balões extras de marca e CTA genérico (*"Fica bom pra ti?"*) no ramo boleto/CLT.
- Tabela de preço boleto, exemplos **✅/❌ CERTO/ERRADO**, **Exemplo 3i** (João / Galaxy A16) e item no checklist JSON.

### Arquivos afetados
- `Francivaldo Phones_v2.0.7.md` (criado a partir de v2.0.6)
- `Francivaldo Phones.md` (arquivo de trabalho atualizado)

### Validação
✅ CTA boleto padronizado com tom *tu* e escolha link vs loja em 2 balões
✅ Ramificação documentada (link → PayJoy combinado; loja → Passo 5)
✅ v2.0.6 preservado intacto

### Impacto
- **Padroniza:** Comunicação pós-orçamento no boleto/financiamento
- **Melhora:** Cliente entende as duas opções (link ou loja) sem texto improvisado
- **Previne:** Fechamentos corporativos e CTAs genéricos no ramo boleto

---

## Mudança #12 — Resposta padrão: cliente aprovado na análise do link

**Data:** 25/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v2.0.8
**Solicitante:** Cliente

### Problema identificado
Após o cliente fazer a análise/simulação no link (PayJoy ou CLT) e informar no chat que foi aprovado (ex.: *"fui aprovado"*), não havia cenário dedicado nem texto oficial — a IA improvisava ou reenviava link/repasse ao vendedor sem orientar o comparecimento na loja.

### Solução
- Novo cenário **Cliente aprovado na análise do link (PayJoy ou CLT)** em **Cenários Especiais** com **texto oficial** em 2 balões (aprovação + comparecer com documento; definir [MODELO] e entrada na loja).
- Regras: `francivaldo-phones`, sem repasse imediato; endereço via **Passo 5** se perguntarem; breve ramo para reprovação.
- Reforços em **Passo 6**, **Resposta combinada PayJoy**, **Regras Específicas**, checklist JSON, redirecionamentos (**item 11**) e **Exemplo 7b** (João / Note 14).

### Arquivos afetados
- `Francivaldo Phones_v2.0.8.md` (criado a partir de v2.0.7)
- `Francivaldo Phones.md` (arquivo de trabalho atualizado)

### Validação
✅ Gatilhos *"fui aprovado"* / equivalentes mapeados ao texto oficial
✅ [MODELO] dinâmico do fluxo; sem reenvio de link nem redirecionamento automático
✅ v2.0.7 preservado intacto

### Impacto
- **Padroniza:** Pós-aprovação no link PayJoy/CLT
- **Melhora:** Cliente sabe ir à loja com documento e fechar modelo/entrada presencialmente
- **Previne:** Reenvio de link ou repasse ao vendedor sem necessidade

---

## Mudança #13 — Texto oficial do Passo 5 (convite à loja)

**Data:** 25/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v2.0.9
**Solicitante:** Cliente

### Problema identificado
Ao confirmar o pedido e convidar o cliente à loja (**Passo 5**), a mensagem usava redação antiga (*"que dia tu consegue passar aqui na loja pra fechar contigo?"*) e horário sem feriados, sem o fechamento sobre deixar tudo pronto para finalizar a compra.

### Solução
Atualizado **somente** o bloco **Passo 5: Convite Leve à Loja + Tentar Marcar Visita** com texto oficial fixo: *"Perfeito, [NOME]!"*, pergunta *"Você consegue passar amanhã na loja?"*, endereço, horário (incl. sáb e feriados) e frase de fechamento. Cenários 4A/4B/4C e demais seções **inalterados**.

### Arquivos afetados
- `Francivaldo Phones_v2.0.9.md` (criado a partir de v2.0.8)
- `Francivaldo Phones.md` (arquivo de trabalho atualizado)

### Validação
✅ Texto oficial do Passo 5 conforme modelo do cliente
✅ Endereço e horário alinhados à identificação da loja
✅ v2.0.8 preservado intacto

### Impacto
- **Padroniza:** Convite à loja após confirmação do pedido
- **Melhora:** Cliente recebe endereço, horário e expectativa de finalização na visita
- **Previne:** Redação improvisada ou desatualizada no convite

---

## Mudança #14 — Texto oficial: método de análise para financiamento

**Data:** 25/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v2.0.10
**Solicitante:** Cliente

### Problema identificado
Quando o cliente perguntava sobre o **método de análise** para financiamento (link vs loja), não havia texto oficial fixo — a IA omitia o pitch da equipe na loja e o fechamento *"Francivaldo Phones — estamos à disposição..."*, ou confundia com o FAQ de documentos (Resposta combinada PayJoy).

### Solução
- Novo cenário **Cliente pergunta sobre o método de análise para financiamento** em **Cenários Especiais** com **texto oficial completo** em 3 parágrafos (link vs loja + equipe na loja + fechamento Francivaldo Phones), sem omitir nenhuma linha.
- FAQ documentos/requisitos atualizado para **não** absorver perguntas de método de análise.
- Reforços em **Regras Específicas**, checklist JSON e **Exemplo 3j**.

### Arquivos afetados
- `Francivaldo Phones_v2.0.10.md` (criado a partir de v2.0.9)
- `Francivaldo Phones.md` (arquivo de trabalho atualizado)

### Validação
✅ Texto completo conforme modelo do cliente (3 parágrafos, sem omissão)
✅ Distinção método de análise vs FAQ documentos vs CTA pós-orçamento
✅ v2.0.9 preservado intacto

### Impacto
- **Padroniza:** Resposta quando o cliente pergunta como fazer a análise (link ou loja)
- **Melhora:** Cliente recebe orientação completa sobre as duas opções e suporte presencial
- **Previne:** Respostas parciais ou troca indevida pela Resposta combinada PayJoy

---

## Mudança #15 — Anti-repetição: não repetir perguntas já respondidas

**Data:** 03/07/2026
**Status:** ✅ EXECUTADO
**Versão:** v2.0.11
**Solicitante:** Cliente

### Problema identificado
Caso real (Maria / Redmi Note 13 / boleto): após a IA perguntar o valor da entrada, a cliente respondeu *"200"* e, no turno seguinte, a IA repetiu exatamente a mesma pergunta (*"Maria, qual valor você pretende dar de entrada?"*), interrompendo o fluxo.

### Solução
- Nova seção **Anti-repetição — validar histórico antes de perguntar** em **Regras de Comunicação** — checklist Passos 1–4 e regra de ler a mensagem mais recente do cliente antes de perguntar.
- **Passo 4** reforçado: se entrada **já informada**, pular pergunta, confirmar valor, requisitos **só se faltarem**, avançar para `ESTOQUE`/CTA ou **Passo 5**.
- Tabela **Passo 3** (ramo boleto), **Regras Específicas**, checklist JSON e **Exemplo 3f-b** (Maria / R$ 200) atualizados.

### Arquivos afetados
- `Francivaldo Phones_v2.0.11.md` (criado a partir de v2.0.10)
- `Francivaldo Phones.md` (arquivo de trabalho atualizado)

### Validação
✅ Resposta *"200"* após pergunta de entrada não dispara nova pergunta de entrada
✅ Caso real Maria documentado como ERRADO vs CERTO
✅ v2.0.10 preservado intacto

### Impacto
- **Corrige:** Repetição de pergunta de entrada (e demais passos de qualificação) quando o cliente já respondeu
- **Melhora:** Fluxo contínuo após informações fornecidas
- **Previne:** Atendimento repetitivo e experiência ruim no WhatsApp

---

## Mudança #16 — Saudação enxuta e pagamento personalizado por aparelho

**Data:** 03/07/2026
**Status:** ✅ EXECUTADO
**Versão:** v2.0.12
**Solicitante:** Cliente

### Problema identificado
Na saudação inicial, a IA enviava bloco extenso com marcas **e** todas as formas de pagamento (cartão, boleto, CLT), gerando impressão de que **todas** as condições se aplicam a **todas** as marcas — especialmente **iPhone** (que **não** entra no boleto bancário do aparelho).

### Solução
- **Passo 2 (pós-nome):** texto oficial **único** em 1 balão — *"Prazer, [NOME]! Qual modelo… Samsung, Motorola, Realme, Xiaomi e iPhone."* — **sem** condições de pagamento; aguardar resposta do cliente.
- **Primeira mensagem com nome:** até 4 balões (saudação + Maria + Passo 2) — **sem** parcelas/boleto/CLT.
- **Passo 3:** formas de pagamento **compatíveis** apresentadas **somente após** modelo/marca — Android lacrado (4 opções) vs **iPhone** (à vista, cartão, CLT — **sem boleto**).
- Exemplos **2**, **3**, **3b**, **3b-i** e checklist JSON atualizados.

### Arquivos afetados
- `Francivaldo Phones_v2.0.12.md` (criado a partir de v2.0.11)
- `Francivaldo Phones.md` (arquivo de trabalho atualizado)

### Validação
✅ Saudação não inclui formas de pagamento antes do modelo
✅ iPhone no Passo 3 sem oferta de boleto do aparelho
✅ v2.0.11 preservado intacto

### Impacto
- **Corrige:** Interpretação equivocada de que boleto vale para iPhone na abertura
- **Melhora:** Fluxo em etapas (nome → modelo → pagamento compatível)
- **Padroniza:** Abertura curta e condições personalizadas por produto

---

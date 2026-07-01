# Registro de Mudanças — TS STORE

> Arquivo de controle de versões do prompt da assistente virtual Ana (TS Store — Passo Fundo/RS).
> **Regra:** nunca modificar o arquivo de versão anterior. Cada mudança gera um novo arquivo versionado.

---

## Mudança #1 — Versão inicial do prompt

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.0
**Solicitante:** Cliente

### Problema identificado
Projeto novo **TS STORE** sem estrutura de versionamento no repositório M4IA. Necessidade de registrar o prompt original antes de aplicar ajustes solicitados pelo cliente.

### Solução
Criação da pasta do projeto com:
- `Prompt Original.md` — snapshot imutável do prompt recebido do cliente
- `TS STORE.md` — arquivo de trabalho (versão atual)
- `TS STORE_v1.0.0.md` — primeira versão versionada (padrão M4IA)

### Arquivos afetados
- `Prompt Original.md` (criado)
- `TS STORE.md` (criado)
- `TS STORE_v1.0.0.md` (criado a partir do prompt original)
- `CAMBIOS_PROMPT.md` (criado)

### Validação
✅ Prompt original preservado integralmente em `Prompt Original.md`
✅ Versão inicial v1.0.0 criada e registrada
✅ Estrutura alinhada ao padrão M4IA

### Impacto
- **Padroniza:** Controle de versões para o projeto TS STORE
- **Previne:** Perda do prompt base ao aplicar futuras modificações
- **Melhora:** Rastreabilidade de cada ajuste solicitado pelo cliente

---

## Mudança #2 — Não repetir pergunta de modelo após resposta inicial

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.1
**Solicitante:** Cliente

### Problema identificado
Após a apresentação inicial com pergunta combinada (*"Qual o seu nome e qual modelo você tem interesse?"*), a IA confirmava o nome com *"Show, [nome]!"* e **perguntava de novo** *"Qual modelo de iPhone você tem interesse?"*, mesmo quando o cliente já havia informado o modelo (ex.: "Esther" + "Tenho interesse no iPhone 17") ou múltiplos modelos (ex.: "16 ou 17" + "Quanto está").

### Solução
Reforço cirúrgico nas seções de interação inicial e qualificação:
- **APRESENTAÇÃO INICIAL OBRIGATÓRIA:** bloco **"NUNCA repetir pergunta de modelo ou nome já respondidos (LEITURA DE CONTEXTO)"** com fluxo pós-pergunta combinada, regra de múltiplos modelos e exemplos ❌/✅ dos casos reais (Esther/iPhone 17 e Milena/16 ou 17)
- **REGRAS DE COMUNICAÇÃO → Nome do cliente e confirmações:** regra explícita de que *"Show, [nome]!"* após nome+modelo **não** pode ser seguido de nova pergunta de modelo
- **IDENTIFICAÇÃO DO INTERESSE:** nova subseção **LEITURA DE CONTEXTO — ANTES DE QUALIFICAR** (tabela de ações); regras de qualificação ampliadas para múltiplos modelos e resposta à pergunta combinada
- **Fluxo de Qualificação:** passo 1 = leitura de contexto; passo MODELO só se não informado em nenhuma mensagem
- **Checklist antes de enviar:** item de verificação de contexto lido

### Arquivos afetados
- `TS STORE_v1.0.1.md` (criado a partir de v1.0.0)
- `TS STORE.md` (sincronizado com v1.0.1)
- `CAMBIOS_PROMPT.md` (Mudança #2)
- `.cursor/rules/prompt-versioning.mdc` (TS STORE → v1.0.1)

### Validação
✅ Regra explícita contra repetir modelo após resposta à pergunta combinada
✅ Múltiplos modelos ("16 ou 17") tratados como interesse definido
✅ Exemplos ❌/✅ alinhados aos screenshots do cliente
✅ Seções VBT, pagamento, tags e demais fluxos não alterados

### Impacto
- **Previne:** Cliente repetir informações já fornecidas (nome e/ou modelo)
- **Corrige:** Fluxo pós-apresentação inicial indo direto para `aparelhos_disponiveis` → `ESTOQUE` ou capacidade
- **Melhora:** Experiência de qualificação mais fluida no início da conversa

---

## Mudança #3 — Fluxo explícito quando cliente pergunta sobre boleto

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.2
**Solicitante:** Cliente

### Problema identificado
Quando o cliente perguntava especificamente se a loja trabalha com boleto, a IA podia **apenas recusar** e **encerrar** a interação — sem seguir com o orçamento (à vista + 12x + 18x), mesmo quando o modelo já estava definido no contexto da conversa.

### Solução
Nova subseção **`### Cliente pergunta sobre BOLETO`** em **FORMAS DE PAGAMENTO** (após mensagem padrão genérica):
- Gatilhos explícitos (aceita boleto?, trabalham com boleto?, etc.)
- Fluxo obrigatório: resposta curta "Não trabalhamos com boleto." + **continuar** com orçamento se modelo no contexto (`aparelhos_disponiveis` + `ESTOQUE` + `TAXAS_MAQ` + `Calculator`)
- Se só boleto sem modelo: recusar + informar PIX/dinheiro/cartão + perguntar modelo (sem repetir se já informado)
- Exemplos ❌/✅ e JSON de referência para os dois cenários (com e sem modelo)
- Proibição de parar só na recusa quando já houver contexto para orçar

### Arquivos afetados
- `TS STORE_v1.0.2.md` (criado a partir de v1.0.1)
- `TS STORE.md` (sincronizado com v1.0.2)
- `CAMBIOS_PROMPT.md` (Mudança #3)
- `.cursor/rules/prompt-versioning.mdc` (TS STORE → v1.0.2)

### Validação
✅ Regra explícita: recusar boleto **e** apresentar orçamento quando modelo definido
✅ Cenário sem modelo: redirecionar para PIX/cartão + perguntar modelo
✅ Exemplos ❌/✅ e JSON alinhados ao formato TS Store
✅ Seções VBT, apresentação inicial, tags e demais fluxos não alterados

### Impacto
- **Corrige:** IA parando após recusar boleto sem enviar valores
- **Melhora:** Conversão — cliente que pergunta forma de pagamento ainda recebe orçamento completo
- **Padroniza:** Fluxo específico para pergunta sobre boleto vs. mensagem genérica de pagamento

---

## Mudança #4 — Produto sob encomenda redireciona à venda (sem orçamento)

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.3
**Solicitante:** Cliente

### Problema identificado
Quando a Ana informava que um produto era **sob encomenda** (linha iPhone 17, iPad, MacBook, etc.), o fluxo **continuava** com orçamento (à vista + 12x + 18x), perguntas de capacidade/cor, script de três bolhas para "tem pronta entrega?" ou catálogo como substituto de atendente — em vez de **redirecionar à equipe de vendas**.

### Solução
Ajustes cirúrgicos nas seções de encomenda:
- **IDENTIFICAÇÃO DA LOJA → OUTROS PRODUTOS APPLE:** explicação curta + handoff imediato `departamento: venda`, `redirecionamento: true` — **proibido** ESTOQUE, orçamento e qualificação como substituto; catálogo opcional **antes** do handoff, nunca no lugar dele
- **LINHA IPHONE 17 — SEMPRE SOB ENCOMENDA:** substituído fluxo `aparelhos_disponiveis` → ESTOQUE → orçamento por explicação + handoff; exemplos ❌/✅
- **Pergunta "tem pronta entrega?" — produto sob encomenda:** substituído script de três bolhas + CTA por confirmação curta + handoff; exemplos ❌/✅
- **Mensagens separadas / Contextualização / Qualificação / VERIFICAÇÃO DE DISPONIBILIDADE:** exceção explícita para produtos sob encomenda (sem tools de orçamento)
- **ENTREGA → Produtos sob Encomenda** e **REDIRECIONAMENTOS:** tabela atualizada (`venda` + `true`); exemplo JSON iPhone 17 corrigido para handoff
- **HORÁRIO DE ATENDIMENTO:** mantido — fora do expediente ainda faz handoff com aviso de horário

### Arquivos afetados
- `TS STORE_v1.0.3.md` (criado a partir de v1.0.2)
- `TS STORE.md` (sincronizado com v1.0.3)
- `CAMBIOS_PROMPT.md` (Mudança #4)
- `.cursor/rules/prompt-versioning.mdc` (TS STORE → v1.0.3)

### Validação
✅ Sob encomenda → handoff venda, sem orçamento/opções
✅ "Tem pronta entrega?" em produto sob encomenda → handoff, não três bolhas + CTA
✅ Exemplos ❌/✅ nos casos iPhone 17, iPad e pronta entrega
✅ Boleto, VBT, pagamento e demais fluxos não alterados

### Impacto
- **Corrige:** IA cotando ou qualificando após dizer "sob encomenda"
- **Melhora:** Cliente de encomenda vai direto para humano que combina pedido
- **Padroniza:** Política única de handoff para linha 17 e demais Apple sob encomenda

---

## Mudança #5 — Encerramento natural quando cliente pausa ou encerra conversa

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.4
**Solicitante:** Cliente

### Problema identificado
Quando o cliente sinalizava pausa ou encerramento ("amanhã eu vejo certinho, obrigada", "vou dar uma olhada depois", "muito obrigado"), a IA continuava fazendo novas perguntas de qualificação, CTA de orçamento ou push de venda — mantendo a conversa ativa até tarde da noite em vez de encerrar naturalmente.

### Solução
Nova subseção **`### Encerramento ou pausa da conversa pelo cliente`** em **Respostas Contextuais Curtas**, com gatilhos, proibições, copy de referência (tom TS Store: "Tranquilo"/"Show", não "Perfeito") e exemplos ❌/✅ para o caso "amanhã eu vejo certinho, obrigada". Reforços cruzados em:
- **Concisão e Fluxo** — exceção à regra de CTA obrigatório
- **Respostas Contextuais Curtas** — bullet de espera/encerramento atualizado
- **RESERVA DE PRODUTO → CTAs permitidos** — referência à nova regra
- **Sistema de Perguntas de Call to Action → REGRA CRÍTICA** — exceção pausa/encerramento
- **Resposta a Agradecimentos Após Orçamento** — distinguir agradecimento com pausa vs. ainda em aberto
- **FINALIZAÇÃO SEM VENDA → Cliente Hesitante** — pausa = encerrar; hesitação em aberto = qualificar objeção
- **Checklist antes de enviar** — item de verificação pausa/encerramento

### Arquivos afetados
- `TS STORE_v1.0.4.md` (criado a partir de v1.0.3)
- `TS STORE.md` (sincronizado com v1.0.4)
- `CAMBIOS_PROMPT.md` (Mudança #5)
- `.cursor/rules/prompt-versioning.mdc` (TS STORE → v1.0.4)

### Validação
✅ Gatilhos explícitos: "amanhã vejo", "vou dar uma olhada", "depois te falo", agradecimento em despedida
✅ Proibido: nova pergunta, CTA com "?", handoff sem pedido de humano
✅ Obrigatório: 1–2 bolhas curtas, `departamento: ts_store`, `redirecionamento: false`
✅ Exemplo ❌/✅ JSON para "amanhã eu vejo certinho, obrigada"
✅ Seções encomenda, boleto, VBT, pagamento e demais fluxos não alterados

### Impacto
- **Previne:** IA insistindo com perguntas após sinal claro de pausa/encerramento
- **Corrige:** Conversas prolongadas à noite quando cliente já disse que retoma depois
- **Melhora:** Experiência de encerramento natural e respeitosa, alinhada ao tom TS Store

---

## Mudança #6 — Remoção do aviso predeterminado de fora do horário

**Data:** 17/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.5
**Solicitante:** Cliente

### Problema identificado
A IA enviava automaticamente o bloco de mensagem de fora do horário (*"Boa noite! No momento nossa equipe está fora do horário de atendimento…"*) em conversas de venda normais — por exemplo, quando o cliente apenas perguntava preço de iPhone 14/15 às 19h — em vez de continuar qualificação e orçamento.

### Solução
Na seção **HORÁRIO DE ATENDIMENTO DA EQUIPE**:
- Removida a subseção **Quando avisar horário + redirecionar ao grupo** e o template de resposta obrigatória (linhas 153–163 da v1.0.4)
- Nova subseção **Proibido — aviso predeterminado de fora do horário**: proibição explícita de enviar esse bloco em **qualquer** cenário
- Regra de supersessão: esta seção prevalece sobre outras instruções que mandem o aviso na `message`
- Handoffs fora do expediente passam a usar copy normal de **REDIRECIONAMENTOS** (*"em instantes"*, *"nossa equipe"*, etc.)

Em **REDIRECIONAMENTOS → Pré-requisito — fora do horário da equipe**:
- Removida a **Frase complementar obrigatória em handoff fora do horário**
- Linha `Fora do expediente` atualizada para proibir o bloco predeterminado

### Arquivos afetados
- `TS STORE_v1.0.5.md` (criado a partir de v1.0.4)

### Validação
✅ Template predeterminado de fora do horário removido
✅ Proibição explícita em qualquer cenário (preço, humano, handoff, garantia)
✅ Handoffs fora do expediente mantidos com copy normal e `redirecionamento: true`
✅ Demais fluxos (orçamento, VBT, encomenda, encerramento) não alterados

### Impacto
- **Previne:** Mensagem de fora do horário em perguntas de preço/modelo fora do expediente
- **Remove:** Bloco automático "Registrei seu contato e nossa equipe retorna…"
- **Mantém:** Ana atendendo 24h e handoffs normais ao grupo

---

## Mudança #7 — Horário de funcionamento somente quando o cliente perguntar

**Data:** 17/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.6
**Solicitante:** Cliente

### Problema identificado
Após remover o aviso automático de fora do horário (v1.0.5), era necessário garantir que a informação de horário de funcionamento da loja permaneça disponível quando o cliente perguntar — sem reintroduzir uma regra que interrompa o fluxo normal (orçamento, preço, qualificação).

### Solução
Subseção **Perguntas só sobre horário** substituída por **Quando o cliente perguntar sobre horário de funcionamento**, com:
- Gatilhos explícitos (*"Qual o horário?"*, *"Vocês estão abertos agora?"*, etc.)
- Texto de referência com horários Seg–Sex, Sábado e Domingo (mesmo conteúdo da v1.0.4)
- Regra: responder **somente** quando perguntado; `redirecionamento: false`, `departamento: ts_store`
- Exemplo ✅ JSON e ❌ de enviar horário sem pergunta
- Atualização em **INFORMAÇÕES DA EMPRESA** e tabela **REDIRECIONAMENTOS** (pergunta se loja está aberta → horários, sem bloco proibido)

### Arquivos afetados
- `TS STORE_v1.0.6.md` (criado a partir de v1.0.5)

### Validação
✅ Horários de funcionamento preservados no prompt
✅ Resposta obrigatória apenas quando cliente pergunta
✅ Proibido enviar horário em perguntas de preço/modelo sem gatilho
✅ Bloco automático de fora do horário continua proibido (v1.0.5)

### Impacto
- **Mantém:** Cliente que pergunta horário recebe informação completa da loja
- **Previne:** Horário interrompendo fluxo de venda sem pergunta do cliente
- **Melhora:** Distinção clara entre "perguntou horário" vs "só quer preço"

---

## Mudança #8 — Saúde de bateria dos seminovos atualizada para acima de 90%

**Data:** 01/07/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.7
**Solicitante:** Cliente

### Problema identificado
A IA informava aos clientes que os aparelhos seminovos possuem saúde de bateria acima de **80%**. Essa informação estava desatualizada: a política atual da loja é comercializar seminovos com saúde de bateria acima de **90%**.

### Solução
Dois pontos ajustados:
- **Diferenciais da TS Store:** adicionado bullet explícito — *"Seminovos com saúde de bateria acima de 90% — todos os aparelhos passam por revisão antes da venda"*
- **FAQ — Saúde da bateria dos seminovos:** nova subseção antes do bloco de garantia, com gatilhos, regra de resposta obrigatória (sempre acima de 90%), exemplo de frase ao cliente e proibição explícita de usar qualquer percentual diferente de 90%

### Arquivos afetados
- `TS STORE_v1.0.7.md` (criado a partir de v1.0.6)

### Validação
✅ Diferenciais atualizados com threshold correto de 90%
✅ Regra explícita de resposta ao cliente quando perguntado sobre bateria dos seminovos
✅ Proibição de informar percentual diferente de 90%
✅ Fluxos de VBT, pagamento, encomenda e demais seções não alterados

### Impacto
- **Corrige:** IA informando 80% de saúde de bateria para os seminovos vendidos pela loja
- **Padroniza:** Threshold único de 90% para comunicação com o cliente sobre bateria dos seminovos
- **Melhora:** Alinhamento entre a política real da loja e o que a IA informa ao cliente

---

## Mudança #9 — Mensagem de encerramento mais acolhedora e perguntas de qualificação para cliente hesitante

**Data:** 01/07/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.8
**Solicitante:** Cliente

### Problema identificado
A mensagem de encerramento usada quando o cliente informa que vai continuar depois era fria e perdia a oportunidade de manter o cliente engajado. Exemplo da copy anterior: *"Vamos deixar para continuar depois. Qualquer coisa, alguém da equipe entra em contato caso necessário."*

Além disso, o bloco de cliente hesitante (ainda em aberto) não tinha exemplos concretos de perguntas de qualificação para identificar objeções.

### Solução
Três ajustes aplicados na seção **Encerramento ou pausa da conversa pelo cliente** e em **FINALIZAÇÃO SEM VENDA → Cliente Hesitante**:

1. **Copy de referência atualizado** — novas frases acolhedoras com convite à visita na loja quando fizer sentido; regra explícita de quando incluir o convite (não forçar em todo encerramento)
2. **Exemplo `✅ CORRETO` atualizado** — JSON com nova copy em 2 bolhas: acolhimento + convite à visita
3. **Perguntas de qualificação adicionadas** em Cliente Hesitante (ainda em aberto): *"Ficou dentro do que você busca?"*, *"Tem algo que podemos ajustar?"*, *"O que te impede de fecharmos hoje?"*

### Arquivos afetados
- `TS STORE_v1.0.8.md` (criado a partir de v1.0.7)

### Validação
✅ Copy de encerramento atualizado para tom acolhedor com convite à visita
✅ Regra de quando incluir o convite (contexto apropriado, não forçado)
✅ Exemplo JSON `✅ CORRETO` atualizado com nova copy em 2 bolhas
✅ Perguntas de qualificação adicionadas para cliente hesitante em aberto
✅ Regras de proibição (sem CTA, sem "?" no final, sem handoff) mantidas
✅ Fluxos de VBT, pagamento, bateria e demais seções não alterados

### Impacto
- **Corrige:** Mensagem de encerramento fria e sem engajamento
- **Melhora:** Experiência de saída do cliente — tom acolhedor, convite à loja
- **Melhora:** Qualificação de objeções com perguntas direcionadas para clientes hesitantes em aberto

---

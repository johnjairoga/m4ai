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

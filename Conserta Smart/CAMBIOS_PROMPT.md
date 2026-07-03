# Registro de Mudanças — Conserta Smart

> Arquivo de controle de versões do prompt da IA Gizele (Conserta Smart & Eletro — Unidade Ceilândia).
> **Regra:** nunca modificar o arquivo de versão anterior. Cada mudança gera um novo arquivo versionado.

---

## Mudança #1 - Versão inicial do prompt

**Data:** 08/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.0
**Solicitante:** Cliente

### Descrição
Criação do prompt inicial da atendente virtual Gizele para a Conserta Smart & Eletro — Unidade Ceilândia.

### Funcionalidades implementadas
- Persona: Gizele, estagiária da Conserta Smart & Eletro, Unidade Ceilândia
- Regras de segurança e anti-injeção de prompt
- Fluxo de apresentação (Cenário A e Cenário B)
- Triagem de modelo e defeito do aparelho
- Integração com tool MANUT para consulta de preços
- Fluxo de orçamento com múltiplas opções de peça (VIVID, Gold Prime, OLED)
- Taxa de análise técnica R$100 para problemas graves (não liga, molhado, placa)
- Protocolo de produto sem estoque (sinal de 50%)
- Brinde de película para troca de tela
- Formulário de ordem de serviço (6 campos, sem CPF)
- Fechamento com resumo para equipe
- Parcelamento em até 18x (4x sem juros)
- Desconto de até 10% no PIX/espécie (carta reservada para objeção)
- Tratamento de objeções de preço (3 etapas) e indecisão
- Redirecionamentos: especialista técnico, financeiro, setor responsável, gerente, acessórios, vendas
- Suporte a peças Apple IRP (originais, 10-15 dias úteis)
- Regras de peças originais Samsung/Motorola/Xiaomi
- Horários dinâmicos injetados (open/closed em tempo real)
- Escopo: somente smartphones (sem notebooks, tablets, TVs, etc.)
- Formato de saída JSON com array de strings (`message[]`)

### Arquivos criados
- `Conserta Smart_v1.0.0.md` — prompt inicial completo

---

## Mudança #2 - Fluxo mais suave + endereço atualizado + localização

**Data:** 08/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.1
**Solicitante:** Cliente

### Etapa 1 — Fluxo de OS menos agressivo

**Problema:** A IA estava forçando a abertura de OS imediatamente após o cliente confirmar interesse, sem antes convidá-lo a visitar a loja.

**Solução:** Adicionado novo **passo 4.5** no fluxo de atendimento e nova **seção 6.11**. Após confirmação de interesse, a IA agora:
1. Convida o cliente a visitar a loja
2. Informa horários de funcionamento + endereço + link do Maps
3. Oferece o pré-registro (OS) como opção opcional — sem pressão

**Regras da nova seção 6.11:**
- NUNCA enviar formulário de OS antes de convidar o cliente à loja
- Pré-registro é opcional — NÃO forçar
- Sempre incluir horários + endereço + link no momento do convite

### Etapa 2 — Endereço atualizado

**Endereço anterior:** `QNM 17 Conjunto A, 49, loja 2 — Ceilândia/DF`
**Endereço novo:** `St. M QNM 17 Ceilândia Sul, N° 49, loja 02 — Ceilândia, Brasília - DF, 72215-171`

Horários confirmados iguais ao Google Maps — sem alteração necessária.

### Etapa 3 — Link Google Maps adicionado

**Link:** https://maps.app.goo.gl/kYqeiMRaffKKNa7p8

Adicionado em todos os locais onde o endereço é enviado ao cliente:
- Seção 3.1 (definição da loja)
- Seção 6.5 (convite presencial quando cliente recusa sinal)
- Seção 6.11 (novo convite à loja)
- Seção 9.6 PASSO 2 (fechamento da OS)

### Arquivos afetados
- `Conserta Smart_v1.0.1.md` (criado a partir de v1.0.0)

---

## Mudança #3 - Nova saudação inicial (3 balões)

**Data:** 08/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.2
**Solicitante:** Cliente

### Descrição
Atualização do texto e estrutura dos balões de apresentação da Gizele. A saudação foi reestruturada de **2 balões** para **3 balões** e o texto foi reformulado conforme solicitação do cliente.

### Texto anterior (2 balões)
- Balão 1: `"Olá! 👋"`
- Balão 2: `"Seja bem-vindo(a) à Conserta Smart, a maior rede de assistência técnica especializada em smartphones, tablets e Eletro do Brasil.\nSou a Gizele, da equipe Conserta Smart Ceilândia. 😊"`

### Texto novo (3 balões)
- Balão 1: `"Olá!"`
- Balão 2: `"Seja bem-vindo à Conserta Smart Ceilândia, a maior rede de assistência especializada em smartphone, tablets e eletro do Brasil."`
- Balão 3: `"Sou a Gizele, vou continuar seu atendimento por aqui 😊"`

### Regra reforçada
A saudação é **sempre obrigatória**, mesmo que o cliente vá direto ao ponto (Cenário B). Os 3 balões de apresentação sempre são enviados antes de qualquer resposta ao pedido do cliente.

### Arquivos afetados
- Seção 1.2 (Cenário A e Cenário B) — definição dos formatos
- Seção 12.3 (contagens de balões) — atualizado para refletir nova estrutura
- Seção 12.4 (estrutura obrigatória Cenário B) — atualizado
- Seção 12.5 (4 exemplos JSON) — todos atualizados com os 3 novos balões
- `Conserta Smart_v1.0.2.md` (criado a partir de v1.0.1)

---

## Mudança #4 - Avaliação presencial antes de redirecionar + orçamento preliminar (15Mai - 01)

**Data:** 10/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.3
**Solicitante:** Cliente (15Mai - 01)

### Problema identificado
Quando o cliente reportava defeitos de **causa incerta ou intermitente** (ex.: ghost touch no S23 Ultra), a IA redirecionava imediatamente ao especialista técnico com a frase canônica — **sem** citar os principais motivos do problema e **sem** direcionar o cliente à loja para avaliação presencial.

**Caso real (screenshot):** Cliente informou *"Tenho um S23 Ultra e ele está apresentando ghost touch"* → Gizele respondeu só com redirecionamento ao especialista técnico (com aviso de loja fechada).

### Solução

#### 1. Nova seção **6.3.5 — Problemas com causa incerta — avaliação presencial**

Fluxo obrigatório **antes** de redirecionar ao especialista:

**Etapa 1 (sempre):**
1. Reação curta + **2–4 principais motivos** do defeito (adaptar ao caso)
2. Direcionar à **avaliação presencial na loja**
3. Convite com horários + endereço + link Maps
4. `redirecionamento`: `false`

**Etapa 2 — só se cliente INSISTE em orçamento preliminar:**
- **Atualização de software:** média de **R$ 80,00**
- **Troca de tela:** consultar MANUT (`"Tela [Marca Modelo]"`) e apresentar orçamento da base (seção 6.6)
- Reforço: valor exato depende da avaliação presencial

**Etapa 3 — redirecionamento especialista técnico:** último recurso (MANUT falhou após insistência, ou cliente pede técnico)

#### 2. Motivos citados para ghost touch
- Defeito no módulo touch da tela
- Problema de software ou calibração
- Umidade ou sujeira na tela
- Pressão interna (bateria inchada empurrando o display)

#### 3. Seções alinhadas

| Seção | Mudança |
|---|---|
| Validação MANUT (topo) | Não redirecionar imediato — verificar 6.3.5 |
| Cenário B (modelo + defeito) | Bifurcação: óbvio orçável vs intermitente/incerto |
| Protocolo MANUT (6.2) | 6.3.5 antes de redirecionar em defeitos incertos |
| 6.4 Validação MANUT | Incompatível + causa incerta → 6.3.5 |
| 11.1 Tabela frases canônicas | Especialista só após 6.3.5 quando aplicável |
| 11.2 Especialista técnico | Proibição explícita de redirecionar como primeira resposta |
| 3.3 Serviços | Atualização de software (média R$ 80,00) |
| 12.5 Exemplos | Novo exemplo JSON — S23 Ultra ghost touch |

### Arquivos afetados
- `Conserta Smart_v1.0.3.md` (criado a partir de v1.0.2)

### Validação
✅ Seção 6.3.5 com fluxo em 3 etapas (causas → loja → orçamento preliminar se insistir)
✅ Ghost touch com motivos específicos e exemplo S23 Ultra
✅ Software: R$ 80,00 média documentada no prompt
✅ Troca de tela: MANUT obrigatório quando cliente insiste em preço
✅ Redirecionamento especialista como último recurso, não primeira ação
✅ Exemplo JSON na seção 12.5 alinhado ao caso real do screenshot
✅ Tudo em português do Brasil

### Impacto
- **Previne:** Handoff prematuro ao especialista técnico em defeitos diagnósticos
- **Melhora:** Cliente entende causas possíveis e é convidado à loja com endereço/horários
- **Mantém:** Orçamento preliminar (software R$ 80 + tela via MANUT) quando cliente insiste em valor antes de ir à loja

---

## Mudança #5 - Saudação obrigatória mesmo com lead direto ao ponto

**Data:** 10/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.4
**Solicitante:** Cliente

### Problema identificado
Quando o lead já ia **direto ao ponto** na primeira mensagem (produto, serviço, peça ou disponibilidade), a IA **pulava a saudação** e respondia imediatamente com triagem ou redirecionamento ao especialista técnico.

**Caso real (screenshot):** Cliente: *"Você tem bateria para edge 60"* → Gizele respondeu direto com validação de versão + redirecionamento ao especialista, **sem** os 3 balões de apresentação.

### Solução

#### 1. Novo bloco **SAUDAÇÃO OBRIGATÓRIA MESMO COM LEAD DIRETO AO PONTO** (seção 1.2)

Mesmo com pergunta direta sobre produto/serviço/peça, a **primeira resposta** deve **sempre** incluir os 3 balões de saudação na mesma rodada, antes de triagem, MANUT ou redirecionamento.

**Texto fixo atualizado (sugestão do cliente):**
```
Olá!
Seja bem-vindo à Conserta Smart Ceilândia, a maior rede de assistência especializada em smartphone, tablets e eletro do Brasil.
Sou a Gizele, eu vou continuar seu atendimento.
```

#### 2. Proibições explícitas na primeira interação
- Iniciar com triagem sem saudação
- Iniciar com redirecionamento ao especialista sem saudação
- Pular apresentação porque o cliente já pediu algo específico

#### 3. Detecção ampliada
Perguntas de disponibilidade (*"você tem bateria"*, *"tem peça"*, *"tem para Edge 60"*) → **Cenário B** com saudação obrigatória.

#### 4. Exemplo JSON — bateria Edge 60 (seção 12.5)
Saudação + pergunta de variante na mesma resposta; após cliente informar Fusion → MANUT, não redirecionar imediato.

### Texto anterior do balão 3
`"Sou a Gizele, vou continuar seu atendimento por aqui 😊"`

### Texto novo
`"Sou a Gizele, eu vou continuar seu atendimento."`

### Arquivos afetados
- `Conserta Smart_v1.0.4.md` (criado a partir de v1.0.3)
- Seções 1.2, 12.4, 12.5 e todos os exemplos JSON

### Validação
✅ 3 balões de saudação obrigatórios na primeira interação — inclusive lead direto
✅ Texto fixo conforme sugestão do cliente
✅ Proibições explícitas documentadas
✅ Exemplo Edge 60 bateria alinhado ao screenshot
✅ Erro grave declarado: pular saudação na primeira interação

### Impacto
- **Padroniza:** Experiência de boas-vindas em 100% dos primeiros contatos
- **Previne:** Resposta robótica que começa com triagem ou handoff sem apresentação
- **Mantém:** Resposta ao pedido na mesma rodada (após os 3 balões)

---

## Mudança #6 — Tratamento de indecisão por valor com encaminhamento ao gerente

**Data:** 03/07/2025
**Status:** ✅ EXECUTADO
**Versão:** v1.0.5
**Solicitante:** Cliente

### Problema identificado
Quando o cliente dizia "vai pensar" e o motivo identificado era o valor do produto, a IA seguia o fluxo genérico de indecisão (PASSO 2 — riscos de postergar), sem aproveitar a oportunidade de buscar uma condição melhor. Não havia tratamento específico para objeção de valor dentro do fluxo de indecisão.

### Solução
Adicionado **PASSO 1.5** na seção **10.3 (Tratamento de indecisão)**. Quando o cliente confirmar que a indecisão é por causa do valor, a IA **não** segue para o PASSO 2 — em vez disso, envia a seguinte mensagem e encaminha para o gerente:

> "Entendo perfeitamente! Como o valor foi o ponto que te deixou em dúvida, vou conversar com o gerente para verificar se conseguimos alguma condição melhor para você. Já vou encaminhar seu atendimento para que possamos te dar um retorno o quanto antes."

→ Redirect: `gerenteResponsavel`

O PASSO 2 (riscos de postergar por componente) passa a se aplicar apenas quando o motivo **não** for o valor.

A tabela da seção **11.1** foi atualizada para documentar que `gerenteResponsavel` também é acionado neste cenário de indecisão por valor, com a frase específica da seção 10.3 (diferente da frase canônica usada para oferta de concorrente).

### Arquivos afetados
- `Conserta Smart_v1.0.5.md` (criado a partir de v1.0.4)

### Validação
✅ PASSO 1.5 inserido entre PASSO 1 e PASSO 2 na seção 10.3
✅ Frase exata conforme sugestão do cliente
✅ PASSO 2 restrito a motivos que não sejam valor
✅ Tabela 11.1 atualizada com os dois triggers do `gerenteResponsavel`
✅ Nenhum bloco protegido (tags, tools, QUEBRA) foi alterado

### Impacto
- **Melhora:** Conversão em situações de indecisão por preço — cliente recebe atenção imediata do gerente em vez de argumento genérico sobre riscos de postergar
- **Previne:** Perda de lead por falta de negociação quando o valor é o ponto decisivo
- **Padroniza:** Encaminhamento ao gerente como resposta padrão para objeção de valor na fase de indecisão

---

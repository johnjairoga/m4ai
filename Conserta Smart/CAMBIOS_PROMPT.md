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

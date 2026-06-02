# Registro de Mudanças no Prompt - AcheiMeuApple

## Mudança #1 - Correção de Seção "Manejo de Receios sobre Seminovos"

**Data:** 29/05/2026 - 14:35  
**Status:** ✅ EXECUTADO  
**Versão:** v1.1.0  
**Solicitante:** Cliente

### Descrição
Atualizar seção "Manejo de Receios sobre Seminovos" para incluir duas respostas predeterminadas:
1. Resposta OBRIGATÓRIA com pontos-chave de procedência
2. Resposta solicitada pelo cliente como comportamento da IA (abordagem mais humanizada)

### Linhas Afetadas
Linhas 908-933 em `achei meu Apple.md`

### Validação
✅ Primeira resposta cumpre regra OBRIGATÓRIA com 5 pontos-chave  
✅ Segunda resposta mantém humanidade e empatia conforme solicitado  
✅ Ambas em português do Brasil  
✅ Formato correto para WhatsApp

### Respostas Predeterminadas

#### **Resposta 1 - OBRIGATÓRIA (Procedência e Confiança)**
```
Nossos iphones vêm direto de fornecedor, não de troca.

Aqui você tem a total segurança que está adquirindo um produto todo revisado, testado, impecável, com garantia e acessórios.

Hoje 90% de nossas vendas são de iPhones seminovos justamente pela procedência e qualidade que entregamos.

Caso for nos pesquisar no Google vai ver que já passamos quase 900 clientes que nos avaliaram 5 ⭐⭐⭐⭐⭐ no Google.

Isso já diz muita coisa né!
```

#### **Resposta 2 - Humanizada (Comportamento da IA solicitado)**
```
Super entendo você optar pelo NOVO, e ter o receio de adquirir um seminovo, até porque é um investimento que você está fazendo.

Mas aqui em nossa loja esse medo não existe, temos seminovos de alto padrão, com procedência 100% garantida.

Aqui você adquire o melhor produto, se optar pelo seminovo, eu garanto para você a qualidade e procedência, pode confiar em nosso trabalho
```

### Critério de Uso
- **Resposta 1:** Quando cliente questiona diretamente sobre origem/procedência/confiança
- **Resposta 2:** Para reforçar humanidade e empatia após primeira resposta, ou como alternativa mais pessoal

---

## Mudança #2 - Correção Crítica: Ordem de Apresentação de Formas de Pagamento

**Data:** 30/05/2026  
**Status:** ✅ EXECUTADO  
**Versão:** v1.1.1  
**Solicitante:** Cliente / Análise de AI Agent

### Problema Identificado
A IA estava enviando o bloco `[FORMAS_PAGAMENTO]` ANTES de apresentar a lista de telefones/modelos disponíveis quando o cliente perguntava sobre formas de pagamento após mencionar interesse em um modelo específico.

**Exemplo do erro:**
```
Cliente: "Eu to interessada no iphone 15 moça"
Cliente: "Que forma de pagamentos vocês têm"
IA ERRADA: [Envia FORMAS_PAGAMENTO sem antes mostrar os modelos 15 disponíveis]
```

### Causa Raiz
Falta de clareza no prompt sobre quando usar a resposta avulsa `[FORMAS_PAGAMENTO]` vs. quando incluir formas dentro do `[PRIMEIRO_ORÇAMENTO]`

### Descrição da Mudança
Implementar regra crítica que diferencia dois cenários completamente diferentes:

**Cenário 1 - Cliente especificou modelo:**
- Consulte ESTOQUE → Apresente ORÇAMENTO COMPLETO (com formas de pagamento DENTRO)
- NÃO use `[FORMAS_PAGAMENTO]` como resposta avulsa

**Cenário 2 - Cliente ainda não especificou modelo:**
- PRIMEIRO: Pergunte qual modelo de interesse e apresente LISTA DE TELEFONES disponíveis
- DEPOIS: Envie `[FORMAS_PAGAMENTO]` como resposta avulsa
- ⚠️ NUNCA envie formas antes de mostrar lista de modelos

### Linhas Afetadas
- **Linha ~354:** Ampliar instrução sobre ordem de prioridade (REGRA CRÍTICA - ORDEM DE PRIORIDADE)
- **Linha ~1093:** Inserir nova seção "🚨 REGRA CRÍTICA - Quando Enviar FORMAS DE PAGAMENTO" 
- **Linha ~1122:** Melhorar encabezado de "Todas as Formas de Pagamento" com esclarecimentos

### Mudanças Específicas

#### 1. Expansão de linha 354 - REGRA CRÍTICA - ORDEM DE PRIORIDADE
```
Adicionado:
- Diferenciação clara entre CASO A (cliente especificou modelo) e CASO B (cliente NÃO especificou)
- Exemplo visual do erro a evitar
- Instruções precisas para cada caso
```

#### 2. Nova Seção - 🚨 REGRA CRÍTICA - Quando Enviar FORMAS DE PAGAMENTO
```
Inserida antes de "Todas as Formas de Pagamento":
- Cenário 1: Cliente especificou modelo
  * Ação correta: ORÇAMENTO completo com formas dentro
  * Ação incorreta: [FORMAS_PAGAMENTO] como resposta avulsa
  
- Cenário 2: Cliente NÃO especificou modelo
  * Ação correta: LISTA DE TELEFONES → DEPOIS [FORMAS_PAGAMENTO]
  * Ação incorreta: Enviar [FORMAS_PAGAMENTO] antes da lista de modelos
```

#### 3. Melhoria de Encabezado - Todas as Formas de Pagamento
```
Mudança de: "## Todas as Formas de Pagamento (Quando o cliente perguntar)"
Para: "## Todas as Formas de Pagamento - RESPOSTA AVULSA (Cenário 2)"

Adicionado:
- ⚠️ Aviso explícito de que é SOMENTE para Cenário 2
- Esclarecimento de que se já especificou modelo, use ORÇAMENTO
- Reiteração de NÃO usar [FORMAS_PAGAMENTO] como resposta separada
```

### Validação
✅ Regra claramente diferencia os dois cenários  
✅ Exemplos visuais de erro e correção  
✅ Tudo em português do Brasil  
✅ Integração com fluxo existente de ORÇAMENTO  
✅ Previne repetição do erro com instruções explícitas  

### Impacto
- **Previne:** Envio prematuro de formas de pagamento antes de mostrar lista de modelos
- **Melhora:** Clareza sobre o fluxo obrigatório: SEMPRE lista de telefones PRIMEIRO, formas depois
- **Alinha:** Com fluxo obrigatório: PASSO 1 (modelo) → PASSO 2 (análise) → PASSO 3 (valor) → PASSO 4 (orçamento com formas)
- **Garante:** Em ambos cenários, cliente VÊ modelos disponíveis antes de decisão de pagamento

### Notas de Implementação
- Mudanças são retrocompatíveis (não afetam comportamento quando seguindo corretamente)
- Clareza beneficia tanto à IA quanto a futuras auditorias
- Estrutura paralela facilita memorização: "Caso A ou Caso B"

---

## Mudança #3 - Regra Crítica: NÃO Pedir Vídeo Novamente

**Data:** 30/05/2026  
**Status:** ✅ EXECUTADO  
**Versão:** v1.1.2  
**Solicitante:** Cliente (feedback de atendimento)

### Problema Identificado
A IA estava pedindo vídeo do aparelho NOVAMENTE mesmo após o cliente JÁ TER ENVIADO um vídeo na conversa. Isso causa frustração do cliente e pareça robótico/desatento.

**Exemplo do erro:**
```
Cliente: [Envia vídeo do iPhone 15 para análise]
IA ERRADA: "Quer que eu te mande um vídeo desse aparelho?"
```

### Causa Raiz
Falta de verificação de histórico - a IA não analisa se `[IMAGEM_RECEBIDA]` já aparece nas mensagens anteriores antes de perguntar sobre vídeo

### Descrição da Mudança
Expandir regra existente de CTA - Oferecer Vídeo do Aparelho com checklist claro:
1. Pergunte sobre vídeo **UMA VEZ** após orçamento
2. **NUNCA repita** se cliente já enviou (bloco `[IMAGEM_RECEBIDA]` no histórico)
3. **NUNCA repita** se cliente já respondeu ("não precisa", "já vi", ignorou)
4. Continue com próximos passos do fluxo

### Linhas Afetadas
- **Linha ~926-929:** Seção "IMPORTANTE" - expandida com REGRA CRÍTICA explícita
- Adicionado: Exemplos visuais de erro vs. correto

### Mudanças Específicas

#### Expansão de linha 926 - Seção IMPORTANTE (CTA)
```
Adicionado:
- Checklist claro: "Pergunte UMA VEZ"
- ⛔ Dois cenários PROIBIDOS de repetição:
  * Cliente já enviou vídeo ([IMAGEM_RECEBIDA] no histórico)
  * Cliente já respondeu à pergunta
- Exemplo visual do erro
- Instrução de continuar com próximos passos
```

### Validação
✅ Regra é clara e explícita  
✅ Tem exemplos visuais de erro vs. correto  
✅ Vinculada à regra existente de linha 122 sobre [IMAGEM_RECEBIDA]  
✅ Tudo em português do Brasil  
✅ Previne repetição robótica  

### Impacto
- **Previne:** IA pedindo vídeo após cliente já ter enviado
- **Melhora:** Experiência do cliente - IA parece mais atenta e humanizada
- **Alinha:** Com princípio de não repetir informações já passadas
- **Garante:** Fluxo continua naturalmente após resposta do cliente

### Notas de Implementação
- Regra está integrada na seção existente de CTA
- Referencia a regra de [IMAGEM_RECEBIDA] da linha 122
- Simples de verificar: revisar histórico antes de fazer CTA sobre vídeo

---

## Mudança #4 - Quebra de Objeção: Cliente vai pesquisar em outra loja

**Data:** 02/06/2026  
**Status:** ✅ EXECUTADO  
**Versão:** v1.1.3  
**Solicitante:** Cliente (27Abr - 02)

### Problema Identificado
Quando o cliente diz que vai pesquisar em outra loja, a IA não tinha fluxo específico — só existia o tratamento de **concorrência** ("achei mais barato" + print + gerente), que é outro momento do funil.

O cliente questionou se deveria usar argumento e se é interessante **perguntar o que está faltando para fechar**.

### Estratégia adotada (referência: atendimento humano Juliano)
1. Validar sem pressionar ("Combinado!")
2. Liberar para pesquisar
3. **Argumento educativo:** orientar a comparar mesmo modelo, condição (lacrado/seminovo) e forma de pagamento
4. **Pergunta única** sobre o que falta para fechar (abre objeção real)

**Diferença do fluxo de concorrência:** neste cenário **não** pedir print nem gerente — o cliente ainda vai sair para pesquisar.

### Linhas Afetadas
- **Seção Persuasão:** nova `## Quebra de Objeção — Cliente vai pesquisar em outra loja`
- **Persuasão (bullet):** referência cruzada ao novo fluxo

### Respostas modelo (adaptar modelo/capacidade/condição reais)

```
Combinado, [nome]!
Fica bem à vontade pra pesquisar 😊
Só cuida pra comparar o mesmo modelo (iPhone 16 128GB lacrado) e a forma de pagamento, porque isso muda bastante.
O que ficou faltando pra gente fechar? Posso te ajudar em alguma coisa?
```

### Validação
✅ Fluxo separado do de concorrência (print/gerente)  
✅ Argumento de comparação justa (modelo + condição + pagamento)  
✅ Pergunta única sobre o que falta para fechar  
✅ Exemplo real do WhatsApp documentado  
✅ Tudo em português do Brasil  

### Impacto
- **Previne:** IA sem resposta ou usando fluxo errado (gerente/print) quando cliente só vai pesquisar
- **Melhora:** Tom consultivo — ajuda o cliente a comparar corretamente e revela objeção oculta
- **Alinha:** Com atendimento humano da loja (print de referência 27/04)

---

## Mudança #5 - Qualificação de Modalidade de Pagamento com Linguagem de Proposta Exclusiva

**Data:** 02/06/2026  
**Status:** ✅ EXECUTADO  
**Versão:** v1.1.4  
**Solicitante:** Cliente

### Problema Identificado
A abordagem de perguntar modelo + capacidade + forma de pagamento **já apresentava bons resultados**, mas não estava padronizada nem reforçada no prompt. A IA apresentava o orçamento completo sem antes confirmar a modalidade de pagamento (à vista ou parcelado), perdendo uma oportunidade de gerar comprometimento e sensação de proposta personalizada.

### Estratégia Adotada
Inserir um novo passo de qualificação (**PASSO 3.5**) no fluxo obrigatório: após confirmar modelo e capacidade, e **antes** de consultar ESTOQUE e montar o orçamento, a IA pergunta a modalidade de pagamento usando linguagem que transmite proposta exclusiva e especial.

**Frase modelo do cliente:**
> "Me confirma então de que forma você tem interesse: à vista ou parcelado? Assim eu já monto uma proposta super especial e exclusiva para você."

### Linhas Afetadas
- **Linha ~347:** Inserção do novo `PASSO 3.5` (entre PASSO 3 e PASSO 4 do fluxo de atendimento)
- **Linhas ~370-372 (CASO A):** Atualização da REGRA CRÍTICA de ORDEM DE PRIORIDADE
- **Linhas ~382-391 (EXEMPLO):** Atualização do exemplo de fluxo correto
- **Linhas ~444-452 (Outras informações):** Nova regra `🚨 FORMATO DA PERGUNTA DE MODALIDADE DE PAGAMENTO`
- **Linha ~1626 (VBT checklist):** Inserção do passo 2.5 na checklist de qualificação VBT

### Mudanças Específicas

#### 1. Novo PASSO 3.5 — Confirmar Modalidade Antes do Orçamento
```
Inserido entre PASSO 3 e PASSO 4:
- Se cliente já informou modalidade → pula para PASSO 4 direto
- Se modalidade ainda não está clara → PERGUNTAR antes de consultar ESTOQUE
- AGUARDAR resposta antes de calcular qualquer valor
```

#### 2. Atualização do CASO A — REGRA CRÍTICA ORDEM DE PRIORIDADE
```
Mudança de: "PRIMEIRO: Consulte ESTOQUE → DEPOIS: pergunte forma de pagamento"
Para: "PRIMEIRO (PASSO 3.5): confirmar à vista/parcelado → SEGUNDO (PASSO 4): consultar ESTOQUE e apresentar orçamento"
```

#### 3. Exemplo do Fluxo Correto Atualizado
```
Antes mostrava: Cliente diz modelo → IA consulta estoque → IA apresenta orçamento
Agora mostra:   Cliente diz modelo + GB → IA pergunta à vista/parcelado → Cliente responde → IA consulta estoque → IA apresenta orçamento
```

#### 4. Nova Regra de Formato (Outras informações)
```
🚨 FORMATO DA PERGUNTA DE MODALIDADE DE PAGAMENTO (qualificação antes do orçamento)
- Quando usar: modelo + capacidade já confirmados, modalidade ainda não
- NUNCA listar todas as formas de pagamento nesta etapa (só qualificação rápida)
- 4 variações obrigatórias para rotação (evitar robótico)
```

#### 5. VBT Checklist — Passo 2.5
```
Inserido entre passo 2 (capacidade) e passo 3 (calcular):
2.5: Confirmou modalidade de pagamento? Se não → perguntar com proposta exclusiva → PARE até resposta
```

### Variações da Frase (para rotação natural)
- "Me confirma então de que forma você tem interesse: à vista ou parcelado? Assim eu já monto uma proposta super especial e exclusiva para você."
- "Só me confirma: você prefere à vista ou parcelado? Assim eu já preparo uma proposta certinha e exclusiva pra você 😊"
- "Me fala como você prefere: à vista ou parcelado? Assim já monto uma proposta especial para você."
- "De que forma você prefere pagar: à vista ou parcelado? Assim eu já monto uma proposta super especial pra você!"

### Validação
✅ PASSO 3.5 inserido no fluxo obrigatório (entre PASSO 3 e PASSO 4)  
✅ Regra de pular o passo se modalidade já foi informada  
✅ CASO A da REGRA CRÍTICA atualizado para refletir nova ordem  
✅ Exemplo de fluxo correto atualizado e consistente com nova regra  
✅ Regra de formato com 4 variações para evitar resposta robótica  
✅ Checklist VBT atualizado com passo 2.5  
✅ Tudo em português do Brasil  
✅ Não conflita com regra de FORMAS_PAGAMENTO (essa distinção está clara)  

### Impacto
- **Melhora:** Coleta de informações — a IA sabe à vista/parcelado antes de montar o orçamento
- **Aumenta:** Conversão — linguagem de "proposta especial e exclusiva" gera comprometimento e valor percebido
- **Padroniza:** Abordagem que já estava gerando bons resultados no atendimento humano
- **Alinha:** Fluxo VBT também passa a incluir qualificação de modalidade antes do cálculo

---

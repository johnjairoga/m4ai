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

## Mudança #6 - Promoções Redirect + VBT Múltiplos Modelos

**Data:** 05/06/2026  
**Status:** ✅ EXECUTADO  
**Versão:** v1.1.5  
**Solicitante:** Cliente (sincronização de ajustes feitos por colega)

### Descrição
Três alterações sincronizadas da versão do colega para a versão do sistema:

1. Seção "Referências a Stories/Posts do Instagram" substituída por nova seção "Promoções / Ofertas - Redirecionamento Obrigatório"
2. Seção "Modelo de interesse (VBT)" atualizada para suportar múltiplos modelos na comparação
3. Regra "Apresente apenas 1 aparelho em VBT" substituída pela nova seção "Múltiplos modelos na troca (comparação)"

### Detalhes das Mudanças

#### 1. Promoções — Redirecionamento Obrigatório (substitui seção Instagram)
```
ANTES: Seção focada em Instagram (stories, posts, reels) — pedia print ao cliente
AGORA: Qualquer menção a promoção/oferta/desconto → redirecionar com frase exata:
"Que ótimo que você se interessou pela nossa promoção! 😊 Vou te transferir para um de nossos
atendentes que vai poder te passar todos os detalhes dessa promoção."

Regras adicionais:
- NÃO pedir print
- NÃO tentar adivinhar a promoção
- NÃO explicar condições
- NÃO alterar o texto da frase (detecção de keyword depende das palavras exatas)
- Enviar em única mensagem, sem asteriscos
```

#### 2. Modelo de interesse VBT — Suporte a múltiplos modelos
```
ADICIONADO novo bullet na seção "Modelo de interesse (antes de calcular — OBRIGATÓRIO)":
"Se o cliente citar mais de um modelo para comparar (ex.: '16 ou 17', 'me passa os dois'):
 isso é permitido — siga o fluxo de múltiplos orçamentos VBT. Não force a escolha de um só."

ATUALIZADO bullet "capacidade genérica":
ANTES: "abre exceção à regra de apresentar apenas 1 aparelho em VBT"
AGORA: "um bloco de orçamento VBT por capacidade (respeitando o limite de 3 por resposta)"
```

#### 3. Nova seção — Múltiplos modelos na troca (comparação)
```
ANTES: "⚠️ Apresente apenas 1 aparelho desejado em VBT. Se em dúvida entre modelos, peça que defina UM."
AGORA: Seção completa "Múltiplos modelos na troca (comparação)":
- Quando cliente pedir comparação (ex.: "me passa os dois", "16 ou 17"): NÃO recuse — calcule e apresente 1 orçamento VBT por modelo
- Fluxo: analise_vbt uma única vez → para cada modelo repita PASSOSs 3-5 → 1 bloco [ORÇAMENTO] por modelo
- Limite: máximo 3 modelos por resposta
- Se cliente não pediu comparação: pode perguntar qual prefere; se pediu explicitamente: apresente todos (até 3)
```

### Arquivos Afetados
- `achei meu Apple_v1.1.5.md` (criado — não modifica `achei meu Apple.md`)

### Validação
✅ Seção Instagram removida e substituída pela seção de Promoções com frase obrigatória exata  
✅ Frase de redirecionamento sem asteriscos, enviada em mensagem única  
✅ Novo bullet de múltiplos modelos adicionado na seção "Modelo de interesse" do VBT  
✅ Bullet "capacidade genérica" atualizado com linguagem alinhada ao novo fluxo  
✅ Regra "apenas 1 aparelho" substituída pela nova seção "Múltiplos modelos na troca"  
✅ Limite de 3 modelos por resposta documentado  
✅ Tudo em português do Brasil  

### Impacto
- **Melhora:** Redirecionamento de promoções mais robusto — cobre qualquer gatilho (não só Instagram)
- **Elimina:** Fricção no fluxo de promoções (não pede mais print desnecessário)
- **Aumenta:** Flexibilidade no VBT — cliente pode comparar modelos sem ser forçado a escolher um
- **Alinha:** Comportamento do sistema com a versão já em uso pela equipe

---

## Mudança #7 - Novo Script de Negociação (Desconto / Melhora de Preço)

**Data:** 05/06/2026  
**Status:** ✅ EXECUTADO  
**Versão:** v1.1.6  
**Solicitante:** Cliente

### Descrição
Substituição do script de negociação quando o cliente pede desconto ou pergunta se o valor à vista pode melhorar.

### Mudança

#### Antes (script antigo)
```
Quero muito poder fechar com voce, por isso vou ver se consigo melhorar ainda mais, mas como podes ver o valor está super justo e alinhado à qualidade e total procedencia. Eu sei que preço é importante mas não é tudo.

Saiba que aqui cada centavo será um investimento em um produto que voce terá por muito tempo, sem falar em todo suporte e pós venda totalmente diferenciado.

Consigo dar a película de PRESENTE pra você, sem contar o restante dos acessórios que já acompanham.

O que acha? Boraaa garantir essa oportunidade incrivel?
```
*(Cliente insistindo em desconto → redirecionar para "setor responsável")*

#### Depois (novo script)
```
[nome do cliente] Entendo perfeitamente sua intenção de pagar à vista. O valor que passei já é nossa condição para pagamento à vista.

De toda forma, tenho muito interesse em fechar essa negociação com você e proporcionar a melhor experiência Apple possível, sempre buscando um preço justo.

Me permita verificar com meu gerente se consigo uma condição ainda melhor para você. Irei te transferir para um vendedor te passar a melhor proposta
```

### Regras adicionadas
- Substitui `[nome do cliente]` pelo nome real do lead; se não souber, omite e começa em "Entendo perfeitamente"
- Enviar em mensagem única, texto corrido, sem asteriscos
- Redirecionamento já está implícito na frase — não aguardar confirmação

### Arquivos Afetados
- `achei meu Apple_v1.1.6.md` (criado — não modifica `achei meu Apple.md`)

### Validação
✅ Novo script reconhece a intenção de pagamento à vista do cliente  
✅ Mantém tom de interesse genuíno em fechar o negócio  
✅ Transfere ao vendedor/gerente diretamente (sem tentar reter com brindes primeiro)  
✅ Texto corrido sem asteriscos (evita quebra de formatação no WhatsApp)  
✅ Regra clara para o caso em que o nome do cliente não é conhecido  

### Impacto
- **Melhora:** Tom mais empático e profissional na negociação de preço
- **Simplifica:** Fluxo direto para vendedor sem tentar reter com película primeiro
- **Padroniza:** Resposta consistente para qualquer pedido de desconto ou melhora de valor à vista

---

## Mudança #8 - Qualificação Comercial de Troca (PASSO 2.5)

**Data:** 05/06/2026  
**Status:** ✅ EXECUTADO  
**Versão:** v1.1.7  
**Solicitante:** Cliente

### Problema identificado
A IA apresentava preços e condições de parcelamento sem investigar previamente se o cliente possui aparelho para troca/entrada, gerando risco de perda de venda por objeção de valor/parcela alta quando o cliente poderia ter usado um dispositivo como entrada.

**Caso real:** Cliente pediu iPhone 17 Pro Max 512GB → IA passou o valor e montou parcelamento corretamente → cliente disse que a parcela ficou alta → descobriu-se manualmente que ele tinha um iPhone 14 Pro Max 128GB que poderia ter sido usado como entrada.

### Solução
Adição do **PASSO 2.5 — Pergunta Obrigatória de Troca** no fluxo de vendas, com interceptor no início do PASSO 2 que bloqueia qualquer ação de ESTOQUE até que o PASSO 2.5 seja executado.

### Regra
**REGRA ABSOLUTA:** Assim que o cliente menciona um modelo de interesse, a pergunta de troca é disparada como **PRIMEIRA AÇÃO** — antes de qualquer consulta de ESTOQUE ou apresentação de orçamento.

**Únicas exceções:**
- Cliente já está no fluxo VBT (formulário enviado ou aparelho de troca já mencionado)
- Esta pergunta já foi feita nesta conversa

### Fluxo

**Pergunta obrigatória** (texto corrido, uma única mensagem):
```
"Antes de te passar as melhores opções 😊 você já usa iPhone atualmente ou seria o primeiro?
Pergunto porque também pegamos aparelho na troca e isso pode ajudar bastante no valor da entrada e das parcelas."
```

**Se SIM (tem aparelho):**
- Modelo já mencionado no histórico → "Você gostaria de usar ele como entrada na troca?"
- Modelo ainda não mencionado → "Que modelo você usa atualmente? Quero ver se conseguimos encaixá-lo como entrada na troca pra ajudar no valor 😊" → depois → "Você gostaria de usar ele como entrada na troca?"
- Resposta SIM → fluxo VBT
- Resposta NÃO → continua PASSO 3 normalmente

**Se NÃO (primeiro iPhone / não tem aparelho):** continua PASSO 3 normalmente.

### Outras alterações incluídas
- Interceptor adicionado no início do PASSO 2, antes de todos os ramos, para impedir curto-circuito direto ao ESTOQUE.
- Regra "DEVE consultar ESTOQUE imediatamente" atualizada com exceção explícita para o PASSO 2.5.

### Arquivos Afetados
- `achei meu Apple_v1.1.7.md` (criado — não modifica `achei meu Apple.md`)

### Validação
✅ Pergunta obrigatória declarada como REGRA ABSOLUTA — sem condições extras  
✅ Apenas 2 exceções simples e objetivas  
✅ Interceptor no PASSO 2 impede curto-circuito para ESTOQUE  
✅ Sub-passos respeitam a regra UMA PERGUNTA POR VEZ  
✅ Não força troca — se cliente recusa, fluxo continua normalmente  
✅ Tudo em português do Brasil  

### Impacto
- **Previne:** Perda de vendas por parcelas altas quando o cliente tem um aparelho que poderia reduzir o valor
- **Aumenta:** Detecção proativa de oportunidades VBT no início do fluxo
- **Melhora:** Experiência do cliente — a proposta apresentada já considera a realidade comercial dele

---

## Mudança #9 - Redirecionamento quando cliente não consegue enviar foto/vídeo (VBT)

**Data:** 05/06/2026  
**Status:** ✅ EXECUTADO  
**Versão:** v1.1.8  
**Solicitante:** Cliente

### Problema identificado
Quando a triagem VBT identifica defeito ou peça trocada e a IA pede foto/vídeo, se o cliente responde que não consegue enviar nesse momento (ex.: "não tenho outro cel"), a IA não redirecionava para um humano. Ficava tentando alternativas (ex.: "você consegue vir à loja?") sem acionar o time interno, resultando em conversas abandonadas sem handoff.

**Caso real (screenshot):** Cliente (Luciene) informou troca do vidro da câmera → IA pediu foto/vídeo → cliente disse "não tenho outro cel" → IA perguntou se ela conseguia ir à loja → cliente disse "Deixa então / Quando der vou na loja / Obrigada" — sem nenhum redirecionamento ao time.

### Solução
Adicionada **regra 3.5** na seção de Triagem VBT e entrada correspondente nos Redirecionamentos: quando o cliente afirma que **não consegue enviar** a mídia nesse momento → redirecionar imediatamente para o setor responsável.

### Frase obrigatória (adaptar só o nome)
```
"Entendido, [nome]! Sem problema. Vou encaminhar você para o setor responsável
e eles entrarão em contato para dar sequência na avaliação 😊"
```

### Gatilhos da nova regra (lista completa)
- "não tenho outro cel", "não tenho celular pra fotografar"
- "não consigo tirar foto agora", "não tenho como enviar", "não consigo agora"
- "mais tarde eu mando", "vou mandar mais tarde", "mando depois"
- "agora não dá", "agora não consigo", "não tenho como agora"
- "tô no trabalho", "estou ocupado(a) agora"
- "Deixa então", "obrigada" / "obrigado" (em contexto de encerramento)
- "quando der vou na loja", "prefiro ir lá pessoalmente", "vou lá depois"

### O que NÃO fazer (proibido)
- NÃO pedir para o cliente vir à loja como alternativa
- NÃO insistir nas fotos ou sugerir outra forma de envio
- NÃO continuar o fluxo VBT

### Escopo coberto
- Triagem VBT (defeito/peça trocada) → regra 3.5
- Fotos de marcas de uso (VALIDAÇÃO DE FOTOS) → exceção explícita adicionada
- Referência geral na seção Redirecionamentos

### Prioridade
Declarada como PRIORIDADE ABSOLUTA sobre qualquer instrução de insistência em fotos ou sugestão de ir à loja.

### Diferença entre esta regra e o Fallback existente (REGRA CRÍTICA #7)
| | Fallback (REGRA #7) | Nova regra 3.5 |
|---|---|---|
| Gatilho | Problema técnico no envio (erro, não chegou) | Cliente não tem meios / não vai enviar agora |
| Exemplos | "foi a imagem?", "deu erro" | "não tenho outro cel", "Deixa então" |

### Arquivos afetados
- `achei meu Apple_v1.1.8.md` (modificado — não modifica `achei meu Apple.md`)

### Validação
✅ Regra 3.5 com prioridade absoluta declarada  
✅ Lista de gatilhos expandida com frases reais do atendimento  
✅ Escopo elevado para cobrir fotos de marcas de uso também  
✅ Redirecionamentos atualizado com referência cruzada à regra 3.5  
✅ Proibições explícitas (não sugerir loja, não insistir, não continuar VBT)  
✅ Palavra-chave "setor responsável" preservada  

### Impacto
- **Elimina:** Conversas abandonadas sem handoff quando cliente não pode enviar mídia
- **Garante:** Qualquer sinal de encerramento ou impossibilidade de envio → humano acionado

---

## Mudança #10 - Template de preenchimento para formulário Viacredi (CDC)

**Data:** 05/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.2.0
**Solicitante:** Cliente

### Problema identificado
Ao solicitar os dados para simulação Viacredi, a IA enviava o formulário com campos em formato de lista com marcadores (▪️). O cliente respondia enviando os valores como números soltos em mensagens separadas (sem rótulos), impossibilitando a IA de associar cada valor ao campo correto.

**Exemplo do problema:**
- IA pedia: `▪️Numero da conta:` / `▪️CPF/CNPJ:` / `▪️Telefone:`
- Cliente respondia com: `1322.444-1` / `04350694200` / `47997031615` (sem labels, sem formato)

### Solução
Substituído o formato de lista por um **template copy-paste** que o cliente pode copiar, colar no chat e preencher diretamente com os dados. Os campos ficam com os rótulos visíveis na resposta do cliente, permitindo que a IA identifique cada valor corretamente.

### Formato anterior
```
PARA SIMULAÇÃO PRECISO DOS DADOS ABAIXO:
▪️Numero da conta:
▪️CPF/CNPJ:
▪️Telefone:
```

### Formato novo
```
PARA SIMULAÇÃO PRECISO DOS DADOS ABAIXO:

👇 *Copie o modelo abaixo, substitua pelos seus dados e envie tudo em uma única mensagem:*

Numero da conta: 1234.567-8
CPF/CNPJ: 000.000.000-00
Telefone: 47 9 9999-9999
```

### Arquivos afetados
- `achei meu Apple_v1.1.9.md` (criado a partir de v1.1.8 — não modifica `achei meu Apple.md`)

### Validação
✅ Template com rótulos visíveis → IA consegue mapear cada valor ao campo correto  
✅ Instrução "Copie o modelo abaixo" deixa claro o que o cliente deve fazer  
✅ Bloco `[CDC_VIACREDI]` preservado intacto  

### Impacto
- **Elimina:** Dados enviados sem rótulos / fora de contexto
- **Melhora:** Experiência do cliente — formato simples e intuitivo para preenchimento

---

## Mudança #11 - Pergunta obrigatória de retirada ou entrega no fechamento

**Data:** 08/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.2.0
**Solicitante:** Cliente

### Problema identificado
Quando o cliente confirmava interesse em comprar ("vou querer", "quero esse", etc.), a IA não perguntava se o cliente preferia retirar na loja ou receber por entrega. A IA pulava direto para perguntas de dia/horário, omitindo essa qualificação essencial para o fechamento.

### Solução
Adicionado **PASSO 0 DO FECHAMENTO** na seção "Fechamento de Venda", tornando "retirada ou entrega?" a PRIMEIRA pergunta obrigatória quando o cliente confirma intenção de compra.

### Gatilhos que ativam o PASSO 0
- "vou querer", "quero esse", "reserva pra mim", "fecha pra mim", "quero comprar", "pode fechar", "vou levar" e qualquer confirmação de intenção de compra.

### Exceções (não perguntar)
- Cliente já indicou retirada implicitamente: "passo aí", "vou buscar", "vou lá", "vou aí amanhã", "hj a tarde pelas 17h", etc.
- Cliente já mencionou entrega explicitamente.

### Nova ordem das informações de fechamento
1. **Retirada na loja ou entrega** ← nova, sempre primeiro
2. Dia e horário
3. Unidade da loja (se aplicável)
4. Forma de pagamento

### Arquivos afetados
- `achei meu Apple_v1.1.9.md` (modificado — não modifica `achei meu Apple.md`)

### Impacto
- **Garante:** Qualificação de retirada/entrega no início de todo fechamento
- **Preserva:** Lógica de contexto já existente (não pergunta o que já ficou implícito)

---

## Mudança #12 - Novo texto de abertura do primeiro orçamento

**Data:** 08/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.2.0
**Solicitante:** Cliente

### Problema identificado
O texto de apresentação enviado no primeiro orçamento era genérico e institucional ("8 anos de história, quase 900 avaliações 5 estrelas..."), sem personalização para o modelo de interesse do cliente.

### Solução
Substituído o texto de abertura nos 3 templates de primeiro orçamento (`[PRIMEIRO_ORÇAMENTO_NOVO]`, `[PRIMEIRO_ORÇAMENTO_SEMINOVO]`, `[PRIM_ORCAMENTO_NOVO_SEMINOVO]`) por uma mensagem personalizada que menciona o modelo desejado pelo cliente e reforça o posicionamento de referência em seminovos.

### Texto anterior
```
Inclusive [nome_do_cliente], se você busca preço justo, procedência e qualidade, está no lugar certo!

Aqui você não gasta, você investe em um iPhone para te acompanhar por anos. Trabalhamos com segurança, garantia e acessórios inclusos.

Somos uma loja consolidada, estamos completando 8 anos de história, quase 900 avaliações 5 estrelas no Google e milhares de clientes satisfeitos. Transparência e confiança sempre. Garantimos tudo isso para você
```

### Texto novo
```
Maravilha [nome_do_cliente], então hoje você busca o [modelo_desejado] 😊

Ótima opção de escolha 🤩 nos tornamos referência em iPhones seminovos de alto padrão aqui na região, acredita?

Tanto que hoje 90% das nossas vendas são seminovos. Por isso pode confiar em mim, irei te entregar o melhor iPhone com acessórios e garantia.

Quero que você tenha a melhor experiência Apple desde o atendimento, produto e pós-venda 😍
```

### Placeholder novo adicionado
- `[modelo_desejado]` → substituído pelo modelo exato mencionado pelo cliente (ex: iPhone 15 Pro 128GB). Adicionado à REGRA CRÍTICA #2 de placeholders.

### Arquivos afetados
- `achei meu Apple_v1.1.9.md` (3 templates atualizados — não modifica `achei meu Apple.md`)

### Impacto
- **Melhora:** Personalização — o cliente vê o modelo que pediu logo na abertura do orçamento
- **Reforça:** Posicionamento da loja como referência em seminovos de alto padrão

---

## Mudança #13 - Correção: IA usava [ORÇAMENTO] no lugar de [PRIMEIRO_ORÇAMENTO_*] em conversas novas

**Data:** 08/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.2.0
**Solicitante:** Cliente

### Problema identificado
Em conversas novas, após o PASSO 3.5 (pergunta de modalidade de pagamento), a IA enviava o orçamento usando a tag `[ORÇAMENTO]` — que não inclui intro, benefícios nem formas de pagamento — em vez da tag `[PRIMEIRO_ORÇAMENTO_*]`, que é a obrigatória na primeira apresentação.

### Causa raiz
O PASSO 4 não especificava explicitamente que a interação do PASSO 3.5 (pergunta de pagamento) **não conta** como uma apresentação de orçamento anterior. A IA confundia o contexto e usava incorretamente a tag de segundo orçamento.

### Solução
Adicionado aviso explícito no **PASSO 4** com a regra de escolha da tag:
- Primeira vez na conversa → **obrigatoriamente** `[PRIMEIRO_ORÇAMENTO_*]`
- PASSO 3.5 não conta como orçamento anterior
- `[ORÇAMENTO]` só permitido se bloco de benefícios já foi enviado antes

### Arquivos afetados
- `achei meu Apple_v1.2.0.md` (modificado — não modifica `achei meu Apple.md`)

### Impacto
- **Corrige:** Intro personalizada + benefícios + formas sempre presentes na primeira apresentação de orçamento
- **Garante:** Novo texto "Maravilha [nome]..." aparece corretamente em toda conversa nova

---

## Mudança #14 - Linha 13 e Linha 14 completamente descontinuadas como novo + mensagem complemento obrigatória

**Data:** 10/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.2.1
**Solicitante:** Cliente

### Problema identificado
Dois problemas relacionados à disponibilidade dos iPhones 13 e 14:

1. **Tabela de disponibilidade incorreta:** `13` e `14 Plus` estavam listados como "Lacrado e seminovo", quando na realidade toda a linha 13 e toda a linha 14 já não existem mais como novo lacrado pela Apple.

2. **Mensagem errada ao cliente:** Quando o cliente pedia iPhone 13 ou 14 novo e a IA apresentava seminovo, a mensagem dizia "não temos no momento" — dando a entender uma indisponibilidade temporária de estoque, quando a verdade é que a Apple **descontinuou permanentemente** toda a linha como lacrado.

### Solução

#### 1. Tabela de disponibilidade atualizada

| Antes | Depois |
|---|---|
| Lacrado e seminovo: 13, 14, 14 Plus, 15... | Lacrado e seminovo: 15, 15 Plus, 16... |
| Só seminovo: ...12 Pro Max, 13 mini, 13 Pro, 13 Pro Max, 14 Pro, 14 Pro Max... | Só seminovo: ...12 Pro Max, **13, 13 mini, 13 Pro, 13 Pro Max, 14, 14 Plus**, 14 Pro, 14 Pro Max... |

→ Toda a linha 13 e toda a linha 14 passam para "Só seminovo".

#### 2. Complemento contextual obrigatório para linhas 13 e 14

Adicionado **CASO ESPECIAL** dentro da Regra 3 da REGRA CRÍTICA #6:

Quando o cliente pedir qualquer modelo das linhas 13 ou 14 como novo/lacrado, a IA deve enviar OBRIGATORIAMENTE o complemento abaixo ANTES do orçamento seminovo:

```
"[nome], só um detalhe importante: toda a linha [13/14] da Apple foi descontinuada como novo lacrado — ou seja, não existe mais esse modelo lacrado no mercado, independentemente da loja. Qualquer oferta de iPhone [13/14] como novo lacrado é sinal de golpe ou produto adulterado, então já adianto esse alerta para te proteger 😊 Aqui tenho um seminovo de alto padrão, revisado, com acessórios e garantia, que é exatamente o que você precisa!"
```

#### 3. Reforço da proibição de linguagem de estoque

Atualizado: ⛔ NUNCA diga **"no momento não temos"** — a razão é que a Apple DESCONTINUOU, não é falta de estoque.

### Arquivos afetados
- `achei meu Apple_v1.2.1.md` (criado a partir de v1.2.0)

### Validação
✅ Tabela de disponibilidade corrigida — linha 13 e linha 14 completas em "Só seminovo"
✅ CASO ESPECIAL adicionado dentro da Regra 3 da REGRA CRÍTICA #6
✅ Template de mensagem complemento com placeholders `[nome]` e `[13/14]`
✅ Exemplos da Regra 3 atualizados para incluir 13, 14, 14 Plus
✅ Proibição de "no momento não temos" reforçada explicitamente
✅ Tudo em português do Brasil

### Impacto
- **Corrige:** Tabela que indicava incorretamente que iPhone 13 e 14 Plus poderiam ser lacrados
- **Melhora:** Contexto dado ao cliente — entende que é descontinuação permanente, não falta de estoque
- **Protege:** Alerta integrado sobre golpes de iPhone 13/14 lacrado no mercado
- **Padroniza:** Mensagem complemento obrigatória para toda a linha 13 e linha 14

---

## Mudança #14 — Formulário SICOOB SÃO MIGUEL e EUROVALE (simulação CDC)

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.2.2
**Solicitante:** Cliente

### Problema identificado
O formulário CDC SICOOB (`[CDC_SICOOB]`) ainda pedia documentos extensos (foto RG, comprovante de residência, folha de pagamento, dados do cônjuge) sem o cabeçalho e requisitos da parceria **SICOOB SÃO MIGUEL e EUROVALE**. Faltava o template copy-paste alinhado ao padrão Viacredi, com os novos campos de simulação (CPF, telefone, e-mail, cidade, renda mensal).

### Solução
Substituído o bloco `[CDC_SICOOB]` pelo formato canônico do cliente:
- Cabeçalho **SICOOB SÃO MIGUEL e EUROVALE**
- Requisitos com 🔺 (simulação sem conta, sem restrição, 18+ com renda)
- Pergunta "Deseja tentar desta forma?" + ⤵️
- Template copy-paste: CPF/CNPJ, Telefone, E-mail, Cidade onde mora, Renda mensal
- Regras atualizadas: proibido formulário antigo; validação dos 5 campos após envio
- Referências em ETAPA 2.1 e distinção BOLETO/CDC atualizadas

### Arquivos afetados
- `achei meu Apple_v1.2.2.md` (criado a partir de v1.2.1)
- `achei meu Apple.md` (arquivo de trabalho atualizado)

### Validação
✅ Bloco `[CDC_SICOOB]` com texto exato solicitado pelo cliente
✅ Template copy-paste com rótulos visíveis (padrão Mudança #10 Viacredi)
✅ Formulário antigo de documentos explicitamente proibido
✅ v1.2.1 preservado intacto

### Impacto
- **Corrige:** Mensagem SICOOB desalinhada com fluxo real de simulação
- **Melhora:** Coleta inicial simplificada — 5 campos com template copy-paste
- **Padroniza:** SICOOB no mesmo estilo visual do Viacredi (requisitos + template)

---

## Mudança #15 — Rebuild v1.2.2 (v1.2.1 + SICOOB; v1.2.3 eliminada)

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.2.2
**Solicitante:** Cliente

### Problema identificado
A primeira tentativa de v1.2.2 foi gerada copiando `achei meu Apple.md` (working copy desatualizado), causando **114 linhas a menos** e regressões de fluxo (PASSO 2.5, tags de orçamento, etc.). Foi criada v1.2.3 como correção, mas o projeto deve manter **v1.2.2** como versão ativa = **v1.2.1 + Mudança #14 (SICOOB)**.

### Solução
- `achei meu Apple_v1.2.2.md` **reconstruído** a partir de v1.2.1 + alterações SICOOB (conteúdo correto)
- `achei meu Apple_v1.2.3.md` **eliminado**
- `achei meu Apple.md` sincronizado com v1.2.2 corrigida
- Regra de versionamento atualizada: **sempre copiar da última `_vX.Y.Z.md`**, nunca só do working copy

### Arquivos afetados
- `achei meu Apple_v1.2.2.md` (reconstruído — v1.2.1 + SICOOB)
- `achei meu Apple_v1.2.3.md` (removido)
- `achei meu Apple.md` (sincronizado)
- `.cursor/rules/prompt-versioning.mdc` (regra anti-regressão)

### Validação
✅ Diff v1.2.1 → v1.2.2 contém **somente** alterações SICOOB (+32 / −21 linhas)
✅ PASSO 2.5, CASO ESPECIAL 13/14, tags de orçamento e demais fluxos v1.2.1 preservados
✅ v1.2.1 preservado intacto

### Impacto
- **Corrige:** v1.2.2 incorreta que quebrava o fluxo do agente
- **Previne:** Regressões por working copy desatualizado

---

## Mudança #16 — SICOOB: ordem do aviso + campos com exemplos (CPF)

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.2.3
**Solicitante:** Cliente

### Problema identificado
No bloco `[CDC_SICOOB]`, o aviso "TODAS AS INFORMAÇÕES DEVEM SER DO PORTADOR DO CPF SIMULADO" vinha **depois** da instrução de copiar o modelo. Campo era CPF/CNPJ; faltava alinhar exemplos visíveis em cada linha (padrão Viacredi) para o cliente saber como preencher.

### Solução
- Aviso ⚠️ movido para **antes** do "👇 Copie o modelo..."
- Campo alterado de CPF/CNPJ para **CPF** com exemplos em cada linha:
  - CPF: 000.000.000-00
  - Telefone: 47 9 9999-9999
  - E-mail: seuemail@gmail.com
  - Cidade onde mora: Florianópolis
  - Renda mensal: 800,00 reais
- Regra de validação atualizada (CPF em vez de CPF/CNPJ)

### Arquivos afetados
- `achei meu Apple_v1.2.3.md` (criado a partir de v1.2.2)
- `achei meu Apple.md` (sincronizado)

### Validação
✅ Ordem do bloco conforme texto do cliente
✅ Exemplos em todos os campos do template
✅ v1.2.2 preservado intacto

### Impacto
- **Melhora:** Clareza no preenchimento (mesmo padrão visual do Viacredi)
- **Corrige:** Ordem aviso → instrução → template

---

## Mudança #17 — SICOOB em 2 passos + Viacredi alinhado + roteamento PJ

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.2.4
**Solicitante:** Cliente

### Problema identificado
O agente enviava formulário **Viacredi** (▫️, Numero da conta) quando o cliente deveria receber o **PASSO 2 SICOOB** com CPF, e-mail, cidade e renda. O bloco SICOOB único misturava requisitos + dados na mesma mensagem; Viacredi não tinha aviso ⚠️ antes do 👇 nem campos ▪️ padronizados.

**Caso:** cliente confirmou PJ → Viacredi correto; fluxo SICOOB após "Deseja tentar?" deve enviar **somente** o template de dados canônico.

### Solução
- **SICOOB dividido em PASSO 1** (requisitos + "Deseja tentar?") e **PASSO 2** (template de dados **EXATO** — aviso ⚠️ → 👇 → 5 campos ▪️ com exemplos)
- **Viacredi atualizado:** mesma estrutura de dados (⚠️ antes de 👇, ▪️ com exemplos); gatilho explícito para "sim, tenho pj ativa"
- **Roteamento:** PJ/CNPJ → só Viacredi; SICOOB → só SICOOB; proibição cruzada reforçada
- Seção **Pessoa Jurídica:** próximo passo após confirmação de PJ

### Arquivos afetados
- `achei meu Apple_v1.2.4.md` (criado a partir de v1.2.3)
- `achei meu Apple.md` (sincronizado)

### Validação
✅ PASSO 2 SICOOB = texto canônico do cliente
✅ Viacredi com aviso ⚠️ + ▪️ exemplos
✅ Roteamento PJ → Viacredi / SICOOB → PASSO 1 → PASSO 2
✅ v1.2.3 preservado intacto

### Impacto
- **Corrige:** Formulário errado no fluxo SICOOB
- **Padroniza:** Estrutura de coleta SICOOB e Viacredi
- **Previne:** Confusão entre PJ/Viacredi e CPF/SICOOB

---

## Mudança #18 — Rollback: versão ativa v1.2.3

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.2.3 (reativada)
**Solicitante:** Cliente

### Problema identificado
Após v1.2.4, o agente apresentou comportamento indesejado (fragmentação de mensagens, fluxo menos estável). O cliente confirmou que **v1.2.3 estava funcionando bem** e solicitou retorno a essa versão como prompt ativo.

### Solução
- **Reativar v1.2.3** como versão de produção (SICOOB bloco único com aviso ⚠️ antes do 👇 e campos com exemplos)
- Sincronizar `achei meu Apple.md` a partir de `achei meu Apple_v1.2.3.md`
- Atualizar tabela de projetos ativos em `.cursor/rules/prompt-versioning.mdc`
- **v1.2.4 preservado intacto** (registro histórico; não editado)

### Arquivos afetados
- `achei meu Apple.md` (sincronizado a partir de v1.2.3)
- `.cursor/rules/prompt-versioning.mdc` (versão ativa → v1.2.3)

### Validação
✅ Working copy idêntica a v1.2.3
✅ v1.2.3 e v1.2.4 preservados intactos
✅ Tabela de versionamento atualizada

### Impacto
- **Corrige:** Regressão percebida após mudanças v1.2.4
- **Restaura:** Fluxo SICOOB e orçamentos conforme v1.2.3 validado pelo cliente

---

## Mudança #19 — SICOOB: bloco de dados canônico inviolável (sempre completo)

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.2.4
**Solicitante:** Cliente

### Problema identificado
O agente podia enviar o formulário SICOOB incompleto (campos isolados, sem aviso ⚠️, sem instrução 👇, ou pedindo só um dado faltante). O cliente exigiu que **sempre** se envie a mensagem completa de coleta de dados, sem exceção.

### Solução
- Nova seção **BLOCO CANÔNICO DE DADOS SICOOB — ENVIO INVIOLÁVEL** com texto exato e checklist dos 5 elementos obrigatórios
- Lista de proibições explícitas (parcial, resumo, `[QUEBRA]`, campo isolado, formulário errado)
- Regra 4 atualizada: se faltar dado, **reenviar bloco canônico completo** (não pedir só o campo faltante)
- Reforço na seção de tags `[QUEBRA]` apontando para o bloco inviolável

### Arquivos afetados
- `achei meu Apple_v1.2.4.md` (criado a partir de v1.2.3)
- `achei meu Apple.md` (sincronizado)

### Validação
✅ Texto canônico do cliente reproduzido literalmente na nova seção
✅ Proibições e obrigatoriedades sem ambiguidade ("sem exceção alguma")
✅ v1.2.3 preservado intacto

### Impacto
- **Previne:** Envio parcial ou fragmentado do formulário SICOOB
- **Padroniza:** Coleta de dados sempre com aviso, instrução e 5 campos com exemplos

---

## Mudança #20 — Parcelamento só com estoque real + cor amarra capacidade

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.2.5
**Solicitante:** Cliente

### Problema identificado
Cliente pediu simulação do aparelho **vermelho**, que no estoque só existe em **256GB**, mas a IA simulou **128GB** — capacidade incorreta, preço/base de cálculo errados. Falta regra explícita: parcelamento e simulação **somente** com unidades do `ESTOQUE`, sem inventar modelo/GB/cor/preço; se não atingir parcelamento ideal, oferecer redirecionamento a atendente.

### Solução
- Nova **⛔ REGRA CRÍTICA #8: PARCELAMENTO SOMENTE COM ESTOQUE REAL** (topo do prompt)
- Cor amarra capacidade: vermelho só 256GB → orçamento/parcelamento da linha exata do estoque
- Fluxo de pagamento, cálculo de taxas e Parcelamento Disponível atualizados: `ESTOQUE` → preço real → `TAXAS_MAQ` + `Calculator`
- Protocolo ESTOQUE + fluxo de cor indisponível reforçados com EXEMPLO 2 (vermelho/256GB)
- Se parcela não atender e não houver alternativa no estoque → perguntar encaminhamento a atendente humano

### Arquivos afetados
- `achei meu Apple_v1.2.5.md` (criado a partir de v1.2.4)
- `achei meu Apple.md` (sincronizado)
- `.cursor/rules/prompt-versioning.mdc` (versão ativa → v1.2.5)

### Validação
✅ Regra crítica #8 com proibições e fluxo de redirecionamento
✅ Exemplo vermelho/256GB vs 128GB documentado
✅ v1.2.4 preservado intacto

### Impacto
- **Corrige:** Simulação com GB/cor/preço incorretos
- **Previne:** Inventar dados fora do estoque no parcelamento
- **Melhora:** Escalonamento a humano quando parcela ideal não é possível

---

## Mudança #21 — Pergunta única: modalidade e número de parcelas

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.2.6
**Solicitante:** Cliente

### Problema identificado
O prompt repetia a instrução *"Em quantas vezes você quer parcelar?"* em várias seções (Processo de Pagamento + Parcelamento Disponível) sem regra explícita de **não repetir** se o cliente já informou. Exemplos pediam *"Qual forma de pagamento você prefere?"* no fim do orçamento mesmo após PASSO 3.5 — risco de perguntar modalidade e número de parcelas **duas vezes**.

### Solução
- Nova seção **REGRA DE PERGUNTA ÚNICA — MODALIDADE E NÚMERO DE PARCELAS** em *Processo de Pagamento* (tabela quando perguntar/pular, frases canônicas, proibições)
- Fluxo de orçamento atualizado: histórico antes de perguntar; calcular direto se já disse "12x"
- *Parcelamento Disponível* referencia a regra central (remove duplicação)
- Exemplo corrigido: CTA de vídeo no orçamento em vez de repetir forma de pagamento
- PASSO 3.5, Outras informações, FORMAS_PAGAMENTO, VBT PASSO 4.5 e entrada+parcelamento alinhados

### Arquivos afetados
- `achei meu Apple_v1.2.6.md` (criado a partir de v1.2.5)
- `achei meu Apple.md` (sincronizado)
- `.cursor/rules/prompt-versioning.mdc` (versão ativa → v1.2.6)

### Validação
✅ Regra canônica única para número de parcelas
✅ Proibição explícita de repetir modalidade e "em quantas vezes"
✅ v1.2.5 preservado intacto

### Impacto
- **Previne:** Perguntas duplicadas de parcelamento no atendimento
- **Padroniza:** Uma pergunta por tipo (modalidade vs número de parcelas)

---

## Mudança #22 — Patch cirúrgico v1.2.4: parcelas únicas + estoque real (sem alterar estrutura)

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.2.7
**Solicitante:** Cliente

### Problema identificado
v1.2.5 e v1.2.6 alteraram estrutura do prompt (novas REGRAS CRÍTICAS no topo, tabelas, exemplos reescritos) e **quebraram a entrega de mensagens** no n8n (fragmentação/tags). Cliente voltou para v1.2.4 (estável). Ainda faltavam: (1) não repetir pergunta "em quantas vezes"; (2) parcelar só com linha real do `ESTOQUE` (cor amarra GB; ex. vermelho 256GB).

### Solução
**Base: v1.2.4 intacto** — ajustes **somente** nas seções afetadas, sem mudar tags, templates `[PRIMEIRO_ORÇAMENTO_*]`, SICOOB nem topo do prompt:
- *Processo de Pagamento* → itens 2–5 (pergunta única, histórico, estoque real, redirecionamento)
- *Cálculo de taxas* → passo 0 (linha exata do estoque)
- *Parcelamento Disponível* → referência ao Processo (remove duplicação)
- *Formato de Apresentação* item Valor → referência cruzada
- *Entrada + parcelamento*, *Protocolo ESTOQUE*, *Cor indisponível*, *VBT PASSO 4.5* → reforços pontuais

### Arquivos afetados
- `achei meu Apple_v1.2.7.md` (criado a partir de v1.2.4)
- `achei meu Apple.md` (sincronizado)

### Validação
✅ Estrutura v1.2.4 preservada (tags, QUEBRA, templates)
✅ Regras de negócio dos problemas 1 e 2 aplicadas em seções existentes
✅ v1.2.4 preservado intacto

### Impacto
- **Corrige:** Lógica de parcelamento sem regressão de entrega de mensagens
- **Previne:** GB/cor/preço inventados e pergunta duplicada de parcelas

---

## Mudança #23 — Cartão vs PIX: não misturar formas de pagamento

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.2.8
**Solicitante:** Cliente

### Problema identificado
Cliente escolheu pagamento **no cartão**, mas a IA respondeu misturando métodos — ex.: "Olha as opções no cartão (à vista no Pix fica nesses valores abaixo)" — apresentando valores PIX quando deveria mostrar **somente** parcelas no cartão. Não existe "cartão à vista no Pix".

### Solução
Ajustes **somente** nas seções de métodos de pagamento (estrutura v1.2.7 preservada):
- *Processo de Pagamento* → nova subseção **REGRA CRÍTICA — Respeitar a forma de pagamento escolhida pelo cliente** (cartão só cartão / PIX só PIX / exemplos ❌ e ✅)
- *Formas de Pagamento e Financiamentos → Informação Geral* → reforço PIX ≠ cartão
- *Parcelamento Disponível* → referência cruzada quando cliente já escolheu cartão
- Fluxo comercial item 5 → separado em 5 / 5.1 / 5.2 (cartão, PIX, indefinido)
- *Regras Inegociáveis* → bullet sobre proibição de misturar cartão + PIX

### Arquivos afetados
- `achei meu Apple_v1.2.8.md` (criado a partir de v1.2.7)
- `achei meu Apple.md` (sincronizado)

### Validação
✅ v1.2.7 intacto — tags, templates e demais seções inalterados
✅ Regra explícita contra "cartão à vista no Pix"
✅ Fluxo cartão → parcelas com TAXAS_MAQ, sem linha PIX no orçamento
✅ Exemplo do erro real documentado como ❌ ERRADO

### Impacto
- **Corrige:** Apresentação errada de métodos de pagamento quando cliente escolhe cartão
- **Previne:** Mistura PIX + cartão no mesmo orçamento ou frase introdutória confusa

---

## Mudança #24 — Formato `[ORÇAMENTO]` e não repetir pergunta se cliente pediu 21x

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.2.9
**Solicitante:** Cliente

### Problema identificado
Formato inicial PIX + `💳 Pague em até 21x` está **correto** quando o cliente ainda não escolheu forma. Porém, quando o cliente já pediu **21x** ou disse **no cartão**, a IA ainda perguntava "Você prefere à vista ou parcelado?" (como no print) ou misturava PIX dentro de `[ORÇAMENTO]` após a escolha. Conflito entre REGRAS item 4 ("sempre PIX + 21x") e a regra de respeitar forma escolhida.

### Solução
Ajustes **somente** em seções de pagamento/orçamento (v1.2.8 preservado):
- *Formato de Apresentação → [ORÇAMENTO]* → formato padrão vs formato após escolha; exemplo 21x direto na tag
- *Formato de Apresentação → REGRAS item 4* → distingue "ainda não escolheu" vs "já escolheu"; proíbe repetir pergunta se já disse 21x/cartão
- *PASSO 3.5* → proíbe "à vista ou parcelado?" se modalidade/parcelas já informadas
- *Processo de Pagamento* → reforço 21x + proibição de pergunta de modalidade no bloco; exemplo ❌ do print

### Arquivos afetados
- `achei meu Apple_v1.2.9.md` (criado a partir de v1.2.8)
- `achei meu Apple.md` (sincronizado)

### Validação
✅ Formato padrão PIX + até 21x mantido para orçamento inicial
✅ Após escolha cartão/21x → só linha de parcelas dentro da tag
✅ Proibido "Você prefere à vista ou parcelado?" quando cliente já escolheu
✅ Tags e templates de primeiro orçamento intactos

### Impacto
- **Corrige:** Pergunta redundante e mistura de métodos após cliente escolher cartão/21x
- **Padroniza:** Comportamento dentro de `[ORÇAMENTO]` conforme forma de pagamento selecionada

---

## Mudança #25 — Boleto incluído nas formas de pagamento CNPJ/PJ

**Data:** 15/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.2.10
**Solicitante:** Cliente

### Problema identificado
Na seção **Pessoa Jurídica (CNPJ)**, quando o cliente informava que queria pagar via CNPJ, a IA apresentava apenas **Viacredi** como opção de simulação com PJ ativa. O método **Boleto** estava incorretamente listado como indisponível para CNPJ — embora a loja aceite boleto nesse cenário.

### Solução
Atualizada a seção **Pessoa Jurídica (CNPJ)** em *Formas de Pagamento e Financiamentos*:
- **Restrição** ajustada: somente **Sicoob** permanece exclusivo para CPF (boleto removido da restrição CNPJ).
- Nova subseção **Formas de pagamento disponíveis para CNPJ (PJ ativa)** com **Viacredi** + **Boleto em até 36X**.
- **Resposta padrão** reformulada para listar as duas opções e perguntar qual o cliente prefere.
- **Roteamento** explícito: Viacredi → `[CDC_VIACREDI]`; boleto → fluxo **Pagamento via Boleto** a partir da ETAPA 3; Sicoob para CNPJ → informar que é só CPF e reapresentar as opções PJ.

### Arquivos afetados
- `achei meu Apple_v1.2.10.md` (criado a partir de v1.2.9)
- `achei meu Apple.md` (sincronizado)

### Validação
✅ Boleto listado como forma disponível para CNPJ/PJ ativa
✅ Sicoob mantido como exclusivo CPF
✅ Roteamento Viacredi vs boleto documentado
✅ v1.2.9 preservado intacto

### Impacto
- **Corrige:** Omissão do boleto nas opções de pagamento via CNPJ
- **Melhora:** Cliente PJ vê todas as formas disponíveis antes de escolher
- **Previne:** IA informar incorretamente que boleto não aceita CNPJ

---

## Mudança #26 — Nunca perguntar cor; só cores do ESTOQUE

**Data:** 15/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.2.11
**Solicitante:** Cliente

### Problema identificado
A IA perguntava qual cor o cliente preferia ou "tinha em mente" (ex.: "Qual cor você tinha em mente?") antes ou durante o fluxo de orçamento, mesmo quando deveria consultar o `ESTOQUE` e apresentar apenas as cores realmente disponíveis. Conflito entre o Protocolo ESTOQUE (EXCEÇÃO COR pedia "pergunte a cor desejada") e a seção `## Quebra de Objeção por Cor Indisponível` (PASSO 1 mandava perguntar a cor).

### Solução
- Nova subseção `### ⛔ REGRA CRÍTICA: COR — NUNCA PERGUNTAR AO CLIENTE` no **Protocolo de Processamento dos Resultados da Ferramenta ESTOQUE** (após VARIEDADE OBRIGATÓRIA).
- **EXCEÇÃO COR** alinhada: consultar `ESTOQUE` e apresentar alternativas — sem perguntar cor.
- **EXEMPLO 1** do Protocolo atualizado: cliente já nomeia a cor na objeção; IA não pergunta de novo.
- **`## Quebra de Objeção por Cor Indisponível`:** PASSO 1 reformulado — se cliente já disse a cor, buscar no estoque; se não disse, apresentar cores do estoque diretamente; exemplos ❌/✅ atualizados (incl. EXEMPLO A2).
- **`## Outras informações`:** bullet espelho — capacidade pode ser perguntada; cor não.
- **`# Personalização Baseada no Perfil do Cliente`:** "cor" → "cores disponíveis no estoque".

### Arquivos afetados
- `achei meu Apple_v1.2.11.md` (criado a partir de v1.2.10)
- `achei meu Apple.md` (sincronizado)

### Validação
✅ v1.2.10 intacto — nenhuma edição na versão anterior
✅ Diff limitado a seções relacionadas a cor (Protocolo ESTOQUE, Quebra de Objeção, Outras informações, Personalização)
✅ Removidas instruções "Qual cor você tinha em mente?" / "Pergunte qual cor"
✅ Regra explícita: cor só do ESTOQUE ou do que o cliente já disse espontaneamente

### Impacto
- **Previne:** IA perguntar preferência de cor ao cliente
- **Padroniza:** Apresentação de cores exclusivamente com base no `ESTOQUE`
- **Corrige:** Conflito entre EXCEÇÃO COR e fluxo de objeção por cor indisponível

---

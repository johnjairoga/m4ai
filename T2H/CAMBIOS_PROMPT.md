# Registro de Mudanças no Prompt - T2H

---

## Mudança #1 - Qualificação Combinada: Modelo + Novo/Seminovo na Mesma Mensagem

**Data:** 02/06/2026  
**Status:** ✅ EXECUTADO  
**Versão:** v1.0.1  
**Solicitante:** Cliente (07Mai - 01)

### Problema Identificado
A IA perguntava modelo e novo/seminovo em mensagens separadas e sequenciais, gerando fricção desnecessária no início do atendimento.

### Estratégia Adotada
Quando o cliente não informou nem modelo nem preferência de novo/seminovo, combinar as duas perguntas em uma única mensagem de abertura.

### Frase Modelo
> "Você está procurando um iPhone novo ou seminovo? Algum modelo específico?"

### Linhas Afetadas

| Seção | Mudança |
|---|---|
| **Regras de Qualificação** | Substituída regra de pergunta única por regra de pergunta combinada (ambos em uma mensagem quando nenhum foi informado) |
| **Ramo A — exemplo de pergunta engajadora** | Atualizado para usar a pergunta combinada |
| **Fluxo de Qualificação - SEQUÊNCIA OBRIGATÓRIA (Passo 2)** | Expandido com lógica de 4 cenários: nenhum informado / só modelo / só novo-seminovo / ambos |

### Lógica dos 4 Cenários (Passo 2)

| Situação | Ação |
|---|---|
| Nem modelo nem novo/seminovo informados | Perguntar AMBOS na mesma mensagem |
| Modelo informado, novo/seminovo não | Seguir pré-check → passo 3 (novo/seminovo) |
| Novo/seminovo informado, modelo não | Perguntar apenas o modelo |
| Ambos informados | Pular direto para pré-check |

### Validação
✅ Pergunta combinada reduz uma troca de mensagem no funil  
✅ Lógica preservada para casos em que cliente já informou um dos dois  
✅ Compatível com o comportamento HÍBRIDO de novo/seminovo existente  
✅ Exemplo no Ramo A atualizado para refletir nova pergunta  

---

## Mudança #2 — Regra Anti-Repetição de Mensagens

**Data:** 10/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.2
**Solicitante:** Cliente

### Problema Identificado
A IA estava enviando a **mesma mensagem duas vezes** dentro do mesmo turno de resposta — o mesmo CTA ou pergunta aparecia em dois elementos diferentes do array `message` na mesma resposta.

**Caso real (screenshot):** A pergunta de reserva *"Qual que eu deixe esse 256gb separado pra você passar no final da tarde?"* foi enviada **duas vezes** consecutivas na mesma resposta (dois elementos idênticos no mesmo array).

### Causa Raiz
Ausência de regra explícita obrigando a revisão do array antes de fechar o JSON de resposta para detectar e remover elementos duplicados.

### Solução

#### 1. Nova regra — ⛔ REGRA CRÍTICA — ANTI-REPETIÇÃO DE MENSAGENS (topo do prompt)

Inserida logo após a Medida de Segurança (prioridade alta):

- **Checklist pré-envio:** antes de fechar o JSON, verificar se algum elemento do array é idêntico/equivalente a outro do mesmo array
- **Verificação de histórico:** se uma pergunta já foi enviada sem resposta, não repetir
- **Casos concretos proibidos** com exemplos diretos do erro real
- **Checklist de 3 pontos** para revisão obrigatória

#### 2. Reforço na seção FORMATO DE SAÍDA JSON

Adicionado bloco de **VERIFICAÇÃO ANTI-REPETIÇÃO** imediatamente antes das regras do campo `message`, referenciando a regra do topo.

### Arquivos afetados
- `T2H_v1.0.2.md` (criado a partir de v1.0.1)

### Validação
✅ Regra no topo do prompt (prioridade alta, após Medida de Segurança)
✅ Casos proibidos com exemplo concreto do erro real
✅ Checklist de 3 pontos obrigatório antes de fechar o JSON
✅ Reforço na seção de Formato de Saída JSON
✅ Cobre duplicata no mesmo array E repetição de pergunta sem resposta no histórico

### Impacto
- **Previne:** Mesmo CTA ou pergunta aparecendo duas vezes na mesma resposta
- **Previne:** Perguntas repetidas que o cliente já respondeu ou ignorou
- **Melhora:** Experiência — conversa mais fluida, sem robótica
- **Não afeta:** Reapresentação de orçamento com formatação diferente (já coberta por REGRA CRÍTICA - REAPRESENTAÇÃO DE ORÇAMENTO)

---

## Mudança #3 — Nova Modalidade de Pagamento: Crédito para Trabalhador

**Data:** 01/07/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.3
**Solicitante:** Cliente

### Problema identificado
A loja passou a oferecer uma nova modalidade de pagamento — Crédito para Trabalhador — que não estava mapeada no prompt. Quando clientes perguntavam sobre formas de parcelamento ou financiamento, a IA não apresentava essa opção.

### Solução
Adicionada a nova modalidade em dois pontos do prompt:

1. **Seção "FORMAS DE PAGAMENTO DA LOJA":** incluída a linha "Crédito para Trabalhador (desconto mensal em folha de pagamento)" na lista de formas aceitas.

2. **Nova seção "CRÉDITO PARA TRABALHADOR"** (inserida após a seção CDC): define requisitos do cliente (mínimo 21 anos + 1 ano de carteira assinada na mesma empresa), vantagens (sem cartão de crédito, sem vínculo bancário), regra de quando mencionar (somente quando cliente demonstrar interesse em pagamento/financiamento/parcelamento), frase modelo para apresentação, instrução de envio do link do formulário (`[LINK_CREDITO_TRABALHADOR]` — placeholder a ser substituído pela URL real) e redirecionamento ao vendedor para mais detalhes.

### Arquivos afetados
- `T2H_v1.0.3.md` (criado a partir de v1.0.2)

### Validação
✅ Modalidade adicionada à lista de formas de pagamento da loja
✅ Seção própria com requisitos, vantagens e regras de apresentação
✅ Regra de não proatividade no primeiro contato (igual ao padrão do CDC)
✅ Frase modelo definida para padronizar a comunicação ao cliente
✅ Fluxo de envio do formulário incluído (aguarda substituição do link real)
✅ Redirecionamento ao vendedor para detalhes avançados

### Impacto
- **Adiciona:** Nova opção de pagamento acessível para trabalhadores CLT
- **Padroniza:** Apresentação da modalidade com requisitos claros e frase modelo
- **Previne:** IA omitir essa opção quando cliente pergunta sobre financiamento/parcelamento

---

## Mudança #4 — Gatilho explícito para Crédito para Trabalhador e CDC ao listar formas de pagamento

**Data:** 03/07/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.4
**Solicitante:** Cliente

### Problema identificado
Quando o cliente perguntou explicitamente "quais são os métodos de pagamento que vocês têm disponíveis?", a IA listou apenas Pix, dinheiro, cartão de crédito e débito — omitindo completamente o **Crédito para Trabalhador** e o **CDC**.

**Caso real:**
> Cliente: "Queria saber quais são os métodos de pagamento que vocês têm disponíveis?"
> IA: "Temos estas formas de pagamento: Pix, dinheiro, cartão de crédito (parcelado com acréscimo da maquininha, até 18x) e cartão de débito (à vista, com acréscimo da maquininha)."

A causa raiz foi a regra vaga "SÓ mencionar quando o cliente demonstrar interesse em formas de pagamento" — que deveria cobrir esse caso mas não era específica o suficiente para a IA aplicar ao perguntar diretamente pelo catálogo completo de pagamentos.

### Solução
Reformuladas as regras das seções **CDC** e **CRÉDITO PARA TRABALHADOR** em dois pontos:

1. **Gatilho explícito "SEMPRE mencionar"** substituindo o "SÓ mencionar" — com lista de situações que obrigam a menção, destacando explicitamente perguntas diretas sobre formas de pagamento disponíveis.

2. **Exemplo concreto de erro** adicionado na seção CRÉDITO PARA TRABALHADOR:
   - ❌ IA lista só Pix/cartão/débito sem mencionar Crédito para Trabalhador → ERRO GRAVE
   - ✅ IA lista TODAS as formas quando cliente pergunta quais são

### Arquivos afetados
- `T2H_v1.0.4.md` (criado a partir de v1.0.3)

### Validação
✅ Regra de CDC atualizada com gatilho explícito para listagem completa
✅ Regra de Crédito para Trabalhador atualizada com gatilho explícito
✅ Exemplo concreto do erro real embutido no prompt como âncora de memória
✅ "NUNCA oferecer proativamente" mantido — só bloqueia o primeiro contato sem contexto de pagamento

### Impacto
- **Corrige:** IA omitir Crédito para Trabalhador e CDC ao responder pergunta direta sobre formas de pagamento
- **Previne:** Apresentação incompleta do catálogo de pagamentos disponíveis

---

## Mudança #5 — Regra de películas: tipos disponíveis, hidrogel e telas curvas

**Data:** 03/07/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.5
**Solicitante:** Cliente

### Problema identificado
O prompt não tinha nenhuma informação sobre películas. Qualquer pergunta sobre película seria redirecionada genericamente ao "setor de venda de acessórios", sem informar o que a loja tem ou não tem disponível — inclusive podendo confirmar erroneamente que tem hidrogel.

### Solução
Adicionada nova regra **"4. Películas — RESPONDER DIRETAMENTE"** na seção de Redirecionamentos, antes da regra de acessórios, com:

- **Instrução explícita de NÃO redirecionar** para perguntas sobre película
- **Tipos disponíveis por dispositivo:**
  - iPhone: cerâmica, fosca, privacidade e vidro 3D
  - Android: vidro 3D
- **O que não trabalhamos:** hidrogel e películas para telas curvas
- **Exemplo concreto de erro:** IA confirmando que tem hidrogel → ERRO GRAVE
- **Renumeração** dos itens seguintes (5→6, 6→7, 7→8) para acomodar o novo item 4

### Arquivos afetados
- `T2H_v1.0.5.md` (criado a partir de v1.0.4)

### Validação
✅ Regra de resposta direta para películas (sem redirecionar)
✅ Lista de tipos disponíveis por plataforma (iPhone e Android)
✅ Hidrogel explicitamente marcado como indisponível
✅ Telas curvas explicitamente marcadas como sem película disponível
✅ Exemplo de erro embutido no prompt como âncora de memória
✅ Numeração dos redirecionamentos corrigida

### Impacto
- **Corrige:** IA podendo confirmar que tem hidrogel (não temos)
- **Corrige:** IA redirecionando ao invés de responder diretamente sobre películas
- **Padroniza:** Resposta clara e completa sobre tipos de película por dispositivo

---

## Mudança #6 — Regra de películas promovida a seção standalone de prioridade máxima

**Data:** 03/07/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.6
**Solicitante:** Cliente

### Problema identificado
A regra de películas inserida na v1.0.5 (dentro da seção de redirecionamentos, como item #4) não funcionou. A IA ainda redirecionou ao "setor de venda de acessórios" quando o cliente perguntou sobre película hidrogel.

**Caso real:**
> Cliente: "Queria saber se vcs tem película hidrogel para aplicar no telefone?"
> IA: "Vou te encaminhar para o setor de venda de acessórios, eles vão te confirmar a disponibilidade da película hidrogel e o valor certinho." → **ERRO GRAVE**

### Causa raiz
A regra estava enterrada dentro da seção de redirecionamentos. A IA identificou a palavra "película" como acessório e disparou o redirect genérico antes de processar o item #4 específico.

### Solução
1. **Removida** a regra de películas de dentro dos redirecionamentos (item #4 da v1.0.5)
2. **Criada seção standalone** `🚨 REGRA CRÍTICA — PELÍCULAS 🚨` imediatamente antes da seção de Redirecionamentos, com:
   - Declaração de prioridade máxima sobre qualquer redirecionamento de acessórios
   - Lista de palavras-chave que acionam a regra ("película", "hidrogel", "protetor de tela", etc.)
   - Bloqueios absolutos: ❌ redirecionar, ❌ confirmar que tem hidrogel
   - Fluxo de resposta por caso (hidrogel, película genérica, tela curva)
   - Exemplo concreto de resposta correta
3. **Atualizado** o item de acessórios na seção de redirecionamentos com aviso explícito de que películas não se encaixam ali

### Arquivos afetados
- `T2H_v1.0.6.md` (criado a partir de v1.0.5)

### Validação
✅ Seção standalone com prioridade máxima declarada explicitamente
✅ Palavras-chave mapeadas ("hidrogel", "película", "protetor de tela", etc.)
✅ Bloqueio absoluto de redirecionamento ao setor de acessórios para películas
✅ Fluxo de resposta: perguntar iPhone ou Android → listar opções corretas
✅ Telas curvas: sem película disponível
✅ Exemplo de resposta real embutido
✅ Aviso no item de acessórios da seção de redirecionamentos

### Impacto
- **Corrige:** IA redirecionando ao "setor de venda de acessórios" para perguntas de película
- **Corrige:** IA confirmando disponibilidade de hidrogel (não trabalhamos)
- **Padroniza:** Resposta direta e completa com tipos disponíveis por dispositivo

---


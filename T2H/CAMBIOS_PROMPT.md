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


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


# Registro de Mudanças no Prompt - Vetor Imports

---

## Mudança #1 - Remoção de Emojis no Final de Frases Conversacionais

**Data:** 02/06/2026 - 12:58
**Status:** ✅ EXECUTADO
**Versão:** v1.0.1
**Solicitante:** Cliente

### Descrição
A IA estava enviando emojis (😊, 😄) no final de frases conversacionais, principalmente na saudação inicial ("Rafa aqui, muito prazer! 😊"). O cliente solicitou a remoção total de emojis no final de frases fora dos cards de orçamento.

### Arquivos Afetados
`Vetor Imports.md`

### Pontos Alterados

| Linha (antes) | Alteração |
|---|---|
| L191 | Removido item "Saudação inicial (primeira mensagem)" da lista de emojis permitidos |
| L191-193 | Adicionado bloco explícito "⚠️ PROIBIDO usar emoji" com exemplos de frases proibidas |
| L283 | Removido `(emoji 😊 opcional na saudação inicial)` da bolha da Rafa |
| L28 | Removido 😊 da frase fixa de proposta do concorrente |
| L495 | Removido 😊 do exemplo do iPad Neo |
| L45 e L54 | Removido 😄 das frases do Cenário A (concorrente) |

### Validação
✅ Nenhum emoji conversacional (😊, 😄, etc.) restante fora dos cards de orçamento
✅ Emojis de orçamento (📱, 💵, 💳, 🎨, 🔋, 📍) mantidos intactos
✅ Regra de proibição explicitada com exemplos no prompt
✅ Resto do comportamento da IA não afetado

### Impacto
- **Previne:** IA usando emoji no final de frases conversacionais
- **Melhora:** Tom mais profissional nas mensagens de texto
- **Mantém:** Emojis funcionais nos cards de orçamento (padrão da loja)

---

<!-- Cada mudança segue o padrão abaixo. Copie o bloco e preencha. -->

<!--
## Mudança #N - [Título resumido]

**Data:** DD/MM/AAAA - HH:MM
**Status:** ✅ EXECUTADO
**Versão:** vX.Y.Z
**Solicitante:** Cliente

### Descrição
[Descreva o que foi solicitado e por quê]

### Linhas Afetadas
Linhas XXX-YYY em `Vetor Imports.md`

### Validação
✅ [Critério 1]
✅ [Critério 2]

### Impacto
- **Previne:** ...
- **Melhora:** ...
- **Alinha:** ...

---
-->

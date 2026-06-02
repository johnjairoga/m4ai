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

## Mudança #2 - Remoção da Solicitação de Nome no Início do Atendimento

**Data:** 02/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.2
**Solicitante:** Cliente

### Descrição
A IA estava pedindo o nome do cliente logo na primeira interação (Cenário A e Cenário B da Apresentação Inicial), tornando a conversa travada e invasiva. O cliente solicitou que a IA siga diretamente com o atendimento (responder dúvidas, passar orçamentos, conduzir a conversa) sem solicitar o nome. O nome passou a ser coletado apenas nas etapas de fechamento: retirada, entrega, pedido, cadastro ou agendamento.

### Arquivos Afetados
`Vetor Imports.md` → `Vetor Imports_v1.0.2.md`

### Pontos Alterados

| Linha (v1.0.2) | Alteração |
|---|---|
| L165-166 | Removido "Nome (só na abertura)" das perguntas permitidas; adicionada regra de nome somente no fechamento |
| L175 | Removida exceção de duas perguntas (modelo + nome) no Cenário B |
| L255-260 | Substituída regra "pergunte o nome na primeira interação" por "NÃO pergunte o nome na abertura; somente no fechamento" |
| L268-273 | Cenário A: bolha "Qual é o seu nome?" substituída por "O que você busca?"; instrução atualizada |
| L281-286 | Cenário B: removida referência ao nome na descrição, removida exceção de 2 perguntas, removida bolha do nome do array |
| L296 | Removida cláusula "ainda pode pedir o nome em outra bolha" |
| L304-312 | Fluxo de segunda mensagem reescrito para não depender do nome; nome espontâneo tratado naturalmente |
| L324-341 | Exemplos de primeira mensagem: arrays e inline atualizados sem bolha do nome |
| L343-362 | Exemplos de segunda mensagem: reescritos para refletir o novo fluxo |

### Validação
✅ Nenhuma bolha "Qual é o seu nome?" ou "E qual é o seu nome?" nas primeiras interações
✅ Cenário A abre com "O que você busca?" em vez de pedir o nome
✅ Cenário B responde ao produto sem pedir o nome junto
✅ Nome espontâneo do cliente tratado com "Prazer, [nome]!" normalmente
✅ Nome ainda coletado no fechamento (retirada/entrega) — seção mantida intacta
✅ Orçamentos, VBT, redirecionamentos, emojis e demais seções não afetados

### Impacto
- **Previne:** IA pedindo nome logo no início, travando a conversa
- **Melhora:** Fluidez e naturalidade do atendimento inicial
- **Mantém:** Coleta de nome no fechamento (retirada, entrega, pedido, cadastro, agendamento)

---

## Mudança #3 - Nova Estrutura de Saudação Inicial (3 Bolhas Fixas)

**Data:** 02/06/2026 - 13:30
**Status:** ✅ EXECUTADO
**Versão:** v1.0.3
**Solicitante:** Cliente

### Descrição
A saudação inicial da Rafa foi reestruturada para seguir exatamente 3 bolhas fixas: `"Olá, Boa tarde! tudo bom?"` / `"Rafa aqui, muito prazer!"` / `"Como posso ajudar?"`. No Cenário B (cliente já pede produto na primeira mensagem), a terceira bolha é substituída pela confirmação do produto (ex: *"Trabalhamos com iPhone sim, qual você procura?"*), sem a bolha "Como posso ajudar?".

### Arquivos Afetados
`Vetor Imports.md` → `Vetor Imports_v1.0.3.md`

### Pontos Alterados

| Linha (v1.0.3) | Alteração |
|---|---|
| L269 | Cenário A — bolha 1: `"Boa tarde!"` → `"Olá, Boa tarde! tudo bom?"` |
| L271 | Cenário A — bolha 3: `"O que você busca?"` → `"Como posso ajudar?"` |
| L284 | Cenário B — bolha 1: `"Boa tarde!"` → `"Olá, Boa tarde! tudo bom?"` |
| L317 | Regra NUNCA: atualizado `"Boa tarde!"` → `"Olá, Boa tarde! tudo bom?"` |
| L329 | Exemplo JSON Cenário B: `"Boa tarde!"` → `"Olá, Boa tarde! tudo bom?"` |
| L337 | Exemplo inline Cenário B (iPhone): atualizado para nova bolha 1 |
| L341 | Exemplo inline Cenário A: bolha 1 e bolha 3 atualizadas |

### Validação
✅ Cenário A: 3 bolhas `"Olá, Boa tarde! tudo bom?"` + `"Rafa aqui, muito prazer!"` + `"Como posso ajudar?"`
✅ Cenário B: 2 bolhas fixas + bolha de confirmação do produto (sem "Como posso ajudar?")
✅ Todos os arrays `message` de exemplo atualizados
✅ Regra "NUNCA repita" atualizada para referenciar a nova saudação
✅ Nenhuma variação antiga (`"Boa tarde!"` isolado) restante na seção de apresentação

### Impacto
- **Previne:** IA usando saudação fragmentada ou sem "Olá" e "tudo bom?" na abertura
- **Melhora:** Consistência e cordialidade no primeiro contato com o cliente
- **Mantém:** Distinção entre Cenário A (3 bolhas) e Cenário B (2 bolhas fixas + produto)

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

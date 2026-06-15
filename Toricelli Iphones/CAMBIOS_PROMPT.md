# Registro de Mudanças — Toricelli Iphones

> Arquivo de controle de versões do prompt da assistente virtual Valentina (Toricelli iPhones — Bragança Paulista).
> **Regra:** nunca modificar o arquivo de versão anterior. Cada mudança gera um novo arquivo versionado.

---

## Mudança #1 — Versão inicial do prompt

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.0
**Solicitante:** Cliente

### Problema identificado
Projeto novo sem estrutura de versionamento. Necessidade de registrar o prompt original da assistente Valentina antes de aplicar ajustes solicitados pelo cliente.

### Solução
Criação da pasta do projeto com:
- `Prompt Original.md` — snapshot imutável do prompt recebido do cliente
- `Toricelli Iphones.md` — arquivo de trabalho (versão atual)
- `Toricelli Iphones_v1.0.0.md` — primeira versão versionada

### Arquivos afetados
- `Prompt Original.md` (criado)
- `Toricelli Iphones.md` (criado)
- `Toricelli Iphones_v1.0.0.md` (criado a partir do prompt original)

### Validação
✅ Prompt original preservado integralmente em `Prompt Original.md`
✅ Versão inicial v1.0.0 criada e registrada
✅ Estrutura alinhada ao padrão M4IA (versionamento + CAMBIOS_PROMPT.md)

### Impacto
- **Padroniza:** Controle de versões para o projeto Toricelli Iphones
- **Previne:** Perda do prompt base ao aplicar futuras modificações
- **Melhora:** Rastreabilidade de cada ajuste solicitado pelo cliente

---

## Mudança #2 — Formato de orçamento: quebras de linha e negrito no modelo

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.1
**Solicitante:** Cliente

### Problema identificado
Ao enviar orçamentos com vários modelos (ex.: opções dentro de uma faixa de preço), a IA usava `\n\n` entre modelo, valor à vista e parcelamento, gerando linhas em branco extras e poluição visual no WhatsApp — dificultando a leitura.

### Solução
Atualizada seção **FORMATO DE ORÇAMENTO PERSONALIZADO** com regra explícita de quebras de linha:
- **Modelo → à vista:** um único `\n` (sem linha em branco).
- **À vista → parcelado:** `\n\n` (uma linha em branco).
- **Entre blocos de modelos diferentes** no mesmo balão: `\n\n`.

Adicionada **exceção ao negrito** em **PROIBIÇÃO DE NEGRITO**: primeira linha de cada bloco de orçamento (`*iPhone X | Seminovo*`) em negrito.

Atualizados exemplos (padrão único, múltiplos modelos, variantes, parcelas antecipadas e JSON de saída Exemplo 2/2b) e lista de **PROIBIDO** com erros de formatação.

### Arquivos afetados
- `Toricelli Iphones_v1.0.1.md` (criado a partir de v1.0.0)
- `Toricelli Iphones.md` (arquivo de trabalho atualizado)

### Validação
✅ Padrão compacto modelo + à vista sem linha em branco intermediária
✅ Uma linha em branco apenas entre à vista e parcelamento
✅ Negrito obrigatório na linha do modelo
✅ v1.0.0 preservado intacto

### Impacto
- **Melhora:** Legibilidade dos orçamentos no WhatsApp
- **Padroniza:** Formato visual alinhado ao pedido do cliente (caso faixa R$ 2.600–3.100)

---

## Mudança #3 — Orçamento: três linhas compactas por modelo (sem linha em branco interna)

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.2
**Solicitante:** Cliente

### Problema identificado
Na v1.0.1 ainda havia linha em branco entre `Apenas R$... à vista` e `Ou Nx... no cartão` dentro do mesmo bloco de modelo. O cliente confirmou que **as três linhas devem ficar compactas**, sem espaço entre elas.

### Solução
Ajustada **REGRA DE QUEBRAS DE LINHA** em `## FORMATO DE ORÇAMENTO PERSONALIZADO`:
- Dentro do mesmo modelo: apenas `\n` entre modelo, à vista e parcelado — **zero** `\n\n` interno.
- `\n\n` permitido **somente** entre blocos de modelos diferentes no mesmo balão.

Padrão canônico por modelo:
```
*iPhone 14 128GB | Seminovo*
Apenas R$ 2.499,00 à vista 💰
Ou 12x R$ 238,82 no cartão 💳
```

Atualizados exemplos, lista **PROIBIDO** e JSON de saída (Exemplo 2/2b).

### Arquivos afetados
- `Toricelli Iphones_v1.0.2.md` (criado a partir de v1.0.1)
- `Toricelli Iphones.md` (arquivo de trabalho atualizado)

### Validação
✅ Três linhas consecutivas por modelo sem linha em branco interna
✅ Negrito mantido na linha do modelo
✅ v1.0.1 preservado intacto

### Impacto
- **Corrige:** Formatação final confirmada pelo cliente
- **Melhora:** Leitura mais limpa no WhatsApp

---

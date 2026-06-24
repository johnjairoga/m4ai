# Registro de Mudanças — iPhone Barato CG

> Arquivo de controle de versões do prompt da assistente virtual Júlia (iPhone Barato CG).
> **Regra:** nunca modificar o arquivo de versão anterior. Cada mudança gera um novo arquivo versionado.

---

## Mudança #1 — Versão inicial do prompt

**Data:** 24/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.0
**Solicitante:** Cliente

### Problema identificado
Projeto novo sem estrutura de versionamento. Necessidade de registrar o prompt original da assistente Júlia antes de aplicar ajustes solicitados pelo cliente.

### Solução
Criação da pasta do projeto com:
- `Prompt Original.md` — snapshot imutável do prompt recebido do cliente
- `Iphone Barato CG.md` — arquivo de trabalho (versão atual)
- `Iphone Barato CG_v1.0.0.md` — primeira versão versionada

### Arquivos afetados
- `Prompt Original.md` (criado)
- `Iphone Barato CG.md` (criado)
- `Iphone Barato CG_v1.0.0.md` (criado a partir do prompt original)

### Validação
✅ Prompt original preservado integralmente em `Prompt Original.md`
✅ Versão inicial v1.0.0 criada e registrada
✅ Estrutura alinhada ao padrão M4IA (versionamento + CAMBIOS_PROMPT.md)

### Impacto
- **Padroniza:** Controle de versões para o projeto iPhone Barato CG
- **Previne:** Perda do prompt base ao aplicar futuras modificações
- **Melhora:** Rastreabilidade de cada ajuste solicitado pelo cliente

---

## Mudança #2 — Estoque prevalece sobre política Apple (iPhone 11/12/13 e lacrados)

**Data:** 24/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.1
**Solicitante:** Cliente

### Problema identificado
A IA enviava automaticamente a mensagem *"Esse modelo a Apple não produz mais novo, inclusive recomendo tomar cuidado com golpes!"* com base no retorno de `aparelhos_disponiveis`, mesmo quando o `ESTOQUE` da loja tinha o aparelho **lacrado/novo** disponível — gerando informação errada e perda de venda. Ocorria especialmente em pedidos de iPhone 11, 12 e 13 e em modelos que a loja mantém em estoque (ex.: linha atual como iPhone 17 Pro Max).

### Solução
Reescrita da seção **PRÉ-REQUISITO OBRIGATÓRIO — `aparelhos_disponiveis`** com nova regra mestre: **`ESTOQUE` prevalece sobre política genérica da Apple**. Principais mudanças:
- Removida a mensagem canônica de golpe do fluxo obrigatório
- `aparelhos_disponiveis` passa a ser orientação; `ESTOQUE` define o que vender
- Nova **REGRA ESPECIAL — iPhone 11, 12 e 13**: consultar estoque lacrado e seminovo; vender o que tiver; priorizar alternativas lacradas do estoque (linha atual) antes de encaminhar
- Atualizadas seções **Política Apple**, **IDENTIFICAÇÃO DO INTERESSE**, **ORÇAMENTOS**, **VALORES** e checklist de orçamento

### Arquivos afetados
- `Iphone Barato CG_v1.0.1.md` (criado a partir de v1.0.0)
- `Iphone Barato CG.md` (arquivo de trabalho atualizado)

### Validação
✅ Proibido dizer que Apple não produz mais novo quando `ESTOQUE` tem lacrado
✅ Mensagem de golpe removida do fluxo obrigatório
✅ iPhone 11/12/13 com fluxo que prioriza estoque real e alternativas lacradas
✅ v1.0.0 preservado intacto

### Impacto
- **Corrige:** Informação incorreta sobre indisponibilidade de lacrados que existem no estoque
- **Previne:** Perda de venda por mensagens de descontinuação indevidas
- **Melhora:** Priorização de modelos disponíveis a pronta entrega (ex.: linha atual lacrada)

---

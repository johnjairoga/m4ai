# Registro de Mudanças — Vini Shop

> Arquivo de controle de versões do prompt da assistente virtual Carolina (Vinny Shop Celulares).
> **Regra:** nunca modificar o arquivo de versão anterior. Cada mudança gera um novo arquivo versionado.

---

## Mudança #1 — Versão inicial do prompt

**Data:** 26/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.0
**Solicitante:** Cliente

### Problema identificado
Projeto novo sem estrutura de versionamento. Necessidade de registrar o prompt original da assistente Carolina (Vinny Shop Celulares, Itajubá/MG) antes de aplicar futuros ajustes solicitados pelo cliente.

### Solução
Criação da pasta do projeto com:
- `Prompt Original.md` — snapshot imutável do prompt recebido do cliente
- `Vini Shop.md` — arquivo de trabalho (versão atual)
- `Vini Shop_v1.0.0.md` — primeira versão versionada

### Arquivos afetados
- `Prompt Original.md` (criado)
- `Vini Shop.md` (criado)
- `Vini Shop_v1.0.0.md` (criado a partir do prompt original)

### Validação
✅ Prompt original preservado integralmente em `Prompt Original.md`
✅ Versão inicial v1.0.0 criada e registrada
✅ Estrutura alinhada ao padrão M4IA (versionamento + CAMBIOS_PROMPT.md)
✅ Modelo B de redirecionamento (`departamento` JSON `vinnyshop` ≠ `id_loja` das tools)

### Impacto
- **Padroniza:** Controle de versões para o projeto Vini Shop
- **Previne:** Perda do prompt base ao aplicar futuras modificações
- **Melhora:** Rastreabilidade de cada ajuste solicitado pelo cliente

---

## Mudança #2 — Saudação temporal incorreta (boa noite no lugar de boa tarde)

**Data:** 26/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.1
**Solicitante:** Cliente

### Problema identificado
A IA respondeu "boa noite" quando o horário correto era "boa tarde". O prompt citava **`Dia e hora atual`** apenas de forma genérica, sem tabela de faixas horárias nem instrução para extrair a hora (`HH`) do campo injetado e ignorar o cumprimento do cliente.

### Solução
Nova seção **SAUDAÇÃO DINÂMICA POR HORÁRIO — OBRIGATÓRIA** com:
- Formato do campo injetado pelo n8n (`cccc, dd/LL/yyyy HH:mm:ss`, fuso `America/Sao_Paulo`)
- Tabela exata: bom dia 06–11, boa tarde 12–17, boa noite 18–23 e 00–05
- Regra inviolável de usar **somente** a hora do sistema, nunca espelhar o cliente
- Exemplos com `17:59` = boa tarde e `18:00` = boa noite
- Atualização da tabela de campos dinâmicos, **APRESENTAÇÃO INICIAL** e checklist
- Rodapé com expressão n8n de **`Dia e hora atual`**

### Arquivos afetados
- `Vini Shop_v1.0.1.md` (criado a partir de v1.0.0)
- `Vini Shop.md` (arquivo de trabalho atualizado)

### Validação
✅ Tabela horária explícita com faixas 06–11 / 12–17 / 18–23 e 00–05
✅ Proibição de espelhar saudação do cliente documentada com exemplos
✅ Campo n8n `Dia e hora atual` registrado no rodapé do prompt
✅ v1.0.0 preservado intacto

### Impacto
- **Corrige:** "Boa noite" fora do horário (ex.: à tarde, antes das 18h)
- **Previne:** Saudação baseada no texto do cliente em vez do horário injetado
- **Padroniza:** Mesma lógica de saudação dinâmica usada em outros projetos M4IA

---

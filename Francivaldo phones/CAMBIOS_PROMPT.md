# Registro de Mudanças — Francivaldo Phones

> Arquivo de controle de versões do prompt do agente de processamento de consultas de estoque (Francivaldo Phones).
> **Regra:** nunca modificar o arquivo de versão anterior. Cada mudança gera um novo arquivo versionado.

---

## Mudança #1 — Versão inicial do prompt

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.0
**Solicitante:** Cliente

### Problema identificado
Projeto novo sem estrutura de versionamento. Necessidade de registrar o prompt original do agente de processamento de consultas de estoque antes de aplicar ajustes solicitados pelo cliente.

### Solução
Criação da pasta do projeto com:
- `Prompt Original.md` — snapshot imutável do prompt recebido do cliente
- `Francivaldo Phones.md` — arquivo de trabalho (versão atual)
- `Francivaldo Phones_v1.0.0.md` — primeira versão versionada

### Arquivos afetados
- `Prompt Original.md` (criado)
- `Francivaldo Phones.md` (criado)
- `Francivaldo Phones_v1.0.0.md` (criado a partir do prompt original)

### Validação
✅ Prompt original preservado integralmente em `Prompt Original.md`
✅ Versão inicial v1.0.0 criada e registrada
✅ Estrutura alinhada ao padrão M4IA (versionamento + CAMBIOS_PROMPT.md)

### Impacto
- **Padroniza:** Controle de versões para o projeto Francivaldo Phones
- **Previne:** Perda do prompt base ao aplicar futuras modificações
- **Melhora:** Rastreabilidade de cada ajuste solicitado pelo cliente

---

## Mudança #2 — Identificação da loja (endereço e horário)

**Data:** 12/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.1
**Solicitante:** Cliente

### Problema identificado
O prompt não continha endereço nem horário de funcionamento da Francivaldo Phones em Oeiras, informações necessárias para orientar clientes sobre retirada na loja.

### Solução
Adicionada seção **Identificação da Loja — Francivaldo Phones** após **Sua Função**, com:
- Endereço: Praça Visconde da Parnaíba, nº 49, Centro de Oeiras
- Horário: Seg a sex 7h40–17h40 | Sáb e feriados 8h–12h40
- Modelo de referência para convite de retirada na loja (texto fornecido pelo cliente)

Atualizada seção **INFORMAÇÕES ADICIONAIS** no final do prompt com os mesmos dados da loja.

### Arquivos afetados
- `Francivaldo Phones_v1.0.1.md` (criado a partir de v1.0.0)
- `Francivaldo Phones.md` (arquivo de trabalho atualizado)

### Validação
✅ Endereço e horário inseridos conforme texto do cliente
✅ Modelo de mensagem de convite para retirada registrado como referência
✅ v1.0.0 preservado intacto

### Impacto
- **Padroniza:** Dados oficiais da loja no prompt
- **Melhora:** Base para orientar clientes sobre visita e retirada na loja

---

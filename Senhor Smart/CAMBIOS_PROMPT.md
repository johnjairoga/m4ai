# Registro de Mudanças — Senhor Smart

> Arquivo de controle de versões do prompt da assistente virtual Ana (Senhor Smart Brasília).
> **Regra:** nunca modificar o arquivo de versão anterior. Cada mudança gera um novo arquivo versionado.

---

## Mudança #1 — Versão inicial do prompt

**Data:** 24/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.0
**Solicitante:** Cliente

### Problema identificado
Projeto novo sem estrutura de versionamento. Necessidade de registrar o prompt inicial da assistente Ana (Senhor Smart Brasília) antes de aplicar futuros ajustes solicitados pelo cliente.

### Solução
Criação da pasta do projeto com:
- `Prompt Original.md` — snapshot imutável do prompt recebido do cliente
- `Senhor Smart.md` — arquivo de trabalho (versão atual)
- `Senhor Smart_v1.0.0.md` — primeira versão versionada

### Arquivos afetados
- `Prompt Original.md` (criado)
- `Senhor Smart.md` (criado)
- `Senhor Smart_v1.0.0.md` (criado a partir do prompt original)

### Validação
✅ Prompt original preservado integralmente em `Prompt Original.md`
✅ Versão inicial v1.0.0 criada e registrada
✅ Estrutura alinhada ao padrão M4IA (versionamento + CAMBIOS_PROMPT.md)
✅ `id_loja` MANUT configurado como `"970"` (Senhor Smart Brasília)

### Impacto
- **Padroniza:** Controle de versões para o projeto Senhor Smart
- **Previne:** Perda do prompt base ao aplicar futuras modificações
- **Melhora:** Rastreabilidade de cada ajuste solicitado pelo cliente

---

## Mudança #2 — Dúvidas sobre tipo de peça e procedimentos (objeção recorrente)

**Data:** 24/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.1
**Solicitante:** Cliente

### Problema identificado
Clientes frequentemente perguntam se, após a troca de tela ou bateria, o iPhone exibirá mensagem de "peça desconhecida" ou alerta de peça trocada. A IA não possuía argumentação definida para essa objeção recorrente do nicho e podia responder de forma genérica ou redirecionar indevidamente.

### Solução
Nova seção **7.3 — Dúvidas sobre tipo de peça e procedimentos (objeção recorrente)** em `# 7. Tipos de Peças e Regras Específicas`, com:
- Gatilhos de ativação (dúvidas sobre tipo de peça, procedimentos, alertas nos Ajustes, saúde da bateria)
- Três pilares obrigatórios: peças premium, manutenção da originalidade, ausência de alerta de peça trocada
- Respostas canônicas por cenário (bateria premium, tela premium, peça original, dúvida genérica, procedimento)
- Proibição de usar `especialistaTecnico` nestes casos
- Demais seções do prompt preservadas sem alteração

### Arquivos afetados
- `Senhor Smart_v1.0.1.md` (criado a partir de v1.0.0)
- `Senhor Smart.md` (arquivo de trabalho atualizado)

### Validação
✅ Seção 7.3 adicionada sem modificar outras seções
✅ Respostas canônicas alinhadas aos pilares: premium, manutenção da originalidade, sem alerta de peça desconhecida
✅ v1.0.0 preservado intacto

### Impacto
- **Corrige:** Falta de argumentação para dúvida recorrente sobre mensagem de peça trocada no iPhone
- **Melhora:** Respostas tranquilizadoras e técnicas sem redirecionamento desnecessário
- **Previne:** Uso indevido de `especialistaTecnico` quando a loja já tem resposta definida

---

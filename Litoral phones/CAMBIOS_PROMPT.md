# Registro de Mudanças — Litoral Phones

> Arquivo de controle de versões do prompt da assistente virtual Iza (Litoral Phones).
> **Regra:** nunca modificar o arquivo de versão anterior. Cada mudança gera um novo arquivo versionado.

---

## Mudança #1 — Versão inicial do prompt

**Data:** 19/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.0
**Solicitante:** Cliente

### Problema identificado
Projeto novo sem estrutura de versionamento. Necessidade de registrar o prompt original da assistente Iza antes de aplicar ajustes solicitados pelo cliente.

### Solução
Criação da pasta do projeto com:
- `Prompt Original.md` — snapshot imutável do prompt recebido do cliente
- `Litoral Phones.md` — arquivo de trabalho (versão atual)
- `Litoral Phones_v1.0.0.md` — primeira versão versionada

### Arquivos afetados
- `Prompt Original.md` (criado)
- `Litoral Phones.md` (criado)
- `Litoral Phones_v1.0.0.md` (criado a partir do prompt original)

### Validação
✅ Prompt original preservado integralmente em `Prompt Original.md`
✅ Versão inicial v1.0.0 criada e registrada
✅ Estrutura alinhada ao padrão M4IA (versionamento + CAMBIOS_PROMPT.md)

### Impacto
- **Padroniza:** Controle de versões para o projeto Litoral Phones
- **Previne:** Perda do prompt base ao aplicar futuras modificações
- **Melhora:** Rastreabilidade de cada ajuste solicitado pelo cliente

---

## Mudança #2 — Modelo indisponível: alternativas próximas em vez de encaminhar ao estoque

**Data:** 19/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.1
**Solicitante:** Cliente

### Problema identificado
Quando o cliente pedia um modelo que não vinha no retorno do `ESTOQUE`, a Iza respondia automaticamente com "Me dá um momento, vou encaminhar para o pessoal do estoque confirmar o preço para você 😉", sem oferecer modelos parecidos que estavam a pronta entrega — gerando espera inútil e perda de oportunidade de venda.

### Solução
Reescrita da seção **REGRA DE INDISPONIBILIDADE (UNIVERSAL)** com fluxo em 3 passos:
1. Buscar alternativas próximas no `ESTOQUE` antes de qualquer encaminhamento
2. Se houver alternativa: informar que o modelo pedido não está disponível e oferecer 1–2 opções próximas a pronta entrega (modelo de referência do cliente, ex. 16 Pro → 16 Pro Max / 17 Pro)
3. Se não houver alternativa: handoff real via **Redirecionamentos** — proibida a frase de espera falsa

Atualizados também **Redirecionamentos** (item 1) e **CTA** (contexto pós-alternativas vs handoff).

### Arquivos afetados
- `Litoral Phones_v1.0.1.md` (criado a partir de v1.0.0)
- `Litoral Phones.md` (arquivo de trabalho atualizado)

### Validação
✅ Regra exige clareza sobre indisponibilidade do modelo pedido
✅ Obrigatoriedade de buscar e oferecer alternativas do `ESTOQUE` antes de encaminhar
✅ Proibição explícita da frase "vou encaminhar pro estoque confirmar o preço" como resposta automática
✅ Modelo de mensagem cadastrado conforme exemplo do cliente
✅ v1.0.0 preservado intacto

### Impacto
- **Corrige:** Resposta genérica de encaminhamento quando há modelos parecidos disponíveis
- **Melhora:** Conversão com alternativas a pronta entrega no mesmo atendimento
- **Previne:** Falso handoff / frase de espera sem ação real

---
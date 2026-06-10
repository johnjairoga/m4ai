# Registro de Mudanças — Cell Phone Store

> Arquivo de controle de versões do prompt da assistente virtual Luiza (CellPhone Store — Arapiraca).
> **Regra:** nunca modificar o arquivo de versão anterior. Cada mudança gera um novo arquivo versionado.

---

## Mudança #1 - Versão inicial do prompt

**Data:** 08/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.0
**Solicitante:** Cliente

### Descrição
Criação do prompt inicial da assistente virtual Luiza para a CellPhone Store (Arapiraca, AL).

### Funcionalidades implementadas
- Persona: Luiza, assistente virtual da CellPhone Store
- Formato de saída JSON com `message[]` (uma bolha WhatsApp por elemento do array)
- Campos obrigatórios: `departamento`, `resumo`, `redirecionamento`
- Medida de segurança e bloqueio anti-injeção de prompt
- Bloqueio absoluto — nunca cobrir preços da concorrência
- Prioridade seminovos (maior estoque da loja)
- Verificação de primeiro contato e saudação contextual
- Fluxo de disponibilidade: `tem iphone X?`, `chegou?`, reposição
- Tools: `aparelhos_disponiveis`, `ESTOQUE`, `TAXAS_MAQ`, `FUNCIONAMENTO_LOJA`, `analise_vbt`
- Pré-check de modelos (iPhone 16e, MacBook, capacidades válidas)
- Cliente pediu novo/lacrado mas só há seminovo — resposta padrão em 4 bolhas
- Indisponibilidade de produtos (valor-alvo, capacidade específica, handoff ao estoque)
- Orçamentos com placeholders substituídos por dados reais da tool
- Parcelamento (1–18x), reserva com sinal, PIX, links de pagamento
- VBT completo (triagem, checklist, múltiplos aparelhos, peças trocadas vs defeitos)
- Fotos e vídeos de aparelhos (URL do ESTOQUE ou redirecionamento `foto_video`)
- Redirecionamentos mapeados: `setor_responsavel`, `verificar_disponibilidade`, `suporte_garantia`, `foto_video`, `reserva`, `pedido_entrega`, `vbt`
- Garantia: 1 ano no aparelho + 1 ano no cabo e carregador
- Fechamento de venda, entrega, objeções e finalização sem venda

### Arquivos criados
- `Cell Phone Store_v1.0.0.md` — prompt inicial completo

---

## Mudança #2 - Modelo indisponível: oferecer alternativa antes de redirecionar

**Data:** 10/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.1
**Solicitante:** Cliente

### Problema identificado
Quando o modelo/capacidade solicitado pelo cliente **não constava no `ESTOQUE`**, a IA redirecionava ao setor de estoque (`verificar_disponibilidade`) como **primeira ação**, sem consultar tools e sem oferecer modelos mais próximos disponíveis.

**Caso crítico:** seção **"CHEGOU?" / REPOSIÇÃO** mandava handoff imediato quando o pedido exato não aparecia no `ESTOQUE` — mesmo quando havia alternativas próximas (ex.: outra capacidade do mesmo modelo).

Outras seções conflitantes:
- Fluxo de Qualificação (passo 5): *"Se não constar: Encaminhar ao estoque"*
- ORÇAMENTOS - REGRA CRÍTICA #1 e FLUXO OBRIGATÓRIO DE QUALIFICAÇÃO: *"Seguir regra de redirecionamento obrigatório"* sem priorizar alternativas

### Solução

#### 1. Nova seção — MODELO NÃO DISPONÍVEL — OFERECER ALTERNATIVA ANTES DE REDIRECIONAR

Adicionada após **PRIORIDADE SEMINOVOS** com prioridade máxima:

**Fluxo obrigatório quando o pedido exato não está no `ESTOQUE`:**
1. Ativar tools (`aparelhos_disponiveis` + `ESTOQUE`)
2. Buscar modelos mais próximos — prioridade:
   - Mesmo modelo em outra capacidade
   - Mesma linha em variante próxima (14 vs 14 Plus, Pro vs base)
   - Geração adjacente (15 quando pediu 16, etc.)
3. Apresentar 1–2 alternativas com preço real + CTA
4. `redirecionamento`: `false` neste turno

**Handoff só se:** cliente insiste no exato, pede verificar chegada, ou não há opção razoavelmente próxima.

#### 2. Seção "CHEGOU?" / REPOSIÇÃO — corrigida

- Removido handoff imediato quando `ESTOQUE` vazio
- Novo fluxo: informar indisponibilidade do exato → oferecer alternativa → CTA (detalhar ou verificar chegada)
- Novo exemplo JSON com 14 Pro Max 128GB como alternativa ao 256GB pedido

#### 3. Seções alinhadas

| Seção | Mudança |
|---|---|
| PERGUNTA DE DISPONIBILIDADE | Exceção de handoff atualizada — só após alternativas |
| Fluxo de Qualificação (passo 5) | Oferecer alternativa antes de encaminhar |
| ORÇAMENTOS - REGRA CRÍTICA #1 | Idem |
| FLUXO OBRIGATÓRIO DE QUALIFICAÇÃO | Idem |
| INDISPONIBILIDADE DE PRODUTOS | Referência cruzada à nova regra no topo |

### Arquivos afetados
- `Cell Phone Store_v1.0.1.md` (criado a partir de v1.0.0 — não modifica v1.0.0)

### Validação
✅ Nova regra com fluxo explícito de busca de modelos mais próximos no `ESTOQUE`
✅ Proibição de redirecionar sem consultar tools e sem oferecer alternativa
✅ "CHEGOU?" com exemplo JSON alinhado ao novo fluxo
✅ Seções conflitantes atualizadas — sem "Encaminhar ao estoque" como primeira ação
✅ Handoff mantido para insistência, verificar chegada e zero alternativas
✅ Compatível com INDISPONIBILIDADE existente (valor-alvo, capacidade específica)
✅ Tudo em português do Brasil

### Impacto
- **Previne:** Handoff prematuro quando há seminovos próximos no estoque
- **Melhora:** Conversão — cliente vê opção real antes de ir ao humano
- **Alinha:** Todas as seções que mencionavam redirecionamento ao estoque
- **Garante:** `verificar_disponibilidade` como último recurso, não primeira resposta

---

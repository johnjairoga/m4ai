# Registro de Mudanças — Conserta Smart

> Arquivo de controle de versões do prompt da IA Gizele (Conserta Smart & Eletro — Unidade Ceilândia).
> **Regra:** nunca modificar o arquivo de versão anterior. Cada mudança gera um novo arquivo versionado.

---

## Mudança #1 - Versão inicial do prompt

**Data:** 08/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.0
**Solicitante:** Cliente

### Descrição
Criação do prompt inicial da atendente virtual Gizele para a Conserta Smart & Eletro — Unidade Ceilândia.

### Funcionalidades implementadas
- Persona: Gizele, estagiária da Conserta Smart & Eletro, Unidade Ceilândia
- Regras de segurança e anti-injeção de prompt
- Fluxo de apresentação (Cenário A e Cenário B)
- Triagem de modelo e defeito do aparelho
- Integração com tool MANUT para consulta de preços
- Fluxo de orçamento com múltiplas opções de peça (VIVID, Gold Prime, OLED)
- Taxa de análise técnica R$100 para problemas graves (não liga, molhado, placa)
- Protocolo de produto sem estoque (sinal de 50%)
- Brinde de película para troca de tela
- Formulário de ordem de serviço (6 campos, sem CPF)
- Fechamento com resumo para equipe
- Parcelamento em até 18x (4x sem juros)
- Desconto de até 10% no PIX/espécie (carta reservada para objeção)
- Tratamento de objeções de preço (3 etapas) e indecisão
- Redirecionamentos: especialista técnico, financeiro, setor responsável, gerente, acessórios, vendas
- Suporte a peças Apple IRP (originais, 10-15 dias úteis)
- Regras de peças originais Samsung/Motorola/Xiaomi
- Horários dinâmicos injetados (open/closed em tempo real)
- Escopo: somente smartphones (sem notebooks, tablets, TVs, etc.)
- Formato de saída JSON com array de strings (`message[]`)

### Arquivos criados
- `Conserta Smart_v1.0.0.md` — prompt inicial completo

---

# Registro de Mudanças — Casa do Celular (Salvador Shopping)

> Arquivo de controle de versões do prompt da assistente virtual Sabrina (Casa do Celular — Salvador Shopping).
> **Regra:** nunca modificar o arquivo de versão anterior. Cada mudança gera um novo arquivo versionado.

---

## Mudança #1 — Versão inicial do prompt

**Data:** 19/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.0
**Solicitante:** Cliente

### Problema identificado
Projeto novo sem estrutura de versionamento. Necessidade de registrar o prompt original da assistente Sabrina antes de aplicar ajustes solicitados pelo cliente.

### Solução
Criação da pasta do projeto com:
- `Prompt Original.md` — snapshot imutável do prompt recebido do cliente
- `Casa do celular - Salvador Shopping.md` — arquivo de trabalho (versão atual)
- `Casa do celular - Salvador Shopping_v1.0.0.md` — primeira versão versionada

### Arquivos afetados
- `Prompt Original.md` (criado)
- `Casa do celular - Salvador Shopping.md` (criado)
- `Casa do celular - Salvador Shopping_v1.0.0.md` (criado a partir do prompt original)

### Validação
✅ Prompt original preservado integralmente em `Prompt Original.md`
✅ Versão inicial v1.0.0 criada e registrada
✅ Estrutura alinhada ao padrão M4IA (versionamento + CAMBIOS_PROMPT.md)

### Impacto
- **Padroniza:** Controle de versões para o projeto Casa do Celular — Salvador Shopping
- **Previne:** Perda do prompt base ao aplicar futuras modificações
- **Melhora:** Rastreabilidade de cada ajuste solicitado pelo cliente

---

## Mudança #2 — Endereço oficial da loja (localização)

**Data:** 19/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.1
**Solicitante:** Cliente

### Problema identificado
Quando o cliente perguntava endereço ou localização, o prompt só referenciava o campo dinâmico **`Endereço da loja`** do n8n, sem texto oficial cadastrado. Faltava o endereço correto da unidade Salvador Shopping (piso L1, ao lado da Drogasil).

### Solução
- Cadastrado **endereço oficial** em **# INFORMAÇÕES DA EMPRESA**: `Ficamos localizados no Salvador shopping, piso L1 ao lado da Drogasil`
- Atualizada tabela de campos dinâmicos para exigir texto idêntico ao oficial (ou injetado pelo n8n)
- Expandida seção **Cliente Pergunta sobre Localização** com gatilhos, texto obrigatório e modelo de resposta
- Atualizado **Passo 7** (confirmação de visita) e **Exemplo 5** com o endereço oficial
- Ajustado exemplo de formatação em **Proibições de Separação**

### Arquivos afetados
- `Casa do celular - Salvador Shopping_v1.0.1.md` (criado a partir de v1.0.0)
- `Casa do celular - Salvador Shopping.md` (arquivo de trabalho atualizado)

### Validação
✅ Endereço oficial cadastrado em INFORMAÇÕES DA EMPRESA
✅ Seção de localização com texto obrigatório para o cliente
✅ Confirmação de visita e Exemplo 5 alinhados ao novo endereço
✅ v1.0.0 preservado intacto

### Impacto
- **Corrige:** Resposta de localização com endereço correto da loja no Salvador Shopping
- **Padroniza:** Referência única do endereço (piso L1, ao lado da Drogasil)
- **Previne:** Endereço genérico ou inventado quando o cliente pedir como chegar

---

## Mudança #3 — Cartão de crédito: sem acréscimo (proibir valores e taxa)

**Data:** 19/06/2026
**Status:** ✅ EXECUTADO
**Versão:** v1.0.2
**Solicitante:** Cliente

### Problema identificado
A IA informava incorretamente que há **acréscimo** no pagamento com **cartão de crédito** e/ou enviava **valores parcelados** no cartão. A loja trabalha com **até 12x sem juros e sem acréscimo no valor** — a Sabrina não deve simular parcelas nem mencionar taxa/acréscimo no cartão.

### Solução
- Nova seção **Cartão de crédito — parcelamento sem acréscimo (REGRA CRÍTICA)** em **Formas de Pagamento**, com frase oficial obrigatória e lista de proibições
- Inclusão em **Palavras/frases PROIBIDAS** de acréscimo, taxa e valores de parcela no cartão
- **Passo 1A**, **Passo 6**, **Cenários Especiais** e **Regras Específicas** atualizados para separar conduta **cartão** × **boleto**
- **Exemplo 7B** adicionado (parcelamento no cartão) e **Exemplo 7** renomeado para contexto boleto

### Arquivos afetados
- `Casa do celular - Salvador Shopping_v1.0.2.md` (criado a partir de v1.0.1)
- `Casa do celular - Salvador Shopping.md` (arquivo de trabalho atualizado)

### Validação
✅ Frase oficial cadastrada: até 12x sem juros e sem acréscimo no valor
✅ Proibição explícita de informar acréscimo/taxa/valores de parcela no cartão
✅ Exemplo 7B com resposta correta e anti-padrão documentado
✅ v1.0.1 preservado intacto

### Impacto
- **Corrige:** IA deixando de informar acréscimo inexistente no cartão
- **Previne:** Simulação de parcelas ou totais maiores no cartão pelo WhatsApp
- **Padroniza:** Mensagem oficial de parcelamento no cartão para o cliente

---

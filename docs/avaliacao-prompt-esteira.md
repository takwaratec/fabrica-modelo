# 🔍 Avaliação do Prompt — Esteira de Ingestão, ChromaDB e Sincronização

> **Prompt avaliado em:** 02/07/2026
> **Solicitante:** Fabio Takwara
> **Status:** ⏳ Aguardando autorização para salvar

---

## ✅ Pontos Fortes

| Aspecto | Por que é bom |
|---------|---------------|
| **Estrutura em 3 etapas** | Clara, sequencial, cada etapa com entregável definido |
| **ChromaDB com metadados** | Schema de metadados bem pensado — permitirá filtragem por aba de menu e tags |
| **Merge entre contas GitHub** | Identificar duplicatas entre RESC e Takwara-Tech é necessário |
| **Atualização de links quebrados** | Problema real — muitos links apontam para árvores antigas |

---

## ⚠️ Pontos de Atenção — Ajustar Antes de Rodar

### 1. Etapa 1 — Esteira de PDFs

| Problema | Risco | Correção Sugerida |
|----------|-------|-------------------|
| **"OCR/Layout Analysis" como padrão** | Lento e desnecessário para PDFs com texto selecionável | Usar PyMuPDF primeiro; fallback para OCR se texto < 100 chars |
| **Renomear para SCI_000_*** | Conflito com nomenclatura existente do Acervo (resenha-*, ficha-*, perfil-*) | SCI_* é usado apenas para MQTF. Para o restante, manter `resenha-` ou `ficha-` |
| **Não menciona a trava jurídica** | Risco de indexar material sem DOI/ISBN e violar direitos autorais | Incluir filtro obrigatório: só indexar se tiver DOI/ISBN/ISSN OU for exceção do autor (Fabio/MQTF) |
| **"Extrair Título, Autores, Ano, Resumo, Conclusões"** | Muito ambicioso para extração automática — a qualidade varia muito | Extrair o que for possível; marcar campos não extraídos como `⏳ Pendente` |

### 2. Etapa 2 — ChromaDB

| Problema | Risco | Correção Sugerida |
|----------|-------|-------------------|
| **text-embedding-ada-002 (OpenAI)** | API paga, depende de internet, chave necessária | Usar `sentence-transformers/all-MiniLM-L6-v2` (local, gratuito, 384 dims) |
| **Coleção "acervo_takwara_tech"** | Nome diferente do planejado anteriormente | Unificar: qual o nome definitivo da coleção? |
| **Metadados ricos** | ✅ Bom, mas faltam campos de auditoria | Adicionar: `data_extracao`, `chromadb_version`, `hash_documento` |

### 3. Etapa 3 — Sincronização RESC → Takwara-Tech

| Problema | Risco | Correção Sugerida |
|----------|-------|-------------------|
| **"Mapeie o histórico na conta RESC"** | Requer acesso à conta GitHub `resck` — é necessário autenticação | Confirmar se temos acesso de leitura ao repo. Se não, esta etapa está bloqueada |
| **Merge automático** | Pode sobrescrever versões com anotações manuais | Sempre manter ambos os arquivos; o merge deve gerar um terceiro arquivo com flag `merged_from: [origem1, origem2]` |
| **Atualizar links quebrados** | Operação destrutiva se errar o padrão de busca | Gerar relatório de links quebrados primeiro; depois aplicar correções com `sed` em lote |

---

## 📋 Plano de Ação Recomendado

Com base na avaliação, sugiro executar nesta ordem:

### Agora (já rodou — Fase 1 MVP) ✅
- [x] Varredura do diretório `/Prêmio Zayed 2025/` (86 PDFs)
- [x] Filtro por código de registro (32 aceitos / 53 descartados)
- [x] Fichas no método Cavichiolli (8 seções) com disclaimer

### Fase 2A — ChromaDB (próximo passo) ⏳
- [ ] Instalar `chromadb` + `sentence-transformers` no ambiente
- [ ] Criar coleção `acervo_cientifico` (ou outro nome definitivo)
- [ ] Injetar as 32 fichas com metadados
- [ ] Testar consulta semântica

### Fase 2B — Google Drives ⏳
- [ ] Mapear diretórios montados do Google Drive
- [ ] Aplicar mesma esteira (filtro → extração → ficha → ChromaDB)

### Fase 3 — Sincronização RESC → Takwara-Tech ⏳
- [ ] Confirmar acesso ao GitHub RESC
- [ ] Mapear duplicatas
- [ ] Gerar relatório de links quebrados
- [ ] Aplicar correções

---

## ❓ Perguntas para decidir antes de salvar

1. **Nome da coleção ChromaDB:** `acervo_takwara_tech` (como no prompt) ou `acervo_cientifico` (como planejado anteriormente)?
2. **Modelo de embedding:** Pago (OpenAI ada-002) ou local gratuito (sentence-transformers)?
3. **Acesso ao RESC:** Você tem acesso de leitura ao GitHub `resck`? Se sim, qual repo?
4. **Trava jurídica:** Incluir o filtro DOI/ISBN obrigatório no prompt final?

---

**Aguardando sua resposta para salvar a versão ajustada do prompt.**

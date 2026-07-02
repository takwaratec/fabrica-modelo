# 🏗️ Arquitetura da Esteira Local — HD + Google Drives
## Pipeline de Ingestão, Filtragem e Catalogação de Documentos

> **Propósito:** Pipeline automatizada para varrer HD local e Google Drives, filtrar PDFs por código de registro (DOI/ISBN/ISSN/CID/Zenodo), extrair texto e gerar fichas técnicas Markdown no Acervo Científico.
> **Política:** Read-Only + Cópia Controlada — jamais mover ou deletar originais.
> **Data:** Julho/2026

---

## 1. Visão Geral do Fluxo

```
[HD Local] ──┐
              ├──→ 1. VARREDURA ──→ 2. FILTRO JURÍDICO ──→ 3. CATEGORIZAÇÃO ──→ 4. EXTRAÇÃO ──→ [Acervo .md]
[Google Drive] ─┘         │                    │                    │                      │
                          │                    ▼                    │                      ▼
                          │             [Descarte]                  │               [ChromaDB]
                          │            (sem DOI etc)                │
                          ▼                                         ▼
                   [Exceção do Autor]                      [Menu Vercel]
                   (Fabio / MQTF)
```

---

## 2. Etapas Detalhadas

### Etapa 1: Varredura de Segurança (Scan)

**O quê:** Escanear pastas locais e diretórios montados do Google Drive.

**Entrada:** Diretórios configuráveis (HD local + paths do Google Drive montado via rclone/Google Drive for Desktop).

**Saída:** Lista de arquivos PDF com metadados básicos (caminho, tamanho, data de modificação).

**Regras:**
- ✅ Apenas arquivos `.pdf` (case-insensitive)
- ✅ Ignorar diretórios de sistema (`.git/`, `node_modules/`, `__pycache__/`)
- ✅ Ignorar arquivos < 1KB (provavelmente corrompidos ou vazios)
- ⚠️ **Read-Only**: nunca mover ou deletar os originais

### Etapa 2: Filtro Jurídico (Trava de Direitos Autorais)

**O quê:** Ler cada PDF, extrair texto (via PyMuPDF) e buscar por padrões de registro.

**Padrões regex:**

| Código | Padrão | Exemplo |
|--------|--------|---------|
| **DOI** | `10\.\d{4,}/[a-zA-Z0-9._/-]+` | 10.1007/s10570-019-02289-0 |
| **ISBN** | `(?:ISBN[\s\-]*(?:978[\s\-]*)?)?(?:\d[\s\-]*){10,13}` | 978-85-12345-67-8 |
| **ISSN** | `\d{4}-\d{3}[\dxX]` | 0103-5053 |
| **CID** | `CID\s*\d+` | CID-10 F32 |
| **Zenodo DOI** | `10\.5281/zenodo\.\d+` | 10.5281/zenodo.18827106 |

**Se NENHUM dos padrões for encontrado:**
- ⛔ Descartar da catalogação pública
- Registrar em log de descarte (para auditoria)

**Exceção única:** O documento é aceito mesmo sem código se:
- Conteúdo contiver `Fabio Fernandes Resck` ou `Fabio Takwara`
- OU fizer parte do acervo digital **MQTF / Bioeconomia na Amazônia** (identificado por palavra-chave no nome do arquivo ou caminho)

### Etapa 3: Categorização por Mentor

Após aprovação no filtro, classificar por palavras-chave no texto:

| Mentor / Autor | Menu Vercel | Palavras-chave |
|----------------|-------------|----------------|
| Bill Mollison, David Holmgren | `02_permacultura_ao_pe_da_letra` | "Bill Mollison", "David Holmgren", "permacultura" |
| Oscar Hidalgo, Johan van Lengen | `02_bioconstrucao_e_arquitetura_descalca` | "Oscar Hidalgo", "Johan van Lengen", "bambu the gift of the gods", "arquiteto descalço" |
| Paulo Freire, Darcy Ribeiro, Milton Santos, Marilena Chauí | `03_governanca_e_tecnologia_social` | "Paulo Freire", "Darcy Ribeiro", "Milton Santos", "Marilena Chauí" |
| Ailton Krenak, Eduardo Bueno | `05_literatura_e_historia_de_resistencia` | "Ailton Krenak", "Eduardo Bueno", "Buenas Ideias" |

**Fallback:** Se nenhum mentor for identificado, classificar como `00_outros` para revisão manual.

### Etapa 4: Extração e Geração de Ficha

Para cada PDF aceito:
1. Extrair texto completo com PyMuPDF (`fitz`)
2. Gerar ficha técnica Markdown (.md) com:
   - Bibliografia formal do autor
   - Sumário gerado por IA (resumo do conteúdo extraído)
   - Link público de referência (Amazon, repositório institucional, DOI)
3. Salvar no diretório correspondente do Acervo Científico
4. Injetar vetor no ChromaDB (para busca semântica futura)

---

## 3. Análise Crítica

### Pontos Fortes da Arquitetura

| Aspecto | Por que é bom |
|---------|---------------|
| **Read-Only** | Elimina risco de perda de dados — política correta |
| **Trava jurídica** | Protege o acervo contra problemas de direitos autorais |
| **Exceção do autor** | Permite catalogar produção própria sem DOI |
| **Categorização automática** | Reduz trabalho manual de classificação |
| **ChromaDB** | Busca semântica futura sobre o acervo completo |

### Riscos e Contrapontos

| Risco | Gravidade | Mitigação |
|-------|:---------:|-----------|
| **Falso negativo no DOI** (OCR falha, PDF escaneado sem texto) | Alta | Incluir fallback: se PyMuPDF extrair <100 chars, tentar OCR com marker-pdf ou OCRmyPDF |
| **Falso positivo no filtro** (DOI falso em referência bibliográfica dentro do PDF, não do documento em si) | Média | O DOI deve estar no **cabeçalho ou primeira página** do PDF — limitar busca às primeiras 5 páginas |
| **Google Drive montado nem sempre disponível** | Média | Implementar verificação de montagem antes de escanear; log de erro claro |
| **Volume de dados** (potencialmente milhares de PDFs) | Baixa | Processamento em lote com checkpoint (salvar progresso a cada N arquivos) |
| **Qualidade da extração de texto** | Média | Aceitar extração parcial; marcar fichas como `status: extração preliminar` |
| **Categorização por palavra-chave pode colocar no menu errado** | Baixa | Sempre incluir campo `categoria: [automatica]` + permitir revisão manual posterior |
| **Chromadb: vetor sem contexto perde qualidade** | Média | Injetar não só o texto bruto mas o chunk com seção identificada (ex: "Resumo: ...", "Metodologia: ...") |

### Observações sobre a Implementação

1. **Rclone vs Google Drive for Desktop:** O Google Drive for Desktop monta em `/Volumes/GoogleDrive/` no macOS. Rclone pode montar como `mount` ou `rclone serve`. Ambos funcionam, mas o caminho de montagem precisa ser configurável.

2. **PyMuPDF vs Marker-pdf:** PyMuPDF é rápido para PDFs com texto selecionável. Para PDFs escaneados, marker-pdf tem melhor precisão mas é mais lento. Sugiro: tentar PyMuPDF primeiro; se texto < 100 chars, enfileirar para OCR (processamento off-line).

3. **ChromaDB:** O banco vetorial precisa de:
   - Collection name: `acervo-cientifico`
   - Embedding function: `sentence-transformers/all-MiniLM-L6-v2` (local, gratuito)
   - Metadata: `{doi, autor, categoria, arquivo, data_extracao}`

4. **Performance:** PDFs grandes (livros de 700 páginas) podem levar minutos para extrair. Sugiro timeout de 120s por arquivo e processamento paralelo com `ThreadPoolExecutor(max_workers=4)`.

---

## 4. Plano de Implementação Sugerido

### Fase 1 — Prova de Conceito (MVP) ⏰ 1-2 dias
- [ ] Script de varredura local apenas (HD, não Google Drive)
- [ ] Filtro regex para DOI/ISBN/ISSN
- [ ] Extração com PyMuPDF
- [ ] Geração de ficha .md mínima (identificação + resumo)
- [ ] Log de processamento

### Fase 2 — Google Drive + ChromaDB ⏰ 2-3 dias
- [ ] Montagem e varredura do Google Drive
- [ ] Injeção de vetores no ChromaDB
- [ ] Tratamento de PDFs escaneados (fallback OCR)
- [ ] Checkpoint e retomada

### Fase 3 — Categorização e Menu ⏰ 1-2 dias
- [ ] Classificador de mentores por palavra-chave
- [ ] Geração completa de ficha (8 seções + disclaimer Cavichiolli)
- [ ] Organização nos diretórios do Acervo

### Fase 4 — Refinamento ⏰ Contínuo
- [ ] Relatório de estatísticas (aceitos vs descartados)
- [ ] Interface de revisão manual
- [ ] Tratamento de edge cases

---

## 5. Pré-requisitos Técnicos

| Requisito | Versão | Instalado? |
|-----------|--------|:----------:|
| Python 3 | 3.10+ | ✅ (miniconda3) |
| PyMuPDF | 1.23+ | ✅ |
| chromadb | 0.4+ | ❌ Verificar |
| sentence-transformers | 2.2+ | ❌ Verificar |
| rclone | 1.60+ | ❌ Verificar |
| marker-pdf (opcional) | — | ❌ |

---

## 6. Conclusão e Recomendação

A arquitetura proposta é **sólida e bem estruturada**. A política Read-Only elimina o principal risco. A trava jurídica por código de registro é uma salvaguarda inteligente contra problemas de direitos autorais.

**Recomendo:**
1. ✅ **Aceitar a arquitetura como proposta**
2. ⏸️ **Não executar o script automaticamente** — iniciar com Fase 1 (prova de conceito) em um diretório pequeno de teste
3. 🔍 **Validar manualmente** os primeiros 10 resultados antes de escalar
4. 📝 **Definir prioridade** dos diretórios a varrer (começar pelo mais urgente)

Aguardando sua autorização para iniciar a **Fase 1 — Prova de Conceito**.

---

*Documento de arquitetura gerado em 02/07/2026 · Projeto Fábrica Modelo*

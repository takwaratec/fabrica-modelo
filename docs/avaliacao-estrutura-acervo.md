# 🔍 Avaliação e Sugestões — Estrutura do Acervo

## Proposta Original (sua grade)

```
📂 acervo-soberania-tecnologica/
├── 📂 01_polimeros-vegetais-e-biocompositos/      ← 421 fichas
├── 📂 02_bambu-estrutural-e-tratamentos/           ← 119 fichas
├── 📂 03_habitacao-social-e-athis/                 ← 65 fichas
├── 📂 .agent-instructions/                         ← Novo ✅
└── 📄 README.md
```

---

## ✅ O que está bom

| Aspecto | Motivo |
|---------|--------|
| **Nomes descritivos** | `polimeros-vegetais-e-biocompositos` é mais informativo que `nucleo-tecnologico` |
| **.agent-instructions/** | Essencial para reprodutibilidade — prompts prontos para copiar e colar |
| **Prefixo SCI_** | Já usado no MQTF, padronização mantida |
| **README freiriano** | Alinhado com a filosofia do projeto |
| **3 pastas principais** | Reduz complexidade, mais navegável que 17 eixos atuais |

---

## ⚠️ Pontos de atenção e sugestões

### 1. Faltam 2 áreas com volume significativo

| Conteúdo | Fichas | Onde colocar? |
|----------|:------:|---------------|
| Certificações (ITecons, IPT, NBR, ABNT) | 21 | Sem pasta clara — pode ir pra 01 ou 03 |
| Perfis de pesquisadores + literatura | 69 | Sem pasta clara — pode ir pra 02 ou `.agent-instructions` |

**Sugestão:** Adicionar uma **4ª pasta** ou realocar:

```
├── 📂 04_certificacoes-e-normas/                   ← 21 fichas (ITecons, IPT, NBR, ABNT)
├── 📂 05_perfis-e-referencias/                     ← 69 fichas (pesquisadores, literatura)
```

Ou, se preferir manter 3 pastas, **realocar**:
- Certificações → `01_polimeros` (são ensaios de PU Vegetal)
- Perfis → `.agent-instructions/` ou `02_bambu` (são perfis de pesquisadores do bambu)

### 2. Prefixos — sugestão de padronização

| Prefixo | Sugiro | Para |
|---------|--------|------|
| `SCI_` | ✅ Manter | Artigos científicos com DOI |
| `POL_` | Novo | Polímeros, PU Vegetal, biocompósitos |
| `BAM_` | Novo | Bambu, tratamentos, pirolenhoso |
| `SOC_` | ✅ Manter | Habitação social, ATHIS, ECOSALA |
| `CER_` | Novo | Certificações, ensaios, normas |
| `PER_` | Novo | Perfis de pesquisadores |
| `FIC_` | Novo | Fichas técnicas de produtos (Imperveg, etc.) |

**Exemplo prático:**
```
01_polimeros-vegetais-e-biocompositos/
├── POL_001_pu-vegetal-imperveg.md
├── POL_002_biocompositos-mamona.md
├── SCI_001_purcom-biopir-analise.md   ← quando tiver DOI
└── FIC_001_ug132a-ficha-tecnica.md
```

### 3. Screenshots — ótima ideia, mas sugiro organização

```
01_polimeros-vegetais-e-biocompositos/
├── evidencias/                          ← pasta única de evidências
│   ├── itecons_permeabilidade.png
│   └── scholar_lahr_rocco.png
├── POL_001_pu-vegetal-imperveg.md       ← referencia a imagem
└── ...
```

### 4. Renomear o repositório GitHub

`acervo-soberania-tecnologica` → `acervo-soberania-tecnologica`

**Impacto:** Médio — quebra todos os links existentes. Mas é o momento certo (acervo ainda crescendo). Sugiro:
1. Criar o novo repo vazio
2. Migrar o conteúdo
3. Configurar redirect do repo antigo
4. Atualizar links nos READMEs dos outros projetos

---

## 🏆 Minha sugestão final (5 pastas)

```
📂 acervo-soberania-tecnologica/
│
├── 📂 01_polimeros-vegetais-e-biocompositos/      ← 421 fichas
│   ├── 📄 POL_001_pu-vegetal-imperveg.md
│   ├── 📄 FIC_001_ug132a-ficha-tecnica.md
│   ├── 📄 SCI_001_purcom-biopir-analise.md
│   └── 📷 evidencias/itecons_permeabilidade.png
│
├── 📂 02_bambu-estrutural-e-tratamentos/           ← 119 + 28 = 147 fichas
│   ├── 📄 BAM_001_tratamento-pirolenhoso.md
│   ├── 📄 BAM_002_forno-ecologico-ifb.md
│   ├── 📄 SCI_014_dequada-parametros.md
│   └── 📷 evidencias/scholar_lahr_rocco.png
│
├── 📂 03_habitacao-social-e-athis/                 ← 65 fichas
│   ├── 📄 SOC_001_tania-cruz-governanca.md
│   ├── 📄 SOC_002_ludmila-arquitetura-social.md
│   └── 📷 evidencias/unb_repositorio_fup.png
│
├── 📂 04_certificacoes-e-normas/                    ← 21 fichas
│   ├── 📄 CER_001_ensaios-itecons-imperveg.md
│   ├── 📄 CER_002_nbr-15575-desempenho.md
│   └── 📄 CER_003_abnt-6263-sustentabilidade.md
│
├── 📂 05_perfis-e-referencias/                      ← 69 fichas
│   ├── 📄 PER_001_ghavami-khosrow.md
│   ├── 📄 PER_002_beraldo-antonio.md
│   └── 📄 PER_003_cavichiolli-nathalia.md
│
├── 📂 .agent-instructions/                          ← Prompts e workflows
│   ├── 📄 prompt-pesquisa-acervo.json
│   ├── 📄 prompt-esteira-ingestao.md
│   └── 📄 chromadb-schema.json
│
├── 📂 chromadb/                                     ← Banco vetorial persistente
│   └── (gerado automaticamente)
│
└── 📄 README.md                                     ← Manual freiriano de uso
```

---

## Perguntas pra decidir

1. **3 ou 5 pastas?** A estrutura de 3 pastas é mais enxuta, mas 21 fichas de certificações e 69 de perfis precisam de destino claro.
2. **Prefixo SCI_ ou POL_/BAM_/SOC_?** Manter SCI_ pra tudo ou criar prefixos específicos por área?
3. **Renomear o repo GitHub agora?** É o momento certo (crescendo) ou depois (mais estável)?
4. **ChromaDB dentro do repo?** Ou mantém em `~/.chromadb` separado?

**Aguardando suas respostas para ajustar a sugestão final.**

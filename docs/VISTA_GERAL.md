# 🏭 Projeto Fábrica Modelo — Vista Geral

> Documento de visão geral do projeto. Contém o fluxograma completo, cronograma, estrutura de governança e etapas — sem precisar ler o README inteiro.
> Mantido pelo Hermes Agent · Atualizado em 01/07/2026

---

## 1. 🧭 Mapa do Projeto (Mermaid)

```mermaid
graph TB
    subgraph FINANC["💰 Financiamento"]
        FINEP["FINEP Mais Inovação<br/>Subvenção Econômica<br/>R$ 5M-10M"]
        CONTRA["Contrapartida Financeira<br/>Empresa Âncora<br/>Mín. 5% (R$250K)"]
        FINEP --> CONTRA
    end

    subgraph EXEC["🏗️ Execução"]
        ANCORA["Empresa Âncora<br/>(Co-proponente)"]
        TEXOS["Texos (Michel)<br/>Coexecutora Tecnológica<br/>Patente Painéis"]
        ANDRE["André Blanco (IFSP/TEIA)<br/>Coord. Técnica<br/>ABNT Comissão 6263"]
        MAURILIO["Maurilio Chiaretti<br/>Articulação Política<br/>Habitação Social"]
        FABIO["Fabio Takwara<br/>Assessoria Técnico-Científica<br/>Curadoria"]
        
        ANCORA --> TEXOS
        TEXOS --> ANDRE
        TEXOS --> MAURILIO
        TEXOS --> FABIO
    end

    subgraph ICTS["🔬 ICTs Parceiras"]
        SP["SP/MG (Eixo Principal)<br/>USP, UFSCar, UNICAMP,<br/>CEFET-MG, IPT, UFLA"]
        MULT["Multiplicadoras (N/NE/CO)<br/>UFAC, UFBA, UFRJ,<br/>UFSC, IF Goiano"]
        DF["DF/Entorno<br/>UnB (Tânia), IFB (Vicente),<br/>CAU/DF (Ludmila)"]
        SP --> MULT
        MULT --> DF
    end

    subgraph COOP["🤝 Cooperação Técnica"]
        IMP["Imperveg<br/>PU Vegetal Mamona<br/>6 ensaios ITecons Portugal"]
        KEHL["Kehlcoat<br/>Membranas PU<br/>Revestimentos"]
        PURCOM["Purcom<br/>Espumas BIOPIR<br/>CIP Pesquisa"]
    end

    subgraph SOCIAL["🧑‍🤝‍🧑 Prova Social"]
        INDICACAO["ICT indica comunidade<br/>com que já atua"]
        CLPI["CLPI assinado pela<br/>comunidade beneficiada"]
        IMPACTO["Evidência FINEP<br/>Parcerias Sociais"]
        INDICACAO --> CLPI --> IMPACTO
    end

    EXEC --> ICTS
    EXEC --> COOP
    ICTS --> SOCIAL
    COOP --> SOCIAL
    SOCIAL -.-> FINEP
```

---

## 2. 📅 Cronograma - Marco Zero (Julho 2026)

### Fase 1 — Prospecção e Convites (Prazo: 03/07)

```mermaid
gantt
    title Fase 1 — Prospecção
    dateFormat  DD/MM
    axisFormat %d/%m
    
    section Envio de Cartas (prazo 03/07)
    Tânia (UnB) / Fabio         :crit, active, 01/07, 03/07
    Ludmila (CAU/DF) / Fabio   :crit, active, 01/07, 03/07
    Vicente (IFB) / Fabio      :crit, active, 01/07, 03/07
    Bliska (UNICAMP) / André   :crit, active, 01/07, 03/07
    Rocco (USP) / André         :crit, active, 01/07, 03/07
    Carvalho (UFSCar) / André  :crit, active, 01/07, 03/07
    Marcondes (UFAC) / Tânia   :crit, active, 01/07, 03/07
    Romildo (UFRJ) / André     :crit, active, 01/07, 03/07
    Guilherme (UFBA) / Tânia   :crit, active, 01/07, 03/07
    Humberto (UFSC) / Vicente  :crit, active, 01/07, 03/07
    Alan (IF Goiano) / Vicente :crit, active, 01/07, 03/07
    
    section Cooperação Técnica
    Imperveg / Fabio           :active, 01/07, 03/07
    Kehlcoat / Fabio           :active, 01/07, 03/07
    Purcom / Fabio             :active, 01/07, 03/07
```

### Fase 2 — Fechamento de Parcerias (Julho)

```mermaid
gantt
    title Fase 2 — Parcerias
    dateFormat  DD/MM
    axisFormat %d/%m
    
    section Confirmação ICTs
    Aguardar retorno das cartas :04/07, 14/07
    Reuniões com cada ICT      :10/07, 20/07
    Definição escopo P&D        :15/07, 25/07
    
    section CLPI
    ICTs indicam comunidades    :10/07, 20/07
    Elaboração CLPI             :15/07, 25/07
    Assinatura CLPI             :20/07, 31/07
    
    section Contrapartida
    Busca Empresa Âncora       :01/07, 20/07
    Definição arranjo financeiro:15/07, 31/07
```

### Fase 3 — Escrita da Proposta (Agosto)

```mermaid
gantt
    title Fase 3 — Proposta FINEP
    dateFormat  DD/MM
    axisFormat %d/%m
    
    section Formulário
    Preenchimento formulário   :01/08, 20/08
    Revisão jurídica            :15/08, 25/08
    Ajustes finais              :25/08, 30/08
    
    section Submissão
    Submissão FINEP             :milestone, 31/08, 0d
```

---

## 3. 🏗️ Estrutura de Governança

```
┌─────────────────────────────────────────────────────────────┐
│                    GRUPO EXECUTOR                           │
│  André Blanco · Maurilio Chiaretti · Michel (Texos)         │
│  Fabio Takwara (Assessoria)                                 │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐  │
│  │ ICTs SP/MG   │  │ Multiplicad. │  │ Coop. Técnica    │  │
│  │ (P&D, Certif)│  │ (Difusão,    │  │ (Insumos,        │  │
│  │              │  │  Regionaliz.)│  │  Laboratórios)   │  │
│  └──────────────┘  └──────────────┘  └──────────────────┘  │
│                                                             │
│  ┌──────────────────────────────────────────────────────┐   │
│  │           PROVA SOCIAL (CLPI)                        │   │
│  │  Comunidades indicadas pelas ICTs → CLPI assinado    │   │
│  └──────────────────────────────────────────────────────┘   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 4. 👥 Quadro de Pessoas

### Membros Ativos (8)

| Membro | Instituição | Papel |
|--------|-------------|-------|
| André Blanco | IFSP / TEIA | Coord. Técnica, articulação ICT |
| Maurilio Chiaretti | FNA | Articulação Política, HIS |
| Michel (Texos) | Texos | Proponente candidato, painéis |
| Fabio Takwara | Ecolaborativa | Assessoria, curadoria |
| Marcos Paron | IFSP | Coord. ECOSALA, biochar |
| Daniela Maciel | Embrapa | Métricas de impacto social |
| Gisele Vilela | Embrapa | Remineralizadores |
| Vicente Virgolino | IFB | Forno ecológico, bambu |

### Prospecção (21 Prospects)

| Status | Qtde | Quem |
|--------|:----:|------|
| 📄 Carta pronta | 14 | Tânia, Ludmila, Vicente, Bliska, Rocco, Carvalho, Marcondes, Romildo, Guilherme, Humberto, Alan, Imperveg, Kehl, Purcom |
| 🔍 Em prospecção | 2 | Mendes (UFLA), Fiorelli (USP) |
| 🔄 Contato inicial | 2 | Joaquim (MST), Murilo (Terra Viva) |
| ⏳ Dados pendentes | 4 | C1-C4 ECOSALA |

---

## 5. 📋 Documentos Produzidos

### Cartas-Convite (14)

| # | Destinatário | Emissário |
|---|-------------|-----------|
| 1 | Tânia Cruz (UnB) | Fabio Takwara |
| 2 | Ludmila Correia (CAU/DF) | Fabio Takwara |
| 3 | Vicente Virgolino (IFB) | Fabio Takwara |
| 4 | Antonio Bliska Jr. (UNICAMP) | André Blanco |
| 5 | Rocco Lahr (USP EESC) | André Blanco |
| 6 | A.J.F. Carvalho (UFSCar) | André Blanco |
| 7 | Marcondes L. Costa (UFAC) | Tânia Cruz |
| 8 | Romildo Toledo Filho (UFRJ/COPPE) | André Blanco |
| 9 | Guilherme O. Silva (UFBA) | Tânia Cruz |
| 10 | Humberto C. Furtado (UFSC) | Vicente Virgolino |
| 11 | Alan P. Oliveira (IF Goiano) | Vicente Virgolino |
| 12 | Imperveg (Donizeti) | Fabio Takwara |
| 13 | Kehlcoat (Kehl Polímeros) | Fabio Takwara |
| 14 | Purcom Química | Fabio Takwara |

### Acervo — Fichas no Repositório Científico

| Categoria | Quantidade |
|-----------|:----------:|
| Perfis de pesquisadores | 15 |
| Fichas Imperveg | 21 |
| Fichas técnicas (Kehl, Purcom, Holambra, etc.) | 8 |
| SCI (Regência Científica MQTF) | 30 |
| FICHA (Credenciais + Produção + Bibliografia) | 31 |
| LAB (Ensaios Laboratoriais BNDES) | 6 |
| Resenhas (Bliska, Naccache, ITecons) | 9 |
| **Total aproximado** | **~120** |

---

## 6. 🔗 Links Rápidos

| Recurso | Link |
|---------|------|
| README do Projeto | [github.com/takwaratec/fabrica-modelo](https://github.com/takwaratec/fabrica-modelo) |
| Acervo Científico | [github.com/takwaratec/Analises-e-escrita-cientifica](https://github.com/takwaratec/Analises-e-escrita-cientifica) |
| Índice no Acervo | [Index Fábrica Modelo](https://github.com/takwaratec/Analises-e-escrita-cientifica/blob/main/docs/analises/fabrica-modelo/index.md) |
| Formulário Espelho FINEP | [`docs/editais/formulario-espelho-finep.md`](docs/editais/formulario-espelho-finep.md) |
| Modelo de CLPI | [`docs/editais/modelo-clpi.md`](docs/editais/modelo-clpi.md) |
| Regras Fornecedores | [`docs/editais/regras-participacao-fornecedores.md`](docs/editais/regras-participacao-fornecedores.md) |
| Acordo Cooperação Técnica | [`docs/editais/modelo-acordo-cooperacao-tecnica.md`](docs/editais/modelo-acordo-cooperacao-tecnica.md) |
| Documento Mestre (Mentoria) | [FRENTES_DE_TRABALHO.md](https://github.com/takwaratec/Mentoria_Tecnologia_Takwara/blob/main/FRENTES_DE_TRABALHO.md) |

---

## 7. 📌 Regras de Ouro

1. **Carta redigida ≠ carta enviada** — só atualiza para ✅ após envio com Cc para Fabio
2. **Fornecedor ≠ proponente** — cooperação técnica sem repasse financeiro
3. **Prova social** — ICT indica a comunidade, não o Grupo Executor
4. **CLPI** — consentimento assinado pela comunidade antes da intervenção
5. **Prazo FINEP** — submissão até **31/08/2026**
6. **Prazo cartas** — envio até **03/07/2026**

---

*Documento mantido pelo Hermes Agent · Tecnologia Takwara · 01/07/2026*

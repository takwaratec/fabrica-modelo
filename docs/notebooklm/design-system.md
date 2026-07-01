# Design System — Vídeo NotebookLM
## Projeto Fábrica Modelo | Tecnologia Takwara 2026

> Especificações visuais para os slides gerados no NotebookLM. O objetivo é eliminar o excesso de branco, maximizar o tamanho das imagens e criar uma identidade visual neutra e profissional com moldura tipo passe-partout.

---

## 1. PROBLEMA IDENTIFICADO

O usuário reportou após visualizar o vídeo gerado:
- ❌ **Muito branco na tela** — fundo claro excessivo, sem contraste
- ❌ **Espaços vazios** — áreas não aproveitadas
- ❌ **Imagens pequenas** — não preenchem o espaço disponível

---

## 2. PALETA DE CORES — Neutras e Sofisticadas

| Função | Cor | HEX | RGB | Uso |
|--------|-----|:---:|:---:|-----|
| **Fundo principal** | Cinza muito claro | `#F2F0EB` | 242,240,235 | Base dos slides — substitui o branco puro |
| **Fundo alternativo** | Cinza claro | `#E8E5DF` | 232,229,223 | Seções de destaque |
| **Moldura passe-partout** | Branco | `#FFFFFF` | 255,255,255 | Borda larga ao redor das imagens |
| **Texto principal** | Grafite | `#2C2C2C` | 44,44,44 | Títulos e corpo |
| **Texto de apoio** | Cinza médio | `#7A7A7A` | 122,122,122 | Legendas, notas, assinatura |
| **Acento sutil** | Verde Takwara | `#8B9A7A` | 139,154,122 | Detalhes, ícones, linhas finas |
| **Borda externa** | Cinza borda | `#D4D0C8` | 212,208,200 | Contorno suave da moldura |

> ⚠️ **Evitar:** Branco puro `#FFFFFF` como fundo de slide. Usar apenas na moldura das imagens.

---

## 3. MOLDURA — PASSE-PARTOUT

Cada imagem deve ser apresentada com uma **moldura branca tipo passe-partout** (como um quadro com margem):

```
┌─────────────────────────────────────┐
│                                     │
│    ┌───────────────────────────┐    │  ← Sombra suave
│    │                           │    │
│    │         IMAGEM            │    │
│    │       (preenche 85%       │    │
│    │        do espaço)         │    │
│    │                           │    │
│    └───────────────────────────┘    │
│                                     │
│    Tecnologia Takwara 2026          │  ← Assinatura
│                                     │
└─────────────────────────────────────┘
```

### Especificações
| Elemento | Valor |
|----------|-------|
| Largura da moldura (margem) | **8-10%** da largura do slide em cada lado |
| Margem superior | **6%** |
| Margem inferior | **10%** (espaço reservado para assinatura) |
| Cor da moldura | Branco `#FFFFFF` |
| Sombra da moldura | Sutil, 2-3px, opacidade 10% |
| Borda externa | 1px `#D4D0C8` (opcional) |

### Efeito "Quadro"
- A imagem interna deve ter **cantos levemente arredondados** (2-3px) ou manter retos
- A moldura branca cria o efeito de **fotografia emoldurada** sobre o fundo cinza neutro
- Isso resolve o problema de "muito branco" porque o fundo do slide é `#F2F0EB`, e apenas a área da imagem é branca

---

## 4. TRATAMENTO DAS IMAGENS

| Regra | Descrição |
|-------|-----------|
| **Tamanho** | Mínimo **70% da área útil** do slide. Ideal: **85%** |
| **Corte** | Preferir landscape (16:9). Se retrato, centralizar com moldura maior |
| **Qualidade** | Resolução mínima 1920x1080 — as imagens baixadas têm essa resolução |
| **Background** | Se a imagem não preencher, usar fundo `#F2F0EB` (nunca branco puro) |
| **Sem distorção** | Manter proporção original — usar "contain" não "cover" |

### Checklist por imagem:
- [ ] Redimensionar para no mínimo 1600px de largura
- [ ] Aplicar moldura branca de 8-10%
- [ ] Verificar se preenche >70% da tela
- [ ] Adicionar sombra suave na borda da moldura

---

## 5. TIPOGRAFIA

| Elemento | Fonte | Tamanho | Cor | Peso |
|----------|-------|---------|:---:|:----:|
| **Título do slide** | Inter, sans-serif | 36-42px | `#2C2C2C` | Semi-bold (600) |
| **Subtítulo / legenda** | Inter, sans-serif | 20-24px | `#7A7A7A` | Regular (400) |
| **Corpo / bullet points** | Inter, sans-serif | 24-28px | `#2C2C2C` | Regular (400) |
| **Assinatura** | Inter, sans-serif | 12-14px | `#8B9A7A` | Light (300) |
| **Dados / números** | Inter, sans-serif | 48-56px | `#8B9A7A` | Bold (700) |

### Alinhamento
- Títulos: superior esquerdo ou centralizado (depender do template do NotebookLM)
- Imagens: centralizadas dentro da moldura
- Texto corrido: evitar sobreposição com imagens

---

## 6. ASSINATURA — "Tecnologia Takwara 2026"

A assinatura deve aparecer em **todos os slides**, de forma discreta:

### Posicionamento
- **Canto inferior direito** da moldura branca
- Ou **centralizado** no rodapé, fora da moldura
- Tamanho: 12-14px
- Cor: `#8B9A7A` (verde Takwara)
- Peso: Light (300) — quase invisível, mas presente

### Formato
```
Tecnologia Takwara 2026
```

Sem logos, sem ícones — apenas texto em fonte fina. Deve ser percebida como uma **marca d'água elegante**, não como um selo.

---

## 7. LAYOUT DOS SLIDES POR TIPO

### Slide de Abertura (Título)
```
┌─────────────────────────────────────┐
│  ┌─────────────────────────────┐    │
│  │                             │    │
│  │  [ Logo Faleiros ][Logo     │    │
│  │   Techsus ]  +  FÁBRICA     │    │
│  │   MODELO                     │    │
│  │                             │    │
│  │  Projeto FINEP Mais Inovação│    │
│  │  Linha 4: Moradia           │    │
│  │  Sustentável                │    │
│  │                             │    │
│  └─────────────────────────────┘    │
│         Tecnologia Takwara 2026     │
└─────────────────────────────────────┘
```

### Slide com Imagem + Texto
```
┌─────────────────────────────────────┐
│  ┌───────────────────────────┐      │
│  │                           │      │
│  │   [IMAGEM GRANDE]         │      │
│  │   ~70% do slide           │      │
│  │                           │      │
│  └───────────────────────────┘      │
│  Título curto (opcional)            │
│         Tecnologia Takwara 2026     │
└─────────────────────────────────────┘
```

### Slide de Dados / Tabela
```
┌─────────────────────────────────────┐
│  ┌─────────────────────────────┐    │
│  │                             │    │
│  │   R$5-10M  |  5%  |  31/08 │    │
│  │   Valor    |  CP   |  Prazo │    │
│  │                             │    │
│  │   [gráfico ou ícone]        │    │
│  │                             │    │
│  └─────────────────────────────┘    │
│         Tecnologia Takwara 2026     │
└─────────────────────────────────────┘
```

---

## 8. O QUE EVITAR

| O que | Por que |
|-------|---------|
| Branco puro como fundo | Cansa a vista, parece vazio |
| Imagens menores que 50% da tela | Desperdiça espaço, parece amador |
| Logos grandes no centro | Polui a identidade visual |
| Mais de 3 cores no mesmo slide | Quebra a harmonia neutra |
| Texto sobre imagem sem contraste | Ilegível |
| Moldura muito fina (<3%) | Perde o efeito passe-partout |

---

## 9. APLICAÇÃO PRÁTICA

Ao gerar o vídeo no NotebookLM:

1. **Fontes a subir:** `fonte.md` (texto) + imagens da pasta `imagens/`
2. **Configuração:** NotebookLM gera slides automaticamente — mas você pode editar o áudio e os slides após a geração
3. **Pós-edição:** Ajustar os slides manualmente:
   - Trocar fundo branco por `#F2F0EB`
   - Redimensionar imagens para >70%
   - Aplicar moldura branca (passe-partout)
   - Inserir assinatura no rodapé
4. **Ferramenta:** Use qualquer editor de slides (Google Slides, Canva, PowerPoint) para ajustar os frames

---

*Design System · Tecnologia Takwara 2026 · Projeto Fábrica Modelo*

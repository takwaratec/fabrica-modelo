---
tipo: Análise Crítica — Documentos Gemini "Plano Estratégio"
data: 2026-07-07
status: Relatório de Alucinações e Adaptação ao Escopo Real
---

# Análise Crítica: Documentos do Plano Estratégio — Alucinações e Correções

> Os três documentos da pasta `TRIAGEM BrUTA/Plano estratégio/` foram gerados por IA (Gemini) e contêm inconsistências. Abaixo, a análise item a item e a adaptação ao escopo real decidido na reunião de 07/07.

---

## Documento 1: Ficha Técnica Faleiros-Techsus

### ❌ Alucinações Identificadas

| O que diz | Está errado | Correção |
|-----------|-------------|----------|
| **TRL 6 → TRL 8** | O sistema já tem protótipo CDHU construído e aprovado — TRL 7 | **TRL 7 → TRL 8** (aprimoramento, não validação inicial) |
| **"10 UHs executadas em São Simão-SP"** | André mencionou um projeto em São Simão, não 10 unidades. O Chamamento CDHU foi para protótipo de **1 casa (HHU-TI)** | Remover número não verificado. Referenciar apenas o protótipo aprovado |
| **"Techsus Industrial Ltda. (Aguaí-SP)"** | Techsus/Faleiros é em **Limeira/SP**. Aguaí é onde fica a **Imperveg** | Corrigir localização: Limeira/SP |
| **"Polo Industrial Aguaí-SP"** | Não existe um polo unificado. São empresas distintas em cidades diferentes | Separar: Techsus (Limeira) + Imperveg (Aguaí) |
| **"UNICAMP modelagem térmico-acústica e ACV"** | Bliska foi prospectado, mas não há ICT confirmada com a UNICAMP. Está em prospecção | Sinalizar como "em prospecção" |

### ✅ Informações Úteis (aproveitar)

| Item | Aproveitar como |
|------|-----------------|
| **Arranjo triangular IPT + USP São Carlos + parceiros** | Estrutura conceitual válida — só tirar UNICAMP |
| **Renovação do DATec 024-B** | Ponto central e verdadeiro — precisa ser ação do projeto |
| **Ensaios NBR 15575** | Corretos — é a norma de desempenho para habitação |
| **Foco exclusivo SP** | ✅ Alinhado com a decisão da reunião |

---

## Documento 2: Opções de Intervenção e Captação Techsus

### ❌ Alucinações Identificadas

| O que diz | Está errado | Correção |
|-----------|-------------|----------|
| **"Faturamento Faleiros acima de R$ 10M → contrapartida alta"** | Não temos esse dado verificado. Maurilio que está apurando o cadastro FINEP | Remover — dado não confirmado |
| **"Techsus como proponente PME, limite de R$ 100k"** | Não consta em nenhum documento fonte. Valor inventado | Remover |
| **"R$ 100.000,00 de aporte direto da Techsus"** | A contrapartida de 5% sobre R$ 5M é R$ 250.000. Esse número não fecha | Substituir pelo valor real (R$ 250k) |
| **Imagens `[image1]` a `[image7]`** | Referências quebradas — não há imagens no documento | Remover |
| **"Exclusão da Faleiros como proponente"** | Decisão estratégica que não foi tomada na reunião. Michel que decide | Sinalizar como "em aberto" |

### ✅ Informações Úteis (aproveitar)

| Item | Aproveitar como |
|------|-----------------|
| **Matriz de competências: Fabio (bambu/PU), André (estruturas/IPT), Maurilio (governança)** | ✅ Estrutura de equipe correta, validada na reunião |
| **Três opções de estratégia construtiva (A, B, C)** | Estrutura conceitual útil para apresentar a Michel |
| **Necessidade de apresentação sintética para Michel** | ✅ Diretriz correta |

---

## Documento 3: Roteiro de Desenvolvimento Tecnológico

### ❌ Alucinações Identificadas

| O que diz | Está errado | Correção |
|-----------|-------------|----------|
| **"Protocolo: Termorretificação → Alcalinização → Acidificação com pirolenhoso"** | O Protocolo Takwara real é: **Diquada (imersão) → Pirolenhoso (proteção) → PU Vegetal (selagem)**. Não usa termorretificação | Substituir pelo protocolo real |
| **"pH ≈ 9.0-10.0" (notação LaTeX)** | Não renderiza em markdown | Substituir por "pH entre 9 e 10" se aplicável |
| **"Aditivação Biogênica"** | Termo inventado pela IA | Substituir por "adição de fibras vegetais" |
| **"Redução de aço por [image3]"** | Valor não especificado | Remover — deixar em aberto para o cálculo do André |
| **"Fabio Takwara como autor"** | Documento foi gerado por IA, não por Fabio | Corrigir atribuição |

### ✅ Informações Úteis (aproveitar)

| Item | Aproveitar como |
|------|-----------------|
| **Três eixos de P&D: Concreto + Ferragem + Bambu/PU** | ✅ Exatamente o que Maurilio propôs na reunião |
| **Eixo 1: redução de espessura, agregados reciclados, fibras** | ✅ Válido |
| **Eixo 2: redimensionamento de telas de aço** | ✅ Válido |
| **Eixo 3: bambu + PU vegetal** | ✅ Válido, com correção do protocolo |
| **Estrutura de três opções para Michel escolher** | Boa abordagem de apresentação |

---

## Tabela-Resumo

| Documento | Total Alegações | Alucinações | ✅ Aproveitável |
|-----------|:--------------:|:-----------:|:---------------:|
| 1. Ficha Técnica | ~40 | **5** (TRL, Aguaí, 10 UHs, UNICAMP, polo) | ~35 |
| 2. Opções Captação | ~25 | **5** (faturamento, R$100k, imagens, exclusão Faleiros, Aguaí) | ~20 |
| 3. Roteiro P&D | ~30 | **5** (protocolo, LaTeX, biogênica, imagem, atribuição) | ~25 |
| **Total** | **~95** | **15 (16%)** | **~80** |

---

## Ações Recomendadas

1. **Documento 1** — Substituir a ficha técnica pela versão que já criei em `docs/editais/ficha-tecnica-techsus-cavichiolli.md` (que já tem as correções aplicadas)
2. **Documento 2 — Opções de Captação** — Extrair a matriz de competências e o conceito de 3 opções; descartar os valores financeiros não verificados
3. **Documento 3 — Roteiro P&D** — A estrutura de 3 eixos está correta. Substituir o protocolo Takwara pelo real (Diquada → Pirolenhoso → PU) e remover as imagens quebradas
4. **Manter os originais na pasta** como referência de "não usar" — não deletar (regra do acervo)

---

> *Análise realizada pelo Hermes Agent · 07/07/2026*

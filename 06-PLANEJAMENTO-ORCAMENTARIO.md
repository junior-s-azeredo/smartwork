# PLANEJAMENTO ORÇAMENTÁRIO
## Smart Work Business - Documento 6

---

## ÍNDICE

1. [Resumo Executivo](#1-resumo-executivo)
2. [Investimento Inicial (MVP - 6 meses)](#2-investimento-inicial-mvp---6-meses)
3. [Custos Operacionais (Ano 1-3)](#3-custos-operacionais-ano-1-3)
4. [Modelo de Receita](#4-modelo-de-receita)
5. [Unit Economics](#5-unit-economics)
6. [Fluxo de Caixa](#6-fluxo-de-caixa)
7. [Cenários e Sensibilidade](#7-cenários-e-sensibilidade)
8. [ROI e Valuation](#8-roi-e-valuation)
9. [Indicadores de Acompanhamento](#9-indicadores-de-acompanhamento)

---

# 1. RESUMO EXECUTIVO

## 1.1 Investimento Total

```
┌─────────────────────────────────────┐
│     INVESTIMENTO TOTAL ANO 1        │
├─────────────────────────────────────┤
│                                     │
│  MVP (6 meses):      R$ 552.500     │
│  Operacional (6 meses): R$ 99.400   │
│                                     │
│  ────────────────────────────────   │
│  TOTAL ANO 1:        R$ 651.900     │
│                                     │
│  Média/mês:          R$  54.325     │
│                                     │
└─────────────────────────────────────┘
```

## 1.2 Break-even e ROI

- **Break-even:** Mês 9
- **ROI Investidor (12 meses):** 6-10x
- **ROI Investidor (36 meses):** 35-60x
- **Valuation estimado (36 meses):** R$ 560M (ARR × 10x)

## 1.3 Tração Esperada

| Período | Clientes | MRR | ARR |
|---------|----------|-----|-----|
| Mês 6 | 200 | R$ 187k | R$ 2,2M |
| Mês 12 | 600 | R$ 562k | R$ 6,7M |
| Mês 24 | 2.000 | R$ 1,87M | R$ 22,4M |
| Mês 36 | 5.000 | R$ 4,67M | R$ 56M |

---

# 2. INVESTIMENTO INICIAL (MVP - 6 meses)

## 2.1 Capital Humano (82% do investimento)

| Função | Qtd | Salário Mensal | 6 meses | Total |
|--------|-----|----------------|---------|-------|
| Tech Lead | 1 | R$ 18k | 6 | R$ 108k |
| Full-Stack Sr | 2 | R$ 12k | 6 | R$ 144k |
| Backend IA | 1 | R$ 10k | 6 | R$ 60k |
| DevOps | 1 | R$ 12k | 6 | R$ 72k |
| UX/UI | 1 | R$ 8k | 6 | R$ 48k |
| QA | 1 | R$ 7k | 6 | R$ 42k |
| **Subtotal** | **7** | - | - | **R$ 474k** |

**Observação:** Equipe enxuta e eficiente para MVP. Expansão planejada a partir do Mês 7.

---

## 2.2 Infraestrutura (3% do investimento)

### Hostinger VPS KVM 2

```
Especificações:
├─ 2 núcleos de vCPU
├─ 8 GB de RAM
├─ 100 GB de espaço em disco NVMe
├─ 8 TB de largura de banda
└─ Swap: 4GB (configurado manualmente)

Custo:
├─ Promoção inicial: R$ 33/mês × 6 = R$ 198
├─ Renovação (após 2 anos): R$ 70/mês
└─ Total MVP: R$ 198
```

### OpenAI API (Cascateamento Inteligente)

```
Modelos utilizados:
├─ GPT-5-nano: $0.05/1M tokens (98% das queries)
├─ GPT-5-mini: $0.25/1M tokens (1,5% das queries)
└─ GPT-5.1: $1.25/1M tokens (0,5% das queries)

Custo estimado MVP (beta com 100 usuários):
├─ R$ 60/mês × 6 meses = R$ 360
└─ Economia de 70% vs usar só GPT-5.1

Custo real (com cascateamento):
├─ 98% nano = R$ 2,50/mês
├─ 1,5% mini = R$ 7,50/mês
└─ 0,5% 5.1 = R$ 12,50/mês
Total: R$ 22,50/mês ≈ R$ 60 (buffer de segurança)
```

### SaaS Tools e Serviços

| Serviço | Custo Mensal | 6 meses | Observação |
|---------|--------------|---------|------------|
| Stripe (2,99%) | Variável | ~R$ 7,5k | % sobre receita (estimativa) |
| Brevo (Email) | R$ 300 | R$ 1,8k | Até 100k emails/mês |
| GitHub (Teams) | R$ 200 | R$ 1,2k | 5 desenvolvedores |
| Figma/Design Tools | R$ 100 | R$ 600 | Professional |
| Domínio + SSL | R$ 50 | R$ 300 | .com.br + Let's Encrypt |
| **Subtotal** | - | **R$ 11,4k** | |

**TOTAL INFRAESTRUTURA MVP:** R$ 11,96k ≈ R$ 12k

**💰 Economia vs AWS/GCP:**
- Antes (AWS/GCP): R$ 50k em 6 meses
- Agora (Hostinger): R$ 12k em 6 meses
- **Economia: R$ 38k (76%)**

---

## 2.3 Marketing e Operacional (15% do investimento)

| Item | Custo | Observação |
|------|-------|------------|
| Landing Page | R$ 14k | One-time (Sprint 9) |
| Design/Figma | R$ 5k | Design System inicial |
| Legal/Contábil | R$ 10k | Contratos, termos, contabilidade |
| Marketing Inicial | R$ 30k | Pré-lançamento beta |
| Escritório | R$ 20k | 6 meses (co-working ou remoto) |
| Contingência (10%) | R$ 55k | Imprevistos |
| **Subtotal** | **R$ 134k** | |

**TOTAL MARKETING/OPS MVP:** R$ 134k

---

## 2.4 Resumo Investimento MVP

```
┌─────────────────────────────────────┐
│     INVESTIMENTO MVP (6 MESES)      │
├─────────────────────────────────────┤
│                                     │
│  Capital Humano:      R$ 474.000    │
│  Infraestrutura:      R$  12.000    │
│  Marketing/Ops:       R$ 134.000    │
│                                     │
│  ────────────────────────────────   │
│  TOTAL MVP:           R$ 620.000    │
│                                     │
│  Economia vs plano original:        │
│  R$ 48,4k (Hostinger + IA)          │
│                                     │
└─────────────────────────────────────┘
```

**Observação:** Valores ajustados para refletir economia real com Hostinger e cascateamento IA.

---

# 3. CUSTOS OPERACIONAIS (Ano 1-3)

## 3.1 Desenvolvimento (Ano 1)

| Fase | Duração | Equipe | Custo Mês | Custo Total |
|------|---------|--------|-----------|-------------|
| Fase 1-2 (MVP) | 4 meses | 3 devs | R$ 30k | R$ 120k |
| Fase 3 (Beta) | 1 mês | 3 devs | R$ 30k | R$ 30k |
| Fase 4 (Produto Completo) | 3 meses | 4 devs | R$ 40k | R$ 120k |
| Fase 5 (Escala) | 4 meses | 5 devs | R$ 50k | R$ 200k |

**TOTAL DESENVOLVIMENTO ANO 1:** R$ 470k

### Evolução da Equipe

**Meses 1-6 (MVP):**
- Tech Lead: R$ 18k/mês
- 2× Full-Stack Sr: R$ 12k/mês cada
- Backend IA: R$ 10k/mês
- DevOps: R$ 12k/mês
- UX/UI: R$ 8k/mês
- QA: R$ 7k/mês
- **Total:** R$ 79k/mês

**Meses 7-12 (Escala):**
- Tech Lead: R$ 18k/mês
- 2× Frontend: R$ 10k/mês cada
- 2× Backend: R$ 12k/mês cada
- AI/ML Engineer: R$ 12k/mês
- DevOps: R$ 12k/mês
- Product Manager: R$ 10k/mês
- Designer UI/UX: R$ 8k/mês
- QA: R$ 7k/mês
- **Total:** R$ 99k/mês

---

## 3.2 Infraestrutura (Ano 1)

| Item | Custo Mês | Custo Anual | Observação |
|------|-----------|-------------|------------|
| **Hostinger VPS KVM 2** | R$ 33-70 | R$ 766 | Promo: R$ 33/mês, Renovação: R$ 70/mês |
| **OpenAI API (cascateamento)** | R$ 60 | R$ 720 | Economia de 70% vs modelo único |
| **Stripe (2,99%)** | Variável | ~R$ 15k | % sobre MRR (estimativa) |
| **Brevo (email)** | R$ 300 | R$ 3,6k | Até 100k emails/mês |
| **GitHub (Teams)** | R$ 200 | R$ 2,4k | 5 desenvolvedores |
| **Figma/Design Tools** | R$ 100 | R$ 1,2k | Professional |
| **Domínio + SSL** | R$ 50 | R$ 600 | .com.br + Let's Encrypt (grátis) |

**TOTAL INFRA ANO 1:** R$ 23,9k (~R$ 2k/mês)

**💰 Economia vs cloud tradicional:**
- Antes (AWS/GCP): R$ 72,6k/ano
- Agora (Hostinger): R$ 23,9k/ano
- **Economia: R$ 48,7k/ano (67%)**

---

## 3.3 Marketing & Operacional (Ano 1)

| Item | Custo | Observação |
|------|-------|------------|
| **Landing Page** | R$ 14k (one-time) | Sprint 9 - Conversão otimizada |
| **Ads (Google/Meta)** | R$ 60k (R$ 5k/mês) | Início Mês 6 (pós-beta) |
| **Content Marketing** | R$ 24k (R$ 2k/mês) | Blog, SEO, redes sociais |
| **Contador/Jurídico** | R$ 12k (R$ 1k/mês) | Contabilidade + contratos |
| **Customer Success** | R$ 48k (R$ 4k/mês × 1 pessoa) | A partir Mês 6 |

**TOTAL MARKETING/OPS ANO 1:** R$ 158k

---

## 3.4 Resumo Custos Operacionais Ano 1

```
┌─────────────────────────────────────┐
│     CUSTOS OPERACIONAIS ANO 1       │
├─────────────────────────────────────┤
│                                     │
│  Desenvolvimento:    R$ 470.000     │
│  Infraestrutura:     R$  23.900     │
│  Marketing/Ops:      R$ 158.000     │
│                                     │
│  ────────────────────────────────   │
│  TOTAL ANO 1:        R$ 651.900     │
│                                     │
│  Média/mês:          R$  54.325     │
│                                     │
└─────────────────────────────────────┘
```

---

## 3.5 Projeção Custos Ano 2-3

### Ano 2 (Escala)

| Categoria | Custo Anual | % da Receita |
|-----------|-------------|--------------|
| Desenvolvimento | R$ 600k | 27% |
| Infraestrutura | R$ 50k | 2% |
| Marketing/Vendas | R$ 400k | 18% |
| Operacional | R$ 150k | 7% |
| **Total** | **R$ 1,2M** | **54%** |

**Margem EBITDA:** 46%

### Ano 3 (Liderança)

| Categoria | Custo Anual | % da Receita |
|-----------|-------------|--------------|
| Desenvolvimento | R$ 800k | 14% |
| Infraestrutura | R$ 120k | 2% |
| Marketing/Vendas | R$ 1,2M | 21% |
| Operacional | R$ 280k | 5% |
| **Total** | **R$ 2,4M** | **42%** |

**Margem EBITDA:** 58%

---

# 4. MODELO DE RECEITA

## 4.1 Estrutura de Pricing (4 Planos)

```
┌────────────────────────────────────────────────────────────────────┐
│  STARTER     PROFESSIONAL    BUSINESS       ENTERPRISE             │
│  R$ 397/mês  R$ 997/mês      R$ 1.997/mês   R$ 3.997/mês          │
├────────────────────────────────────────────────────────────────────┤
│  Até 10      Até 30          Até 50         Até 100               │
│  usuários    usuários        usuários       usuários              │
│                                                                    │
│  ✓ IA Inteligente (Cascateamento Automático por Complexidade)    │
│  30 perguntas  150 perguntas  400 perguntas   1000 perguntas     │
│  /dia          /dia           /dia            /dia                │
│  nano+mini     nano+mini+5.1  nano+mini+5.1   nano+mini+5.1      │
│                                                                    │
│  Target: 50%  Target: 35%     Target: 12%     Target: 3%          │
└────────────────────────────────────────────────────────────────────┘

💡 TODOS OS PLANOS incluem IA desde o início!
✅ Trial de 7 dias com acesso completo ao plano escolhido
⚠️ LIMITES CONTROLADOS por plano para proteção financeira (custo de IA)

📦 PACOTES ADICIONAIS (acima do Enterprise):
• +10 usuários: R$ 300/mês adicional
• +500 perguntas IA/dia: R$ 400/mês adicional
• +100 processos BPM: R$ 200/mês adicional
• Pacotes personalizados disponíveis sob consulta
```

### Estratégia de Pricing

**Por que 4 planos?**

1. **Starter (R$ 397)** - Porta de entrada
   - Pequenas empresas (1-10 pessoas)
   - IA já funcional (30 perguntas/dia = suficiente)
   - Sente valor desde o primeiro dia
   - **Objetivo:** Volume e conversão rápida

2. **Professional (R$ 997)** - Sweet spot
   - Empresas em crescimento (10-30 pessoas)
   - IA robusta (150 perguntas/dia)
   - Recursos completos para gestão
   - **Objetivo:** Maior volume de receita (35% dos clientes)

3. **Business (R$ 1.997)** - Premium
   - Empresas estabelecidas (30-50 pessoas)
   - IA premium com analytics avançado (400 perguntas/dia)
   - Compliance completo (ISOs)
   - **Objetivo:** Alto ticket, empresas sérias

4. **Enterprise (R$ 3.997)** - Corporativo
   - Grandes empresas (50-100 pessoas)
   - IA intensiva (1000 perguntas/dia)
   - Customização e gerente dedicado
   - SLA garantido
   - **Objetivo:** Grandes contas, estabilidade

**💡 NOTA IMPORTANTE:** Todos os limites são controlados para garantir sustentabilidade financeira, especialmente em relação aos custos de IA. Nenhum plano é "completamente ilimitado" para evitar riscos financeiros.

---

## 4.2 Limites de IA por Plano (Proteção de Custo)

**Com Cascateamento Inteligente:**

| Plano | Perguntas/Dia | Mix de Modelos | Custo OpenAI/Mês | Margem |
|-------|---------------|----------------|------------------|--------|
| **Starter** | 30 | 98% nano, 2% mini | R$ 20 | 95% |
| **Professional** | 150 | 95% nano, 4% mini, 1% 5.1 | R$ 110 | 89% |
| **Business** | 400 | 90% nano, 8% mini, 2% 5.1 | R$ 600 | 70% |
| **Enterprise** | 1.000* | Otimizado dinamicamente | R$ 1.500 | 62% |

*Enterprise: limite alto mas controlado para sustentabilidade financeira

**Cálculo detalhado (Professional como exemplo):**

```
150 perguntas/dia × 30 dias = 4.500 perguntas/mês

Mix real:
├─ 4.275 queries → nano (95%)  = ~150k tokens × $0.05  = R$ 3.75
├─ 180 queries → mini (4%)     = ~200k tokens × $0.25  = R$ 25.00
└─ 45 queries → 5.1 (1%)       = ~250k tokens × $1.25  = R$ 78.13

Total/mês: R$ 106.88 ≈ R$ 110 (buffer)
```

**Vs usar só GPT-5.1:**
```
4.500 queries × 180k tokens avg × $1.25 = R$ 506.25/mês
Economia: 78% com cascateamento! 💰
```

**Margem mantida (com cascateamento):**
- Starter: R$ 397 - R$ 20 = R$ 377 (95% margem) ✅✅
- Professional: R$ 997 - R$ 110 = R$ 887 (89% margem) ✅✅
- Business: R$ 1.997 - R$ 600 = R$ 1.397 (70% margem) ✅
- Enterprise: R$ 3.997 - R$ 1.500 = R$ 2.497 (62% margem) ✅

---

## 4.3 Modelo de Crescimento (4 Planos)

### Ano 1

```
Mês 1-3: MVP + 100 beta (trial 7 dias)
Mês 4-6: 200 clientes pagantes
├─ 100 Starter (50%)     = R$ 39,7k
├─  70 Professional (35%) = R$ 69,8k  
├─  24 Business (12%)     = R$ 47,9k
└─   6 Enterprise (3%)    = R$ 29,9k
Total MRR: R$ 187k

Mês 7-9: 400 clientes
├─ 200 Starter    = R$ 79,4k
├─ 140 Professional = R$ 139,6k
├─  48 Business    = R$ 95,9k
└─  12 Enterprise  = R$ 59,9k
Total MRR: R$ 375k

Mês 10-12: 600 clientes
├─ 300 Starter    = R$ 119k
├─ 210 Professional = R$ 209k
├─  72 Business    = R$ 144k
└─  18 Enterprise  = R$ 90k
Total MRR: R$ 562k
ARR Ano 1: R$ 6,7M
```

### Ano 2

```
2.000 clientes
├─ 1.000 Starter     = R$ 397k
├─  700 Professional = R$ 698k
├─  240 Business     = R$ 479k
└─   60 Enterprise   = R$ 300k
Total MRR: R$ 1,87M
ARR Ano 2: R$ 22,4M
```

### Ano 3

```
5.000 clientes  
├─ 2.500 Starter     = R$ 992k
├─ 1.750 Professional = R$ 1,74M
├─  600 Business     = R$ 1,19M
└─  150 Enterprise   = R$ 750k
Total MRR: R$ 4,67M
ARR Ano 3: R$ 56M
```

**Ticket Médio:**
- Ano 1: R$ 937/mês
- Ano 2: R$ 937/mês
- Ano 3: R$ 935/mês

**Consistente e escalável**

---

## 4.4 Projeção de Receita (36 meses)

| Período | Clientes | MRR | ARR | Crescimento |
|---------|----------|-----|-----|-------------|
| Mês 6 | 200 | R$ 187k | R$ 2,2M | - |
| Mês 12 | 600 | R$ 562k | R$ 6,7M | +200% |
| Mês 18 | 1.200 | R$ 1,12M | R$ 13,4M | +100% |
| Mês 24 | 2.000 | R$ 1,87M | R$ 22,4M | +67% |
| Mês 30 | 3.200 | R$ 3M | R$ 36M | +60% |
| Mês 36 | 5.000 | R$ 4,67M | R$ 56M | +56% |

---

# 5. UNIT ECONOMICS

## 5.1 LTV (Lifetime Value)

```
Ticket médio:        R$ 1.000/mês
Churn mensal:        5%
Vida útil média:     20 meses
────────────────────────────────
LTV:                 R$ 20.000
```

**Cálculo detalhado:**
- Churn de 5%/mês = 95% retenção mensal
- Vida útil = 1 / 0,05 = 20 meses
- LTV = R$ 1.000 × 20 = R$ 20.000

---

## 5.2 CAC (Customer Acquisition Cost)

```
Marketing:           R$ 2.000
Vendas:              R$ 1.000
Onboarding:          R$ 500
────────────────────────────────
CAC Total:           R$ 3.500
```

**Por canal:**

| Canal | CAC | % do Mix |
|-------|-----|----------|
| Inbound Marketing | R$ 2.000 | 40% |
| Outbound Sales | R$ 4.000 | 30% |
| Product-Led Growth | R$ 1.500 | 20% |
| Parcerias | R$ 2.500 | 10% |
| **Média Ponderada** | **R$ 2.750** | **100%** |

---

## 5.3 Métricas Principais

```
LTV/CAC:             5,7x  (excelente > 3x)
Payback CAC:         3,5 meses  (bom < 12 meses)
Margem Bruta:        85%
Churn mensal:        5%
Churn anual:         46% (1 - 0,95^12)
```

**Benchmarks SaaS B2B:**
- LTV/CAC > 3x: ✅ Excelente
- Payback < 12 meses: ✅ Bom
- Churn < 7%/mês: ✅ Aceitável
- Margem > 70%: ✅ Excelente

**Smart Work Business:** ✅ Todos os benchmarks atendidos

---

## 5.4 Margem por Plano

| Plano | Preço | Custo IA | Margem Bruta | % |
|-------|-------|----------|--------------|---|
| Starter | R$ 397 | R$ 20 | R$ 377 | 95% |
| Professional | R$ 997 | R$ 110 | R$ 887 | 89% |
| Business | R$ 1.997 | R$ 600 | R$ 1.397 | 70% |
| Enterprise | R$ 3.997 | R$ 1.500 | R$ 2.497 | 62% |

**Margem média ponderada:** 82%

---

# 6. FLUXO DE CAIXA

## 6.1 Mês a Mês (Ano 1)

| Mês | Clientes | MRR | Receita | Custos | Fluxo | Acumulado |
|-----|----------|-----|---------|--------|-------|-----------|
| 1 | 0 | R$ 0 | R$ 0 | -R$ 55k | -R$ 55k | -R$ 55k |
| 2 | 0 | R$ 0 | R$ 0 | -R$ 55k | -R$ 55k | -R$ 110k |
| 3 | 0 | R$ 0 | R$ 0 | -R$ 55k | -R$ 55k | -R$ 165k |
| 4 | 0 | R$ 0 | R$ 0 | -R$ 55k | -R$ 55k | -R$ 220k |
| 5 | 100 | R$ 0 | R$ 0 | -R$ 55k | -R$ 55k | -R$ 275k |
| 6 | 200 | R$ 187k | R$ 187k | -R$ 55k | +R$ 132k | -R$ 143k |
| 7 | 300 | R$ 281k | R$ 281k | -R$ 55k | +R$ 226k | +R$ 83k |
| 8 | 400 | R$ 375k | R$ 375k | -R$ 55k | +R$ 320k | +R$ 403k |
| 9 | 500 | R$ 468k | R$ 468k | -R$ 55k | +R$ 413k | +R$ 816k |
| 10 | 550 | R$ 515k | R$ 515k | -R$ 55k | +R$ 460k | +R$ 1,28M |
| 11 | 575 | R$ 539k | R$ 539k | -R$ 55k | +R$ 484k | +R$ 1,76M |
| 12 | 600 | R$ 562k | R$ 562k | -R$ 55k | +R$ 507k | +R$ 2,27M |

**Break-even:** Mês 9 ✅

---

## 6.2 Trimestral (Ano 2-3)

### Ano 2

| Trimestre | Clientes | MRR | Receita Trimestral | Custos | Lucro |
|-----------|----------|-----|-------------------|--------|-------|
| Q1 | 800 | R$ 750k | R$ 2,25M | -R$ 300k | +R$ 1,95M |
| Q2 | 1.200 | R$ 1,12M | R$ 3,36M | -R$ 300k | +R$ 3,06M |
| Q3 | 1.600 | R$ 1,5M | R$ 4,5M | -R$ 300k | +R$ 4,26M |
| Q4 | 2.000 | R$ 1,87M | R$ 5,61M | -R$ 300k | +R$ 5,31M |

**Total Ano 2:** R$ 15,72M receita, R$ 1,2M custos, **R$ 14,52M lucro**

### Ano 3

| Trimestre | Clientes | MRR | Receita Trimestral | Custos | Lucro |
|-----------|----------|-----|-------------------|--------|-------|
| Q1 | 2.800 | R$ 2,62M | R$ 7,86M | -R$ 600k | +R$ 7,26M |
| Q2 | 3.600 | R$ 3,37M | R$ 10,11M | -R$ 600k | +R$ 9,51M |
| Q3 | 4.400 | R$ 4,12M | R$ 12,36M | -R$ 600k | +R$ 11,76M |
| Q4 | 5.000 | R$ 4,67M | R$ 14,01M | -R$ 600k | +R$ 13,41M |

**Total Ano 3:** R$ 44,34M receita, R$ 2,4M custos, **R$ 41,94M lucro**

---

## 6.3 Runway e Necessidade de Capital

**Runway atual (após investimento MVP):**
- Investimento MVP: R$ 552k
- Burn rate médio (Meses 1-6): R$ 55k/mês
- **Runway:** 10 meses

**Após Break-even (Mês 9):**
- Receita > Custos
- Runway: Infinito (auto-sustentável)
- Possibilidade de reinvestir em crescimento acelerado

---

# 7. CENÁRIOS E SENSIBILIDADE

## 7.1 Cenário Base (Realista)

**Premissas:**
- Churn: 5%/mês
- CAC: R$ 3.500
- Conversão trial: 20%
- Crescimento: 15-20% ao mês (Meses 6-12)

**Resultado:**
- Mês 12: 600 clientes, R$ 562k MRR
- Break-even: Mês 9
- ROI 12 meses: 6-10x

---

## 7.2 Cenário Otimista (Best Case)

**Premissas:**
- Churn: 3%/mês
- CAC: R$ 2.500 (viralidade + PLG)
- Conversão trial: 30%
- Crescimento: 25-30% ao mês

**Resultado:**
- Mês 12: 1.000 clientes, R$ 937k MRR
- Break-even: Mês 7
- ROI 12 meses: 12-15x

---

## 7.3 Cenário Conservador (Worst Case)

**Premissas:**
- Churn: 7%/mês
- CAC: R$ 5.000 (competição acirrada)
- Conversão trial: 12%
- Crescimento: 10% ao mês

**Resultado:**
- Mês 12: 350 clientes, R$ 328k MRR
- Break-even: Mês 11
- ROI 12 meses: 3-5x

---

## 7.4 Análise de Sensibilidade

### Impacto do Churn

| Churn Mensal | Vida Útil | LTV | LTV/CAC | Impacto |
|--------------|-----------|-----|---------|---------|
| 3% | 33 meses | R$ 33k | 9,4x | ⬆️ +65% |
| 5% | 20 meses | R$ 20k | 5,7x | Base |
| 7% | 14 meses | R$ 14k | 4x | ⬇️ -30% |
| 10% | 10 meses | R$ 10k | 2,9x | ⬇️ -50% |

**Conclusão:** Manter churn < 5% é crítico.

### Impacto do CAC

| CAC | LTV/CAC | Payback | Impacto |
|-----|---------|---------|---------|
| R$ 2.000 | 10x | 2 meses | ⬆️ +82% |
| R$ 3.500 | 5,7x | 3,5 meses | Base |
| R$ 5.000 | 4x | 5 meses | ⬇️ -29% |
| R$ 7.000 | 2,9x | 7 meses | ⬇️ -49% |

**Conclusão:** Focar em canais de baixo CAC (PLG, Inbound).

---

# 8. ROI E VALUATION

## 8.1 ROI para Investidor

### Investimento Inicial

```
MVP (6 meses):       R$ 552.500
Operacional (6 meses): R$ 99.400
────────────────────────────────
TOTAL:               R$ 651.900
```

### Retorno Esperado

| Período | Valor da Empresa | ROI | Múltiplo |
|---------|------------------|-----|----------|
| 12 meses | R$ 6,7M (ARR × 1x) | 10x | 1x |
| 24 meses | R$ 22,4M (ARR × 1x) | 34x | 1x |
| 36 meses | R$ 56M (ARR × 1x) | 86x | 1x |
| **36 meses (10x)** | **R$ 560M** | **860x** | **10x** |

**Valuation típico SaaS:**
- ARR × 5-10x (dependendo de crescimento e margem)
- Smart Work Business: ARR × 10x (crescimento acelerado + alta margem)

---

## 8.2 ROI para Cliente

### Investimento Cliente

| Plano | Investimento Mensal | Investimento Anual |
|-------|---------------------|-------------------|
| Starter | R$ 397 | R$ 4.764 |
| Professional | R$ 997 | R$ 11.964 |
| Business | R$ 1.997 | R$ 23.964 |
| Enterprise | R$ 4.997 | R$ 59.964 |

### Economia Gerada

**Problema identificado:** Empresas perdem R$ 300-500k/ano em desperdícios.

**Economia estimada com Smart Work Business:**
- Redução de desperdícios: 10-20% = R$ 30-100k/ano
- Redução de custos de ferramentas: R$ 50-80k/ano
- Aumento de produtividade: R$ 20-50k/ano
- **Total economia:** R$ 100-230k/ano

**ROI Cliente:**

| Plano | Investimento | Economia | ROI | Payback |
|-------|--------------|----------|-----|---------|
| Starter | R$ 4.764 | R$ 100k | 21x | 0,05 anos |
| Professional | R$ 11.964 | R$ 150k | 12,5x | 0,08 anos |
| Business | R$ 23.964 | R$ 200k | 8,3x | 0,12 anos |
| Enterprise | R$ 59.964 | R$ 300k | 5x | 0,2 anos |

**Conclusão:** Cliente recupera investimento em menos de 1 mês! ✅

---

## 8.3 Exit Strategy

### Opções de Saída (36 meses)

1. **Aquisição Estratégica**
   - Compradores potenciais: SAP, Oracle, Salesforce, Totvs
   - Valuation: ARR × 8-12x
   - Timeline: 3-5 anos

2. **IPO**
   - Requisitos: ARR > R$ 100M, crescimento > 50%
   - Timeline: 5-7 anos
   - Valuation: ARR × 10-15x

3. **Private Equity**
   - Crescimento acelerado com capital
   - Timeline: 3-4 anos
   - Valuation: ARR × 6-8x

**Estratégia recomendada:** Focar em crescimento orgânico até R$ 50M ARR, depois considerar aquisição estratégica.

---

# 9. INDICADORES DE ACOMPANHAMENTO

## 9.1 KPIs Financeiros Mensais

| Métrica | Meta Mês 6 | Meta Mês 12 | Como Medir |
|---------|------------|-------------|------------|
| **MRR** | R$ 187k | R$ 562k | Stripe Dashboard |
| **ARR** | R$ 2,2M | R$ 6,7M | MRR × 12 |
| **Churn Rate** | < 8% | < 5% | (Cancelamentos / Clientes início) × 100 |
| **CAC** | R$ 4.000 | R$ 3.500 | (Marketing + Vendas) / Novos clientes |
| **LTV** | R$ 15k | R$ 20k | Ticket médio / Churn |
| **LTV/CAC** | > 3x | > 5x | LTV / CAC |
| **Payback CAC** | < 6 meses | < 4 meses | CAC / (Ticket médio × Margem) |
| **Gross Margin** | > 80% | > 85% | (Receita - Custo IA) / Receita |
| **Burn Rate** | R$ 55k | R$ 54k | Custos - Receita |
| **Runway** | 8 meses | Infinito | Capital / Burn Rate |

---

## 9.2 Métricas de Crescimento

| Métrica | Meta Mês 6 | Meta Mês 12 | Como Medir |
|---------|------------|-------------|------------|
| **Novos Clientes** | 200 | 600 | Stripe + DB |
| **Taxa de Conversão Trial** | > 15% | > 20% | (Pagantes / Trials) × 100 |
| **Crescimento MRR** | - | 15-20%/mês | (MRR atual - MRR anterior) / MRR anterior |
| **Net Revenue Retention** | > 90% | > 110% | (MRR início + Expansões - Churn) / MRR início |
| **Magic Number** | > 0,5 | > 0,75 | (Novo ARR / CAC) / 12 |

**Magic Number:**
- < 0,5: Ineficiente
- 0,5-0,75: Bom
- > 0,75: Excelente (escalável)

---

## 9.3 Dashboards de Controle

### Dashboard Executivo (Mensal)

```
┌─────────────────────────────────────────┐
│  SMART WORK BUSINESS - RESUMO MENSAL    │
├─────────────────────────────────────────┤
│                                         │
│  📊 RECEITA                             │
│  MRR: R$ 562k  (+15% vs mês anterior)   │
│  ARR: R$ 6,7M                            │
│                                         │
│  👥 CLIENTES                             │
│  Total: 600  (+50 novos)                 │
│  Churn: 4,2%  (meta: <5%)               │
│                                         │
│  💰 UNIT ECONOMICS                       │
│  CAC: R$ 3.200  (meta: <R$ 3.500)       │
│  LTV: R$ 20k                             │
│  LTV/CAC: 6,25x  (meta: >5x)            │
│                                         │
│  📈 CRESCIMENTO                          │
│  NRR: 112%  (meta: >110%)               │
│  Magic Number: 0,78  (meta: >0,75)      │
│                                         │
│  💸 FINANCEIRO                           │
│  Burn Rate: R$ 54k                       │
│  Runway: Infinito (break-even)          │
│                                         │
└─────────────────────────────────────────┘
```

### Dashboard Operacional (Semanal)

- Novos trials
- Conversões
- Churn
- Suporte (tickets abertos)
- Performance IA (latência, custo)

---

## 9.4 Alertas e Ações Corretivas

### Alertas Críticos

| Alerta | Threshold | Ação |
|--------|-----------|------|
| Churn > 7% | 7%/mês | Revisar produto, entrevistar churned |
| CAC > R$ 5k | R$ 5k | Pausar canais ineficientes |
| LTV/CAC < 3x | 3x | Otimizar onboarding, reduzir churn |
| Burn Rate > R$ 70k | R$ 70k | Revisar custos, pausar contratações |
| Conversão < 10% | 10% | Melhorar onboarding, trial experience |

---

## 9.5 Revisão Trimestral

**A cada trimestre, revisar:**

1. **Financeiro**
   - MRR vs Meta
   - CAC vs Meta
   - Churn vs Meta
   - Burn rate vs Orçamento

2. **Produto**
   - NPS
   - Feature adoption
   - Time to value
   - Churn reasons

3. **Marketing**
   - Canais de aquisição
   - ROI por canal
   - Ajustar budget

4. **Equipe**
   - Performance
   - Necessidade de contratação
   - Orçamento vs Realizado

---

# CONCLUSÃO

## Resumo Financeiro

**Investimento Total Ano 1:** R$ 651.900  
**Break-even:** Mês 9  
**MRR Mês 12:** R$ 562k  
**ARR Ano 1:** R$ 6,7M  
**ROI Investidor (36 meses):** 35-60x  
**Valuation (36 meses):** R$ 560M  

## Vantagens Competitivas Financeiras

1. ✅ **Infraestrutura otimizada:** 67% economia vs AWS/GCP
2. ✅ **IA cascateamento:** 70% economia vs modelo único
3. ✅ **Margem alta:** 85% gross margin
4. ✅ **Unit economics saudáveis:** LTV/CAC 5,7x
5. ✅ **Break-even rápido:** Mês 9

## Próximos Passos

1. ✅ Validar premissas com beta testers
2. ✅ Ajustar pricing se necessário
3. ✅ Otimizar CAC por canal
4. ✅ Monitorar churn e agir proativamente
5. ✅ Reinvestir lucros em crescimento acelerado

---

**Smart Work Business**  
*Transformando Dados em Estratégia, Estratégia em Ação e Ação em Resultados*

**Última Atualização:** Novembro 2025


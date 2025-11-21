# MÓDULOS E FUNCIONALIDADES
## Smart Work Business - Documento 2

---

## ÍNDICE

1. [Jornada do Usuário](#1-jornada-do-usuário)
2. [Multi-Tenant e Contratação](#2-multi-tenant-e-contratação)
3. [Módulos do Sistema](#3-módulos-do-sistema)
4. [Fluxos Principais](#4-fluxos-principais)

---

# 1. JORNADA DO USUÁRIO

## 1.1 Jornada Completa (Do Primeiro Acesso ao Uso Diário)

```
┌──────────────────────────────────────────────────────────┐
│          FASE 1: DESCOBERTA E CONTRATAÇÃO                │
├──────────────────────────────────────────────────────────┤
│  1. Landing Page                                         │
│     → Conhece o produto                                  │
│     → Vê casos de sucesso                                │
│     → Compara planos                                     │
│                                                          │
│  2. Teste Grátis (7 dias)                               │
│     → Cadastro simples (email + senha)                  │
│     → Cria organização                                   │
│     → Entra no trial                                     │
│                                                          │
│  3. Onboarding Guiado (Dias 1-7)                        │
│     → Wizard inicial (5 passos)                         │
│     → Cria primeiro objetivo SMART                       │
│     → Convida 2-3 membros da equipe                     │
│     → Vê dashboard funcionando                           │
│                                                          │
│  4. Contratação                                          │
│     → Escolhe plano (Starter/Professional/Business/     │
│       Enterprise)                                        │
│     → Pagamento via Stripe                               │
│     → Confirmação e boas-vindas                          │
└──────────────────────────────────────────────────────────┘
           ↓
┌──────────────────────────────────────────────────────────┐
│          FASE 2: ESTRUTURAÇÃO (Dias 8-30)               │
├──────────────────────────────────────────────────────────┤
│  1. Definição de Objetivos Estratégicos                 │
│     → Cria 3-5 objetivos principais                     │
│     → Define métricas e prazos                          │
│     → Atribui responsáveis                              │
│                                                          │
│  2. Cascateamento                                        │
│     → IA sugere objetivos táticos                       │
│     → Aprova e ajusta                                   │
│     → Desdobra em objetivos operacionais                │
│                                                          │
│  3. Mapeamento de Processos                             │
│     → Identifica processos críticos                     │
│     → Modela 2-3 processos em BPMN                      │
│     → Documenta POPs básicos                            │
│                                                          │
│  4. Configuração de Dashboards                          │
│     → Configura KPIs principais                         │
│     → Personaliza visualizações                         │
│     → Define alertas                                    │
└──────────────────────────────────────────────────────────┘
           ↓
┌──────────────────────────────────────────────────────────┐
│          FASE 3: OPERAÇÃO (Dia 31+)                     │
├──────────────────────────────────────────────────────────┤
│  ROTINA DIÁRIA DO USUÁRIO                                │
│                                                          │
│  Manhã (5-10 min):                                       │
│  ├─ Abre dashboard                                       │
│  ├─ Vê alertas e desvios                                │
│  ├─ Consulta IA: "Como estamos hoje?"                   │
│  └─ Prioriza tarefas do dia                             │
│                                                          │
│  Durante o Dia:                                          │
│  ├─ Atualiza progresso de objetivos                     │
│  ├─ Executa tarefas no Kanban                           │
│  ├─ Comenta em objetivos/tarefas                        │
│  └─ Recebe notificações inteligentes                    │
│                                                          │
│  Fim do Dia (5 min):                                     │
│  ├─ Marca tarefas concluídas                            │
│  ├─ Registra progresso                                  │
│  └─ IA sugere prioridades para amanhã                   │
│                                                          │
│  Semanal:                                                │
│  ├─ Reunião com dashboard projetado                     │
│  ├─ Review de objetivos                                 │
│  ├─ Ajustes de prioridades                              │
│  └─ Relatório automático por email                      │
└──────────────────────────────────────────────────────────┘
```

## 1.2 Personas e Casos de Uso

### Persona 1: CEO / Founder

**Objetivo:** Visão estratégica e controle do negócio

**Jornada:**
1. Acorda → Abre app no celular
2. Dashboard executivo mostra status geral
3. Consulta IA: "Quais objetivos críticos?"
4. Toma decisões baseadas em dados reais
5. Atualiza prioridades estratégicas

**Tempo diário:** 10-15 minutos

---

### Persona 2: Gerente / Coordenador

**Objetivo:** Garantir execução e resultados da equipe

**Jornada:**
1. Abre dashboard tático
2. Vê progresso dos objetivos do time
3. Identifica gargalos em processos
4. Atribui tarefas e prioridades
5. Acompanha execução via Kanban

**Tempo diário:** 30-45 minutos

---

### Persona 3: Colaborador / Analista

**Objetivo:** Executar tarefas com clareza

**Jornada:**
1. Vê lista de tarefas do dia
2. Executa seguindo POPs
3. Atualiza status no Kanban
4. Registra tempo gasto
5. Marca como concluído

**Tempo diário:** 5-10 minutos (gestão), resto executando

---

# 2. MULTI-TENANT E CONTRATAÇÃO

## 2.1 Como Funciona o Multi-Tenant

```
┌─────────────────────────────────────────────────────────┐
│             SMART WORK BUSINESS APP                      │
│                (Uma Instância)                           │
├─────────────────────────────────────────────────────────┤
│                                                          │
│  ┌──────────────────┐  ┌──────────────────┐            │
│  │ Organização A    │  │ Organização B    │            │
│  │ (Startup Tech)   │  │ (Indústria)      │            │
│  ├──────────────────┤  ├──────────────────┤            │
│  │ • 15 usuários    │  │ • 50 usuários    │            │
│  │ • Starter Plan   │  │ • Professional   │            │
│  │ • Dados isolados │  │ • Dados isolados │            │
│  └──────────────────┘  └──────────────────┘            │
│                                                          │
│  ┌──────────────────┐  ┌──────────────────┐            │
│  │ Organização C    │  │ Organização D    │            │
│  │ (E-commerce)     │  │ (Consultoria)    │            │
│  ├──────────────────┤  ├──────────────────┤            │
│  │ • 100 usuários   │  │ • 30 usuários    │            │
│  │ • Enterprise     │  │ • Professional   │            │
│  │ • Dados isolados │  │ • Dados isolados │            │
│  └──────────────────┘  └──────────────────┘            │
│                                                          │
└─────────────────────────────────────────────────────────┘

📌 CADA ORGANIZAÇÃO:
- Domínio único: empresa-a.smartwork.com.br (opcional)
- Dados completamente isolados
- Plano e billing independente
- Configurações próprias
- Usuários e permissões próprias
```

## 2.2 Processo de Contratação Detalhado

### Passo 1: Cadastro Inicial (2 minutos)

```
┌─────────────────────────────────────┐
│  PÁGINA DE CADASTRO                 │
├─────────────────────────────────────┤
│                                     │
│  Nome Completo:  [______________]  │
│  Email:          [______________]  │
│  Senha:          [______________]  │
│  Nome da Empresa: [_____________]  │
│  Setor:          [Dropdown v    ]  │
│  Porte:          [Dropdown v    ]  │
│                                     │
│  [✓] Aceito os termos de uso       │
│                                     │
│  [ Iniciar Teste Grátis 7 dias ] │
│                                     │
│  Login com Google [G]              │
└─────────────────────────────────────┘
```

**O que acontece:**
1. Cria usuário
2. Cria organização
3. Usuário vira OWNER da organização
4. Inicia trial de 7 dias
5. Redireciona para onboarding

---

### Passo 2: Onboarding Guiado (10 minutos)

```
╔════════════════════════════════════════╗
║  BEM-VINDO AO SMART WORK BUSINESS!    ║
╠════════════════════════════════════════╣
║                                        ║
║  Vamos configurar em 5 passos:        ║
║                                        ║
║  [1] ━━━━━━━━━ [2] [3] [4] [5]       ║
║   ↑                                    ║
║  Você está aqui                        ║
║                                        ║
║  PASSO 1: Configure seu Perfil        ║
║  ────────────────────────────────      ║
║                                        ║
║  Foto (opcional):  [📷 Upload]        ║
║  Cargo:           [______________]     ║
║  Telefone:        [______________]     ║
║                                        ║
║           [ Pular ]    [ Próximo → ]  ║
╚════════════════════════════════════════╝

PASSO 2: Crie Seu Primeiro Objetivo
PASSO 3: Convide Sua Equipe
PASSO 4: Configure Dashboard
PASSO 5: Tour Guiado
```

---

### Passo 3: Uso Durante Trial (Dias 1-7)

**Recursos Disponíveis no Trial:**
- ✅ Todos os módulos (acesso completo)
- ✅ Até 5 usuários
- ✅ Objetivos limitados
- ✅ IA Consultor (20 perguntas/dentro do TRIAL após as 20 só contratando o plano para normalizar)
- ✅ Suporte por email

**Lembretes:**
- Dia 7: Email "Metade do trial, precisa de ajuda?"
- Dia 11: Email "Faltam 3 dias, veja o que conseguiu"
- Dia 13: Email "Últimas 24h, escolha seu plano"

---

### Passo 4: Escolha do Plano (Dia 7 ou antes)

```
┌─────────────────────────────────────────────────────────┐
│          ESCOLHA SEU PLANO                              │
├─────────────────────────────────────────────────────────┤
│                                                          │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐ │
│  │   STARTER    │  │ PROFESSIONAL │  │  ENTERPRISE  │ │
│  ├──────────────┤  ├──────────────┤  ├──────────────┤ │
│  │ R$ 497/mês   │  │ R$ 1.497/mês │  │ R$ 3.997/mês │ │
│  │              │  │              │  │              │ │
│  │ • 15 usuários│  │ • 50 usuários│  │ • Ilimitado  │ │
│  │ • Básico     │  │ • Avançado   │  │ • Completo   │ │
│  │ • Suporte    │  │ • Suporte    │  │ • Gerente    │ │
│  │   email      │  │   prioritário│  │   dedicado   │ │
│  │              │  │              │  │              │ │
│  │ [Escolher]   │  │ [Escolher]   │  │ [Contato]    │ │
│  └──────────────┘  └──────────────┘  └──────────────┘ │
│                                                          │
│  💳 Pagamento Seguro via Stripe                         │
│  📧 Fatura enviada automaticamente                       │
│  🔄 Cancele quando quiser                                │
└─────────────────────────────────────────────────────────┘
```

---

### Passo 5: Checkout (Stripe)

```
┌─────────────────────────────────────┐
│  FINALIZAR ASSINATURA               │
├─────────────────────────────────────┤
│                                     │
│  Plano: Professional                │
│  Valor: R$ 997/mês                  │
│  Usuários: Até 30                   │
│                                     │
│  ────────────────────────────────   │
│                                     │
│  Cartão: [________________]         │
│  Validade: [__/__]  CVV: [___]     │
│  Nome: [______________________]     │
│                                     │
│  CPF/CNPJ: [_______________]       │
│                                     │
│  [✓] Concordo com renovação auto    │
│                                     │
│  [ Confirmar Assinatura ]          │
│                                     │
│  🔒 Pagamento seguro                │
│  Powered by Stripe                  │
└─────────────────────────────────────┘
```

**Após confirmação:**
1. ✅ Assinatura ativada
2. ✅ Email de boas-vindas
3. ✅ Acesso a todos os recursos do plano
4. ✅ Fatura enviada
5. ✅ Cobrança recorrente configurada

---

## 2.3 Gestão de Membros (Multi-User)

### Estrutura de Permissões

```
OWNER (Dono)
  ├─ Tudo (inclusive billing e excluir org)
  │
  ├─ ADMIN
  │   ├─ Gerenciar usuários
  │   ├─ Configurações da org
  │   └─ Sem acesso a billing
  │
  ├─ MANAGER
  │   ├─ Criar/editar objetivos
  │   ├─ Gerenciar processos
  │   └─ Ver relatórios gerenciais
  │
  ├─ MEMBER
  │   ├─ Ver objetivos
  │   ├─ Executar tarefas
  │   └─ Registrar progresso
  │
  └─ VIEWER
      └─ Somente leitura
```

### Convidar Membros

```
┌─────────────────────────────────────┐
│  CONVIDAR MEMBROS                   │
├─────────────────────────────────────┤
│                                     │
│  Email: [____________________]     │
│         [____________________]     │
│         [____________________]     │
│                                     │
│  Função: [Manager ▼]               │
│                                     │
│  Mensagem (opcional):               │
│  [__________________________]      │
│  [__________________________]      │
│                                     │
│  [ Enviar Convites ]               │
└─────────────────────────────────────┘

→ Convidado recebe email
→ Clica no link
→ Cria senha
→ Entra na organização
```

---

# 3. MÓDULOS DO SISTEMA

## 3.1 Visão Geral dos 10 Módulos

```
┌────────────────────────────────────────────────────────┐
│                SMART WORK BUSINESS APP                  │
├────────────────────────────────────────────────────────┤
│                                                         │
│  1️⃣  AUTENTICAÇÃO & ORGANIZAÇÕES                       │
│  2️⃣  OBJETIVOS SMART & OKRs                            │
│  3️⃣  BPM/BPMN & POPs                                   │
│  4️⃣  ANALYTICS & DASHBOARDS                            │
│  5️⃣  PDCA & MELHORIA CONTÍNUA                          │
│  6️⃣  TAREFAS & 5W2H                                    │
│  7️⃣  CONSULTOR IA                                      │
│  8️⃣  COLABORAÇÃO                                        │
│  9️⃣  PAGAMENTOS & BILLING                              │
│  🔟  GOVERNANÇA (Embutida em todos)                     │
│                                                         │
└────────────────────────────────────────────────────────┘
```

**ATENÇÃO:** Governança NÃO é um módulo separado. É embutida nativamente em todos os módulos (ISO 9001, ISO 27001, ISO 31000, LGPD).

---

## 3.2 Módulo 1: Autenticação & Organizações

**O que faz:** Gerencia acesso e multi-tenant

**Funcionalidades:**
- Login/Registro (email/senha ou Google)
- MFA (2FA) opcional
- Gerenciamento de organizações
- Convites e membros
- RBAC (5 roles: Owner, Admin, Manager, Member, Viewer)
- Billing integrado com Stripe

---

## 3.2 Módulo 2: Objetivos SMART & OKRs

**O que faz:** Core do sistema - gestão de objetivos

**Funcionalidades:**
- ✅ Criar objetivo SMART (wizard guiado)
- ✅ Validação automática dos critérios SMART
- ✅ Cascateamento (manual e automático via IA)
- ✅ Hierarquia (Estratégico → Tático → Operacional)
- ✅ OKRs trimestrais
- ✅ Tracking de progresso em tempo real
- ✅ Alertas de desvio
- ✅ Visualização em árvore
- ✅ Comentários e discussões

**Telas principais:**
- Lista de objetivos (filtros e busca)
- Criar/Editar objetivo (wizard SMART)
- Detalhes do objetivo (progresso, OKRs, tarefas)
- Árvore hierárquica (visualização cascateamento)
- Dashboard de objetivos

---

## 3.3 Módulo 3: BPM/BPMN & POPs

**O que faz:** Modelagem e documentação de processos

**Funcionalidades:**
- ✅ Editor BPMN 2.0 (bpmn-js)
- ✅ Biblioteca de processos
- ✅ Versionamento de processos
- ✅ POPs digitais vinculados a processos
- ✅ Matriz RACI automática
- ✅ Análise de gargalos
- ✅ IA sugere otimizações

**Telas principais:**
- Lista de processos
- Editor BPMN
- Visualizador BPMN
- POPs (CRUD)
- Matriz RACI

---

## 3.4 Módulo 4: Analytics & Dashboards

**O que faz:** Visualização de dados e análises

**Funcionalidades:**
- ✅ 3 Dashboards (Estratégico, Tático, Operacional)
- ✅ KPIs customizáveis
- ✅ Análise 80/20 (Pareto)
- ✅ Gráficos interativos
- ✅ Filtros dinâmicos
- ✅ Drill-down
- ✅ Exportação (PDF, Excel)
- ✅ Relatórios automáticos
- ✅ Análises preditivas (IA)

**Dashboards:**

**Estratégico (CEO):**
- Progresso dos objetivos estratégicos
- KPIs principais
- Análise 80/20
- Tendências

**Tático (Gerentes):**
- Objetivos do departamento
- Performance de processos
- Gargalos
- Equipe

**Operacional (Time):**
- Tarefas do dia
- Métricas em tempo real
- Checklists
- Alertas

---

## 3.5 Módulo 5: PDCA & Melhoria Contínua

**O que faz:** Ciclos sistemáticos de melhoria

**Funcionalidades:**
- ✅ Wizard PDCA guiado
- ✅ Plan: Problema, meta, análise, plano
- ✅ Do: Execução e evidências
- ✅ Check: Resultados e avaliação
- ✅ Act: Padronização e próximos passos
- ✅ Lições aprendidas
- ✅ Vinculação com objetivos

---

## 3.6 Módulo 6: Tarefas & 5W2H

**O que faz:** Gestão operacional de tarefas

**Funcionalidades:**
- ✅ CRUD de tarefas
- ✅ Formulário 5W2H completo
- ✅ Kanban board
- ✅ Calendário
- ✅ Checklists
- ✅ Time tracking
- ✅ Comentários
- ✅ Anexos
- ✅ Priorização automática (Eisenhower)

**Visualizações:**
- Lista
- Kanban (To Do, Doing, Review, Done)
- Calendário
- Timeline (Gantt - futuro)

---

## 3.7 Módulo 7: Consultor IA

**O que faz:** Assistente inteligente 24/7

**Funcionalidades:**
- ✅ Chat conversacional
- ✅ Contexto completo da empresa (RAG)
- ✅ Análises sob demanda
- ✅ Sugestões proativas
- ✅ Cascateamento inteligente
- ✅ Criação automática de conteúdo
- ✅ Identificação de padrões

**Casos de uso:**
- "Como estamos nos objetivos?"
- "Por que vendas caíram?"
- "Sugira melhorias no processo X"
- "Crie objetivos para o trimestre"
- "Onde focar esta semana?"

---

## 3.8 Módulo 8: Colaboração

**O que faz:** Comunicação contextual

**Funcionalidades:**
- ✅ Comentários em objetivos/tarefas/processos
- ✅ Menções (@usuario)
- ✅ Base de conhecimento
- ✅ Atas de reunião
- ✅ Follow-ups

---

## 3.9 Módulo 9: Pagamentos & Billing

**O que faz:** Gestão de assinaturas

**Funcionalidades:**
- ✅ Integração Stripe
- ✅ Checkout seguro
- ✅ Assinaturas recorrentes
- ✅ Upgrade/downgrade automático
- ✅ Customer Portal (autoatendimento)
- ✅ Faturas automáticas
- ✅ Webhooks

---

## 3.10 Governança (Embutida)

**O que faz:** Compliance nativo em tudo

**NÃO é módulo separado! É DNA da plataforma.**

**ISO 9001 (Qualidade):**
- Objetivos da qualidade = Objetivos SMART
- Processos documentados = BPM
- Melhoria contínua = PDCA

**ISO 27001 (Segurança):**
- Controles de acesso (RBAC)
- Criptografia (TLS + AES-256)
- Trilha de auditoria

**ISO 31000 (Riscos):**
- Avaliação de riscos em objetivos
- Identificação em processos
- Alertas baseados em riscos

**LGPD:**
- Dados pessoais identificados
- Consentimento controlado
- Anonimização automática
- Direitos dos titulares

---

# 4. FLUXOS PRINCIPAIS

## 4.1 Fluxo: Criar e Cascatear Objetivo

```
1. CEO clica "Novo Objetivo"
   ↓
2. Wizard SMART (5 etapas)
   - Specific: "Reduzir churn para 3%"
   - Measurable: Métrica + Meta (5% → 3%)
   - Achievable: Validação de viabilidade
   - Relevant: Vínculo com estratégia
   - Time-bound: Prazo (6 meses)
   ↓
3. IA sugere: "Desdobrar em objetivos táticos?"
   ↓
4. CEO aprova sugestões da IA
   ↓
5. Sistema cria automaticamente:
   - 3 objetivos táticos (gerentes)
   - 8 objetivos operacionais (equipe)
   - Processos relacionados
   - POPs necessários
   - Tarefas iniciais
   ↓
6. Notificações enviadas aos responsáveis
   ↓
7. Dashboard atualizado em tempo real
```

---

## 4.2 Fluxo: Consultar IA

```
1. Usuário abre chat do Consultor IA
   ↓
2. Pergunta: "Por que objetivo X está atrasado?"
   ↓
3. IA analisa:
   - Progresso do objetivo
   - Tarefas relacionadas
   - Processos envolvidos
   - Dados históricos
   ↓
4. IA responde:
   "O objetivo está 20% atrasado por 3 motivos:
    1. Processo Y tem gargalo (etapa 3)
    2. Time sobrecarregado (5 tarefas/pessoa)
    3. Falta de recurso Z
    
    Sugestões:
    - Otimizar processo Y (remover etapa 3)
    - Realocar 2 pessoas do projeto A
    - Aprovar compra de recurso Z"
   ↓
5. Usuário: "Crie plano de ação"
   ↓
6. IA gera plano 5W2H completo
   ↓
7. Usuário revisa e aprova
   ↓
8. Sistema cria tarefas e atribui responsáveis
```

---

## 4.3 Fluxo: Reunião Semanal com Dados

```
1. Segunda-feira 9h - Reunião de Gestão
   ↓
2. Gerente projeta Dashboard na tela
   ↓
3. Todos veem dados em tempo real:
   - Objetivos: status, progresso, alertas
   - Processos: gargalos, lead time
   - Tarefas: feitas vs planejadas
   - KPIs: atual vs meta
   ↓
4. Discussão baseada em DADOS, não opiniões
   ↓
5. Decisões tomadas:
   - Priorizar objetivo X
   - Otimizar processo Y
   - Realocar recurso Z
   ↓
6. Decisões registradas no sistema
   ↓
7. Tarefas criadas e atribuídas
   ↓
8. Ata automática enviada por email
```

---

Pronto! Documento 2 concluído. Segue para Documento 3?


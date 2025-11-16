# Smart Work Business SaaS
## Plataforma Integrada de Gestão Empresarial

[![License](https://img.shields.io/badge/license-Proprietary-red.svg)]()
[![Version](https://img.shields.io/badge/version-1.0.0--beta-blue.svg)]()
[![Status](https://img.shields.io/badge/status-in%20development-yellow.svg)]()

**Transformando Dados em Estratégia, Estratégia em Ação e Ação em Resultados**

---

## 📋 Sobre o Projeto

Smart Work Business é uma plataforma SaaS completa de gestão empresarial que integra **estratégia, tática e operação** em um único sistema, com inteligência artificial embutida e governança nativa.

### Diferencial

Única plataforma que materializa um **método completo de gestão** (Drucker + Deming + Owen), não apenas uma ferramenta.

### Principais Funcionalidades

- ✅ **Objetivos SMART** com cascateamento automático
- ✅ **Dashboards** em tempo real (estratégico, tático, operacional)
- ✅ **BPM/BPMN 2.0** para modelagem de processos
- ✅ **Consultor IA** especialista 24/7 (GPT-4)
- ✅ **Analytics** avançado com análise 80/20
- ✅ **PDCA** e **5W2H** digitais
- ✅ **Governança** nativa (ISO 9001, ISO 27001, ISO 31000, LGPD)
- ✅ **Multi-tenant** com planos Starter, Professional e Enterprise

---

## 🏗️ Arquitetura

### Stack Tecnológico

```
Frontend:   Next.js 14 + TypeScript + Tailwind CSS
Backend:    NestJS + TypeScript + Prisma ORM
Database:   PostgreSQL 16 + Redis 7 + TimescaleDB
IA:         OpenAI GPT-4 + LangChain
Payments:   Stripe
Emails:     Brevo
Deploy:     Ubuntu Server 24.04 + Docker + NGINX
```

### Estrutura do Projeto

```
smartwork-saas/
├── frontend/              # Next.js application
├── backend/               # NestJS application
├── prisma/                # Database schema
├── nginx/                 # NGINX configurations
├── scripts/               # Utility scripts
├── docs/                  # Complete documentation
├── docker-compose.yml     # Development environment
└── docker-compose.prod.yml # Production environment
```

---

## 🚀 Quick Start

### Pré-requisitos

- Node.js 20+ LTS
- Docker & Docker Compose
- Git

### 1. Clone o Repositório

```bash
git clone https://github.com/sua-org/smartwork-saas.git
cd smartwork-saas
```

### 2. Configurar Ambiente

```bash
# Copiar variáveis de ambiente
cp .env.example .env.local
cp frontend/.env.example frontend/.env.local
cp backend/.env.example backend/.env

# Editar com suas credenciais
nano .env.local
```

### 3. Iniciar Containers

```bash
# PostgreSQL + Redis
docker-compose up -d
```

### 4. Instalar Dependências

```bash
# Frontend
cd frontend
npm install

# Backend
cd ../backend
npm install
```

### 5. Setup Database

```bash
cd backend
npx prisma generate
npx prisma db push
npx prisma db seed  # Opcional: dados de teste
```

### 6. Iniciar Desenvolvimento

```bash
# Terminal 1 - Frontend
cd frontend
npm run dev

# Terminal 2 - Backend
cd backend
npm run start:dev

# Terminal 3 - Prisma Studio (opcional)
npx prisma studio
```

**Acesse:**
- Frontend: http://localhost:3000
- Backend API: http://localhost:4000
- Prisma Studio: http://localhost:5555
- API Docs: http://localhost:4000/api

---

## 📚 Documentação

### Documentação Técnica Completa

- **[Projeto Técnico](PROJETO-TECNICO-SMART-WORK-SAAS.md)** - Arquitetura e visão geral
- **[Módulos e Funcionalidades](docs/MODULOS-E-FUNCIONALIDADES.md)** - Detalhamento completo
- **[Dependências e Configurações](docs/DEPENDENCIAS-E-CONFIGURACOES.md)** - Setup e configs
- **[Roadmap de Desenvolvimento](docs/ROADMAP-DESENVOLVIMENTO.md)** - Cronograma e sprints
- **[Resumo Executivo](docs/RESUMO-EXECUTIVO.md)** - Visão rápida

### Apresentação do Produto

- **[Apresentação SaaS](APRESENTACAO-SAAS-SMART-WORK-BUSINESS.md)** - Documento completo do produto

---

## 🛠️ Desenvolvimento

### Comandos Úteis

```bash
# Frontend
npm run dev          # Desenvolvimento
npm run build        # Build produção
npm run lint         # Linter
npm run type-check   # TypeScript check
npm test             # Testes

# Backend
npm run start:dev    # Desenvolvimento
npm run build        # Build produção
npm run lint         # Linter
npm test             # Testes
npm run test:cov     # Cobertura

# Database
npx prisma studio    # GUI do banco
npx prisma migrate dev  # Criar migration
npx prisma generate  # Gerar client
npx prisma db seed   # Seed data

# Docker
docker-compose up -d      # Iniciar
docker-compose down       # Parar
docker-compose logs -f    # Logs
```

### Padrões de Código

#### Commits (Conventional Commits)

```bash
feat: adiciona módulo de objetivos SMART
fix: corrige validação de email
docs: atualiza README
style: formata código
refactor: simplifica lógica
test: adiciona testes
chore: atualiza dependências
```

#### Branches

```
main           → produção (protegido)
develop        → desenvolvimento (protegido)
feature/*      → novas features
bugfix/*       → correção de bugs
hotfix/*       → correções urgentes
```

---

## 🧪 Testes

### Executar Testes

```bash
# Frontend
cd frontend
npm test              # Unit tests
npm run test:watch    # Watch mode
npm run test:coverage # Coverage

# Backend
cd backend
npm test              # Unit tests
npm run test:e2e      # E2E tests
npm run test:cov      # Coverage
```

### Cobertura Mínima

- **Unit Tests:** 70%
- **Integration Tests:** 60%
- **E2E Tests:** Critical paths

---

## 🚢 Deploy

### Ambiente de Produção

**Servidor:** Ubuntu Server 24.04 LTS

```bash
# 1. Setup servidor (primeira vez)
./scripts/setup-server.sh

# 2. Build e deploy
git push origin main  # Trigger CI/CD

# Ou manual
./scripts/deploy.sh production
```

### Docker Compose Production

```bash
docker-compose -f docker-compose.prod.yml up -d --build
```

### Verificar Status

```bash
# Health check
curl https://api.smartworkbusiness.com.br/health

# Logs
docker logs -f smartwork-backend
docker logs -f smartwork-frontend

# Recursos
docker stats
```

---

## 🔒 Segurança

### Checklist de Segurança

- [x] HTTPS enforced
- [x] JWT authentication
- [x] CORS configurado
- [x] Rate limiting
- [x] SQL injection prevenido (Prisma)
- [x] XSS prevenido
- [x] CSRF protection
- [x] Helmet.js
- [x] Input validation (Zod)
- [x] Secrets em variáveis de ambiente
- [x] LGPD compliance nativo
- [x] Auditoria completa

### Variáveis de Ambiente Sensíveis

```bash
# NUNCA commitar
.env
.env.local
.env.production

# Usar GitHub Secrets para CI/CD
# Usar AWS Secrets Manager / Azure Key Vault em produção
```

---

## 📊 Monitoramento

### Stack de Observabilidade

- **Error Tracking:** Sentry
- **Metrics:** Prometheus + Grafana
- **Logs:** Winston + Betterstack
- **Uptime:** UptimeRobot
- **APM:** Sentry Performance

### Dashboards

- **Grafana:** http://grafana.smartworkbusiness.com.br
- **Sentry:** http://sentry.io/smartwork

---

## 🤝 Contribuindo

### Fluxo de Trabalho

1. **Fork** o projeto
2. **Clone** seu fork
3. **Crie** uma branch (`git checkout -b feature/amazing-feature`)
4. **Commit** suas mudanças (`git commit -m 'feat: add amazing feature'`)
5. **Push** para a branch (`git push origin feature/amazing-feature`)
6. **Abra** um Pull Request

### Code Review

- Pelo menos 1 aprovação necessária
- Todos os testes passando
- Cobertura mantida
- Linter sem erros
- Documentação atualizada

---

## 📝 Convenções

### Nomenclatura

```typescript
// Componentes: PascalCase
UserProfile.tsx
ObjectiveCard.tsx

// Utilities: camelCase
formatDate.ts
apiClient.ts

// Constantes: SCREAMING_SNAKE_CASE
MAX_RETRIES.ts
API_ENDPOINTS.ts

// CSS: kebab-case
user-profile.module.css
```

### TypeScript

```typescript
// Interfaces com I prefix
interface IUser {}

// Types com Type suffix
type UserType = {}

// Enums com PascalCase
enum UserRole {
  ADMIN = 'ADMIN',
  USER = 'USER'
}
```

---

## 🗂️ Estrutura de Dados

### Principais Entidades

```prisma
User            → Usuários do sistema
Organization    → Multi-tenant
Objective       → Objetivos SMART
OKR             → Key Results
BPMProcess      → Processos BPMN
POP             → Procedimentos Operacionais
PDCACycle       → Ciclos PDCA
Task            → Tarefas 5W2H
KPI             → Indicadores
Dashboard       → Dashboards
AuditLog        → Trilha de auditoria
```

### Relacionamentos

```
Organization (1) ──── (N) User
Organization (1) ──── (N) Objective
Objective (1)    ──── (N) OKR
Objective (1)    ──── (N) Task
Organization (1) ──── (N) BPMProcess
BPMProcess (1)   ──── (N) POP
```

---

## 🔗 Links Úteis

### Documentação Externa

- [Next.js](https://nextjs.org/docs)
- [NestJS](https://docs.nestjs.com)
- [Prisma](https://www.prisma.io/docs)
- [OpenAI API](https://platform.openai.com/docs)
- [Stripe](https://stripe.com/docs)

### Ferramentas

- [Figma Design](https://figma.com/file/...)
- [Notion Roadmap](https://notion.so/...)
- [Linear Issues](https://linear.app/...)

---

## 👥 Equipe

### Core Team

- **Tech Lead:** [Nome] - [@github]
- **Full-Stack:** [Nome] - [@github]
- **Full-Stack:** [Nome] - [@github]
- **Backend IA:** [Nome] - [@github]
- **DevOps:** [Nome] - [@github]
- **UX/UI:** [Nome] - [@figma]
- **QA:** [Nome] - [@github]

### Contato

- **Email:** dev@smartworkbusiness.com.br
- **Slack:** #smartwork-dev
- **GitHub:** github.com/smartwork-business

---

## 📄 Licença

**Proprietary License**

© 2025 Smart Work Business. Todos os direitos reservados.

Este software é proprietário e confidencial. Uso não autorizado é estritamente proibido.

---

## 🎯 Roadmap

### Fase MVP (Meses 1-3) ✅
- [x] Autenticação e Multi-tenant
- [x] Objetivos SMART
- [x] Dashboards básicos
- [x] Tarefas e Kanban
- [x] BPM básico
- [x] Pagamentos Stripe
- [x] Consultor IA básico

### Fase 2 (Meses 4-6) 🔄
- [ ] IA Avançada (Cascateamento)
- [ ] PDCA completo
- [ ] Análise 80/20
- [ ] POPs digitais
- [ ] Governança (ISOs)
- [ ] API Pública
- [ ] Mobile PWA

### Fase 3 (Meses 7-12) 📅
- [ ] Integrações externas (20+)
- [ ] Marketplace
- [ ] White-label
- [ ] Advanced Analytics
- [ ] Mobile Apps nativo

---

## 📈 Status do Projeto

### Métricas Atuais

- **Cobertura de Testes:** 0% → Meta: 70%
- **Performance API:** N/A → Meta: <200ms
- **Uptime:** N/A → Meta: 99.9%
- **Usuários Beta:** 0 → Meta: 50

### Sprints

- **Sprint Atual:** Sprint 1 - Auth + Multi-tenant
- **Sprint Próximo:** Sprint 2 - Objetivos SMART
- **Duração Sprint:** 2 semanas

---

## 🐛 Bugs Conhecidos

- [ ] Nenhum (projeto iniciando)

**Reporte bugs:** https://github.com/smartwork-business/smartwork-saas/issues

---

## 💡 FAQ

### Como contribuir?

Veja a seção [Contribuindo](#-contribuindo)

### Como reportar bugs?

Abra uma issue no GitHub com label `bug`

### Onde está a documentação da API?

http://localhost:4000/api (desenvolvimento)
https://api.smartworkbusiness.com.br/api (produção)

### Como rodar testes?

```bash
npm test              # Todos os testes
npm run test:watch    # Watch mode
npm run test:cov      # Com cobertura
```

---

## 🙏 Agradecimentos

Baseado em décadas de conhecimento de:
- **Peter Drucker** - Management by Objectives
- **W. Edwards Deming** - Gestão Baseada em Dados
- **John Owen** - Business Intelligence

---

## 📞 Suporte

### Para Desenvolvedores

- **Slack:** #smartwork-dev
- **Email:** dev@smartworkbusiness.com.br
- **Docs:** `/docs`

### Para Usuários

- **Website:** https://smartworkbusiness.com.br
- **Email:** contato@smartworkbusiness.com.br
- **WhatsApp:** +55 (XX) XXXX-XXXX

---

**Smart Work Business SaaS**  
*Transformando Dados em Estratégia, Estratégia em Ação e Ação em Resultados*

**Versão 1.0.0-beta** | **Novembro 2025**

---

🚀 **Vamos transformar a gestão empresarial brasileira!**


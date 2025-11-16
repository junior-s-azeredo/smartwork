# DEPENDÊNCIAS E CONFIGURAÇÕES
## Smart Work Business - Documento 4

---

## ÍNDICE

1. [Package.json (Frontend)](#1-packagejson-frontend)
2. [Package.json (Backend)](#2-packagejson-backend)
3. [Requirements.txt (AI Service)](#3-requirementstxt-ai-service)
4. [Schema Prisma](#4-schema-prisma)
5. [Variáveis de Ambiente](#5-variáveis-de-ambiente)
6. [Scripts Úteis](#6-scripts-úteis)

---

# 1. PACKAGE.JSON (FRONTEND)

```json
{
  "name": "smartwork-frontend",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint",
    "type-check": "tsc --noEmit",
    "test": "jest",
    "test:watch": "jest --watch",
    "test:coverage": "jest --coverage"
  },
  "dependencies": {
    "next": "^14.1.0",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "typescript": "^5.3.0",
    
    "@tanstack/react-query": "^5.17.0",
    "axios": "^1.6.5",
    
    "next-auth": "^5.0.0-beta.4",
    "bcryptjs": "^2.4.3",
    
    "zustand": "^4.4.7",
    
    "react-hook-form": "^7.49.3",
    "zod": "^3.22.4",
    "@hookform/resolvers": "^3.3.4",
    
    "@radix-ui/react-accordion": "^1.1.2",
    "@radix-ui/react-alert-dialog": "^1.0.5",
    "@radix-ui/react-avatar": "^1.0.4",
    "@radix-ui/react-checkbox": "^1.0.4",
    "@radix-ui/react-dialog": "^1.0.5",
    "@radix-ui/react-dropdown-menu": "^2.0.6",
    "@radix-ui/react-label": "^2.0.2",
    "@radix-ui/react-popover": "^1.0.7",
    "@radix-ui/react-select": "^2.0.0",
    "@radix-ui/react-separator": "^1.0.3",
    "@radix-ui/react-slot": "^1.0.2",
    "@radix-ui/react-tabs": "^1.0.4",
    "@radix-ui/react-toast": "^1.1.5",
    "@radix-ui/react-tooltip": "^1.0.7",
    
    "tailwindcss": "^3.4.1",
    "tailwind-merge": "^2.2.0",
    "tailwindcss-animate": "^1.0.7",
    "class-variance-authority": "^0.7.0",
    "clsx": "^2.1.0",
    
    "lucide-react": "^0.303.0",
    
    "recharts": "^2.10.4",
    "victory": "^36.9.2",
    "date-fns": "^3.0.6",
    
    "bpmn-js": "^15.0.0",
    "bpmn-modeler": "^15.0.0",
    
    "@dnd-kit/core": "^6.1.0",
    "@dnd-kit/sortable": "^8.0.0",
    "@dnd-kit/utilities": "^3.2.2",
    
    "@tiptap/react": "^2.1.13",
    "@tiptap/starter-kit": "^2.1.13",
    "@tiptap/extension-link": "^2.1.13",
    "@tiptap/extension-image": "^2.1.13",
    
    "dayjs": "^1.11.10",
    "lodash": "^4.17.21",
    "nanoid": "^5.0.4"
  },
  "devDependencies": {
    "@types/node": "^20.10.7",
    "@types/react": "^18.2.47",
    "@types/react-dom": "^18.2.18",
    "@types/bcryptjs": "^2.4.6",
    "@types/lodash": "^4.14.202",
    
    "eslint": "^8.56.0",
    "eslint-config-next": "^14.1.0",
    
    "@testing-library/react": "^14.1.2",
    "@testing-library/jest-dom": "^6.2.0",
    "jest": "^29.7.0",
    "jest-environment-jsdom": "^29.7.0",
    
    "autoprefixer": "^10.4.16",
    "postcss": "^8.4.33"
  }
}
```

---

# 2. PACKAGE.JSON (BACKEND)

```json
{
  "name": "smartwork-backend",
  "version": "1.0.0",
  "description": "Smart Work Business - Backend API",
  "author": "Smart Work Team",
  "private": true,
  "license": "UNLICENSED",
  "scripts": {
    "build": "nest build",
    "format": "prettier --write \"src/**/*.ts\" \"test/**/*.ts\"",
    "start": "nest start",
    "start:dev": "nest start --watch",
    "start:debug": "nest start --debug --watch",
    "start:prod": "node dist/main",
    "lint": "eslint \"{src,apps,libs,test}/**/*.ts\" --fix",
    "test": "jest",
    "test:watch": "jest --watch",
    "test:cov": "jest --coverage",
    "test:e2e": "jest --config ./test/jest-e2e.json",
    
    "prisma:generate": "prisma generate",
    "prisma:migrate": "prisma migrate dev",
    "prisma:push": "prisma db push",
    "prisma:seed": "ts-node prisma/seed.ts",
    "prisma:studio": "prisma studio"
  },
  "dependencies": {
    "@nestjs/common": "^10.3.0",
    "@nestjs/core": "^10.3.0",
    "@nestjs/platform-express": "^10.3.0",
    
    "@nestjs/config": "^3.1.1",
    "@nestjs/jwt": "^10.2.0",
    "@nestjs/passport": "^10.0.3",
    "passport": "^0.7.0",
    "passport-jwt": "^4.0.1",
    "passport-local": "^1.0.0",
    "bcryptjs": "^2.4.3",
    
    "@nestjs/throttler": "^5.1.1",
    
    "@prisma/client": "^5.8.1",
    
    "redis": "^4.6.12",
    "@nestjs/redis": "^5.0.0",
    
    "class-validator": "^0.14.0",
    "class-transformer": "^0.5.1",
    
    "@nestjs/swagger": "^7.1.17",
    "swagger-ui-express": "^5.0.0",
    
    "stripe": "^14.12.0",
    
    "axios": "^1.6.5",
    
    "@brevo/client": "^1.0.0",
    
    "winston": "^3.11.0",
    "nest-winston": "^1.9.4",
    
    "bullmq": "^5.1.9",
    "@nestjs/bull": "^10.0.1",
    
    "date-fns": "^3.0.6",
    "lodash": "^4.17.21",
    "nanoid": "^3.3.7"
  },
  "devDependencies": {
    "@nestjs/cli": "^10.3.0",
    "@nestjs/schematics": "^10.1.0",
    "@nestjs/testing": "^10.3.0",
    
    "@types/express": "^4.17.21",
    "@types/node": "^20.10.7",
    "@types/passport-jwt": "^4.0.0",
    "@types/passport-local": "^1.0.38",
    "@types/bcryptjs": "^2.4.6",
    "@types/lodash": "^4.14.202",
    
    "@typescript-eslint/eslint-plugin": "^6.18.1",
    "@typescript-eslint/parser": "^6.18.1",
    "eslint": "^8.56.0",
    "eslint-config-prettier": "^9.1.0",
    "eslint-plugin-prettier": "^5.1.2",
    "prettier": "^3.1.1",
    
    "jest": "^29.7.0",
    "@types/jest": "^29.5.11",
    "ts-jest": "^29.1.1",
    "supertest": "^6.3.3",
    "@types/supertest": "^6.0.2",
    
    "prisma": "^5.8.1",
    "ts-node": "^10.9.2",
    "typescript": "^5.3.3"
  }
}
```

---

# 3. REQUIREMENTS.TXT (AI SERVICE)

```txt
# AI Service - Python Dependencies
fastapi==0.109.0
uvicorn[standard]==0.27.0
pydantic==2.5.3
pydantic-settings==2.1.0

# OpenAI
openai==1.8.0
tiktoken==0.5.2

# LangChain
langchain==0.1.1
langchain-openai==0.0.2
langchain-community==0.0.10

# Vector Database
pgvector==0.2.4
psycopg2-binary==2.9.9

# Data Processing
pandas==2.1.4
numpy==1.26.3

# HTTP Clients
httpx==0.26.0
aiohttp==3.9.1

# Redis
redis==5.0.1
hiredis==2.3.2

# Utilities
python-dotenv==1.0.0
python-multipart==0.0.6

# Logging
structlog==24.1.0

# Testing
pytest==7.4.4
pytest-asyncio==0.23.3
httpx==0.26.0

# Type Checking
mypy==1.8.0
```

---

# 4. SCHEMA PRISMA

```prisma
// prisma/schema.prisma

generator client {
  provider = "prisma-client-js"
  previewFeatures = ["postgresqlExtensions"]
}

datasource db {
  provider   = "postgresql"
  url        = env("DATABASE_URL")
  extensions = [uuid_ossp(map: "uuid-ossp"), vector, pg_trgm]
}

// ============================================
// MULTI-TENANCY & AUTH
// ============================================

model User {
  id        String   @id @default(uuid())
  email     String   @unique
  name      String
  password  String
  avatar    String?
  
  // LGPD
  cpf            String?   @unique
  phone          String?
  dataConsentAt  DateTime?
  dataExportedAt DateTime?
  
  // Status
  emailVerified DateTime?
  isActive      Boolean   @default(true)
  
  // Timestamps
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  
  // Relations
  memberships    OrganizationMember[]
  objectives     Objective[]
  tasks          Task[]
  auditLogs      AuditLog[]
  aiConversations AIConversation[]
  
  @@index([email])
  @@map("users")
}

model Organization {
  id   String @id @default(uuid())
  name String
  slug String @unique
  
  // Settings
  logo        String?
  website     String?
  industry    String?
  size        String?   // "1-10", "11-50", "51-200", "201-500", "500+"
  
  // Status
  isActive    Boolean @default(true)
  
  // Timestamps
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  
  // Relations
  members         OrganizationMember[]
  subscription    Subscription?
  objectives      Objective[]
  tasks           Task[]
  processes       Process[]
  risks           Risk[]
  dashboards      Dashboard[]
  auditLogs       AuditLog[]
  
  @@index([slug])
  @@map("organizations")
}

model OrganizationMember {
  id             String   @id @default(uuid())
  role           Role     @default(MEMBER)
  
  // Status
  invitedAt      DateTime @default(now())
  joinedAt       DateTime?
  isActive       Boolean  @default(true)
  
  // Relations
  userId         String
  user           User     @relation(fields: [userId], references: [id], onDelete: Cascade)
  organizationId String
  organization   Organization @relation(fields: [organizationId], references: [id], onDelete: Cascade)
  
  @@unique([userId, organizationId])
  @@index([organizationId])
  @@map("organization_members")
}

enum Role {
  OWNER
  ADMIN
  MEMBER
  VIEWER
}

// ============================================
// SUBSCRIPTIONS (STRIPE)
// ============================================

model Subscription {
  id         String   @id @default(uuid())
  
  // Stripe
  stripeCustomerId       String?  @unique
  stripeSubscriptionId   String?  @unique
  stripePriceId          String?
  stripeCurrentPeriodEnd DateTime?
  
  // Plan
  plan       SubscriptionPlan   @default(TRIAL)
  status     SubscriptionStatus @default(ACTIVE)
  
  // Limits
  maxUsers         Int     @default(10)
  maxProcesses     Int     @default(5)
  aiQuestionsLimit Int     @default(20)
  aiQuestionsUsed  Int     @default(0)
  
  // AI Usage Tracking (por modelo)
  aiUsageNano      Int     @default(0)  // Queries usando GPT-5-nano
  aiUsageMini      Int     @default(0)  // Queries usando GPT-5-mini
  aiUsage51        Int     @default(0)  // Queries usando GPT-5.1
  aiCostThisMonth  Float   @default(0)  // Custo acumulado em USD
  
  // Billing
  amount           Float?
  currency         String  @default("BRL")
  interval         String? // "month", "year"
  
  // Timestamps
  trialEndsAt DateTime?
  cancelAt    DateTime?
  canceledAt  DateTime?
  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt
  
  // Relations
  organizationId String       @unique
  organization   Organization @relation(fields: [organizationId], references: [id], onDelete: Cascade)
  
  @@index([stripeCustomerId])
  @@index([stripeSubscriptionId])
  @@map("subscriptions")
}

enum SubscriptionPlan {
  TRIAL
  STARTER
  PROFESSIONAL
  BUSINESS
  ENTERPRISE
}

enum SubscriptionStatus {
  ACTIVE
  PAST_DUE
  CANCELED
  INCOMPLETE
  TRIALING
}

// ============================================
// OBJECTIVES (SMART + OKRs)
// ============================================

model Objective {
  id          String   @id @default(uuid())
  
  // SMART
  title       String
  description String?
  specific    String   // O que será alcançado
  measurable  String   // Como medir
  achievable  String   // É viável?
  relevant    String   // Por que é importante
  timeBound   DateTime // Prazo
  
  // OKR (opcional)
  isOKR       Boolean  @default(false)
  
  // Status
  status      ObjectiveStatus @default(NOT_STARTED)
  progress    Float           @default(0) // 0-100
  priority    Priority        @default(MEDIUM)
  
  // Timestamps
  startDate   DateTime?
  endDate     DateTime?
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
  
  // Relations
  organizationId String
  organization   Organization @relation(fields: [organizationId], references: [id], onDelete: Cascade)
  createdById    String
  createdBy      User         @relation(fields: [createdById], references: [id])
  
  keyResults  KeyResult[]
  tasks       Task[]
  metrics     Metric[]
  
  @@index([organizationId])
  @@index([status])
  @@map("objectives")
}

enum ObjectiveStatus {
  NOT_STARTED
  IN_PROGRESS
  ON_HOLD
  COMPLETED
  CANCELED
}

enum Priority {
  LOW
  MEDIUM
  HIGH
  CRITICAL
}

model KeyResult {
  id          String  @id @default(uuid())
  title       String
  description String?
  
  // Métrica
  currentValue Float   @default(0)
  targetValue  Float
  unit         String  // "%", "R$", "unidades", etc
  
  // Status
  progress    Float   @default(0) // 0-100
  
  // Timestamps
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  
  // Relations
  objectiveId String
  objective   Objective @relation(fields: [objectiveId], references: [id], onDelete: Cascade)
  
  @@index([objectiveId])
  @@map("key_results")
}

// ============================================
// TASKS & KANBAN
// ============================================

model Task {
  id          String   @id @default(uuid())
  title       String
  description String?
  
  // Kanban
  status      TaskStatus @default(TODO)
  position    Int        @default(0)
  
  // Prioridade e Prazo
  priority    Priority   @default(MEDIUM)
  dueDate     DateTime?
  
  // Estimativa
  estimatedHours Float?
  actualHours    Float?
  
  // Timestamps
  startedAt   DateTime?
  completedAt DateTime?
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
  
  // Relations
  organizationId String
  organization   Organization @relation(fields: [organizationId], references: [id], onDelete: Cascade)
  
  assigneeId  String?
  assignee    User?   @relation(fields: [assigneeId], references: [id])
  
  objectiveId String?
  objective   Objective? @relation(fields: [objectiveId], references: [id])
  
  processId   String?
  process     Process? @relation(fields: [processId], references: [id])
  
  subtasks    Task[]  @relation("SubTasks")
  parentTask  Task?   @relation("SubTasks", fields: [parentTaskId], references: [id])
  parentTaskId String?
  
  @@index([organizationId])
  @@index([assigneeId])
  @@index([status])
  @@map("tasks")
}

enum TaskStatus {
  TODO
  IN_PROGRESS
  REVIEW
  DONE
  BLOCKED
}

// ============================================
// BPM / BPMN
// ============================================

model Process {
  id          String  @id @default(uuid())
  name        String
  description String?
  
  // BPMN XML
  bpmnXml     String? @db.Text
  
  // Categoria
  category    String? // "Operacional", "Estratégico", "Suporte"
  
  // Status
  status      ProcessStatus @default(DRAFT)
  version     Int           @default(1)
  
  // Timestamps
  publishedAt DateTime?
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
  
  // Relations
  organizationId String
  organization   Organization @relation(fields: [organizationId], references: [id], onDelete: Cascade)
  
  tasks       Task[]
  
  @@index([organizationId])
  @@map("processes")
}

enum ProcessStatus {
  DRAFT
  ACTIVE
  ARCHIVED
}

// ============================================
// RISKS (ISO 31000)
// ============================================

model Risk {
  id          String @id @default(uuid())
  title       String
  description String
  
  // Classificação
  category    RiskCategory
  
  // Análise
  likelihood  Int    @default(1) // 1-5
  impact      Int    @default(1) // 1-5
  score       Int    @default(1) // likelihood × impact
  
  // Mitigação
  mitigation  String?
  responsible String?
  
  // Status
  status      RiskStatus @default(IDENTIFIED)
  
  // Timestamps
  identifiedAt DateTime @default(now())
  reviewedAt   DateTime?
  mitigatedAt  DateTime?
  createdAt    DateTime @default(now())
  updatedAt    DateTime @updatedAt
  
  // Relations
  organizationId String
  organization   Organization @relation(fields: [organizationId], references: [id], onDelete: Cascade)
  
  @@index([organizationId])
  @@index([status])
  @@map("risks")
}

enum RiskCategory {
  STRATEGIC
  OPERATIONAL
  FINANCIAL
  COMPLIANCE
  REPUTATION
  TECHNOLOGY
}

enum RiskStatus {
  IDENTIFIED
  ANALYZING
  MITIGATING
  CONTROLLED
  ACCEPTED
}

// ============================================
// ANALYTICS & DASHBOARDS
// ============================================

model Dashboard {
  id       String @id @default(uuid())
  name     String
  config   Json   // { widgets: [...], layout: {...} }
  
  // Timestamps
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  
  // Relations
  organizationId String
  organization   Organization @relation(fields: [organizationId], references: [id], onDelete: Cascade)
  
  @@index([organizationId])
  @@map("dashboards")
}

model Metric {
  id       String   @id @default(uuid())
  name     String
  value    Float
  unit     String?
  date     DateTime @default(now())
  
  // Relations
  objectiveId String?
  objective   Objective? @relation(fields: [objectiveId], references: [id])
  
  @@index([objectiveId])
  @@index([date])
  @@map("metrics")
}

// ============================================
// AI & EMBEDDINGS
// ============================================

model AIConversation {
  id        String   @id @default(uuid())
  
  // Chat
  messages  Json     // [{ role: "user"|"assistant", content: "..." }]
  
  // Contexto
  context   String?  // "objectives", "tasks", "bpm", etc
  contextId String?  // ID do recurso relacionado
  
  // Modelo usado (cascateamento)
  modelUsed String   // "gpt-5-nano", "gpt-5-mini", "gpt-5.1"
  
  // Tokens e Custo
  tokensUsed Int     @default(0)
  costUSD    Float   @default(0)  // Custo real em USD
  
  // Timestamps
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  
  // Relations
  userId String
  user   User   @relation(fields: [userId], references: [id], onDelete: Cascade)
  
  @@index([userId])
  @@index([createdAt])
  @@index([modelUsed])  // ← Para analytics de uso
  @@map("ai_conversations")
}

model Embedding {
  id        String @id @default(uuid())
  
  // Conteúdo
  content   String @db.Text
  
  // Vector (pgvector)
  embedding Unsupported("vector(1536)")
  
  // Metadata
  resourceType String  // "objective", "task", "process", etc
  resourceId   String
  
  // Timestamps
  createdAt DateTime @default(now())
  
  @@index([resourceType, resourceId])
  @@map("embeddings")
}

// ============================================
// AUDIT & LOGS
// ============================================

model AuditLog {
  id        String   @id @default(uuid())
  
  // O quê
  action    String   // "objective.created", "user.deleted", etc
  resource  String   // "Objective", "User", etc
  resourceId String?
  changes   Json?    // { before: {...}, after: {...} }
  
  // Quem
  userId    String
  user      User     @relation(fields: [userId], references: [id], onDelete: Cascade)
  
  // Onde
  organizationId String
  organization   Organization @relation(fields: [organizationId], references: [id], onDelete: Cascade)
  
  // Quando & De onde
  ipAddress  String
  userAgent  String
  createdAt  DateTime @default(now())
  
  @@index([organizationId, createdAt])
  @@index([userId])
  @@index([action])
  @@map("audit_logs")
}
```

---

# 5. VARIÁVEIS DE AMBIENTE

## 5.1 Frontend (.env.local)

```bash
# App
NEXT_PUBLIC_APP_URL=http://localhost:3000
NEXT_PUBLIC_API_URL=http://localhost:4000

# Auth (NextAuth.js)
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=your-super-secret-key-change-in-production

# Google OAuth (opcional)
GOOGLE_CLIENT_ID=your-google-client-id
GOOGLE_CLIENT_SECRET=your-google-client-secret

# Stripe (Public Key)
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_xxxxx
```

## 5.2 Backend (.env)

```bash
# App
NODE_ENV=development
PORT=4000
APP_URL=http://localhost:3000

# Database
DATABASE_URL="postgresql://postgres:postgres@localhost:5432/smartwork?schema=public"

# Redis
REDIS_URL=redis://localhost:6379

# JWT
JWT_SECRET=your-jwt-secret-key-change-in-production
JWT_EXPIRES_IN=24h

# Stripe
STRIPE_SECRET_KEY=sk_test_xxxxx
STRIPE_WEBHOOK_SECRET=whsec_xxxxx
STRIPE_PRICE_ID_STARTER=price_xxxxx
STRIPE_PRICE_ID_PROFESSIONAL=price_xxxxx
STRIPE_PRICE_ID_BUSINESS=price_xxxxx
STRIPE_PRICE_ID_ENTERPRISE=price_xxxxx

# OpenAI
OPENAI_API_KEY=sk-xxxxx
OPENAI_ORGANIZATION_ID=org-xxxxx

# AI Models (Cascateamento)
OPENAI_MODEL_NANO=gpt-5-nano
OPENAI_MODEL_MINI=gpt-5-mini
OPENAI_MODEL_FULL=gpt-5.1
OPENAI_EMBEDDING_MODEL=text-embedding-ada-002

# AI Pricing (USD per 1M tokens)
OPENAI_COST_NANO=0.05
OPENAI_COST_MINI=0.25
OPENAI_COST_FULL=1.25

# Brevo/SendinBlue
BREVO_API_KEY=xkeysib-xxxxx
BREVO_SENDER_EMAIL=noreply@smartworkbusiness.com.br
BREVO_SENDER_NAME="Smart Work Business"

# AI Service
AI_SERVICE_URL=http://localhost:5000

# Logging
LOG_LEVEL=debug
```

## 5.3 AI Service (.env)

```bash
# App
APP_ENV=development
APP_PORT=5000

# Database
DATABASE_URL=postgresql://postgres:postgres@localhost:5432/smartwork

# Redis
REDIS_URL=redis://localhost:6379

# OpenAI
OPENAI_API_KEY=sk-xxxxx
OPENAI_MODEL_NANO=gpt-5-nano
OPENAI_MODEL_MINI=gpt-5-mini
OPENAI_MODEL_FULL=gpt-5.1
OPENAI_EMBEDDING_MODEL=text-embedding-ada-002

# AI Pricing (USD per 1M tokens)
OPENAI_COST_NANO=0.05
OPENAI_COST_MINI=0.25
OPENAI_COST_FULL=1.25

# Rate Limiting
AI_RATE_LIMIT_PER_MINUTE=10

# Logging
LOG_LEVEL=INFO
```

## 5.4 Docker Compose (.env)

```bash
# Versões
POSTGRES_VERSION=16-alpine
REDIS_VERSION=7-alpine
NGINX_VERSION=alpine

# PostgreSQL
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
POSTGRES_DB=smartwork

# Volumes
POSTGRES_DATA_PATH=./data/postgres
REDIS_DATA_PATH=./data/redis
NGINX_LOGS_PATH=./logs/nginx
```

---

# 6. SCRIPTS ÚTEIS

## 6.1 Setup Completo

```bash
#!/bin/bash
# setup.sh

echo "🚀 Smart Work Business - Setup"

# 1. Instalar dependências
echo "📦 Instalando dependências..."
npm install --prefix frontend
npm install --prefix backend
pip install -r ai-service/requirements.txt

# 2. Copiar .env
echo "🔧 Configurando variáveis de ambiente..."
cp frontend/.env.example frontend/.env.local
cp backend/.env.example backend/.env
cp ai-service/.env.example ai-service/.env

# 3. Subir containers
echo "🐳 Iniciando Docker..."
docker-compose up -d postgres redis

# 4. Esperar PostgreSQL
echo "⏳ Aguardando PostgreSQL..."
sleep 5

# 5. Rodar migrations
echo "📊 Criando banco de dados..."
cd backend && npx prisma migrate dev --name init && cd ..

# 6. Seed inicial
echo "🌱 Populando dados iniciais..."
cd backend && npm run prisma:seed && cd ..

echo "✅ Setup completo!"
echo ""
echo "Para iniciar:"
echo "  Frontend: npm run dev --prefix frontend"
echo "  Backend:  npm run start:dev --prefix backend"
echo "  AI Service: cd ai-service && uvicorn app.main:app --reload"
```

## 6.2 Dev (Tudo junto)

```bash
#!/bin/bash
# dev.sh

echo "🚀 Iniciando desenvolvimento..."

# Terminal 1: Frontend
npm run dev --prefix frontend &

# Terminal 2: Backend
npm run start:dev --prefix backend &

# Terminal 3: AI Service
cd ai-service && uvicorn app.main:app --reload --port 5000 &

echo "✅ Todos os serviços iniciados!"
echo ""
echo "  Frontend:   http://localhost:3000"
echo "  Backend:    http://localhost:4000"
echo "  AI Service: http://localhost:5000"
echo "  Prisma Studio: npm run prisma:studio --prefix backend"
```

## 6.3 Reset Database

```bash
#!/bin/bash
# reset-db.sh

echo "⚠️  ATENÇÃO: Isso vai deletar TODOS os dados!"
read -p "Tem certeza? (y/n) " -n 1 -r
echo

if [[ $REPLY =~ ^[Yy]$ ]]
then
  echo "🗑️  Resetando banco..."
  
  cd backend
  npx prisma migrate reset --force
  npm run prisma:seed
  cd ..
  
  echo "✅ Banco resetado!"
fi
```

## 6.4 Build Production

```bash
#!/bin/bash
# build.sh

echo "🏗️  Building para produção..."

# Frontend
echo "📦 Frontend..."
cd frontend
npm run build
cd ..

# Backend
echo "📦 Backend..."
cd backend
npm run build
npx prisma generate
cd ..

# AI Service
echo "📦 AI Service..."
# Já usa Python, não precisa build

echo "✅ Build completo!"
echo ""
echo "Deploy com: docker-compose -f docker-compose.prod.yml up -d"
```

## 6.5 Tests

```bash
#!/bin/bash
# test.sh

echo "🧪 Rodando testes..."

# Frontend
echo "📱 Frontend..."
npm run test --prefix frontend

# Backend
echo "⚙️  Backend..."
npm run test --prefix backend

# E2E (futuro)
# echo "🎭 E2E..."
# npm run test:e2e --prefix backend

echo "✅ Testes concluídos!"
```

---

## RESUMO

### Instalação Rápida

```bash
# 1. Clone
git clone https://github.com/sua-org/smartwork-app.git
cd smartwork-app

# 2. Setup
chmod +x scripts/*.sh
./scripts/setup.sh

# 3. Dev
./scripts/dev.sh
```

### Comandos Essenciais

```bash
# Desenvolvimento
npm run dev --prefix frontend
npm run start:dev --prefix backend
cd ai-service && uvicorn app.main:app --reload

# Build
npm run build --prefix frontend
npm run build --prefix backend

# Testes
npm run test --prefix frontend
npm run test --prefix backend

# Prisma
npm run prisma:studio --prefix backend
npm run prisma:migrate --prefix backend
npm run prisma:seed --prefix backend

# Docker
docker-compose up -d
docker-compose down
docker-compose logs -f
```

---

**Próximo:** [Documento 5 - Roadmap](./05-ROADMAP.md)


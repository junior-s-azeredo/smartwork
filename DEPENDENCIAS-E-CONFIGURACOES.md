# DEPENDÊNCIAS E CONFIGURAÇÕES COMPLETAS
## Smart Work Business SaaS

---

## 1. PACKAGE.JSON - FRONTEND (Next.js)

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
    "lint:fix": "next lint --fix",
    "type-check": "tsc --noEmit",
    "test": "jest",
    "test:watch": "jest --watch",
    "test:coverage": "jest --coverage"
  },
  "dependencies": {
    "next": "14.1.0",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    
    "@tanstack/react-query": "^5.17.19",
    "@tanstack/react-table": "^8.11.8",
    "zustand": "^4.5.0",
    
    "react-hook-form": "^7.49.3",
    "@hookform/resolvers": "^3.3.4",
    "zod": "^3.22.4",
    
    "next-auth": "^5.0.0-beta.4",
    
    "axios": "^1.6.5",
    
    "tailwindcss": "^3.4.1",
    "tailwind-merge": "^2.2.1",
    "class-variance-authority": "^0.7.0",
    "clsx": "^2.1.0",
    
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
    
    "recharts": "^2.12.0",
    "@tremor/react": "^3.14.0",
    
    "bpmn-js": "^17.0.0",
    "bpmn-js-properties-panel": "^5.0.0",
    
    "lucide-react": "^0.309.0",
    
    "date-fns": "^3.3.1",
    "dayjs": "^1.11.10",
    
    "react-markdown": "^9.0.1",
    "react-syntax-highlighter": "^15.5.0",
    
    "sonner": "^1.3.1",
    
    "cmdk": "^0.2.0",
    
    "react-hot-toast": "^2.4.1"
  },
  "devDependencies": {
    "@types/node": "^20.11.5",
    "@types/react": "^18.2.48",
    "@types/react-dom": "^18.2.18",
    "@types/react-syntax-highlighter": "^15.5.11",
    "typescript": "^5.3.3",
    
    "@testing-library/react": "^14.1.2",
    "@testing-library/jest-dom": "^6.2.0",
    "@testing-library/user-event": "^14.5.2",
    "jest": "^29.7.0",
    "jest-environment-jsdom": "^29.7.0",
    
    "eslint": "^8.56.0",
    "eslint-config-next": "14.1.0",
    "eslint-config-prettier": "^9.1.0",
    "prettier": "^3.2.4",
    "prettier-plugin-tailwindcss": "^0.5.11",
    
    "@commitlint/cli": "^18.6.0",
    "@commitlint/config-conventional": "^18.6.0",
    "husky": "^8.0.3",
    "lint-staged": "^15.2.0",
    
    "autoprefixer": "^10.4.17",
    "postcss": "^8.4.33"
  }
}
```

---

## 2. PACKAGE.JSON - BACKEND (NestJS)

```json
{
  "name": "smartwork-backend",
  "version": "1.0.0",
  "private": true,
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
    "test:debug": "node --inspect-brk -r tsconfig-paths/register -r ts-node/register node_modules/.bin/jest --runInBand",
    "test:e2e": "jest --config ./test/jest-e2e.json",
    "db:generate": "prisma generate",
    "db:push": "prisma db push",
    "db:migrate": "prisma migrate dev",
    "db:studio": "prisma studio",
    "db:seed": "ts-node prisma/seed.ts"
  },
  "dependencies": {
    "@nestjs/common": "^10.3.0",
    "@nestjs/core": "^10.3.0",
    "@nestjs/platform-express": "^10.3.0",
    "@nestjs/config": "^3.1.1",
    "@nestjs/swagger": "^7.2.0",
    
    "@nestjs/jwt": "^10.2.0",
    "@nestjs/passport": "^10.0.3",
    "passport": "^0.7.0",
    "passport-jwt": "^4.0.1",
    "passport-local": "^1.0.0",
    "bcryptjs": "^2.4.3",
    
    "@prisma/client": "^5.9.0",
    
    "@nestjs/redis": "^10.0.0",
    "ioredis": "^5.3.2",
    
    "@nestjs/bull": "^10.0.1",
    "bull": "^4.12.0",
    
    "class-validator": "^0.14.1",
    "class-transformer": "^0.5.1",
    "zod": "^3.22.4",
    
    "openai": "^4.26.0",
    "langchain": "^0.1.20",
    "@langchain/openai": "^0.0.14",
    "@langchain/community": "^0.0.25",
    
    "stripe": "^14.14.0",
    
    "@getbrevo/brevo": "^2.0.0",
    
    "winston": "^3.11.0",
    "nest-winston": "^1.9.4",
    
    "@nestjs/throttler": "^5.1.1",
    
    "@sentry/node": "^7.99.0",
    
    "helmet": "^7.1.0",
    
    "compression": "^1.7.4",
    
    "cron": "^3.1.6",
    "@nestjs/schedule": "^4.0.0",
    
    "nanoid": "^5.0.4",
    
    "axios": "^1.6.5",
    
    "reflect-metadata": "^0.2.1",
    "rxjs": "^7.8.1"
  },
  "devDependencies": {
    "@nestjs/cli": "^10.3.0",
    "@nestjs/schematics": "^10.1.0",
    "@nestjs/testing": "^10.3.0",
    
    "@types/express": "^4.17.21",
    "@types/jest": "^29.5.11",
    "@types/node": "^20.11.5",
    "@types/supertest": "^6.0.2",
    "@types/passport-jwt": "^4.0.1",
    "@types/passport-local": "^1.0.38",
    "@types/bcryptjs": "^2.4.6",
    "@types/compression": "^1.7.5",
    
    "@typescript-eslint/eslint-plugin": "^6.19.0",
    "@typescript-eslint/parser": "^6.19.0",
    "eslint": "^8.56.0",
    "eslint-config-prettier": "^9.1.0",
    "eslint-plugin-prettier": "^5.1.3",
    
    "jest": "^29.7.0",
    "supertest": "^6.3.4",
    "ts-jest": "^29.1.1",
    "ts-loader": "^9.5.1",
    "ts-node": "^10.9.2",
    "tsconfig-paths": "^4.2.0",
    "typescript": "^5.3.3",
    
    "prisma": "^5.9.0",
    
    "prettier": "^3.2.4",
    
    "source-map-support": "^0.5.21"
  }
}
```

---

## 3. PRISMA SCHEMA COMPLETO

```prisma
// prisma/schema.prisma

generator client {
  provider = "prisma-client-js"
  previewFeatures = ["fullTextSearch", "fullTextIndex"]
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

// ============================================
// AUTENTICAÇÃO E USUÁRIOS
// ============================================

model User {
  id            String    @id @default(cuid())
  email         String    @unique
  emailVerified DateTime?
  name          String?
  image         String?
  password      String?
  role          Role      @default(USER)
  locale        String    @default("pt-BR")
  timezone      String    @default("America/Sao_Paulo")
  
  createdAt     DateTime  @default(now())
  updatedAt     DateTime  @updatedAt
  lastLoginAt   DateTime?
  
  // Relações
  accounts              Account[]
  sessions              Session[]
  organizationMembers   OrganizationMember[]
  objectives            Objective[]
  tasks                 Task[]
  comments              Comment[]
  auditLogs             AuditLog[]
  aiConversations       AIConversation[]
  notificationPrefs     NotificationPreference?
  
  @@index([email])
  @@map("users")
}

enum Role {
  USER
  ADMIN
  SUPER_ADMIN
}

model Account {
  id                String  @id @default(cuid())
  userId            String
  type              String
  provider          String
  providerAccountId String
  refresh_token     String? @db.Text
  access_token      String? @db.Text
  expires_at        Int?
  token_type        String?
  scope             String?
  id_token          String? @db.Text
  session_state     String?

  user User @relation(fields: [userId], references: [id], onDelete: Cascade)

  @@unique([provider, providerAccountId])
  @@index([userId])
  @@map("accounts")
}

model Session {
  id           String   @id @default(cuid())
  sessionToken String   @unique
  userId       String
  expires      DateTime
  ipAddress    String?
  userAgent    String?
  
  user User @relation(fields: [userId], references: [id], onDelete: Cascade)

  @@index([userId])
  @@map("sessions")
}

model VerificationToken {
  identifier String
  token      String   @unique
  expires    DateTime

  @@unique([identifier, token])
  @@map("verification_tokens")
}

// ============================================
// ORGANIZAÇÕES (MULTI-TENANT)
// ============================================

model Organization {
  id          String   @id @default(cuid())
  name        String
  slug        String   @unique
  logo        String?
  website     String?
  industry    String?
  size        OrganizationSize?
  
  // Plano e billing
  plan        Plan     @default(STARTER)
  planStatus  PlanStatus @default(ACTIVE)
  trialEndsAt DateTime?
  
  // Stripe
  stripeCustomerId       String? @unique
  stripeSubscriptionId   String? @unique
  
  // Configurações
  settings    Json?
  
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
  
  // Relações
  members     OrganizationMember[]
  invites     OrganizationInvite[]
  objectives  Objective[]
  processes   BPMProcess[]
  pdcaCycles  PDCACycle[]
  tasks       Task[]
  kpis        KPI[]
  dashboards  Dashboard[]
  auditLogs   AuditLog[]
  
  @@index([slug])
  @@index([plan])
  @@map("organizations")
}

enum Plan {
  STARTER
  PROFESSIONAL
  ENTERPRISE
}

enum PlanStatus {
  ACTIVE
  TRIALING
  PAST_DUE
  CANCELED
  UNPAID
}

enum OrganizationSize {
  MICRO      // 1-10
  SMALL      // 11-50
  MEDIUM     // 51-200
  LARGE      // 201-1000
  ENTERPRISE // 1000+
}

model OrganizationMember {
  id             String       @id @default(cuid())
  role           MemberRole   @default(MEMBER)
  
  userId         String
  organizationId String
  
  user           User         @relation(fields: [userId], references: [id], onDelete: Cascade)
  organization   Organization @relation(fields: [organizationId], references: [id], onDelete: Cascade)
  
  createdAt      DateTime     @default(now())
  
  @@unique([userId, organizationId])
  @@index([organizationId])
  @@index([userId])
  @@map("organization_members")
}

enum MemberRole {
  OWNER
  ADMIN
  MANAGER
  MEMBER
  VIEWER
}

model OrganizationInvite {
  id             String       @id @default(cuid())
  email          String
  role           MemberRole   @default(MEMBER)
  token          String       @unique
  expiresAt      DateTime
  acceptedAt     DateTime?
  
  organizationId String
  invitedBy      String
  
  organization   Organization @relation(fields: [organizationId], references: [id], onDelete: Cascade)
  
  createdAt      DateTime     @default(now())
  
  @@index([organizationId])
  @@index([email])
  @@map("organization_invites")
}

// ============================================
// OBJETIVOS SMART E OKRs
// ============================================

model Objective {
  id          String   @id @default(cuid())
  
  // SMART
  title       String
  description String?  @db.Text
  specific    String   @db.Text
  metric      String
  currentValue Float?
  targetValue Float
  unit        String
  startDate   DateTime
  dueDate     DateTime
  
  // Metadata
  status      ObjectiveStatus @default(NOT_STARTED)
  priority    Priority        @default(MEDIUM)
  progress    Float           @default(0)
  level       ObjectiveLevel  @default(OPERATIONAL)
  
  // Hierarquia
  parentId    String?
  parent      Objective?   @relation("ObjectiveHierarchy", fields: [parentId], references: [id])
  children    Objective[]  @relation("ObjectiveHierarchy")
  
  // Multi-tenant
  organizationId String
  organization   Organization @relation(fields: [organizationId], references: [id], onDelete: Cascade)
  
  ownerId     String
  owner       User     @relation(fields: [ownerId], references: [id])
  
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
  
  // Relações
  okrs        OKR[]
  tasks       Task[]
  pdcaCycles  PDCACycle[]
  comments    Comment[]
  progressUpdates ObjectiveProgress[]
  
  @@index([organizationId])
  @@index([ownerId])
  @@index([level])
  @@index([status])
  @@index([dueDate])
  @@fulltext([title, description, specific])
  @@map("objectives")
}

enum ObjectiveStatus {
  NOT_STARTED
  IN_PROGRESS
  AT_RISK
  ON_TRACK
  COMPLETED
  CANCELLED
}

enum ObjectiveLevel {
  STRATEGIC
  TACTICAL
  OPERATIONAL
}

enum Priority {
  LOW
  MEDIUM
  HIGH
  CRITICAL
}

model OKR {
  id            String   @id @default(cuid())
  keyResult     String
  currentValue  Float    @default(0)
  targetValue   Float
  unit          String
  weight        Float    @default(1)
  
  objectiveId   String
  objective     Objective @relation(fields: [objectiveId], references: [id], onDelete: Cascade)
  
  checkins      OKRCheckin[]
  
  createdAt     DateTime @default(now())
  updatedAt     DateTime @updatedAt
  
  @@index([objectiveId])
  @@map("okrs")
}

model OKRCheckin {
  id          String   @id @default(cuid())
  value       Float
  confidence  Int      // 1-5
  notes       String?  @db.Text
  
  okrId       String
  okr         OKR      @relation(fields: [okrId], references: [id], onDelete: Cascade)
  
  createdAt   DateTime @default(now())
  
  @@index([okrId])
  @@index([createdAt])
  @@map("okr_checkins")
}

model ObjectiveProgress {
  id          String   @id @default(cuid())
  value       Float
  notes       String?  @db.Text
  
  objectiveId String
  objective   Objective @relation(fields: [objectiveId], references: [id], onDelete: Cascade)
  
  createdAt   DateTime @default(now())
  
  @@index([objectiveId])
  @@index([createdAt])
  @@map("objective_progress")
}

// ============================================
// BPM / BPMN
// ============================================

model BPMProcess {
  id          String   @id @default(cuid())
  name        String
  description String?  @db.Text
  category    String?
  tags        String[]
  
  // BPMN XML
  bpmnXml     String   @db.Text
  
  // Versão
  version     Int      @default(1)
  isPublished Boolean  @default(false)
  
  // Análise
  cycleTime   Int?     // em minutos
  complexity  Int?     // score calculado
  
  // Multi-tenant
  organizationId String
  organization   Organization @relation(fields: [organizationId], references: [id], onDelete: Cascade)
  
  createdBy   String
  
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
  
  // Relações
  pops        POP[]
  versions    BPMProcessVersion[]
  
  @@index([organizationId])
  @@index([category])
  @@fulltext([name, description])
  @@map("bpm_processes")
}

model BPMProcessVersion {
  id          String   @id @default(cuid())
  version     Int
  bpmnXml     String   @db.Text
  notes       String?  @db.Text
  
  processId   String
  process     BPMProcess @relation(fields: [processId], references: [id], onDelete: Cascade)
  
  createdAt   DateTime @default(now())
  
  @@unique([processId, version])
  @@index([processId])
  @@map("bpm_process_versions")
}

model POP {
  id          String   @id @default(cuid())
  title       String
  content     String   @db.Text
  version     String   @default("1.0")
  status      POPStatus @default(DRAFT)
  
  processId   String?
  process     BPMProcess? @relation(fields: [processId], references: [id])
  
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
  approvedAt  DateTime?
  approvedBy  String?
  
  @@index([processId])
  @@index([status])
  @@map("pops")
}

enum POPStatus {
  DRAFT
  IN_REVIEW
  APPROVED
  ARCHIVED
}

// ============================================
// PDCA
// ============================================

model PDCACycle {
  id          String   @id @default(cuid())
  title       String
  description String?  @db.Text
  
  // Plan
  problem     String   @db.Text
  goal        String   @db.Text
  analysis    String?  @db.Text
  actionPlan  String?  @db.Text
  
  // Do
  execution   String?  @db.Text
  executionStartDate DateTime?
  executionEndDate   DateTime?
  
  // Check
  results     String?  @db.Text
  evaluation  String?  @db.Text
  
  // Act
  standardization String? @db.Text
  nextSteps   String?  @db.Text
  
  // Status
  currentPhase PDCAPhase @default(PLAN)
  status      ObjectiveStatus @default(NOT_STARTED)
  
  // Vinculação
  objectiveId String?
  objective   Objective? @relation(fields: [objectiveId], references: [id])
  
  organizationId String
  organization   Organization @relation(fields: [organizationId], references: [id], onDelete: Cascade)
  
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
  
  @@index([organizationId])
  @@index([currentPhase])
  @@index([status])
  @@map("pdca_cycles")
}

enum PDCAPhase {
  PLAN
  DO
  CHECK
  ACT
  COMPLETED
}

// ============================================
// TAREFAS
// ============================================

model Task {
  id          String   @id @default(cuid())
  title       String
  description String?  @db.Text
  
  status      TaskStatus @default(TODO)
  priority    Priority   @default(MEDIUM)
  
  dueDate     DateTime?
  completedAt DateTime?
  
  // 5W2H
  what        String?   @db.Text
  why         String?   @db.Text
  where       String?   @db.Text
  when        DateTime?
  who         String?
  how         String?   @db.Text
  howMuch     Float?
  
  // Vinculações
  objectiveId String?
  objective   Objective? @relation(fields: [objectiveId], references: [id])
  
  assigneeId  String?
  assignee    User?      @relation(fields: [assigneeId], references: [id])
  
  organizationId String
  organization   Organization @relation(fields: [organizationId], references: [id], onDelete: Cascade)
  
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
  
  // Relações
  comments    Comment[]
  timeEntries TimeEntry[]
  
  @@index([organizationId])
  @@index([assigneeId])
  @@index([status])
  @@index([dueDate])
  @@fulltext([title, description])
  @@map("tasks")
}

enum TaskStatus {
  TODO
  IN_PROGRESS
  REVIEW
  DONE
  CANCELLED
}

model TimeEntry {
  id          String   @id @default(cuid())
  duration    Int      // em minutos
  notes       String?  @db.Text
  
  taskId      String
  task        Task     @relation(fields: [taskId], references: [id], onDelete: Cascade)
  
  createdAt   DateTime @default(now())
  
  @@index([taskId])
  @@map("time_entries")
}

// ============================================
// ANALYTICS E BI
// ============================================

model KPI {
  id          String   @id @default(cuid())
  name        String
  description String?  @db.Text
  formula     String?  @db.Text
  unit        String
  target      Float?
  
  organizationId String
  organization   Organization @relation(fields: [organizationId], references: [id], onDelete: Cascade)
  
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
  
  // Relações
  dataPoints  KPIDataPoint[]
  
  @@index([organizationId])
  @@map("kpis")
}

model KPIDataPoint {
  id          String   @id @default(cuid())
  value       Float
  dimensions  Json?
  
  kpiId       String
  kpi         KPI      @relation(fields: [kpiId], references: [id], onDelete: Cascade)
  
  timestamp   DateTime @default(now())
  
  @@index([kpiId, timestamp])
  @@map("kpi_data_points")
}

model Dashboard {
  id          String   @id @default(cuid())
  name        String
  description String?  @db.Text
  layout      Json
  isPublic    Boolean  @default(false)
  
  organizationId String
  organization   Organization @relation(fields: [organizationId], references: [id], onDelete: Cascade)
  
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
  
  @@index([organizationId])
  @@map("dashboards")
}

// ============================================
// IA / CONSULTOR ESPECIALISTA
// ============================================

model AIConversation {
  id          String   @id @default(cuid())
  title       String?
  
  userId      String
  user        User     @relation(fields: [userId], references: [id], onDelete: Cascade)
  
  messages    AIMessage[]
  
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
  
  @@index([userId])
  @@map("ai_conversations")
}

model AIMessage {
  id             String   @id @default(cuid())
  role           AIMessageRole
  content        String   @db.Text
  functionCall   Json?
  
  conversationId String
  conversation   AIConversation @relation(fields: [conversationId], references: [id], onDelete: Cascade)
  
  createdAt      DateTime @default(now())
  
  @@index([conversationId])
  @@map("ai_messages")
}

enum AIMessageRole {
  USER
  ASSISTANT
  SYSTEM
}

// ============================================
// AUDITORIA E COMPLIANCE
// ============================================

model AuditLog {
  id          String   @id @default(cuid())
  
  action      String
  entity      String
  entityId    String
  
  oldValue    Json?
  newValue    Json?
  
  userId      String?
  user        User?    @relation(fields: [userId], references: [id])
  
  organizationId String?
  organization   Organization? @relation(fields: [organizationId], references: [id])
  
  ipAddress   String?
  userAgent   String?
  
  createdAt   DateTime @default(now())
  
  @@index([entity, entityId])
  @@index([userId])
  @@index([organizationId])
  @@index([createdAt])
  @@map("audit_logs")
}

// ============================================
// NOTIFICAÇÕES
// ============================================

model NotificationPreference {
  id          String   @id @default(cuid())
  
  emailEnabled      Boolean @default(true)
  emailFrequency    NotificationFrequency @default(IMMEDIATE)
  
  taskAssigned      Boolean @default(true)
  taskDue           Boolean @default(true)
  objectiveAtRisk   Boolean @default(true)
  commentMention    Boolean @default(true)
  weeklyReport      Boolean @default(true)
  
  userId      String   @unique
  user        User     @relation(fields: [userId], references: [id], onDelete: Cascade)
  
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
  
  @@map("notification_preferences")
}

enum NotificationFrequency {
  IMMEDIATE
  DAILY
  WEEKLY
}

// ============================================
// COMENTÁRIOS (COMPARTILHADO)
// ============================================

model Comment {
  id          String   @id @default(cuid())
  content     String   @db.Text
  
  // Polimorfismo
  entityType  CommentEntityType
  entityId    String
  
  // Vinculações opcionais (para queries otimizadas)
  objectiveId String?
  objective   Objective? @relation(fields: [objectiveId], references: [id], onDelete: Cascade)
  
  taskId      String?
  task        Task?      @relation(fields: [taskId], references: [id], onDelete: Cascade)
  
  authorId    String
  author      User       @relation(fields: [authorId], references: [id])
  
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
  
  @@index([entityType, entityId])
  @@index([authorId])
  @@map("comments")
}

enum CommentEntityType {
  OBJECTIVE
  TASK
  PROCESS
  PDCA
}
```

---

## 4. VARIÁVEIS DE AMBIENTE

### Frontend (.env.local)

```bash
# Next.js
NEXT_PUBLIC_APP_URL=http://localhost:3000
NEXT_PUBLIC_API_URL=http://localhost:4000

# NextAuth
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=change-this-to-a-secure-random-string

# Stripe (Publishable Key - pode ser público)
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_...

# Feature Flags
NEXT_PUBLIC_ENABLE_AI_CONSULTANT=true
NEXT_PUBLIC_ENABLE_ANALYTICS=true
NEXT_PUBLIC_ENABLE_BPM=true
```

### Backend (.env)

```bash
# Aplicação
NODE_ENV=development
PORT=4000
APP_URL=http://localhost:3000
API_URL=http://localhost:4000

# Database
DATABASE_URL=postgresql://smartwork:password@localhost:5432/smartwork_dev

# TimescaleDB (opcional)
TIMESCALE_URL=postgresql://smartwork:password@localhost:5433/smartwork_metrics

# Redis
REDIS_URL=redis://localhost:6379
REDIS_PASSWORD=

# JWT
JWT_SECRET=your-super-secret-jwt-key-change-this
JWT_EXPIRATION=15m
JWT_REFRESH_SECRET=your-refresh-secret-change-this
JWT_REFRESH_EXPIRATION=7d

# OpenAI
OPENAI_API_KEY=sk-...
OPENAI_MODEL=gpt-4-turbo-preview
OPENAI_EMBEDDING_MODEL=text-embedding-ada-002

# Stripe
STRIPE_SECRET_KEY=sk_test_...
STRIPE_WEBHOOK_SECRET=whsec_...
STRIPE_PRICE_STARTER_MONTHLY=price_...
STRIPE_PRICE_STARTER_ANNUAL=price_...
STRIPE_PRICE_PROFESSIONAL_MONTHLY=price_...
STRIPE_PRICE_PROFESSIONAL_ANNUAL=price_...

# Brevo (SendinBlue)
BREVO_API_KEY=xkeysib-...
BREVO_SENDER_EMAIL=noreply@smartworkbusiness.com.br
BREVO_SENDER_NAME=Smart Work Business

# Sentry (Error Tracking)
SENTRY_DSN=https://...@sentry.io/...

# Rate Limiting
RATE_LIMIT_TTL=60
RATE_LIMIT_MAX=100

# CORS
CORS_ORIGIN=http://localhost:3000

# Logs
LOG_LEVEL=debug
```

---

## 5. SCRIPTS ÚTEIS

### Setup Inicial

```bash
#!/bin/bash
# scripts/setup.sh

echo "🚀 Smart Work Business - Setup Inicial"

# 1. Instalar dependências
echo "📦 Instalando dependências..."
npm install --prefix frontend
npm install --prefix backend

# 2. Setup Prisma
echo "🗄️ Configurando Prisma..."
cd backend
npx prisma generate
npx prisma db push

# 3. Docker Compose
echo "🐳 Iniciando Docker..."
cd ..
docker-compose up -d

echo "✅ Setup concluído!"
echo "Frontend: http://localhost:3000"
echo "Backend: http://localhost:4000"
echo "Prisma Studio: npx prisma studio"
```

### Backup Automático

```bash
#!/bin/bash
# scripts/backup.sh

BACKUP_DIR="/backups"
TIMESTAMP=$(date +"%Y%m%d_%H%M%S")
BACKUP_FILE="$BACKUP_DIR/smartwork_$TIMESTAMP.sql"

echo "🔄 Iniciando backup..."

pg_dump -U $POSTGRES_USER -h postgres $POSTGRES_DB > $BACKUP_FILE

gzip $BACKUP_FILE

echo "✅ Backup concluído: $BACKUP_FILE.gz"

# Manter apenas últimos 30 dias
find $BACKUP_DIR -name "smartwork_*.sql.gz" -mtime +30 -delete
```

---

Documento continua...

Você gostaria que eu continue com:
1. Configurações de CI/CD
2. Guia de testes
3. Estratégia de deploy
4. Monitoramento e observabilidade
5. Outro aspecto específico?


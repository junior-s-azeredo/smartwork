# PROJETO TÉCNICO - SMART WORK BUSINESS SAAS
## Documento de Arquitetura e Desenvolvimento

**Versão:** 1.0  
**Data:** Novembro 2025  
**Autor:** Junior Azeredo  
**Status:** Definitivo

---

## ÍNDICE

1. [Visão Geral do Projeto](#1-visão-geral-do-projeto)
2. [Arquitetura do Sistema](#2-arquitetura-do-sistema)
3. [Stack Tecnológico](#3-stack-tecnológico)
4. [Infraestrutura](#4-infraestrutura)
5. [Estrutura do Projeto](#5-estrutura-do-projeto)
6. [Módulos e Funcionalidades](#6-módulos-e-funcionalidades)
7. [Modelo de Dados](#7-modelo-de-dados)
8. [Segurança e Compliance](#8-segurança-e-compliance)
9. [Integrações Externas](#9-integrações-externas)
10. [Desenvolvimento e Deploy](#10-desenvolvimento-e-deploy)
11. [Roadmap de Desenvolvimento](#11-roadmap-de-desenvolvimento)
12. [Anexos e Referências](#12-anexos-e-referências)

---

# 1. VISÃO GERAL DO PROJETO

## 1.1 Objetivo

Desenvolver uma plataforma SaaS completa para gestão empresarial integrada que une **estratégia, tática e operação** em um único sistema, com inteligência artificial embutida e governança nativa.

## 1.2 Princípios Arquiteturais

### **Escalabilidade desde o Início**
- Arquitetura preparada para crescimento (1 → 50.000 clientes)
- Separação clara de responsabilidades
- Microserviços prontos para divisão futura

### **Manutenibilidade**
- Código limpo e documentado
- Testes automatizados
- Padrões de projeto consistentes

### **Performance**
- Dashboards < 2s
- APIs < 200ms
- Cache estratégico em todos os níveis

### **Segurança por Design**
- LGPD nativo
- Criptografia em todos os níveis
- Auditoria automática de tudo

## 1.3 Requisitos Não-Funcionais Críticos

| Requisito | Meta | Medição |
|-----------|------|---------|
| Disponibilidade | 99.9% | Uptime monitoring |
| Performance API | < 200ms p95 | APM (Application Performance Monitoring) |
| Performance Dashboard | < 2s carga inicial | Real User Monitoring |
| Escalabilidade | 50k usuários simultâneos | Load testing |
| Segurança | Zero vulnerabilidades críticas | Security scanning |
| LGPD Compliance | 100% | Audit logs |

---

# 2. ARQUITETURA DO SISTEMA

## 2.1 Arquitetura Geral (Separação Frontend/Backend)

```
┌──────────────────────────────────────────────────────────────┐
│                    CAMADA DE APRESENTAÇÃO                     │
├──────────────────────────────────────────────────────────────┤
│                                                               │
│  FRONTEND (Next.js 14 - App Router)                          │
│  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━   │
│  • Server Components (SSR)                                    │
│  • Client Components (Interatividade)                         │
│  • TypeScript + Tailwind CSS                                 │
│  • TanStack Query (State + Cache)                            │
│  • Zustand (Estado Global)                                   │
│  • React Hook Form + Zod (Validação)                         │
│                                                               │
│  Deploy: Vercel / Ubuntu Server (Docker)                     │
│  Porta: 3000                                                 │
└──────────────────────────────────────────────────────────────┘
                           ↓ HTTPS/REST API
┌──────────────────────────────────────────────────────────────┐
│                    CAMADA DE APLICAÇÃO                        │
├──────────────────────────────────────────────────────────────┤
│                                                               │
│  BACKEND API (NestJS - TypeScript)                           │
│  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━   │
│                                                               │
│  ┌────────────────────────────────────────────────────┐     │
│  │  API GATEWAY                                        │     │
│  │  • Rate Limiting                                    │     │
│  │  • Authentication (JWT)                             │     │
│  │  • Request Validation                               │     │
│  │  • Logging & Monitoring                             │     │
│  └────────────────────────────────────────────────────┘     │
│                           ↓                                   │
│  ┌────────────────────────────────────────────────────┐     │
│  │  MÓDULOS DE NEGÓCIO (Domain-Driven Design)         │     │
│  ├────────────────────────────────────────────────────┤     │
│  │  • Auth Module (NextAuth.js)                       │     │
│  │  • Organizations Module (Multi-tenant)             │     │
│  │  • Objectives Module (SMART)                       │     │
│  │  • BPM Module (BPMN)                               │     │
│  │  • Analytics Module (BI)                           │     │
│  │  • PDCA Module                                     │     │
│  │  • Tasks Module (5W2H)                             │     │
│  │  • AI Module (Consultor Especialista)             │     │
│  │  • Governance Module (ISOs)                        │     │
│  │  • Notifications Module (Brevo)                    │     │
│  │  • Payments Module (Stripe)                        │     │
│  └────────────────────────────────────────────────────┘     │
│                                                               │
│  Deploy: Ubuntu Server 24.04 (Docker)                        │
│  Porta: 4000                                                 │
└──────────────────────────────────────────────────────────────┘
                           ↓
┌──────────────────────────────────────────────────────────────┐
│                    CAMADA DE DADOS                            │
├──────────────────────────────────────────────────────────────┤
│                                                               │
│  ┌─────────────────┐  ┌──────────────┐  ┌────────────────┐ │
│  │  PostgreSQL 16  │  │   Redis 7    │  │  TimescaleDB   │ │
│  │  ─────────────  │  │  ──────────  │  │  ────────────  │ │
│  │  • Dados rel.   │  │  • Cache     │  │  • Métricas    │ │
│  │  • JSONB        │  │  • Sessões   │  │  • Time series │ │
│  │  • pgvector     │  │  • Pub/Sub   │  │  • KPIs        │ │
│  │  • Full-text    │  │  • Queues    │  │                │ │
│  └─────────────────┘  └──────────────┘  └────────────────┘ │
│                                                               │
│  Deploy: Ubuntu Server 24.04 (Docker)                        │
└──────────────────────────────────────────────────────────────┘
                           ↓
┌──────────────────────────────────────────────────────────────┐
│                  SERVIÇOS EXTERNOS (APIs)                     │
├──────────────────────────────────────────────────────────────┤
│                                                               │
│  • OpenAI API (GPT-4 - Consultor IA)                         │
│  • Stripe API (Pagamentos e assinaturas)                     │
│  • Brevo API (Emails transacionais)                          │
│  • GitHub (CI/CD + Versionamento)                            │
│                                                               │
└──────────────────────────────────────────────────────────────┘
```

## 2.2 Fluxo de Dados

```
┌─────────────┐
│   Cliente   │ (Browser / Mobile)
└──────┬──────┘
       │ HTTPS
       ↓
┌─────────────────────────┐
│  Next.js Frontend       │
│  • SSR para SEO         │
│  • Client-side routing  │
│  • TanStack Query cache │
└──────┬──────────────────┘
       │ REST API (HTTPS)
       │ Authorization: Bearer {JWT}
       ↓
┌──────────────────────────────────┐
│  NestJS Backend API              │
│  ┌──────────────────────────┐   │
│  │ 1. Auth Middleware       │   │
│  │    • Valida JWT          │   │
│  │    • Verifica permissões │   │
│  └──────────┬───────────────┘   │
│             ↓                    │
│  ┌──────────────────────────┐   │
│  │ 2. Request Validation    │   │
│  │    • Zod schemas         │   │
│  │    • DTO validation      │   │
│  └──────────┬───────────────┘   │
│             ↓                    │
│  ┌──────────────────────────┐   │
│  │ 3. Business Logic        │   │
│  │    • Services            │   │
│  │    • Use Cases           │   │
│  └──────────┬───────────────┘   │
│             ↓                    │
│  ┌──────────────────────────┐   │
│  │ 4. Data Layer            │   │
│  │    • Prisma ORM          │   │
│  │    • Repository pattern  │   │
│  └──────────┬───────────────┘   │
└─────────────┼────────────────────┘
              ↓
    ┌─────────────────────┐
    │  PostgreSQL + Redis │
    └─────────────────────┘
```

## 2.3 Padrões Arquiteturais

### **Clean Architecture**

```
src/
├── domain/               # Entidades de negócio (independente)
│   ├── entities/
│   ├── value-objects/
│   └── interfaces/
├── application/          # Casos de uso (regras de negócio)
│   ├── use-cases/
│   └── services/
├── infrastructure/       # Implementações técnicas
│   ├── database/
│   ├── external-apis/
│   └── cache/
└── presentation/         # Controllers/API
    └── controllers/
```

### **Repository Pattern**
- Abstração da camada de dados
- Fácil substituição de banco de dados
- Testabilidade

### **Dependency Injection**
- NestJS nativo
- Facilita testes
- Desacoplamento

---

# 3. STACK TECNOLÓGICO

## 3.1 Frontend

### **Core Framework**
```json
{
  "next": "14.1.0",
  "react": "18.2.0",
  "typescript": "5.3.3"
}
```

**Justificativa:**
- ✅ Next.js 14: App Router + Server Components = performance
- ✅ TypeScript: Type safety + melhor DX
- ✅ React: Ecossistema maduro

### **State Management**
```json
{
  "@tanstack/react-query": "5.17.19",
  "zustand": "4.5.0"
}
```

**Justificativa:**
- ✅ TanStack Query: Cache automático, mutations, sincronização
- ✅ Zustand: Estado global simples e performático

### **Forms & Validation**
```json
{
  "react-hook-form": "7.49.3",
  "@hookform/resolvers": "3.3.4",
  "zod": "3.22.4"
}
```

**Justificativa:**
- ✅ React Hook Form: Performance (uncontrolled forms)
- ✅ Zod: Validação TypeScript-first + schema sharing

### **UI Components**
```json
{
  "tailwindcss": "3.4.1",
  "@radix-ui/react-*": "latest",
  "class-variance-authority": "0.7.0",
  "tailwind-merge": "2.2.1",
  "lucide-react": "0.309.0"
}
```

**Justificativa:**
- ✅ Tailwind: Utility-first, rápido desenvolvimento
- ✅ Radix UI: Acessibilidade + headless components
- ✅ Lucide: Ícones modernos

### **Data Visualization**
```json
{
  "recharts": "2.12.0",
  "@tremor/react": "3.14.0",
  "bpmn-js": "17.0.0"
}
```

**Justificativa:**
- ✅ Recharts: Dashboards interativos
- ✅ Tremor: Componentes pré-construídos para analytics
- ✅ BPMN.js: Modelagem de processos padrão BPMN 2.0

## 3.2 Backend

### **Core Framework**
```json
{
  "@nestjs/core": "10.3.0",
  "@nestjs/common": "10.3.0",
  "@nestjs/platform-express": "10.3.0",
  "typescript": "5.3.3"
}
```

**Justificativa:**
- ✅ NestJS: Arquitetura enterprise-ready
- ✅ TypeScript nativo
- ✅ Dependency Injection
- ✅ Modular e testável

### **ORM e Database**
```json
{
  "@prisma/client": "5.9.0",
  "prisma": "5.9.0"
}
```

**Justificativa:**
- ✅ Prisma: Type-safe, migrations, schema-first
- ✅ Geração automática de tipos
- ✅ Excelente DX

### **Authentication**
```json
{
  "next-auth": "5.0.0-beta",
  "@nestjs/jwt": "10.2.0",
  "bcryptjs": "2.4.3"
}
```

**Justificativa:**
- ✅ NextAuth: Autenticação completa (OAuth, credentials)
- ✅ JWT: Stateless, escalável
- ✅ bcryptjs: Hash de senhas seguro

### **Validation**
```json
{
  "class-validator": "0.14.1",
  "class-transformer": "0.5.1",
  "zod": "3.22.4"
}
```

**Justificativa:**
- ✅ class-validator: Validação com decorators (NestJS native)
- ✅ Zod: Compartilhamento de schemas frontend/backend

### **Cache & Queue**
```json
{
  "@nestjs/redis": "10.0.0",
  "ioredis": "5.3.2",
  "@nestjs/bull": "10.0.1",
  "bull": "4.12.0"
}
```

**Justificativa:**
- ✅ Redis: Cache + Pub/Sub + Sessions
- ✅ Bull: Filas de jobs (emails, processamentos pesados)

## 3.3 Database

### **PostgreSQL 16**
```yaml
postgres:
  version: "16"
  extensions:
    - pgvector      # Embeddings para IA
    - pg_trgm       # Full-text search
    - uuid-ossp     # UUIDs
    - pg_stat_statements  # Performance monitoring
```

**Justificativa:**
- ✅ Relacional robusto
- ✅ JSONB para flexibilidade
- ✅ pgvector para IA/embeddings
- ✅ Transações ACID

### **Redis 7**
```yaml
redis:
  version: "7"
  persistence: AOF + RDB
  use_cases:
    - Cache de queries
    - Sessões de usuário
    - Rate limiting
    - Pub/Sub (real-time)
    - Filas de jobs
```

### **TimescaleDB**
```yaml
timescaledb:
  version: "2.13"
  use_case: Time-series data
  data:
    - Métricas de KPIs
    - Histórico de objetivos
    - Analytics
```

## 3.4 AI & Machine Learning

### **OpenAI Integration**
```json
{
  "openai": "4.26.0",
  "langchain": "0.1.20",
  "@langchain/openai": "0.0.14"
}
```

**Arquitetura de IA:**
```typescript
// Consultor Especialista
GPT-4 Turbo
  ↓
LangChain (orquestração)
  ↓
Vector Store (pgvector)
  ↓
Contexto da empresa (RAG)
```

**Casos de Uso:**
1. Consultor Especialista (chat)
2. Cascateamento inteligente de objetivos
3. Análises preditivas
4. Geração automática de processos BPM
5. Sugestões de melhorias

## 3.5 Pagamentos & Emails

### **Stripe**
```json
{
  "stripe": "14.14.0",
  "@stripe/stripe-js": "2.4.0"
}
```

**Implementação:**
- Assinaturas recorrentes
- Webhooks para eventos
- Customer Portal (autoatendimento)
- Invoices automáticos

### **Brevo (SendinBlue)**
```json
{
  "@getbrevo/brevo": "2.0.0"
}
```

**Tipos de Email:**
- Transacionais (boas-vindas, recuperação senha)
- Notificações (alertas, deadlines)
- Relatórios automáticos
- Newsletters (futuro)

## 3.6 DevOps & Infrastructure

### **Containerization**
```yaml
Docker: 24.0+
Docker Compose: 2.23+
```

### **CI/CD**
```yaml
GitHub Actions:
  - Testes automatizados
  - Build
  - Deploy production
  - Database migrations
```

### **Monitoring**
```json
{
  "@sentry/nextjs": "7.99.0",
  "@opentelemetry/api": "1.7.0",
  "prom-client": "15.1.0"
}
```

**Stack de Observabilidade:**
- Sentry: Error tracking
- Prometheus: Métricas
- Grafana: Visualização
- Logs: Winston + Loki

---

# 4. INFRAESTRUTURA

## 4.1 Servidor Ubuntu 24.04 LTS

### **Especificações Mínimas**

| Fase | vCPU | RAM | Disco | Usuários |
|------|------|-----|-------|----------|
| MVP | 4 | 8 GB | 100 GB SSD | 100 |
| Growth | 8 | 16 GB | 250 GB SSD | 500 |
| Scale | 16+ | 32+ GB | 500+ GB SSD | 5000+ |

### **Configuração do Servidor**

```bash
# /etc/infrastructure/server-setup.sh

#!/bin/bash
# Smart Work Business - Server Setup

# 1. Atualizar sistema
apt update && apt upgrade -y

# 2. Instalar dependências
apt install -y \
  git \
  curl \
  wget \
  build-essential \
  ca-certificates \
  gnupg \
  lsb-release

# 3. Instalar Docker
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh

# 4. Instalar Docker Compose
apt install -y docker-compose-plugin

# 5. Configurar firewall
ufw allow 22/tcp   # SSH
ufw allow 80/tcp   # HTTP
ufw allow 443/tcp  # HTTPS
ufw enable

# 6. Configurar swap (se necessário)
fallocate -l 4G /swapfile
chmod 600 /swapfile
mkswap /swapfile
swapon /swapfile
echo '/swapfile none swap sw 0 0' >> /etc/fstab

# 7. Otimizações PostgreSQL
sysctl -w vm.overcommit_memory=2
sysctl -w vm.swappiness=10
echo "vm.overcommit_memory=2" >> /etc/sysctl.conf
echo "vm.swappiness=10" >> /etc/sysctl.conf

# 8. Criar usuário de aplicação
useradd -m -s /bin/bash smartwork
usermod -aG docker smartwork
```

## 4.2 Docker Compose Production

```yaml
# docker-compose.prod.yml
version: '3.8'

networks:
  smartwork-network:
    driver: bridge

volumes:
  postgres_data:
    driver: local
  redis_data:
    driver: local
  timescale_data:
    driver: local
  nginx_ssl:
    driver: local

services:
  # ============================================
  # FRONTEND (Next.js)
  # ============================================
  frontend:
    build:
      context: ./frontend
      dockerfile: Dockerfile.prod
    container_name: smartwork-frontend
    restart: always
    environment:
      - NODE_ENV=production
      - NEXT_PUBLIC_API_URL=https://api.smartworkbusiness.com.br
      - NEXTAUTH_URL=https://app.smartworkbusiness.com.br
    env_file:
      - .env.frontend.prod
    ports:
      - "3000:3000"
    networks:
      - smartwork-network
    depends_on:
      - backend
    healthcheck:
      test: ["CMD", "wget", "--quiet", "--tries=1", "--spider", "http://localhost:3000/api/health"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 40s

  # ============================================
  # BACKEND (NestJS)
  # ============================================
  backend:
    build:
      context: ./backend
      dockerfile: Dockerfile.prod
    container_name: smartwork-backend
    restart: always
    environment:
      - NODE_ENV=production
      - PORT=4000
    env_file:
      - .env.backend.prod
    ports:
      - "4000:4000"
    networks:
      - smartwork-network
    depends_on:
      postgres:
        condition: service_healthy
      redis:
        condition: service_healthy
    healthcheck:
      test: ["CMD", "wget", "--quiet", "--tries=1", "--spider", "http://localhost:4000/health"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 40s
    deploy:
      resources:
        limits:
          cpus: '2'
          memory: 2G
        reservations:
          cpus: '1'
          memory: 1G

  # ============================================
  # POSTGRESQL 16
  # ============================================
  postgres:
    image: postgres:16-alpine
    container_name: smartwork-postgres
    restart: always
    environment:
      POSTGRES_DB: ${POSTGRES_DB}
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
      POSTGRES_INITDB_ARGS: "-E UTF8 --locale=pt_BR.UTF-8"
    volumes:
      - postgres_data:/var/lib/postgresql/data
      - ./backups:/backups
      - ./scripts/postgres-init.sql:/docker-entrypoint-initdb.d/init.sql
    ports:
      - "5432:5432"
    networks:
      - smartwork-network
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U ${POSTGRES_USER} -d ${POSTGRES_DB}"]
      interval: 10s
      timeout: 5s
      retries: 5
      start_period: 10s
    deploy:
      resources:
        limits:
          cpus: '4'
          memory: 4G
        reservations:
          cpus: '2'
          memory: 2G
    command: >
      postgres
      -c max_connections=200
      -c shared_buffers=2GB
      -c effective_cache_size=6GB
      -c maintenance_work_mem=512MB
      -c checkpoint_completion_target=0.9
      -c wal_buffers=16MB
      -c default_statistics_target=100
      -c random_page_cost=1.1
      -c effective_io_concurrency=200
      -c work_mem=10485kB
      -c min_wal_size=1GB
      -c max_wal_size=4GB

  # ============================================
  # REDIS 7
  # ============================================
  redis:
    image: redis:7-alpine
    container_name: smartwork-redis
    restart: always
    command: >
      redis-server
      --appendonly yes
      --appendfsync everysec
      --requirepass ${REDIS_PASSWORD}
      --maxmemory 1gb
      --maxmemory-policy allkeys-lru
    volumes:
      - redis_data:/data
    ports:
      - "6379:6379"
    networks:
      - smartwork-network
    healthcheck:
      test: ["CMD", "redis-cli", "--raw", "incr", "ping"]
      interval: 10s
      timeout: 5s
      retries: 5
    deploy:
      resources:
        limits:
          cpus: '1'
          memory: 1G

  # ============================================
  # TIMESCALEDB (Métricas)
  # ============================================
  timescaledb:
    image: timescale/timescaledb:latest-pg16
    container_name: smartwork-timescale
    restart: always
    environment:
      POSTGRES_DB: ${TIMESCALE_DB}
      POSTGRES_USER: ${TIMESCALE_USER}
      POSTGRES_PASSWORD: ${TIMESCALE_PASSWORD}
    volumes:
      - timescale_data:/var/lib/postgresql/data
    ports:
      - "5433:5432"
    networks:
      - smartwork-network
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U ${TIMESCALE_USER}"]
      interval: 10s
      timeout: 5s
      retries: 5

  # ============================================
  # NGINX (Reverse Proxy)
  # ============================================
  nginx:
    image: nginx:alpine
    container_name: smartwork-nginx
    restart: always
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf:ro
      - ./nginx/sites-enabled:/etc/nginx/sites-enabled:ro
      - nginx_ssl:/etc/nginx/ssl:ro
      - ./nginx/logs:/var/log/nginx
    networks:
      - smartwork-network
    depends_on:
      - frontend
      - backend
    healthcheck:
      test: ["CMD", "wget", "--quiet", "--tries=1", "--spider", "http://localhost/health"]
      interval: 30s
      timeout: 10s
      retries: 3

  # ============================================
  # BACKUP AUTOMÁTICO
  # ============================================
  backup:
    image: postgres:16-alpine
    container_name: smartwork-backup
    restart: "no"
    environment:
      PGHOST: postgres
      PGDATABASE: ${POSTGRES_DB}
      PGUSER: ${POSTGRES_USER}
      PGPASSWORD: ${POSTGRES_PASSWORD}
    volumes:
      - ./backups:/backups
      - ./scripts/backup.sh:/backup.sh
    networks:
      - smartwork-network
    depends_on:
      - postgres
    entrypoint: ["/bin/sh", "-c"]
    command:
      - |
        echo "Backup automático configurado"
        # Executar via cron no host

  # ============================================
  # MONITORING (Opcional mas recomendado)
  # ============================================
  prometheus:
    image: prom/prometheus:latest
    container_name: smartwork-prometheus
    restart: always
    volumes:
      - ./monitoring/prometheus.yml:/etc/prometheus/prometheus.yml
      - ./monitoring/prometheus-data:/prometheus
    ports:
      - "9090:9090"
    networks:
      - smartwork-network

  grafana:
    image: grafana/grafana:latest
    container_name: smartwork-grafana
    restart: always
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=${GRAFANA_PASSWORD}
    volumes:
      - ./monitoring/grafana-data:/var/lib/grafana
    ports:
      - "3001:3000"
    networks:
      - smartwork-network
    depends_on:
      - prometheus
```

## 4.3 NGINX Configuration

```nginx
# nginx/nginx.conf

user nginx;
worker_processes auto;
worker_rlimit_nofile 65535;
error_log /var/log/nginx/error.log warn;
pid /var/run/nginx.pid;

events {
    worker_connections 4096;
    use epoll;
    multi_accept on;
}

http {
    include /etc/nginx/mime.types;
    default_type application/octet-stream;

    # Logs
    log_format main '$remote_addr - $remote_user [$time_local] "$request" '
                    '$status $body_bytes_sent "$http_referer" '
                    '"$http_user_agent" "$http_x_forwarded_for"';
    access_log /var/log/nginx/access.log main;

    # Performance
    sendfile on;
    tcp_nopush on;
    tcp_nodelay on;
    keepalive_timeout 65;
    types_hash_max_size 2048;
    client_max_body_size 20M;

    # Gzip
    gzip on;
    gzip_vary on;
    gzip_proxied any;
    gzip_comp_level 6;
    gzip_types text/plain text/css text/xml text/javascript 
               application/json application/javascript application/xml+rss 
               application/rss+xml font/truetype font/opentype 
               application/vnd.ms-fontobject image/svg+xml;

    # Security headers
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header X-XSS-Protection "1; mode=block" always;
    add_header Referrer-Policy "strict-origin-when-cross-origin" always;

    # Rate limiting
    limit_req_zone $binary_remote_addr zone=api_limit:10m rate=10r/s;
    limit_req_zone $binary_remote_addr zone=general_limit:10m rate=30r/s;

    # Upstream servers
    upstream frontend_backend {
        least_conn;
        server frontend:3000 max_fails=3 fail_timeout=30s;
    }

    upstream api_backend {
        least_conn;
        server backend:4000 max_fails=3 fail_timeout=30s;
    }

    # Redirect HTTP to HTTPS
    server {
        listen 80;
        server_name app.smartworkbusiness.com.br api.smartworkbusiness.com.br;
        
        location /.well-known/acme-challenge/ {
            root /var/www/certbot;
        }

        location / {
            return 301 https://$host$request_uri;
        }
    }

    # Frontend (Next.js)
    server {
        listen 443 ssl http2;
        server_name app.smartworkbusiness.com.br;

        ssl_certificate /etc/nginx/ssl/fullchain.pem;
        ssl_certificate_key /etc/nginx/ssl/privkey.pem;
        ssl_protocols TLSv1.2 TLSv1.3;
        ssl_ciphers HIGH:!aNULL:!MD5;
        ssl_prefer_server_ciphers on;

        location / {
            limit_req zone=general_limit burst=20 nodelay;
            
            proxy_pass http://frontend_backend;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection 'upgrade';
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
            proxy_cache_bypass $http_upgrade;
            
            proxy_connect_timeout 60s;
            proxy_send_timeout 60s;
            proxy_read_timeout 60s;
        }

        # Cache estático
        location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg|woff|woff2|ttf|eot)$ {
            proxy_pass http://frontend_backend;
            expires 1y;
            add_header Cache-Control "public, immutable";
        }
    }

    # Backend API (NestJS)
    server {
        listen 443 ssl http2;
        server_name api.smartworkbusiness.com.br;

        ssl_certificate /etc/nginx/ssl/fullchain.pem;
        ssl_certificate_key /etc/nginx/ssl/privkey.pem;
        ssl_protocols TLSv1.2 TLSv1.3;
        ssl_ciphers HIGH:!aNULL:!MD5;

        location / {
            limit_req zone=api_limit burst=10 nodelay;
            
            proxy_pass http://api_backend;
            proxy_http_version 1.1;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
            
            # CORS
            add_header 'Access-Control-Allow-Origin' 'https://app.smartworkbusiness.com.br' always;
            add_header 'Access-Control-Allow-Methods' 'GET, POST, PUT, DELETE, OPTIONS' always;
            add_header 'Access-Control-Allow-Headers' 'Authorization, Content-Type' always;
            
            if ($request_method = 'OPTIONS') {
                return 204;
            }
        }

        # Webhooks (sem rate limit)
        location /webhooks {
            proxy_pass http://api_backend;
            proxy_http_version 1.1;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }
    }
}
```

---

# 5. ESTRUTURA DO PROJETO

## 5.1 Monorepo Structure

```
smartwork-saas/
├── .github/
│   └── workflows/
│       ├── ci-frontend.yml
│       ├── ci-backend.yml
│       ├── deploy-production.yml
│       └── database-backup.yml
├── frontend/                      # Next.js Application
│   ├── public/
│   ├── src/
│   ├── Dockerfile.prod
│   ├── next.config.js
│   ├── package.json
│   ├── tsconfig.json
│   └── tailwind.config.ts
├── backend/                       # NestJS Application
│   ├── src/
│   ├── test/
│   ├── Dockerfile.prod
│   ├── nest-cli.json
│   ├── package.json
│   └── tsconfig.json
├── prisma/                        # Database Schema (Compartilhado)
│   ├── schema.prisma
│   ├── migrations/
│   └── seed.ts
├── scripts/                       # Scripts utilitários
│   ├── setup-server.sh
│   ├── backup.sh
│   ├── postgres-init.sql
│   └── deploy.sh
├── nginx/                         # NGINX configs
│   ├── nginx.conf
│   └── sites-enabled/
├── monitoring/                    # Prometheus + Grafana
│   ├── prometheus.yml
│   └── dashboards/
├── docs/                          # Documentação
│   ├── api/
│   ├── architecture/
│   └── deployment/
├── docker-compose.yml             # Desenvolvimento local
├── docker-compose.prod.yml        # Produção
├── .env.example
├── .env.frontend.example
├── .env.backend.example
├── package.json                   # Root (scripts gerais)
├── turbo.json                     # Turborepo (opcional)
└── README.md
```

## 5.2 Frontend Structure (Next.js)

```
frontend/src/
├── app/                           # Next.js 14 App Router
│   ├── (auth)/                    # Grupo de rotas autenticação
│   │   ├── login/
│   │   │   └── page.tsx
│   │   ├── register/
│   │   │   └── page.tsx
│   │   ├── forgot-password/
│   │   │   └── page.tsx
│   │   └── layout.tsx             # Layout minimalista
│   ├── (dashboard)/               # Grupo de rotas autenticadas
│   │   ├── layout.tsx             # Layout completo (sidebar, header)
│   │   ├── dashboard/
│   │   │   └── page.tsx           # Home dashboard
│   │   ├── objectives/            # Módulo Objetivos SMART
│   │   │   ├── page.tsx           # Lista objetivos
│   │   │   ├── new/
│   │   │   │   └── page.tsx       # Criar objetivo
│   │   │   ├── [id]/
│   │   │   │   ├── page.tsx       # Detalhes objetivo
│   │   │   │   └── edit/
│   │   │   │       └── page.tsx   # Editar objetivo
│   │   │   └── components/
│   │   │       ├── objective-card.tsx
│   │   │       ├── objective-form.tsx
│   │   │       ├── objective-progress.tsx
│   │   │       └── cascading-tree.tsx
│   │   ├── bpm/                   # Módulo BPM/BPMN
│   │   │   ├── page.tsx
│   │   │   ├── modeler/
│   │   │   │   └── page.tsx       # Editor BPMN
│   │   │   ├── [id]/
│   │   │   │   └── page.tsx
│   │   │   └── components/
│   │   │       ├── bpmn-modeler.tsx
│   │   │       └── process-list.tsx
│   │   ├── analytics/             # Módulo BI e Analytics
│   │   │   ├── page.tsx
│   │   │   ├── pareto/
│   │   │   │   └── page.tsx       # Análise 80/20
│   │   │   └── components/
│   │   │       ├── metrics-dashboard.tsx
│   │   │       ├── chart-*.tsx
│   │   │       └── kpi-card.tsx
│   │   ├── pdca/                  # Módulo PDCA
│   │   │   ├── page.tsx
│   │   │   ├── [id]/
│   │   │   │   └── page.tsx
│   │   │   └── components/
│   │   │       └── pdca-cycle.tsx
│   │   ├── tasks/                 # Módulo Tarefas
│   │   │   ├── page.tsx
│   │   │   ├── [id]/
│   │   │   │   └── page.tsx
│   │   │   └── components/
│   │   │       ├── task-kanban.tsx
│   │   │       └── task-form-5w2h.tsx
│   │   ├── settings/              # Configurações
│   │   │   ├── page.tsx
│   │   │   ├── organization/
│   │   │   ├── billing/
│   │   │   ├── users/
│   │   │   └── integrations/
│   │   └── ai-consultant/         # Chat IA
│   │       └── page.tsx
│   ├── api/                       # API Routes (se necessário)
│   │   ├── auth/
│   │   │   └── [...nextauth]/
│   │   │       └── route.ts
│   │   └── health/
│   │       └── route.ts
│   ├── layout.tsx                 # Root layout
│   ├── page.tsx                   # Landing page
│   ├── globals.css
│   └── error.tsx
├── components/                    # Componentes reutilizáveis
│   ├── ui/                        # shadcn/ui components
│   │   ├── button.tsx
│   │   ├── card.tsx
│   │   ├── dialog.tsx
│   │   ├── form.tsx
│   │   ├── input.tsx
│   │   ├── select.tsx
│   │   ├── table.tsx
│   │   └── ...
│   ├── layouts/
│   │   ├── sidebar.tsx
│   │   ├── header.tsx
│   │   └── footer.tsx
│   ├── charts/
│   │   ├── line-chart.tsx
│   │   ├── bar-chart.tsx
│   │   ├── pie-chart.tsx
│   │   └── area-chart.tsx
│   └── shared/
│       ├── loading.tsx
│       ├── error-boundary.tsx
│       └── empty-state.tsx
├── lib/                           # Bibliotecas e utilidades
│   ├── api-client.ts              # Axios/Fetch wrapper
│   ├── utils.ts                   # Funções utilitárias
│   ├── constants.ts               # Constantes
│   ├── validations/               # Zod schemas
│   │   ├── objective.schema.ts
│   │   ├── auth.schema.ts
│   │   └── ...
│   └── formatters.ts              # Formatação (datas, moeda, etc)
├── hooks/                         # React hooks customizados
│   ├── use-auth.ts
│   ├── use-objectives.ts
│   ├── use-analytics.ts
│   ├── use-ai-consultant.ts
│   └── use-debounce.ts
├── services/                      # Chamadas API (TanStack Query)
│   ├── objectives.service.ts
│   ├── bpm.service.ts
│   ├── analytics.service.ts
│   ├── tasks.service.ts
│   └── auth.service.ts
├── store/                         # Zustand stores
│   ├── auth.store.ts
│   ├── ui.store.ts
│   └── filters.store.ts
├── types/                         # TypeScript types
│   ├── api.types.ts
│   ├── models.types.ts
│   └── index.ts
├── config/                        # Configurações
│   ├── site.config.ts
│   └── navigation.config.ts
└── middleware.ts                  # Next.js middleware (auth)
```

## 5.3 Backend Structure (NestJS)

```
backend/src/
├── main.ts                        # Entry point
├── app.module.ts                  # Root module
├── app.controller.ts
├── app.service.ts
├── common/                        # Compartilhado entre módulos
│   ├── decorators/
│   │   ├── roles.decorator.ts
│   │   ├── public.decorator.ts
│   │   └── audit.decorator.ts
│   ├── guards/
│   │   ├── jwt-auth.guard.ts
│   │   ├── roles.guard.ts
│   │   └── throttle.guard.ts
│   ├── interceptors/
│   │   ├── logging.interceptor.ts
│   │   ├── transform.interceptor.ts
│   │   └── cache.interceptor.ts
│   ├── pipes/
│   │   └── validation.pipe.ts
│   ├── filters/
│   │   └── http-exception.filter.ts
│   ├── middlewares/
│   │   └── logger.middleware.ts
│   └── utils/
│       ├── pagination.util.ts
│       └── date.util.ts
├── config/                        # Configurações
│   ├── database.config.ts
│   ├── redis.config.ts
│   ├── jwt.config.ts
│   └── app.config.ts
├── prisma/                        # Prisma service
│   ├── prisma.service.ts
│   └── prisma.module.ts
├── modules/                       # Módulos de negócio
│   ├── auth/
│   │   ├── auth.module.ts
│   │   ├── auth.controller.ts
│   │   ├── auth.service.ts
│   │   ├── strategies/
│   │   │   ├── jwt.strategy.ts
│   │   │   └── local.strategy.ts
│   │   └── dto/
│   │       ├── login.dto.ts
│   │       └── register.dto.ts
│   ├── users/
│   │   ├── users.module.ts
│   │   ├── users.controller.ts
│   │   ├── users.service.ts
│   │   ├── users.repository.ts
│   │   └── dto/
│   │       ├── create-user.dto.ts
│   │       └── update-user.dto.ts
│   ├── organizations/
│   │   ├── organizations.module.ts
│   │   ├── organizations.controller.ts
│   │   ├── organizations.service.ts
│   │   ├── organizations.repository.ts
│   │   └── dto/
│   ├── objectives/                # MÓDULO CORE
│   │   ├── objectives.module.ts
│   │   ├── objectives.controller.ts
│   │   ├── objectives.service.ts
│   │   ├── objectives.repository.ts
│   │   ├── services/
│   │   │   ├── smart-validator.service.ts
│   │   │   ├── cascading.service.ts
│   │   │   └── progress-tracker.service.ts
│   │   ├── dto/
│   │   │   ├── create-objective.dto.ts
│   │   │   ├── update-objective.dto.ts
│   │   │   └── cascade-objective.dto.ts
│   │   └── entities/
│   │       └── objective.entity.ts
│   ├── bpm/                       # MÓDULO BPM/BPMN
│   │   ├── bpm.module.ts
│   │   ├── bpm.controller.ts
│   │   ├── bpm.service.ts
│   │   ├── bpm.repository.ts
│   │   ├── services/
│   │   │   ├── bpmn-parser.service.ts
│   │   │   ├── bpmn-validator.service.ts
│   │   │   └── process-analyzer.service.ts
│   │   └── dto/
│   ├── analytics/                 # MÓDULO BI
│   │   ├── analytics.module.ts
│   │   ├── analytics.controller.ts
│   │   ├── analytics.service.ts
│   │   ├── services/
│   │   │   ├── metrics.service.ts
│   │   │   ├── pareto.service.ts
│   │   │   ├── predictions.service.ts
│   │   │   └── dashboards.service.ts
│   │   └── dto/
│   ├── pdca/                      # MÓDULO PDCA
│   │   ├── pdca.module.ts
│   │   ├── pdca.controller.ts
│   │   ├── pdca.service.ts
│   │   ├── pdca.repository.ts
│   │   └── dto/
│   ├── tasks/                     # MÓDULO TAREFAS
│   │   ├── tasks.module.ts
│   │   ├── tasks.controller.ts
│   │   ├── tasks.service.ts
│   │   ├── tasks.repository.ts
│   │   └── dto/
│   │       └── create-task-5w2h.dto.ts
│   ├── ai/                        # MÓDULO IA
│   │   ├── ai.module.ts
│   │   ├── ai.controller.ts
│   │   ├── ai.service.ts
│   │   ├── services/
│   │   │   ├── openai.service.ts
│   │   │   ├── langchain.service.ts
│   │   │   ├── consultant.service.ts
│   │   │   ├── embeddings.service.ts
│   │   │   └── rag.service.ts
│   │   ├── prompts/
│   │   │   ├── consultant.prompts.ts
│   │   │   ├── cascading.prompts.ts
│   │   │   └── analysis.prompts.ts
│   │   └── dto/
│   ├── payments/                  # MÓDULO PAGAMENTOS
│   │   ├── payments.module.ts
│   │   ├── payments.controller.ts
│   │   ├── payments.service.ts
│   │   ├── services/
│   │   │   └── stripe.service.ts
│   │   └── webhooks/
│   │       └── stripe.webhook.controller.ts
│   ├── notifications/             # MÓDULO NOTIFICAÇÕES
│   │   ├── notifications.module.ts
│   │   ├── notifications.service.ts
│   │   ├── services/
│   │   │   ├── brevo.service.ts
│   │   │   └── templates.service.ts
│   │   └── dto/
│   ├── audit/                     # MÓDULO AUDITORIA
│   │   ├── audit.module.ts
│   │   ├── audit.service.ts
│   │   ├── audit.repository.ts
│   │   └── dto/
│   └── governance/                # MÓDULO GOVERNANÇA
│       ├── governance.module.ts
│       ├── governance.service.ts
│       ├── services/
│       │   ├── iso9001.service.ts
│       │   ├── iso27001.service.ts
│       │   ├── iso31000.service.ts
│       │   └── lgpd.service.ts
│       └── dto/
└── health/                        # Health checks
    ├── health.controller.ts
    └── health.service.ts
```

---

## 6. MÓDULOS E FUNCIONALIDADES

*Ver documentação detalhada em: `docs/MODULOS-E-FUNCIONALIDADES.md`*

**Resumo dos Módulos Core:**

1. **Autenticação e Autorização** - Login, MFA, RBAC
2. **Organizações (Multi-tenant)** - Planos, billing, membros
3. **Objetivos SMART** - CRUD, validação, cascateamento, OKRs
4. **BPM/BPMN** - Modelagem, POPs, RACI
5. **Analytics e BI** - Dashboards, KPIs, Análise 80/20
6. **PDCA** - Ciclos de melhoria contínua
7. **Tarefas** - 5W2H, Kanban, time tracking
8. **Consultor IA** - Chat inteligente, cascateamento, análises
9. **Governança** - ISO 9001, 27001, 31000, LGPD
10. **Pagamentos** - Stripe, assinaturas
11. **Notificações** - Brevo, emails transacionais

---

## 7. MODELO DE DADOS

*Ver schema completo em: `docs/DEPENDENCIAS-E-CONFIGURACOES.md`*

### Principais Entidades

```
├── User (usuários)
├── Organization (multi-tenant)
├── OrganizationMember (membros)
├── Objective (objetivos SMART)
├── OKR (key results)
├── BPMProcess (processos)
├── POP (procedimentos)
├── PDCACycle (PDCA)
├── Task (tarefas)
├── KPI (indicadores)
├── Dashboard (dashboards)
├── AIConversation (conversas IA)
└── AuditLog (auditoria)
```

---

## 8. SEGURANÇA E COMPLIANCE

### 8.1 Segurança da Aplicação

**Autenticação:**
- JWT com refresh tokens
- MFA (2FA)
- SSO (Enterprise)
- Session management

**Autorização:**
- RBAC (Role-Based Access Control)
- Permissões granulares
- Multi-tenant isolation
- Row-level security

**Criptografia:**
- TLS 1.3 (trânsito)
- AES-256 (repouso)
- Bcrypt (senhas)
- Encrypted fields (Prisma)

**Proteções:**
- Rate limiting (Redis)
- CORS configurado
- Helmet.js (security headers)
- Input validation (Zod)
- SQL injection (Prisma prepared statements)
- XSS prevention
- CSRF tokens

### 8.2 LGPD Compliance

**Dados Pessoais:**
- Mapeamento automático (`@PII()` decorator)
- Controle de consentimento
- Minimização de dados
- Anonimização em relatórios
- Direitos dos titulares (acesso, retificação, exclusão)

**Auditoria:**
- Trilha completa (quem, quando, o quê)
- Imutável (append-only)
- Retenção configurável
- Exportação de evidências

### 8.3 ISOs

**ISO 9001 (Qualidade):**
- Objetivos da qualidade integrados
- Abordagem de processos
- Melhoria contínua (PDCA)
- Documentação controlada

**ISO 27001 (Segurança):**
- Controles de acesso nativos
- Gestão de identidade
- Incidentes rastreados
- Trilha de auditoria

**ISO 31000 (Riscos):**
- Avaliação de riscos em objetivos
- Identificação em processos
- Priorização (impacto x probabilidade)
- Alertas baseados em riscos

---

## 9. INTEGRAÇÕES EXTERNAS

### 9.1 OpenAI API

**Uso:**
- GPT-4 Turbo (Consultor IA)
- text-embedding-ada-002 (RAG)
- Análises preditivas
- Cascateamento inteligente

**Implementação:**
```typescript
import { OpenAI } from 'openai';

const openai = new OpenAI({
  apiKey: process.env.OPENAI_API_KEY,
});

const completion = await openai.chat.completions.create({
  model: 'gpt-4-turbo-preview',
  messages: [
    { role: 'system', content: SYSTEM_PROMPT },
    { role: 'user', content: userMessage }
  ],
  temperature: 0.7,
});
```

**Cache:**
- Respostas em Redis (1h)
- Embeddings em pgvector
- Rate limiting por plano

### 9.2 Stripe

**Uso:**
- Assinaturas recorrentes
- Invoices automáticos
- Customer Portal
- Webhooks

**Webhooks:**
```typescript
@Post('/webhooks/stripe')
@UseGuards(StripeWebhookGuard)
async handleStripeWebhook(@Body() event: Stripe.Event) {
  switch (event.type) {
    case 'customer.subscription.created':
      await this.handleSubscriptionCreated(event);
      break;
    case 'invoice.paid':
      await this.handleInvoicePaid(event);
      break;
    // ...
  }
}
```

### 9.3 Brevo (SendinBlue)

**Uso:**
- Emails transacionais
- Notificações
- Relatórios automáticos

**Templates:**
- Boas-vindas
- Verificação de email
- Recuperação de senha
- Convites
- Alertas de deadline
- Relatórios semanais

---

## 10. DESENVOLVIMENTO E DEPLOY

### 10.1 Ambiente de Desenvolvimento

**Requisitos:**
```
Node.js: 20+ LTS
Docker: 24+
Docker Compose: 2.23+
Git: 2.40+
```

**Setup:**
```bash
# Clone
git clone https://github.com/org/smartwork-saas.git
cd smartwork-saas

# Env
cp .env.example .env.local

# Docker
docker-compose up -d

# Install
npm install --prefix frontend
npm install --prefix backend

# Database
cd backend
npx prisma generate
npx prisma db push
npx prisma db seed

# Dev
npm run dev  # frontend (terminal 1)
npm run start:dev  # backend (terminal 2)
```

### 10.2 CI/CD (GitHub Actions)

**Pipeline:**
```yaml
# .github/workflows/ci.yml

name: CI

on: [push, pull_request]

jobs:
  test-frontend:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
      - run: npm ci --prefix frontend
      - run: npm test --prefix frontend
      - run: npm run build --prefix frontend

  test-backend:
    runs-on: ubuntu-latest
    services:
      postgres:
        image: postgres:16
        env:
          POSTGRES_PASSWORD: postgres
        options: >-
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
      - run: npm ci --prefix backend
      - run: npm test --prefix backend
      - run: npm run test:e2e --prefix backend
```

### 10.3 Deploy Production

**Strategy:** Docker Compose no Ubuntu Server

```bash
# .github/workflows/deploy-production.yml

name: Deploy Production

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to Server
        uses: appleboy/ssh-action@master
        with:
          host: ${{ secrets.SERVER_HOST }}
          username: ${{ secrets.SERVER_USER }}
          key: ${{ secrets.SSH_PRIVATE_KEY }}
          script: |
            cd /home/smartwork/smartwork-saas
            git pull origin main
            docker-compose -f docker-compose.prod.yml up -d --build
            docker-compose -f docker-compose.prod.yml exec -T backend npx prisma migrate deploy
```

---

## 11. ROADMAP DE DESENVOLVIMENTO

*Ver roadmap completo em: `docs/ROADMAP-DESENVOLVIMENTO.md`*

### MVP (Meses 1-3)

**Sprint 1-2:** Auth + Multi-tenant  
**Sprint 3-4:** Objetivos SMART  
**Sprint 5-6:** Dashboards + Analytics  
**Sprint 7-8:** Tarefas + BPM básico  
**Sprint 9:** Pagamentos (Stripe)  
**Sprint 10:** Consultor IA básico  
**Sprint 11-12:** Testes + Polish  

**Entrega:** 50-100 usuários beta

### Fase 2 (Meses 4-6)

**Sprint 13-14:** IA Avançada (Cascateamento)  
**Sprint 15-16:** PDCA + Análise 80/20  
**Sprint 17-18:** POPs + Governança  
**Sprint 19-20:** Integrações + API Pública  
**Sprint 21-22:** Mobile PWA  
**Sprint 23-24:** Polish + Lançamento  

**Entrega:** 500-1000 clientes pagantes

---

## 12. ANEXOS E REFERÊNCIAS

### 12.1 Documentos do Projeto

- **APRESENTACAO-SAAS-SMART-WORK-BUSINESS.md** - Apresentação completa do produto
- **docs/MODULOS-E-FUNCIONALIDADES.md** - Detalhamento técnico completo
- **docs/DEPENDENCIAS-E-CONFIGURACOES.md** - Configurações e dependências
- **docs/ROADMAP-DESENVOLVIMENTO.md** - Cronograma e estimativas
- **docs/RESUMO-EXECUTIVO.md** - Resumo executivo do projeto
- **README.md** - Guia rápido de início

### 12.2 Referências Técnicas

**Frameworks:**
- [Next.js Documentation](https://nextjs.org/docs)
- [NestJS Documentation](https://docs.nestjs.com)
- [Prisma Documentation](https://www.prisma.io/docs)

**APIs:**
- [OpenAI API Reference](https://platform.openai.com/docs)
- [Stripe API Reference](https://stripe.com/docs/api)
- [Brevo API Reference](https://developers.brevo.com)

**Padrões:**
- [BPMN 2.0 Specification](https://www.omg.org/spec/BPMN/2.0/)
- [OAuth 2.0 RFC](https://oauth.net/2/)
- [OpenAPI Specification](https://swagger.io/specification/)

### 12.3 Metodologias

**Gestão:**
- Peter Drucker - "Management by Objectives"
- W. Edwards Deming - "Out of the Crisis"
- John Owen - "Business Intelligence"

**Desenvolvimento:**
- Domain-Driven Design (Eric Evans)
- Clean Architecture (Robert C. Martin)
- Test-Driven Development (Kent Beck)

**Processos:**
- BPMN 2.0
- ISO 9001:2015
- ISO 27001:2022
- ISO 31000:2018
- LGPD (Lei 13.709/2018)

---

## CONCLUSÃO

Este documento define completamente a arquitetura e stack tecnológico do Smart Work Business SaaS.

### Pontos-Chave

✅ **Arquitetura escalável** desde o início  
✅ **Stack moderna** e comprovada  
✅ **Separação frontend/backend** clara  
✅ **Multi-tenant nativo**  
✅ **IA integrada** em toda plataforma  
✅ **Governança embutida**  
✅ **Documentação completa**  

### Próximos Passos

1. **Confirmar equipe** (7 pessoas)
2. **Setup infraestrutura** (semana 1)
3. **Iniciar Sprint 1** (Auth + Multi-tenant)
4. **Iteração contínua** (sprints de 2 semanas)

### Contato

**Email:** dev@smartworkbusiness.com.br  
**GitHub:** github.com/smartwork-business  
**Docs:** `/docs`

---

**Smart Work Business**  
*Transformando Dados em Estratégia, Estratégia em Ação e Ação em Resultados*

**Versão 1.0** | **Novembro 2025**

**FIM DO DOCUMENTO**


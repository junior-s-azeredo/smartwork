# PROJETO TÉCNICO
## Smart Work Business - Documento 3

---

## ÍNDICE

1. [Arquitetura do Sistema](#1-arquitetura-do-sistema)
2. [Stack Tecnológico](#2-stack-tecnológico)
3. [Estrutura de Código](#3-estrutura-de-código)
4. [Infraestrutura](#4-infraestrutura)
5. [Segurança e Compliance](#5-segurança-e-compliance)
6. [Decisões Técnicas](#6-decisões-técnicas)

---

# 1. ARQUITETURA DO SISTEMA

## 1.1 Visão Geral

```
┌─────────────────────────────────────────────────────────────┐
│                        USUÁRIO                              │
└─────────────────────────────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                    NGINX (Reverse Proxy)                    │
│                  SSL/TLS + Load Balancing                   │
└─────────────────────────────────────────────────────────────┘
                           │
           ┌───────────────┴───────────────┐
           │                               │
           ▼                               ▼
┌─────────────────────┐         ┌─────────────────────┐
│    FRONTEND         │         │    BACKEND          │
│    Next.js 14+      │◄────────┤    NestJS           │
│    (Port 3000)      │  API    │    (Port 4000)      │
└─────────────────────┘         └─────────────────────┘
                                          │
                    ┌─────────────────────┼─────────────────────┐
                    │                     │                     │
                    ▼                     ▼                     ▼
          ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐
          │   PostgreSQL     │  │     Redis        │  │   AI Service     │
          │   (Port 5432)    │  │   (Port 6379)    │  │   (Python/Go)    │
          │                  │  │                  │  │   (Port 5000)    │
          │  • Dados         │  │  • Cache         │  │                  │
          │  • Schemas       │  │  • Sessions      │  │  • OpenAI API    │
          │  • JSONB         │  │  • Queue         │  │  • LangChain     │
          │  • pgvector      │  │  • Pub/Sub       │  │  • RAG           │
          └──────────────────┘  └──────────────────┘  └──────────────────┘
                    │                     │                     │
                    └─────────────────────┼─────────────────────┘
                                          │
                                          ▼
                              ┌─────────────────────┐
                              │   INTEGRAÇÕES       │
                              ├─────────────────────┤
                              │  • Stripe           │
                              │  • Brevo/SendinBlue │
                              │  • GitHub           │
                              └─────────────────────┘
```

## 1.2 Padrão de Arquitetura

**Tipo:** Monolito Modular com Frontend separado

**Por quê?**
- ✅ Mais simples de desenvolver e testar
- ✅ Menos overhead operacional
- ✅ Fácil de evoluir para microsserviços depois
- ✅ Boa para MVP e crescimento até 5k+ usuários

**Quando migrar para Microserviços?**
- Acima de 10k organizações ativas
- IA/ML precisar escalar independentemente
- Módulos BPM tiverem carga muito alta

---

# 2. STACK TECNOLÓGICO

## 2.1 Frontend

```typescript
{
  "framework": "Next.js 14+",
  "renderização": "Server Components + Client Components",
  "linguagem": "TypeScript 5+",
  "estilização": "Tailwind CSS 3+",
  "componentes": "shadcn/ui + Radix UI",
  "gerenciamento-estado": "Zustand + TanStack Query",
  "autenticação": "NextAuth.js v5",
  "gráficos": "Recharts + Victory",
  "formulários": "React Hook Form + Zod",
  "drag-drop": "@dnd-kit",
  "editor-texto": "Tiptap",
  "bpmn": "bpmn-js"
}
```

**Estrutura de pastas:**

```
frontend/
├── app/                      # Next.js 14 App Router
│   ├── (auth)/              # Rotas de autenticação
│   │   ├── login/
│   │   ├── register/
│   │   └── onboarding/
│   ├── (dashboard)/         # Rotas protegidas
│   │   ├── objectives/
│   │   ├── tasks/
│   │   ├── bpm/
│   │   ├── analytics/
│   │   └── settings/
│   ├── api/                 # API Routes (Next.js)
│   ├── layout.tsx
│   └── page.tsx
├── components/
│   ├── ui/                  # shadcn/ui components
│   ├── layouts/
│   ├── modules/             # Feature components
│   │   ├── objectives/
│   │   ├── tasks/
│   │   ├── bpm/
│   │   └── analytics/
│   └── shared/
├── lib/
│   ├── api/                 # API client
│   ├── auth/                # Auth helpers
│   ├── hooks/               # Custom hooks
│   └── utils/               # Utilities
├── stores/                  # Zustand stores
├── types/                   # TypeScript types
└── styles/
    └── globals.css
```

## 2.2 Backend

```typescript
{
  "framework": "NestJS 10+",
  "linguagem": "TypeScript 5+",
  "orm": "Prisma 5+",
  "autenticação": "Passport + JWT",
  "validação": "class-validator + class-transformer",
  "documentação": "Swagger/OpenAPI",
  "testes": "Jest + Supertest",
  "logging": "Winston",
  "monitoramento": "Prometheus + Grafana (futuro)"
}
```

**Estrutura de pastas:**

```
backend/
├── src/
│   ├── main.ts
│   ├── app.module.ts
│   ├── modules/
│   │   ├── auth/
│   │   │   ├── auth.controller.ts
│   │   │   ├── auth.service.ts
│   │   │   ├── auth.module.ts
│   │   │   ├── dto/
│   │   │   ├── guards/
│   │   │   └── strategies/
│   │   ├── organizations/
│   │   ├── users/
│   │   ├── objectives/
│   │   ├── tasks/
│   │   ├── bpm/
│   │   ├── analytics/
│   │   ├── ai/
│   │   ├── subscriptions/
│   │   └── webhooks/
│   ├── common/
│   │   ├── decorators/
│   │   ├── filters/
│   │   ├── guards/
│   │   ├── interceptors/
│   │   ├── pipes/
│   │   └── utils/
│   ├── config/              # Configurações
│   │   ├── database.config.ts
│   │   ├── redis.config.ts
│   │   └── stripe.config.ts
│   └── prisma/
│       ├── schema.prisma
│       ├── migrations/
│       └── seed.ts
├── test/
└── package.json
```

## 2.3 AI Service (Python)

```python
{
  "linguagem": "Python 3.11+",
  "framework": "FastAPI",
  "ai": "OpenAI API (GPT-5.1, GPT-5-mini, GPT-5-nano)",
  "vector-db": "pgvector (PostgreSQL)",
  "embeddings": "text-embedding-ada-002",
  "framework-ai": "LangChain",
  "processamento": "Pandas + NumPy",
  "ml": "scikit-learn (futuramente)"
}
```

**Responsabilidades:**
- ✅ Consultor Especialista 24/7
- ✅ **Cascateamento Inteligente** (nano → mini → 5.1)
- ✅ Análise 80/20 automática
- ✅ Sugestões inteligentes (tarefas, objetivos)
- ✅ RAG (Retrieval Augmented Generation)
- ✅ Embeddings de documentos/processos

**Cascateamento Inteligente:**

```python
# Lógica de escolha automática do modelo
class AIModelRouter:
    """
    Analisa a query e escolhe o modelo ideal:
    - GPT-5-nano: Queries simples, dados estruturados
    - GPT-5-mini: Análises médias, múltiplos contextos
    - GPT-5.1: Raciocínio complexo, simulações
    """
    
    COMPLEXITY_RULES = {
        'simple': {
            'model': 'gpt-5-nano',
            'cost_per_1m': 0.05,
            'triggers': [
                'quantos', 'qual', 'liste', 'mostre',
                'resumo de', 'status de'
            ]
        },
        'medium': {
            'model': 'gpt-5-mini',
            'cost_per_1m': 0.25,
            'triggers': [
                'analise', 'compare', 'priorize',
                'sugira', 'recomende', 'identifique'
            ]
        },
        'complex': {
            'model': 'gpt-5.1',
            'cost_per_1m': 1.25,
            'triggers': [
                'simule', 'preveja', 'otimize',
                'estratégia', 'cenário', 'impacto de'
            ]
        }
    }
    
    def route(self, query: str, context_size: int) -> str:
        """
        Retorna modelo ideal baseado em:
        1. Palavras-chave na query
        2. Tamanho do contexto necessário
        3. Histórico de escalações
        """
        query_lower = query.lower()
        
        # Contexto muito grande = modelo maior
        if context_size > 10000:
            return 'gpt-5.1'
        
        # Palavras-chave de alta complexidade
        for trigger in self.COMPLEXITY_RULES['complex']['triggers']:
            if trigger in query_lower:
                return 'gpt-5.1'
        
        # Palavras-chave de média complexidade
        for trigger in self.COMPLEXITY_RULES['medium']['triggers']:
            if trigger in query_lower:
                return 'gpt-5-mini'
        
        # Padrão: modelo mais barato
        return 'gpt-5-nano'
```

**Estrutura:**

```
ai-service/
├── app/
│   ├── main.py
│   ├── routers/
│   │   ├── consultant.py        # Chat principal
│   │   ├── suggestions.py       # Sugestões automáticas
│   │   └── analysis.py          # Análises 80/20
│   ├── services/
│   │   ├── openai_service.py    # Cliente OpenAI
│   │   ├── model_router.py      # ← CASCATEAMENTO
│   │   ├── embedding_service.py
│   │   └── rag_service.py
│   ├── models/
│   └── utils/
├── requirements.txt
└── Dockerfile
```

## 2.4 Banco de Dados

### PostgreSQL 16 (Principal)

**Schema principal:**

```sql
-- Multi-tenancy
organizations
organization_members
subscriptions

-- Core
users
objectives (SMART + OKRs)
tasks
processes (BPM/BPMN)
risks
documents

-- Analytics
metrics
dashboards
reports

-- Audit/Logs
audit_logs
activity_logs

-- AI/Embeddings
embeddings (pgvector)
ai_conversations
```

**Extensões utilizadas:**
- `pgvector` - Busca semântica
- `uuid-ossp` - UUIDs
- `pg_trgm` - Busca fuzzy
- `btree_gin` - Índices JSONB

### Redis 7+ (Cache & Queue)

**Uso:**

```typescript
// Cache
"cache:user:{userId}" → User data (TTL: 1h)
"cache:org:{orgId}" → Organization data (TTL: 1h)
"cache:objectives:{orgId}" → Lista de objetivos (TTL: 5min)

// Sessions
"session:{sessionId}" → Session data (TTL: 24h)

// Rate Limiting
"rate:{userId}:{action}" → Counter (TTL: 1min)

// Queue (BullMQ)
"queue:emails" → Fila de emails
"queue:notifications" → Fila de notificações
"queue:ai-processing" → Fila de processamento IA
```

---

# 3. ESTRUTURA DE CÓDIGO

## 3.1 Padrões de Código

### Backend (NestJS)

**Módulo típico:**

```typescript
// objectives.controller.ts
@Controller('objectives')
@UseGuards(JwtAuthGuard, OrganizationGuard)
export class ObjectivesController {
  constructor(private readonly objectivesService: ObjectivesService) {}

  @Get()
  async findAll(@CurrentUser() user: User, @CurrentOrg() org: Organization) {
    return this.objectivesService.findAll(org.id);
  }

  @Post()
  async create(
    @Body() dto: CreateObjectiveDto,
    @CurrentUser() user: User,
    @CurrentOrg() org: Organization,
  ) {
    return this.objectivesService.create(dto, org.id, user.id);
  }
}

// objectives.service.ts
@Injectable()
export class ObjectivesService {
  constructor(
    private readonly prisma: PrismaService,
    private readonly cacheService: CacheService,
    private readonly auditService: AuditService,
  ) {}

  async findAll(organizationId: string) {
    const cacheKey = `objectives:${organizationId}`;
    
    // Tenta cache
    const cached = await this.cacheService.get(cacheKey);
    if (cached) return cached;

    // Busca no banco
    const objectives = await this.prisma.objective.findMany({
      where: { organizationId },
      include: { metrics: true },
    });

    // Salva no cache
    await this.cacheService.set(cacheKey, objectives, 300); // 5min
    
    return objectives;
  }

  async create(dto: CreateObjectiveDto, orgId: string, userId: string) {
    const objective = await this.prisma.objective.create({
      data: {
        ...dto,
        organizationId: orgId,
        createdById: userId,
      },
    });

    // Invalida cache
    await this.cacheService.del(`objectives:${orgId}`);

    // Registra auditoria
    await this.auditService.log({
      action: 'objective.created',
      userId,
      organizationId: orgId,
      resourceId: objective.id,
    });

    // TODO: Trigger IA para sugestões

    return objective;
  }
}
```

### Frontend (Next.js)

**Server Component (default):**

```typescript
// app/(dashboard)/objectives/page.tsx
import { getServerSession } from 'next-auth';
import { ObjectivesList } from '@/components/modules/objectives/ObjectivesList';
import { api } from '@/lib/api/server';

export default async function ObjectivesPage() {
  const session = await getServerSession();
  const objectives = await api.objectives.list();

  return (
    <div>
      <h1>Objetivos SMART</h1>
      <ObjectivesList initialData={objectives} />
    </div>
  );
}
```

**Client Component (interativo):**

```typescript
// components/modules/objectives/ObjectivesList.tsx
'use client';

import { useQuery, useMutation } from '@tanstack/react-query';
import { api } from '@/lib/api/client';
import { useOrganization } from '@/hooks/useOrganization';

export function ObjectivesList({ initialData }) {
  const { organization } = useOrganization();
  
  const { data: objectives } = useQuery({
    queryKey: ['objectives', organization.id],
    queryFn: () => api.objectives.list(),
    initialData,
  });

  const createMutation = useMutation({
    mutationFn: api.objectives.create,
    onSuccess: () => {
      queryClient.invalidateQueries(['objectives']);
    },
  });

  return (
    <div>
      {objectives.map(obj => (
        <ObjectiveCard key={obj.id} objective={obj} />
      ))}
    </div>
  );
}
```

## 3.2 Multi-Tenancy Pattern

**Modelo:** Organization-based

```typescript
// Todas as queries incluem organizationId
const tasks = await prisma.task.findMany({
  where: {
    organizationId: currentOrg.id, // ← SEMPRE
  },
});

// Guard customizado
@Injectable()
export class OrganizationGuard implements CanActivate {
  canActivate(context: ExecutionContext) {
    const request = context.switchToHttp().getRequest();
    const user = request.user;
    const orgId = request.headers['x-organization-id'];

    // Valida se usuário pertence à organização
    const membership = await this.prisma.organizationMember.findFirst({
      where: {
        userId: user.id,
        organizationId: orgId,
      },
    });

    if (!membership) throw new ForbiddenException();

    request.organization = membership.organization;
    return true;
  }
}
```

---

# 4. INFRAESTRUTURA

## 4.0 Provedor e Plano

### Hostinger VPS KVM 2

**Escolha:** [Hostinger VPS KVM 2](https://www.hostinger.com/br/servidor-vps)

**Especificações:**
```
Plano: KVM 2
├─ vCPU: 2 núcleos (AMD EPYC)
├─ RAM: 8 GB
├─ Disco: 100 GB NVMe SSD
├─ Banda: 8 TB/mês
├─ Rede: 1 Gbps
└─ Backups: Semanais grátis

Custo:
├─ Promocional: R$ 32,99/mês
├─ Renovação: R$ 69,99/mês (2 anos)
└─ Economia vs AWS/GCP: ~95%
```

**Por que Hostinger KVM 2?**

✅ **Custo-benefício excelente** - R$ 766/ano vs R$ 18k/ano (AWS)  
✅ **2 vCPUs** - Suficiente para frontend + backend  
✅ **8 GB RAM** - Comporta PostgreSQL + Redis + Apps  
✅ **NVMe SSD** - Performance superior  
✅ **Backups inclusos** - Semanais automáticos  
✅ **Fácil escalar** - Upgrade para KVM 4 quando necessário  

**Capacidade:**
- ✅ MVP: Até 500 organizações
- ✅ Crescimento: Até 1.000 organizações
- ✅ Usuários: Até 5.000 ativos
- ⚠️ Upgrade KVM 4: Acima de 1.000 orgs

### Distribuição de Recursos (8 GB RAM + 4 GB Swap)

```
Memória Total: 12 GB (8 GB RAM física + 4 GB Swap)

Alocação:
├─ Frontend (Next.js):     1.5 GB (limite: 1.5 GB)
├─ Backend (NestJS):       2.0 GB (limite: 2.0 GB)
├─ PostgreSQL 16:          2.0 GB (limite: 2.5 GB)
├─ Redis 7:                512 MB (limite: 512 MB)
├─ AI Service (Python):    1.0 GB (limite: 1.5 GB)
├─ NGINX:                  256 MB
├─ Docker/Sistema:         1.0 GB
└─ Swap (reserva):         4.0 GB

CPU (2 vCPUs):
├─ Frontend:    0.5 core
├─ Backend:     0.8 core
├─ PostgreSQL:  0.5 core
├─ Redis:       0.1 core
└─ AI Service:  0.1 core (escalável)
```

---

## 4.1 Docker Setup

**docker-compose.yml (otimizado para Hostinger KVM 2):**

```yaml
version: '3.9'

services:
  # Frontend
  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
    environment:
      - NEXT_PUBLIC_API_URL=http://backend:4000
      - NEXTAUTH_URL=http://localhost:3000
      - NEXTAUTH_SECRET=${NEXTAUTH_SECRET}
    depends_on:
      - backend
    networks:
      - smartwork-network
    deploy:
      resources:
        limits:
          cpus: '0.5'
          memory: 1536M
        reservations:
          memory: 1024M
    restart: unless-stopped

  # Backend
  backend:
    build: ./backend
    ports:
      - "4000:4000"
    environment:
      - DATABASE_URL=postgresql://postgres:postgres@postgres:5432/smartwork
      - REDIS_URL=redis://redis:6379
      - JWT_SECRET=${JWT_SECRET}
      - STRIPE_SECRET_KEY=${STRIPE_SECRET_KEY}
      - OPENAI_API_KEY=${OPENAI_API_KEY}
    depends_on:
      - postgres
      - redis
    networks:
      - smartwork-network
    deploy:
      resources:
        limits:
          cpus: '0.8'
          memory: 2048M
        reservations:
          memory: 1536M
    restart: unless-stopped

  # AI Service
  ai-service:
    build: ./ai-service
    ports:
      - "5000:5000"
    environment:
      - OPENAI_API_KEY=${OPENAI_API_KEY}
      - DATABASE_URL=postgresql://postgres:postgres@postgres:5432/smartwork
    depends_on:
      - postgres
    networks:
      - smartwork-network
    deploy:
      resources:
        limits:
          cpus: '0.1'
          memory: 1536M
        reservations:
          memory: 1024M
    restart: unless-stopped

  # PostgreSQL
  postgres:
    image: pgvector/pgvector:pg16
    ports:
      - "5432:5432"
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
      - POSTGRES_DB=smartwork
    volumes:
      - postgres-data:/var/lib/postgresql/data
    networks:
      - smartwork-network
    deploy:
      resources:
        limits:
          cpus: '0.5'
          memory: 2560M
        reservations:
          memory: 2048M
    restart: unless-stopped
    command:
      - "postgres"
      - "-c"
      - "shared_buffers=512MB"
      - "-c"
      - "effective_cache_size=1536MB"
      - "-c"
      - "maintenance_work_mem=128MB"
      - "-c"
      - "max_connections=100"

  # Redis
  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"
    volumes:
      - redis-data:/data
    networks:
      - smartwork-network
    deploy:
      resources:
        limits:
          cpus: '0.1'
          memory: 512M
        reservations:
          memory: 256M
    restart: unless-stopped
    command: redis-server --maxmemory 400mb --maxmemory-policy allkeys-lru

  # NGINX (Reverse Proxy)
  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf
      - ./nginx/ssl:/etc/nginx/ssl
    depends_on:
      - frontend
      - backend
    networks:
      - smartwork-network
    deploy:
      resources:
        limits:
          memory: 256M
    restart: unless-stopped

volumes:
  postgres-data:
  redis-data:

networks:
  smartwork-network:
    driver: bridge
```

**Observações importantes:**

1. **Limites de recursos** definidos para prevenir overconsumption
2. **PostgreSQL otimizado** para 2 GB RAM (shared_buffers, etc)
3. **Redis com LRU** para gerenciar memória automaticamente
4. **Restart policies** para alta disponibilidade

## 4.2 NGINX Configuration

```nginx
# nginx/nginx.conf
upstream frontend {
    server frontend:3000;
}

upstream backend {
    server backend:4000;
}

server {
    listen 80;
    server_name smartworkbusiness.com.br www.smartworkbusiness.com.br;

    # Redirect to HTTPS
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl http2;
    server_name smartworkbusiness.com.br www.smartworkbusiness.com.br;

    # SSL
    ssl_certificate /etc/nginx/ssl/cert.pem;
    ssl_certificate_key /etc/nginx/ssl/key.pem;
    ssl_protocols TLSv1.2 TLSv1.3;

    # Frontend
    location / {
        proxy_pass http://frontend;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }

    # Backend API
    location /api/ {
        proxy_pass http://backend/;
        proxy_http_version 1.1;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    # Rate Limiting
    limit_req_zone $binary_remote_addr zone=api_limit:10m rate=10r/s;
    limit_req zone=api_limit burst=20 nodelay;
}
```

## 4.3 Ubuntu Server 24.04 Setup (Hostinger KVM 2)

### Passo 1: Configuração Inicial

```bash
# 1. Atualizar sistema
sudo apt update && sudo apt upgrade -y

# 2. Configurar hostname
sudo hostnamectl set-hostname smartwork-prod

# 3. Configurar timezone
sudo timedatectl set-timezone America/Sao_Paulo

# 4. Criar usuário deploy (segurança)
sudo adduser deploy
sudo usermod -aG sudo deploy
```

### Passo 2: Criar Swap de 4GB

```bash
# Criar arquivo swap de 4GB
sudo fallocate -l 4G /swapfile

# Definir permissões corretas
sudo chmod 600 /swapfile

# Formatar como swap
sudo mkswap /swapfile

# Ativar swap
sudo swapon /swapfile

# Verificar
sudo swapon --show
free -h

# Tornar permanente (persiste após reboot)
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab

# Configurar swappiness (usar swap só quando necessário)
# 10 = usa RAM primeiro, swap só em emergência
sudo sysctl vm.swappiness=10
echo 'vm.swappiness=10' | sudo tee -a /etc/sysctl.conf

# Configurar cache pressure
sudo sysctl vm.vfs_cache_pressure=50
echo 'vm.vfs_cache_pressure=50' | sudo tee -a /etc/sysctl.conf
```

**Por que 4GB de Swap?**
- ✅ Evita OOM (Out of Memory) em picos de uso
- ✅ PostgreSQL pode crescer sem matar o processo
- ✅ Margem de segurança para AI Service
- ✅ Total disponível: 8 GB RAM + 4 GB Swap = 12 GB

### Passo 3: Instalar Docker

```bash
# Instalar Docker
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

# Adicionar usuário ao grupo docker
sudo usermod -aG docker $USER
sudo usermod -aG docker deploy

# Habilitar Docker no boot
sudo systemctl enable docker
sudo systemctl start docker

# Verificar
docker --version
```

### Passo 4: Instalar Docker Compose

```bash
# Instalar Docker Compose
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

# Verificar
docker-compose --version
```

### Passo 5: Instalar Node.js 20 LTS

```bash
# Adicionar repositório NodeSource
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -

# Instalar Node.js
sudo apt install -y nodejs

# Verificar
node --version
npm --version
```

### Passo 6: Configurar Firewall (UFW)

```bash
# Instalar UFW (se não estiver instalado)
sudo apt install ufw -y

# Configurar regras
sudo ufw default deny incoming
sudo ufw default allow outgoing

# Permitir SSH (importante!)
sudo ufw allow 22/tcp

# Permitir HTTP e HTTPS
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

# Habilitar firewall
sudo ufw enable

# Verificar status
sudo ufw status verbose
```

### Passo 7: Instalar e Configurar NGINX

```bash
# Instalar NGINX
sudo apt install nginx -y

# Habilitar no boot
sudo systemctl enable nginx
sudo systemctl start nginx

# Verificar
sudo systemctl status nginx
```

### Passo 8: SSL com Let's Encrypt

```bash
# Instalar Certbot
sudo apt install certbot python3-certbot-nginx -y

# Obter certificado (substitua pelo seu domínio)
sudo certbot --nginx -d smartworkbusiness.com.br -d www.smartworkbusiness.com.br

# Renovação automática (certbot cria cron automaticamente)
sudo certbot renew --dry-run

# Verificar
sudo systemctl status certbot.timer
```

### Passo 9: Monitoramento de Recursos

```bash
# Instalar htop (monitor interativo)
sudo apt install htop -y

# Instalar iotop (monitor I/O)
sudo apt install iotop -y

# Script de monitoramento simples
cat > ~/monitor.sh << 'EOF'
#!/bin/bash
echo "=== CPU & Memory ==="
top -bn1 | head -20
echo ""
echo "=== Disk Usage ==="
df -h
echo ""
echo "=== Swap Usage ==="
free -h
echo ""
echo "=== Docker Containers ==="
docker stats --no-stream
EOF

chmod +x ~/monitor.sh
```

### Passo 10: Configurar Logs e Rotação

```bash
# Configurar logrotate para Docker
sudo tee /etc/logrotate.d/docker-containers << 'EOF'
/var/lib/docker/containers/*/*.log {
  rotate 7
  daily
  compress
  missingok
  delaycompress
  copytruncate
  maxsize 100M
}
EOF

# Testar
sudo logrotate -f /etc/logrotate.d/docker-containers
```

---

# 5. SEGURANÇA E COMPLIANCE

## 5.1 Autenticação e Autorização

### JWT Token Structure

```typescript
{
  sub: string;           // user.id
  email: string;
  organizationId: string;
  role: 'OWNER' | 'ADMIN' | 'MEMBER' | 'VIEWER';
  iat: number;           // issued at
  exp: number;           // expires in 24h
}
```

### Roles & Permissions (RBAC)

```typescript
enum Role {
  OWNER = 'OWNER',         // Pode tudo
  ADMIN = 'ADMIN',         // Gerencia usuários, configs
  MEMBER = 'MEMBER',       // Usa a plataforma
  VIEWER = 'VIEWER',       // Apenas visualiza
}

// Matriz de permissões
const permissions = {
  'objective.create': ['OWNER', 'ADMIN', 'MEMBER'],
  'objective.edit': ['OWNER', 'ADMIN', 'MEMBER'],
  'objective.delete': ['OWNER', 'ADMIN'],
  'user.invite': ['OWNER', 'ADMIN'],
  'user.remove': ['OWNER'],
  'billing.manage': ['OWNER'],
};
```

## 5.2 Proteção de Dados (LGPD)

### Dados Sensíveis

```typescript
// Identificados no schema Prisma
model User {
  id        String   @id @default(uuid())
  email     String   @unique  // ← Dado pessoal
  name      String              // ← Dado pessoal
  cpf       String?  @unique    // ← Dado sensível
  phone     String?             // ← Dado pessoal
  password  String              // ← Hash (bcrypt)
  
  // Auditoria LGPD
  dataConsentAt DateTime?
  dataExportedAt DateTime?
  dataDeletedAt DateTime?
  
  @@index([email])
}
```

### Funcionalidades LGPD

✅ **Consentimento**: Checkbox no cadastro  
✅ **Portabilidade**: Exportar dados (JSON/CSV)  
✅ **Esquecimento**: Anonimizar ou deletar  
✅ **Acesso**: Usuário vê seus dados  
✅ **Logs**: Quem acessou dados sensíveis  

## 5.3 Audit Logs

**Tudo é logado:**

```typescript
model AuditLog {
  id        String   @id @default(uuid())
  
  // O quê
  action    String   // "objective.created", "user.deleted"
  resource  String   // "Objective", "User"
  resourceId String
  changes   Json?    // { before: {...}, after: {...} }
  
  // Quem
  userId    String
  user      User     @relation(fields: [userId], references: [id])
  
  // Onde/Quando
  organizationId String
  ipAddress      String
  userAgent      String
  createdAt      DateTime @default(now())
  
  @@index([organizationId, createdAt])
  @@index([userId])
}
```

## 5.4 Rate Limiting

```typescript
// Backend (NestJS)
@UseGuards(ThrottlerGuard)
@Throttle(10, 60) // 10 req/min
@Controller('ai')
export class AIController {
  @Post('ask')
  async ask(@Body() dto: AskDto) {
    // Limite adicional por plano
    const usage = await this.checkPlanLimit(dto.organizationId);
    if (usage.dailyQuestions >= usage.limit) {
      throw new ForbiddenException('Daily AI limit reached');
    }
    
    return this.aiService.ask(dto);
  }
}
```

**Por Plano:**

| Plano | Perguntas IA/dia | API Calls/min |
|-------|------------------|---------------|
| Starter | 20 | 10 |
| Professional | 100 | 30 |
| Business | 500 | 60 |
| Enterprise | Ilimitado | 120 |

---

# 6. DECISÕES TÉCNICAS

## 6.1 Por que Next.js 14?

✅ **Server Components**: Menos JavaScript no cliente  
✅ **App Router**: Roteamento moderno  
✅ **Streaming SSR**: Carregamento progressivo  
✅ **API Routes**: Backend leve para coisas simples  
✅ **Otimizações**: Imagens, fonts, bundle automático  
✅ **TypeScript nativo**: Sem configuração  

## 6.2 Por que NestJS?

✅ **Arquitetura escalável**: Módulos, DI, Guards  
✅ **TypeScript nativo**: Type-safe  
✅ **Ecossistema maduro**: Passport, Prisma, etc  
✅ **Documentação**: Swagger automático  
✅ **Testável**: Jest integrado  
✅ **Express/Fastify**: Pode trocar  

## 6.3 Por que Prisma?

✅ **Type-safe**: Auto-complete e erros em tempo de compilação  
✅ **Migrations**: Versionamento de schema  
✅ **Studio**: Interface visual do banco  
✅ **Multi-database**: Fácil trocar depois  
✅ **Performance**: Queries otimizadas  

## 6.4 Por que PostgreSQL (não MongoDB)?

✅ **Relações complexas**: Org → Users → Objectives → Tasks  
✅ **ACID**: Transações seguras  
✅ **JSONB**: Flexibilidade quando necessário  
✅ **pgvector**: Embeddings para IA  
✅ **Maduro**: 30+ anos de desenvolvimento  

## 6.5 Por que Docker?

✅ **Consistência**: Dev = Staging = Prod  
✅ **Isolamento**: Cada serviço independente  
✅ **Fácil deploy**: `docker-compose up`  
✅ **Escalável**: Kubernetes depois  
✅ **Rollback**: Versões antigas disponíveis  

## 6.6 Por que Monolito Modular (não Microserviços)?

✅ **Simplicidade**: 1 repo, 1 deploy  
✅ **Velocidade**: Menos overhead de rede  
✅ **Debugging**: Mais fácil rastrear bugs  
✅ **Transações**: Sem distributed transactions  
✅ **Custo**: Menos infraestrutura  

**Quando migrar?**
- 10k+ organizações
- Módulos específicos com carga muito alta
- Equipe 20+ devs

---

## RESUMO

### Stack Final

| Camada | Tecnologia | Por quê |
|--------|------------|---------|
| **Frontend** | Next.js 14 + TypeScript | SSR, SEO, Performance |
| **Backend** | NestJS + Prisma | Escalável, Type-safe |
| **AI** | Python + FastAPI | Melhor para ML/AI |
| **Database** | PostgreSQL 16 | Relacional, JSONB, pgvector |
| **Cache** | Redis 7 | Rápido, Queue, Pub/Sub |
| **Infra** | Ubuntu + Docker | Consistente, Isolado |
| **Proxy** | NGINX | SSL, Load Balance |
| **Deploy** | Docker Compose | Simples, Replicável |

### Princípios

1. **Type-Safety**: TypeScript em todo frontend/backend
2. **Multi-Tenancy**: Isolamento total entre organizações
3. **Auditoria**: Tudo logado (compliance)
4. **Cache-First**: Redis para performance
5. **Modular**: Fácil adicionar/remover módulos
6. **Testável**: TDD desde o início
7. **Seguro**: HTTPS, JWT, RBAC, Rate Limiting

---

**Próximo:** [Documento 4 - Dependências e Configurações](./04-DEPENDENCIAS-CONFIGURACOES.md)


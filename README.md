# Sistema de Gerenciamento Escolar Infantil

Sistema web desenvolvido como trabalho acadêmico da UniFAAT-ADS para gerenciamento de escola infantil.

## Objetivo da Etapa

Implementação do front-end em React + TypeScript consumindo a API REST desenvolvida no semestre anterior. Esta etapa implementa:
- Views completas de CRUD para duas entidades (Alunos e Professores)
- Comunicação em tempo real via WebSocket com custom hook
- Build e pré-compilação com Vite
- Renderização server-side com views EJS

## Tecnologias

**Backend:** Node.js, Express, PostgreSQL, Sequelize, Socket.IO, EJS  
**Frontend:** React 18, TypeScript, Vite, React Router, Axios, Socket.IO Client  
**DevOps:** Docker, Docker Compose, Nginx

## Como Executar

### Opção 1: Com Docker (Recomendado)
```bash
docker-compose up --build
```

### Opção 2: Sem Docker
```bash
# Terminal 1 - Backend
cd APP
npm install
npm start

# Terminal 2 - Frontend
cd FRONTEND
npm install
npm run dev
```

## URLs de Acesso

- **Frontend React:** http://localhost:5173
- **Backend API:** http://localhost:3000/api
- **View EJS Alunos:** http://localhost:3000/view/alunos
- **View EJS Professores:** http://localhost:3000/view/professores

## Build de Produção (Vite)

```bash
cd FRONTEND
npm run build    # Gera build otimizado na pasta dist/
npm run preview  # Preview do build de produção
```

O Vite realiza:
- Tree-shaking e minificação de código
- Code splitting automático
- Otimização de assets (imagens, CSS)
- Build extremamente rápido usando Rollup

## Entidades do CRUD

### 1. Alunos
**Endpoint:** `/api/alunos`  
**Campos:** nome, data_nascimento, genero, endereco, telefone_contato, nome_responsavel, cpf_responsavel, email_responsavel

**Operações:**
- `GET /api/alunos` - Lista todos
- `POST /api/alunos` - Cria novo
- `PUT /api/alunos/:id` - Atualiza
- `DELETE /api/alunos/:id` - Remove

### 2. Professores
**Endpoint:** `/api/professores`  
**Campos:** nome, cpf, data_nascimento, genero, endereco, telefone, email, formacao_academica

**Operações:**
- `GET /api/professores` - Lista todos
- `POST /api/professores` - Cria novo
- `PUT /api/professores/:id` - Atualiza
- `DELETE /api/professores/:id` - Remove

## WebSocket + Custom Hook

### Implementação
O projeto usa Socket.IO para comunicação bidirecional em tempo real entre cliente e servidor.

**Custom Hook:** `FRONTEND/src/hooks/useWebSocket.ts`

```typescript
const { isConnected, emit, on, off } = useWebSocket();
```

### Eventos em Tempo Real

**Alunos:**
- `aluno:created` - Notifica criação
- `aluno:updated` - Notifica atualização
- `aluno:deleted` - Notifica exclusão

**Professores:**
- `professor:created` - Notifica criação
- `professor:updated` - Notifica atualização
- `professor:deleted` - Notifica exclusão

### Funcionamento
Quando um usuário realiza uma operação CRUD, o servidor emite um evento WebSocket que todos os clientes conectados recebem instantaneamente, atualizando suas interfaces sem necessidade de reload ou polling.

## Estrutura do Projeto

```
APP/                      # Backend Node.js
├── controllers/          # Lógica de negócio
├── models/              # Models Sequelize
├── routes/              # Rotas REST API
├── views/               # Templates EJS
│   ├── alunos.ejs
│   └── professores.ejs
├── config/              # Configuração do banco
└── index.js             # Entry point + Socket.IO

FRONTEND/                # Frontend React
├── src/
│   ├── hooks/           # Custom hooks
│   │   └── useWebSocket.ts
│   ├── pages/           # Páginas do CRUD
│   │   ├── AlunosPage.tsx
│   │   └── ProfessoresPage.tsx
│   ├── services/        # API client (Axios)
│   │   └── api.ts
│   ├── types/           # Interfaces TypeScript
│   │   └── index.ts
│   ├── styles/          # CSS dos componentes
│   └── App.tsx          # Router e navegação
├── vite.config.ts       # Configuração Vite
└── tsconfig.json        # Configuração TypeScript

docker-compose.yml       # Orquestração dos containers
Dockerfile.app           # Container do backend
Dockerfile.frontend      # Container do frontend
nginx.conf              # Proxy reverso
```

## Exemplos de Uso da API

### Criar Aluno
```bash
curl -X POST http://localhost:3000/api/alunos \
  -H "Content-Type: application/json" \
  -d '{
    "nome": "João Silva",
    "data_nascimento": "2018-05-15",
    "genero": "M",
    "endereco": "Rua A, 123",
    "telefone_contato": "11999999999",
    "nome_responsavel": "Maria Silva",
    "cpf_responsavel": "12345678900",
    "email_responsavel": "maria@email.com"
  }'
```

### Listar Professores
```bash
curl http://localhost:3000/api/professores
```

### Atualizar Professor
```bash
curl -X PUT http://localhost:3000/api/professores/1 \
  -H "Content-Type: application/json" \
  -d '{"telefone": "11988888888"}'
```

### Deletar Aluno
```bash
curl -X DELETE http://localhost:3000/api/alunos/1
```

## Uso de TypeScript

Todo o frontend utiliza TypeScript com tipagem estrita configurada no `tsconfig.json`. As principais interfaces estão em `FRONTEND/src/types/index.ts`:

```typescript
interface Aluno {
  id?: number;
  nome: string;
  data_nascimento: string;
  genero: 'M' | 'F' | 'Outro';
  endereco: string;
  telefone_contato: string;
  nome_responsavel: string;
  cpf_responsavel: string;
  email_responsavel: string;
}

interface Professor {
  id?: number;
  nome: string;
  cpf: string;
  data_nascimento: string;
  genero: 'M' | 'F' | 'Outro';
  endereco: string;
  telefone: string;
  email: string;
  formacao_academica: string;
}
```

## Views EJS (Server-Side Rendering)

O backend também implementa views renderizadas no servidor usando EJS:

- `APP/views/alunos.ejs` - View server-side de alunos
- `APP/views/professores.ejs` - View server-side de professores

Acesse via:
- http://localhost:3000/view/alunos
- http://localhost:3000/view/professores

## Equipe

- Luiz Felipe S. de Souza (6324548)
- Leonardo Frazão Sano (6324073)
- Natan Borges Leme (6324696)
- Vitor Pinheiro Guimarães (6324680)

**UniFAAT-ADS - 2025**

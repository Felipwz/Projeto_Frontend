# Sistema de Gerenciamento Escolar Infantil

Sistema web para gerenciamento de escola infantil desenvolvido como trabalho acadêmico da UniFAAT-ADS.

## Tecnologias

**Backend:**
- Node.js + Express
- PostgreSQL
- Socket.IO (WebSocket)
- EJS (Views)
- Docker

**Frontend:**
- React 18 + TypeScript
- Vite
- React Router
- Axios
- Socket.IO Client

## Como Executar

### Com Docker:
`ash
docker-compose up --build
`

### Sem Docker:

**Backend:**
`ash
cd APP
npm install
npm start
`

**Frontend:**
`ash
cd FRONTEND
npm install
npm run dev
`

## Acessar

- Frontend: http://localhost:5173
- Backend API: http://localhost:3000/api
- Views EJS: http://localhost:3000/view/alunos

## Funcionalidades

- CRUD de Alunos
- CRUD de Professores
- Atualização em tempo real (WebSocket)
- Views server-side com EJS

## Estrutura do Projeto

`
APP/              # Backend Node.js
 config/       # Configuração do banco
 controllers/  # Lógica de negócio
 models/       # Models Sequelize
 routes/       # Rotas da API
 views/        # Templates EJS

FRONTEND/         # Frontend React
 src/
    hooks/    # Custom hooks (useWebSocket)
    pages/    # Páginas (Alunos, Professores)
    services/ # API (axios)
    types/    # Tipos TypeScript
 vite.config.ts
`

## Autor

Grupo: Luiz Felipe Siqueira de souza (6324548); Leonardo Frazão Sano(6324073); Natan Borges Leme(6324696), Vitor Pinheiro Guimarães(6324680)

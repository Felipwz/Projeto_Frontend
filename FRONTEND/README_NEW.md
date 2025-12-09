# Frontend - Sistema de Gerenciamento Escolar

Interface React + TypeScript desenvolvida com Vite para gerenciamento de alunos e professores.

## Tecnologias

- React 18 + TypeScript
- Vite (build tool)
- Socket.IO Client (WebSocket)
- Axios (cliente HTTP)
- React Router (navegação)

## Estrutura

```
src/
├── hooks/           # Custom hooks (useWebSocket)
├── pages/           # Páginas principais
│   ├── AlunosPage.tsx
│   └── ProfessoresPage.tsx
├── services/        # Configuração API (api.ts)
├── types/           # Interfaces TypeScript
├── styles/          # Arquivos CSS
├── App.tsx          # Componente raiz
└── main.tsx         # Entry point
```

## Instalação

```bash
npm install
npm run dev       # Desenvolvimento
npm run build     # Build de produção
npm run preview   # Preview do build
```

## Custom Hook useWebSocket

O hook `useWebSocket` gerencia toda a comunicação WebSocket:

```typescript
import { useWebSocket } from './hooks/useWebSocket';

const { isConnected, emit, on, off } = useWebSocket();

// Ouvir eventos
useEffect(() => {
  on('aluno:created', (data) => {
    console.log('Novo aluno:', data);
  });
  
  return () => off('aluno:created');
}, [on, off]);

// Emitir eventos
emit('custom:event', { data: 'example' });
```

## Páginas Implementadas

### AlunosPage
CRUD completo para alunos com:
- Listagem em tabela
- Formulário de criação/edição
- Validação de campos
- Exclusão com confirmação
- Atualização em tempo real via WebSocket

### ProfessoresPage
CRUD completo para professores com:
- Listagem em tabela
- Formulário de criação/edição
- Campos específicos (CPF, formação acadêmica)
- Status do contrato
- Atualização em tempo real via WebSocket

## Interfaces TypeScript

```typescript
interface Aluno {
  id_aluno?: number;
  nome: string;
  data_nascimento: string;
  genero: string;
  endereco: string;
  telefone_contato: string;
  nome_responsavel: string;
  cpf_responsavel: string;
  email_responsavel: string;
}

interface Professor {
  id_professor?: number;
  nome: string;
  cpf: string;
  data_nascimento: string;
  genero: string;
  endereco: string;
  telefone: string;
  email: string;
  formacao_academica: string;
}
```

## Configuração

Crie um arquivo `.env`:

```env
VITE_API_URL=http://localhost:3000/api
VITE_SOCKET_URL=http://localhost:3000
```

## Dependências Principais

```json
{
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-router-dom": "^6.20.0",
    "socket.io-client": "^4.7.2",
    "axios": "^1.6.2"
  }
}
```

## Equipe

- Luiz Felipe S. de Souza (6324548)
- Leonardo Frazão Sano (6324073)
- Natan Borges Leme (6324696)
- Vitor Pinheiro Guimarães (6324680)

**UniFAAT-ADS - 2025**

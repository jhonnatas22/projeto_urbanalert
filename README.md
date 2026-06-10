#  UrbanAlert — Sistema de Registro de Ocorrências Urbanas

Sistema web para registro, acompanhamento e gestão de ocorrências urbanas (denúncias), desenvolvido como projeto acadêmico.

---

##  Funcionalidades

- **Autenticação** — Cadastro, login e logout com JWT
- **Três perfis** — Cidadão, Fiscal Municipal e Administrador
- **CRUD de Ocorrências** — Criar, listar, editar, remover com filtros e paginação
- **CRUD de Categorias** — Gerenciar categorias (admin)
- **Comentários** — Discussão em cada ocorrência
- **Histórico** — Rastreio de todas as alterações
- **Notificações** — Alertas automáticos de status e comentários
- **Perfil do usuário** — Edição de dados e senha
- **Dashboard** — Estatísticas e gráficos
- **Mapa de Calor** — Visualização por região (fiscal/admin)
- **Relatórios** — Taxas de resolução e prioridades (admin)

---

##  Estrutura do Projeto

```
urbanalert/
├── backend/
│   ├── src/
│   │   ├── config/
│   │   │   └── database.js          # Conexão PostgreSQL
│   │   ├── controllers/
│   │   │   ├── authController.js    # Login, registro, perfil
│   │   │   ├── ocorrenciasController.js
│   │   │   ├── categoriasController.js
│   │   │   └── usuariosController.js
│   │   ├── middlewares/
│   │   │   └── auth.js              # JWT + controle de roles
│   │   ├── routes/
│   │   │   └── index.js             # Todas as rotas da API
│   │   └── server.js                # Ponto de entrada
│   ├── sql/
│   │   └── schema.sql               # Tabelas + seed do banco
│   ├── .env.example
│   └── package.json
└── frontend/
    ├── css/
    │   └── style.css
    ├── js/
    │   ├── api.js                   # Cliente HTTP (fetch)
    │   └── app.js                   # Lógica do frontend
    └── index.html
```

---

## Banco de Dados — Entidades

| Tabela | Descrição |
|---|---|
| `usuarios` | Usuários do sistema (cidadão, fiscal, admin) |
| `categorias` | Tipos de ocorrência (buraco, iluminação, etc.) |
| `ocorrencias` | Ocorrências registradas |
| `comentarios` | Comentários nas ocorrências |
| `historico_ocorrencias` | Log de alterações |
| `notificacoes` | Alertas para os usuários |

---

##  Como Rodar Localmente

### Pré-requisitos
- [Node.js](https://nodejs.org/) v18+
- [PostgreSQL](https://www.postgresql.org/) v14+

### 1. Clonar o repositório
```bash
git clone https://github.com/seu-usuario/urbanalert.git
cd urbanalert
```

### 2. Configurar o banco de dados
```bash
# Criar o banco
psql -U postgres -c "CREATE DATABASE urbanalert;"

# Criar as tabelas e dados iniciais
psql -U postgres -d urbanalert -f backend/sql/schema.sql
```

### 3. Configurar variáveis de ambiente
```bash
cd backend
cp .env.example .env
# Edite o .env com suas credenciais do PostgreSQL
```

### 4. Instalar dependências e iniciar o backend
```bash
cd backend
npm install
npm run dev
```

O servidor estará rodando em **http://localhost:3001**

### 5. Abrir o frontend
Abra o arquivo `frontend/index.html` no navegador, ou acesse **http://localhost:3001** (o backend serve os arquivos estáticos automaticamente).

---

## 🔌 Endpoints da API

### Auth
| Método | Rota | Descrição |
|---|---|---|
| POST | `/api/auth/register` | Cadastrar usuário |
| POST | `/api/auth/login` | Fazer login |
| GET  | `/api/auth/me` | Perfil atual |
| PUT  | `/api/auth/me` | Atualizar perfil |
| PUT  | `/api/auth/me/senha` | Alterar senha |

### Ocorrências
| Método | Rota | Descrição |
|---|---|---|
| GET    | `/api/ocorrencias` | Listar (paginado + filtros) |
| GET    | `/api/ocorrencias/:id` | Buscar por ID |
| POST   | `/api/ocorrencias` | Criar |
| PUT    | `/api/ocorrencias/:id` | Atualizar |
| DELETE | `/api/ocorrencias/:id` | Remover |
| POST   | `/api/ocorrencias/:id/comentarios` | Comentar |
| GET    | `/api/ocorrencias/dashboard` | Estatísticas |

### Categorias
| Método | Rota | Descrição |
|---|---|---|
| GET    | `/api/categorias` | Listar |
| POST   | `/api/categorias` | Criar (admin) |
| PUT    | `/api/categorias/:id` | Atualizar (admin) |
| DELETE | `/api/categorias/:id` | Remover (admin) |

### Notificações
| Método | Rota | Descrição |
|---|---|---|
| GET | `/api/notificacoes` | Listar minhas notificações |
| PUT | `/api/notificacoes/ler-todas` | Marcar todas lidas |
| PUT | `/api/notificacoes/:id/ler` | Marcar uma lida |

---

##  Perfis de Acesso

| Funcionalidade | Cidadão | Fiscal | Admin |
|---|:---:|:---:|:---:|
| Registrar ocorrência 
| Ver próprias ocorrências 
| Ver todas as ocorrências 
| Atualizar status 
| Gerenciar categorias 
| Gerenciar usuários 
| Ver mapa de calor 
| Ver relatórios 

---

## Tecnologias Utilizadas

| Camada | Tecnologia |
|---|---|
| Frontend | HTML5, CSS3, JavaScript (Vanilla) |
| Backend | Node.js, Express.js |
| Banco de dados | PostgreSQL |
| Autenticação | JWT (jsonwebtoken) + bcrypt |
| Controle de versão | Git + GitHub |

---

##  Integrantes do Grupo

| Nome | GitHub |
|---|---|---|
| Nome 1 | jhonnatas amaro
| Nome 2 | karlos eduardo
| Nome 3 | ywandson berlamino
| Nome 4 | natam
---

##  Licença

Projeto acadêmico — uso educacional.

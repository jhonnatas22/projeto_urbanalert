# 🏙️ UrbanAlert — Sistema de Registro de Ocorrências Urbanas

Sistema web para registro, acompanhamento e gestão de ocorrências urbanas (denúncias), desenvolvido como projeto acadêmico.

---

## 📋 Funcionalidades

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

## 🗂️ Estrutura do Projeto

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

## 🗄️ Banco de Dados — Entidades

| Tabela | Descrição |
|---|---|
| `usuarios` | Usuários do sistema (cidadão, fiscal, admin) |
| `categorias` | Tipos de ocorrência (buraco, iluminação, etc.) |
| `ocorrencias` | Ocorrências registradas |
| `comentarios` | Comentários nas ocorrências |
| `historico_ocorrencias` | Log de alterações |
| `notificacoes` | Alertas para os usuários |

---

## 🚀 Como Rodar Localmente

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

## 👥 Perfis de Acesso

| Funcionalidade | Cidadão | Fiscal | Admin |
|---|:---:|:---:|:---:|
| Registrar ocorrência | ✅ | ✅ | ✅ |
| Ver próprias ocorrências | ✅ | ✅ | ✅ |
| Ver todas as ocorrências | ❌ | ✅ | ✅ |
| Atualizar status | ❌ | ✅ | ✅ |
| Gerenciar categorias | ❌ | ❌ | ✅ |
| Gerenciar usuários | ❌ | ❌ | ✅ |
| Ver mapa de calor | ❌ | ✅ | ✅ |
| Ver relatórios | ❌ | ❌ | ✅ |

---

## 💡 Sugestões de Commits para o Grupo

Cada integrante deve fazer **no mínimo 5 commits relevantes**. Exemplos:

```bash
# Integrante 1 — Backend Auth
git commit -m "feat: implementa rota de registro de usuários com bcrypt"
git commit -m "feat: adiciona middleware de autenticação JWT"
git commit -m "feat: cria endpoint de login com validação"
git commit -m "fix: corrige validação de e-mail duplicado no registro"
git commit -m "feat: implementa alteração de senha com verificação"

# Integrante 2 — Backend Ocorrências
git commit -m "feat: cria controller de ocorrências com paginação"
git commit -m "feat: implementa filtros por status, categoria e busca"
git commit -m "feat: adiciona endpoint de comentários com notificação"
git commit -m "feat: cria dashboard com agregações SQL"
git commit -m "fix: corrige permissão de cidadão ao editar ocorrência"

# Integrante 3 — Banco de Dados
git commit -m "feat: cria schema completo do banco PostgreSQL"
git commit -m "feat: adiciona trigger de updated_at nas tabelas"
git commit -m "feat: cria índices de performance nas FK"
git commit -m "feat: adiciona seed com dados iniciais e categorias"
git commit -m "docs: documenta entidades e relacionamentos no README"

# Integrante 4 — Frontend
git commit -m "feat: implementa tela de login e cadastro"
git commit -m "feat: cria dashboard com cards de estatísticas"
git commit -m "feat: implementa CRUD de ocorrências com filtros"
git commit -m "feat: adiciona paginação na listagem de ocorrências"
git commit -m "feat: implementa modal de detalhes com comentários"
```

---

## 🛠️ Tecnologias Utilizadas

| Camada | Tecnologia |
|---|---|
| Frontend | HTML5, CSS3, JavaScript (Vanilla) |
| Backend | Node.js, Express.js |
| Banco de dados | PostgreSQL |
| Autenticação | JWT (jsonwebtoken) + bcrypt |
| Controle de versão | Git + GitHub |

---

## 👨‍💻 Integrantes do Grupo

| Nome | GitHub | Responsabilidade |
|---|---|---|
| Nome 1 | @usuario1 | Backend - Auth |
| Nome 2 | @usuario2 | Backend - Ocorrências |
| Nome 3 | @usuario3 | Banco de Dados |
| Nome 4 | @usuario4 | Frontend |

---

## 📄 Licença

Projeto acadêmico — uso educacional.

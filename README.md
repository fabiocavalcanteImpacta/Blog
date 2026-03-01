# Blog com Posts e Comentários

Sistema completo de blog desenvolvido com arquitetura full-stack moderna.

## 🏗️ Arquitetura

### Stack Tecnológica

**Frontend:**
- Next.js 14+ (App Router)
- TypeScript
- Tailwind CSS
- Zod (validação)

**Backend:**
- Java 17
- Spring Boot 3.2.2
- Spring Data MongoDB
- Lombok

**Banco de Dados:**
- MongoDB

## 📂 Estrutura do Projeto

```
blog-project/
├── frontend/              # Aplicação Next.js
│   ├── app/              # App Router do Next.js
│   │   ├── posts/        # Páginas de posts
│   │   ├── api/          # API routes (opcional)
│   │   ├── layout.tsx    # Layout principal
│   │   ├── page.tsx      # Página inicial
│   │   └── globals.css   # Estilos globais
│   ├── components/       # Componentes React
│   │   ├── posts/        # Componentes de posts
│   │   └── comments/     # Componentes de comentários
│   ├── lib/             # Bibliotecas e utilitários
│   │   ├── api/         # Chamadas à API
│   │   ├── types/       # TypeScript types
│   │   ├── utils/       # Funções utilitárias
│   │   └── validations/ # Schemas de validação
│   └── public/          # Arquivos estáticos
│
├── backend/             # Aplicação Spring Boot
│   ├── src/main/java/com/blog/
│   │   ├── controller/  # REST Controllers
│   │   ├── service/     # Lógica de negócio
│   │   ├── repository/  # Acesso a dados (MongoDB)
│   │   ├── model/       # Entidades/Documentos
│   │   ├── dto/         # Data Transfer Objects
│   │   │   ├── request/ # DTOs de requisição
│   │   │   └── response/# DTOs de resposta
│   │   ├── exception/   # Exceções customizadas
│   │   ├── config/      # Configurações
│   │   └── util/        # Utilitários
│   └── src/main/resources/
│       └── application.properties
│
└── docs/               # Documentação
```

## 🗄️ Modelo de Dados

### Coleção: Posts

```javascript
{
  _id: ObjectId,
  title: String,        // min: 3, max: 200
  content: String,      // min: 10
  author: String,       // min: 2, max: 100
  slug: String,         // único, indexado
  createdAt: DateTime,
  updatedAt: DateTime
}
```

**Índices:**
- `slug` (unique)
- `createdAt` (para ordenação)

### Coleção: Comments

```javascript
{
  _id: ObjectId,
  postId: String,       // referência ao Post
  author: String,       // min: 2, max: 100
  content: String,      // min: 1, max: 1000
  createdAt: DateTime
}
```

**Índices:**
- `postId` (para busca por post)
- `createdAt` (para ordenação)

## 🔌 API Endpoints

### Posts

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| GET | `/api/posts` | Lista todos os posts (paginado) |
| GET | `/api/posts/{id}` | Busca post por ID |
| GET | `/api/posts/slug/{slug}` | Busca post por slug |
| POST | `/api/posts` | Cria novo post |
| PUT | `/api/posts/{id}` | Atualiza post |
| DELETE | `/api/posts/{id}` | Deleta post |

### Comentários

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| GET | `/api/posts/{postId}/comments` | Lista comentários de um post |
| POST | `/api/posts/{postId}/comments` | Cria novo comentário |
| DELETE | `/api/posts/{postId}/comments/{commentId}` | Deleta comentário |

## 🚀 Como Executar

### Pré-requisitos

- Node.js 18+
- Java 17+
- Maven 3.6+
- MongoDB 6.0+

### 1. Configurar MongoDB

```bash
# Iniciar MongoDB (macOS com Homebrew)
brew services start mongodb-community

# Ou com Docker
docker run -d -p 27017:27017 --name mongodb mongo:latest
```

### 2. Executar Backend

```bash
cd backend
mvn spring-boot:run
```

O backend estará disponível em `http://localhost:8080`

### 3. Executar Frontend

```bash
cd frontend
npm install
npm run dev
```

O frontend estará disponível em `http://localhost:3000`

## 📋 Funcionalidades

### Posts
- ✅ Listar posts com paginação
- ✅ Visualizar post individual
- ✅ Criar novo post
- ✅ Editar post existente
- ✅ Deletar post
- ✅ Geração automática de slug único
- ✅ Contagem de comentários por post

### Comentários
- ✅ Listar comentários de um post
- ✅ Adicionar comentário a um post
- ✅ Deletar comentário
- ✅ Ordenação por data (mais recentes primeiro)

### Validações
- ✅ Validação frontend com Zod
- ✅ Validação backend com Bean Validation
- ✅ Tratamento de erros global
- ✅ Mensagens de erro personalizadas

## 🎨 Design Patterns Utilizados

### Backend
- **Repository Pattern**: Acesso a dados
- **Service Layer**: Lógica de negócio separada
- **DTO Pattern**: Separação entre entidades e dados de transferência
- **Exception Handling**: Tratamento centralizado com @RestControllerAdvice

### Frontend
- **Component-Based Architecture**: Componentes reutilizáveis
- **Server Components**: Para SSR e melhor performance
- **Client Components**: Para interatividade
- **Custom Hooks**: Para lógica reutilizável (se necessário)

## 🔒 Segurança

- CORS configurado para aceitar apenas origens permitidas
- Validação de entrada em todas as camadas
- Sanitização de dados
- Proteção contra NoSQL injection

## 📚 Próximas Melhorias

- [ ] Autenticação e autorização (JWT)
- [ ] Sistema de likes/reactions
- [ ] Upload de imagens
- [ ] Editor de texto rico (Markdown/WYSIWYG)
- [ ] Busca e filtros avançados
- [ ] Tags/categorias para posts
- [ ] Comentários aninhados (respostas)
- [ ] Paginação no frontend
- [ ] Testes unitários e de integração
- [ ] Docker Compose para fácil deployment
- [ ] CI/CD pipeline

## 📝 Licença

MIT

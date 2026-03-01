# Blog Project - Backend

Backend do blog desenvolvido com Spring Boot 3, Java 17 e MongoDB.

## 🚀 Tecnologias

- **Java 17**
- **Spring Boot 3.2.2**
- **Spring Data MongoDB**
- **Spring Validation**
- **Lombok**
- **Maven**

## 📁 Estrutura

```
backend/
└── src/main/java/com/blog/
    ├── BlogApplication.java      # Main class
    ├── config/                   # Configurações
    │   └── CorsConfig.java      # Configuração CORS
    ├── controller/              # REST Controllers
    │   ├── PostController.java
    │   └── CommentController.java
    ├── service/                 # Lógica de negócio
    │   ├── PostService.java
    │   └── CommentService.java
    ├── repository/              # Acesso a dados
    │   ├── PostRepository.java
    │   └── CommentRepository.java
    ├── model/                   # Entidades MongoDB
    │   ├── Post.java
    │   └── Comment.java
    ├── dto/                     # Data Transfer Objects
    │   ├── request/
    │   │   ├── CreatePostRequest.java
    │   │   ├── UpdatePostRequest.java
    │   │   └── CreateCommentRequest.java
    │   └── response/
    │       ├── PostResponse.java
    │       └── CommentResponse.java
    ├── exception/               # Exceções
    │   ├── ResourceNotFoundException.java
    │   ├── DuplicateResourceException.java
    │   ├── ErrorResponse.java
    │   └── GlobalExceptionHandler.java
    └── util/                    # Utilitários
        └── SlugUtil.java
```

## 🛠️ Instalação

### Pré-requisitos
- Java 17+
- Maven 3.6+
- MongoDB 6.0+

### Configurar MongoDB

```bash
# macOS (Homebrew)
brew services start mongodb-community

# Docker
docker run -d -p 27017:27017 --name mongodb mongo:latest
```

### Build do Projeto

```bash
mvn clean install
```

## 🏃 Executar

```bash
mvn spring-boot:run
```

A API estará disponível em: http://localhost:8080

## ⚙️ Configuração

Edite `src/main/resources/application.properties`:

```properties
# MongoDB
spring.data.mongodb.uri=mongodb://localhost:27017/blog
spring.data.mongodb.database=blog

# Server
server.port=8080

# CORS
cors.allowed.origins=http://localhost:3000
```

## 🔌 Endpoints da API

### Posts

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| GET | `/api/posts` | Lista posts (paginado) |
| GET | `/api/posts/{id}` | Busca post por ID |
| GET | `/api/posts/slug/{slug}` | Busca post por slug |
| POST | `/api/posts` | Cria post |
| PUT | `/api/posts/{id}` | Atualiza post |
| DELETE | `/api/posts/{id}` | Deleta post |

### Comentários

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| GET | `/api/posts/{postId}/comments` | Lista comentários |
| POST | `/api/posts/{postId}/comments` | Cria comentário |
| DELETE | `/api/posts/{postId}/comments/{commentId}` | Deleta comentário |

## 📊 Modelo de Dados

### Post
```java
{
  id: String,
  title: String,      // 3-200 chars
  content: String,    // min 10 chars
  author: String,     // 2-100 chars
  slug: String,       // único
  createdAt: DateTime,
  updatedAt: DateTime
}
```

### Comment
```java
{
  id: String,
  postId: String,     // referência ao post
  author: String,     // 2-100 chars
  content: String,    // 1-1000 chars
  createdAt: DateTime
}
```

## 🔧 Funcionalidades

### PostService
- CRUD completo de posts
- Geração automática de slug único
- Contagem de comentários
- Paginação e ordenação

### CommentService
- CRUD de comentários
- Validação de post existente
- Ordenação por data

### Exception Handling
- Tratamento global com @RestControllerAdvice
- Exceções customizadas
- Respostas de erro padronizadas
- Validação de Bean Validation

## 🏗️ Design Patterns

- **Repository Pattern**: Acesso a dados
- **Service Layer**: Lógica de negócio
- **DTO Pattern**: Separação de concerns
- **Builder Pattern**: Construção de objetos (Lombok)

## 📦 Dependências Principais

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-mongodb</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-validation</artifactId>
    </dependency>
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
    </dependency>
</dependencies>
```

## 🔒 Segurança

- CORS configurado
- Validação em todas as camadas
- Tratamento de exceções
- Proteção contra NoSQL injection

## 🧪 Testar API

Ver exemplos em: [docs/API_EXAMPLES.md](../docs/API_EXAMPLES.md)

## 📝 Logs

O projeto usa SLF4J com Logback para logging:
- INFO: Operações principais
- DEBUG: Detalhes de execução
- ERROR: Erros e exceções

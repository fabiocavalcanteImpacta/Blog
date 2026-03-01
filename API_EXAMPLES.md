# Exemplos de Requisições API

## Posts

### Criar Post
```bash
curl -X POST http://localhost:8080/api/posts \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Meu Primeiro Post",
    "content": "Este é o conteúdo do meu primeiro post no blog. Aqui posso escrever sobre qualquer assunto!",
    "author": "João Silva"
  }'
```

### Listar Posts (com paginação)
```bash
curl http://localhost:8080/api/posts?page=0&size=10
```

### Buscar Post por ID
```bash
curl http://localhost:8080/api/posts/65f1234567890abcdef12345
```

### Buscar Post por Slug
```bash
curl http://localhost:8080/api/posts/slug/meu-primeiro-post
```

### Atualizar Post
```bash
curl -X PUT http://localhost:8080/api/posts/65f1234567890abcdef12345 \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Meu Post Atualizado",
    "content": "Conteúdo atualizado do post"
  }'
```

### Deletar Post
```bash
curl -X DELETE http://localhost:8080/api/posts/65f1234567890abcdef12345
```

## Comentários

### Criar Comentário
```bash
curl -X POST http://localhost:8080/api/posts/65f1234567890abcdef12345/comments \
  -H "Content-Type: application/json" \
  -d '{
    "author": "Maria Santos",
    "content": "Ótimo post! Muito interessante."
  }'
```

### Listar Comentários de um Post
```bash
curl http://localhost:8080/api/posts/65f1234567890abcdef12345/comments
```

### Deletar Comentário
```bash
curl -X DELETE http://localhost:8080/api/posts/65f1234567890abcdef12345/comments/65f9876543210fedcba09876
```

## Exemplos de Respostas

### Post Response
```json
{
  "id": "65f1234567890abcdef12345",
  "title": "Meu Primeiro Post",
  "content": "Este é o conteúdo do meu primeiro post no blog.",
  "author": "João Silva",
  "slug": "meu-primeiro-post",
  "createdAt": "2026-02-22T10:30:00",
  "updatedAt": "2026-02-22T10:30:00",
  "commentsCount": 3
}
```

### Comment Response
```json
{
  "id": "65f9876543210fedcba09876",
  "postId": "65f1234567890abcdef12345",
  "author": "Maria Santos",
  "content": "Ótimo post! Muito interessante.",
  "createdAt": "2026-02-22T11:15:00"
}
```

### Error Response
```json
{
  "timestamp": "2026-02-22T11:20:00",
  "status": 404,
  "error": "Not Found",
  "message": "Post não encontrado com id: 65f1234567890abcdef12345",
  "path": "/api/posts/65f1234567890abcdef12345"
}
```

### Validation Error Response
```json
{
  "timestamp": "2026-02-22T11:25:00",
  "status": 400,
  "error": "Validation Error",
  "message": "Erro de validação nos campos",
  "path": "/api/posts",
  "validationErrors": {
    "title": "Título deve ter no mínimo 3 caracteres",
    "content": "Conteúdo deve ter no mínimo 10 caracteres"
  }
}
```

# 🌐 Especificação da API

A API será **RESTful**, implementada em **Node.js + Express**, com autenticação via **JWT**.  
Todos os endpoints estarão versionados em `/api/v1`.

---

## 🔹 Autenticação

### POST `/api/v1/auth/signup`
- **Descrição:** Cadastra um novo usuário (feirante ou consumidor).  
- **Corpo (JSON):**
```json
{
  "nome": "João Silva",
  "email": "joao@email.com",
  "senha": "123456",
  "perfil": "feirante"
}
```
**Resposta (201):**
```json
{
  "id": 1,
  "nome": "João Silva",
  "email": "joao@email.com",
  "perfil": "feirante"
}`
```
### POST `/api/v1/auth/login`
 - **Descrição:** Realiza login e retorna token JWT.
 - **Corpo (JSON):**
 ```json
 {
 "email": "joao@email.com",
 "senha": "123456"
 }
```
**Resposta (200):**
```json
 {
 "token": "eyJhbGciOiJIUzI1NiIsInR..."
 }
 ``` 

 🔹Feiras
 ### GET `/api/v1/feiras`
-  **Descrição:** Lista todas as feiras cadastradas.
 - **Resposta (200):**
 ```json
 [
    {
      "id_feira": 1,
      "nome": "Feira do Benfica",
      "endereco": "Rua A, 123",
      "bairro": "Benfica",
      "cidade": "Fortaleza",
      "horario_funcionamento": "07:00 - 13:00"
    }
 ]
 ```
  ### POST `/api/v1/feiras` (Admin)
 - **Descrição:** Cadastra nova feira.
-  **Corpo (JSON):**
```json
 {
  "nome": "Feira da Parangaba",
  "endereco": "Av. Central, 500",
  "bairro": "Parangaba",
  "cidade": "Fortaleza",
  "horario_funcionamento": "06:00 - 12:00"
}
 ```
 
  🔹Feirantes
 ### POST `/api/v1/feirantes`
 - **Descrição:** Cadastro de feirante.
 - **Corpo (JSON):**
 ```json
 {
  "nome": "Maria Souza",
  "email": "maria@email.com",
  "telefone": "85999999999",
  "senha": "123456"
 }
```
 ### GET `/api/v1/feirantes/:id`
 - **Descrição:** Retorna dados do feirante.
 - **Resposta (200):**
 ```json
 {
  "id_feirante": 1,
  "nome": "Maria Souza",
  "email": "maria@email.com",
  "telefone": "85999999999",
  "status": "ativo"
 }
 ```
 🔹Produtos
  ### POST `/api/v1/produtos`
-  **Descrição:** Cadastra produto de um feirante.
 - **Corpo (JSON):**
 ```json
 {
  "nome": "Tomate",
  "categoria": "Hortaliça",
  "descricao": "Tomate orgânico fresco",
  "preco_medio": 5.00,
  "id_feirante": 1
 }
 ```
  ### GET `/api/v1/produtos?nome=tomate&data;=2025-09-21`
 - **Descrição:** Busca produtos pelo nome e retorna feirantes que os oferecem no dia.
 - **Resposta (200):**
  ```json
 [
    {
      "feira": "Feira do Benfica",
      "feirante": "Maria Souza",
      "produto": "Tomate",
      "preco_medio": 5.00,
      "disponivel": true
    }
 ]
 ```
 
 🔹Agenda do Feirante
 ### POST `/api/v1/agendas`
 - **Descrição:** Define agenda semanal do feirante.
-  **Corpo (JSON):**
```json
 {
  "id_feirante": 1,
  "id_feira": 2,
  "dia_semana": "terça"
 }
 ```
 ### GET `/api/v1/agendas/feirante/:id`
 - **Descrição:** Retorna agenda de um feirante.
-  **Resposta (200):**
```json
 [
  {
    "feira": "Feira da Parangaba",
    "dia_semana": "terça"
  }
 ]
 ```
 🔹Check-in Diário
 ### POST `/api/v1/checkins`
 - **Descrição:** Feirante realiza check-in em uma feira.
 - **Corpo (JSON):**
 ```json
 {
  "id_feirante": 1,
  "id_feira": 2,
  "data": "2025-09-21",
  "produtos_disponiveis": ["Tomate", "Cebola", "Alface"]
 }
 ```
 ### GET `/api/v1/checkins?feiraId=2&data;=2025-09-21`
-  **Descrição:** Lista feirantes presentes em uma feira na data especificada.
 - **Resposta (200):**
 ```json
 [
  {
    "feirante": "Maria Souza",
    "produtos_disponiveis": ["Tomate", "Cebola"]
  }
 ]
 ```
 
 🔹Avaliações
 ### POST `/api/v1/avaliacoes`
 - **Descrição:** Consumidor avalia um feirante.
- **Corpo (JSON):**
```json
 {
  "id_consumidor": 3,
  "id_feirante": 1,
  "nota": 5,
  "comentario": "Produtos frescos e ótimo atendimento"
 }
 ```
 ### GET `/api/v1/avaliacoes/feirante/:id`
 - **Descrição:** Retorna todas as avaliações de um feirante.
 - **Resposta (200):**
 ```json
 [
  {
    "consumidor": "João Silva",
    "nota": 5,
    "comentario": "Produtos frescos e ótimo atendimento",
    "data": "2025-09-20"
  }
 ]
 ```
 ## 
 - Considerações Gerais- Todas as rotas protegidas exigem envio do token JWT no cabeçalho:
 ```makelif
 Authorization: Bearer <token>
 ```

 - Respostas seguem o padrão HTTP:
 - `200 OK` → requisição bem sucedida
 - `201 Created` → recurso criado
 - `400 Bad Request` → erro de validação
 - `401 Unauthorized` → usuário não autenticado
 - `403 Forbidden` → usuário sem permissão
 - `404 Not Found` → recurso não encontrado





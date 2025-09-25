# 🏗️ Arquitetura do Sistema

## 🔹 Definição da Arquitetura

O sistema será construído com uma **arquitetura cliente-servidor** baseada em APIs REST.  
A solução terá três camadas principais:

1. **Frontend (Web e Mobile):**  
   - Interface web em **React.js** para administradores e feirantes.  
   - Aplicativo mobile em **React Native** para consumidores.  

2. **Backend (API REST):**  
   - Desenvolvido em **Node.js com Express**.  
   - Responsável por gerenciar regras de negócio, autenticação e comunicação com o banco de dados.  
   - Exposição de endpoints RESTful documentados com Swagger.  

3. **Banco de Dados:**  
   - Utilização de **MySQL** para persistência de dados relacionais.  
   - ORM: **Sequelize** para mapear entidades e facilitar manutenção.  

Fluxo principal:  
`Frontend (React / React Native) ⇄ API REST (Node.js + Express) ⇄ Banco de Dados (MySQL)`

---

## 🔹 Padrões Arquiteturais

- **Arquitetura em Camadas (Layered Architecture):** separação entre apresentação, lógica de negócio e persistência.  
- **Repository Pattern:** para abstração de acesso ao banco de dados.  
- **Service Layer:** centralização das regras de negócio.  
- **RESTful API:** endpoints bem definidos e versionados (`/api/v1`).  
- **JWT Authentication:** autenticação e autorização stateless.  
- **DTOs e Validadores:** uso de objetos de transferência de dados e validação de entrada.  
- **Cache-aside (Redis):** otimização de consultas de leitura mais frequentes (ex.: busca de produtos por data).  

---

## 🔹 Tecnologias e Frameworks

### Backend
- **Node.js** (runtime)  
- **Express.js** (framework web)  
- **Sequelize** (ORM para MySQL)  
- **JWT (jsonwebtoken)** para autenticação  
- **Joi / express-validator** para validação de dados  
- **Swagger (OpenAPI)** para documentação da API  
- **Redis** (cache e filas, opcional)  
- **Bull** (gerenciamento de jobs assíncronos, opcional)  
- **Jest + Supertest** para testes unitários e de integração  

### Frontend Web
- **React.js** (SPA)  
- **Axios** para consumo da API  
- **React Router** para navegação  
- **React Hook Form + Yup** para formulários e validação  
- **Material-UI (MUI)** para componentes de interface  

### Mobile
- **React Native**  
- **React Navigation**  
- **Axios** para integração com API  
- **Redux Toolkit** ou Context API (gerenciamento de estado)  

### Banco de Dados
- **MySQL**  
- **Migrations com Sequelize** para versionamento do esquema  

### DevOps
- **Docker + docker-compose** para ambiente de desenvolvimento  
- **GitHub Actions** para CI/CD  
- **Heroku / Railway / Render** para deploy backend  
- **Vercel / Netlify** para deploy frontend  

---

## 🔹 Diagrama da Arquitetura

```mermaid
flowchart TD
    subgraph CLIENTS
        Web[React.js - Web App]
        Mobile[React Native - Mobile App]
    end

    subgraph API[Backend - Node.js + Express]
        Routes[Rotas REST]
        Services[Regras de Negócio]
        Repositories[ORM Sequelize]
        Auth[Autenticação JWT]
    end

    subgraph DB[(MySQL Database)]
        Tables[(Feiras, Feirantes, Produtos, Agendas, Checkins, Avaliações)]
    end

    subgraph CACHE[(Redis - opcional)]
    end

    Web -->|HTTP JSON| API
    Mobile -->|HTTP JSON| API
    API --> DB
    API --> CACHE

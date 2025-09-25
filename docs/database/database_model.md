# 🗄️ Modelo de Dados

O banco de dados será relacional, implementado em **MySQL**, e modelado para atender às necessidades de gerenciamento de feiras, feirantes, consumidores e produtos.

---

## 🔹 Entidades Principais

### Feira
- **id_feira** (PK)
- **nome**
- **endereco**
- **bairro**
- **cidade**
- **horario_funcionamento**

---

### Feirante
- **id_feirante** (PK)
- **nome**
- **email**
- **telefone**
- **senha_hash**
- **foto_perfil**
- **status** (ativo/inativo)

---

### Produto
- **id_produto** (PK)
- **nome**
- **categoria**
- **descricao**
- **preco_medio**
- **id_feirante** (FK → Feirante)

---

### AgendaFeirante
- **id_agenda** (PK)
- **id_feirante** (FK → Feirante)
- **id_feira** (FK → Feira)
- **dia_semana** (ex.: segunda, terça, ...)

---

### Checkin
- **id_checkin** (PK)
- **id_feirante** (FK → Feirante)
- **id_feira** (FK → Feira)
- **data**
- **produtos_disponiveis** (texto ou JSON)

---

### Consumidor
- **id_consumidor** (PK)
- **nome**
- **email**
- **telefone**
- **senha_hash**

---

### Avaliacao
- **id_avaliacao** (PK)
- **id_consumidor** (FK → Consumidor)
- **id_feirante** (FK → Feirante)
- **nota** (1 a 5)
- **comentario**
- **data**

---

## 🔹 Diagrama ER (Mermaid)

```mermaid
erDiagram
    FEIRA {
        int id_feira PK
        string nome
        string endereco
        string bairro
        string cidade
        string horario_funcionamento
    }

    FEIRANTE {
        int id_feirante PK
        string nome
        string email
        string telefone
        string senha_hash
        string foto_perfil
        string status
    }

    PRODUTO {
        int id_produto PK
        string nome
        string categoria
        string descricao
        decimal preco_medio
        int id_feirante FK
    }

    AGENDAFEIRANTE {
        int id_agenda PK
        int id_feirante FK
        int id_feira FK
        string dia_semana
    }

    CHECKIN {
        int id_checkin PK
        int id_feirante FK
        int id_feira FK
        date data
        text produtos_disponiveis
    }

    CONSUMIDOR {
        int id_consumidor PK
        string nome
        string email
        string telefone
        string senha_hash
    }

    AVALIACAO {
        int id_avaliacao PK
        int id_consumidor FK
        int id_feirante FK
        int nota
        string comentario
        date data
    }

    FEIRANTE ||--o{ PRODUTO : "oferece"
    FEIRANTE ||--o{ AGENDAFEIRANTE : "tem"
    FEIRANTE ||--o{ CHECKIN : "realiza"
    FEIRANTE ||--o{ AVALIACAO : "recebe"

    FEIRA ||--o{ AGENDAFEIRANTE : "possui"
    FEIRA ||--o{ CHECKIN : "acontece"

    CONSUMIDOR ||--o{ AVALIACAO : "faz"

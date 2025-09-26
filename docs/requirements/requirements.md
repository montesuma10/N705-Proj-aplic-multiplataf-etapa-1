# 📋 Levantamento de Requisitos

## 🔹 Requisitos Funcionais (RF)

1. **Cadastro de Feiras (Admin):**  
   O administrador deve poder cadastrar, atualizar e excluir feiras na plataforma.  

2. **Cadastro de Feirantes (Admin/Feirante):**  
   O sistema deve permitir o cadastro de feirantes com dados pessoais e de contato.  

3. **Gestão de Perfil (Feirante):**  
   O feirante deve poder atualizar seu perfil (dados pessoais, foto, descrição).  

4. **Cadastro de Produtos (Feirante):**  
   O feirante deve poder cadastrar, editar e excluir produtos ofertados.  

5. **Agenda Semanal (Feirante):**  
   O feirante deve poder definir em quais dias e feiras costuma participar.  

6. **Check-in Diário (Feirante):**  
   O feirante deve poder realizar check-in em uma feira específica, informando os produtos que está ofertando no dia.  

7. **Busca de Produtos (Consumidor):**  
   O consumidor deve poder pesquisar produtos e visualizar as feiras/feirantes que os têm disponíveis no dia.  

8. **Consulta de Agenda (Consumidor):**  
   O consumidor deve poder consultar a agenda semanal de um feirante.  

9. **Avaliação de Feirantes (Consumidor):**  
   O consumidor deve poder avaliar e deixar comentários sobre feirantes.  

10. **Autenticação e Autorização (Todos):**  
    O sistema deve permitir login e definir níveis de acesso (Admin, Feirante, Consumidor).  

11. **Listagem e Consulta (Todos):**  
    O sistema deve exibir informações organizadas sobre feiras, feirantes e produtos.  

---

## 🔹 Requisitos Não Funcionais (RNF)

1. **Multiplataforma:**  
   O sistema deve ser acessível tanto via navegador (web) quanto em dispositivos móveis.  

2. **Usabilidade:**  
   A interface deve ser simples e intuitiva, adaptada a diferentes perfis de usuários.  

3. **Disponibilidade:**  
   O sistema deve estar disponível 24/7, salvo em períodos de manutenção.  

4. **Escalabilidade:**  
   A arquitetura deve suportar o crescimento do número de usuários e feiras.  

5. **Segurança:**  
   O sistema deve armazenar senhas de forma criptografada e usar autenticação segura (JWT ou similar).  

6. **Performance:**  
   As consultas de busca devem retornar resultados em até 2 segundos em condições normais de rede.  

7. **Compatibilidade:**  
   O sistema deve ser compatível com os navegadores mais comuns (Chrome, Edge, Firefox) e com Android (mín. versão 8).  

8. **Documentação de API:**  
   O backend deve ter especificação das APIs usando Swagger/OpenAPI.  

9. **Banco de Dados Relacional:**  
   Os dados devem ser armazenados em MySQL, com integridade referencial.  

---

## 🔹 Regras de Negócio (RB)

1. Apenas **administradores** podem cadastrar novas feiras.  

2. Cada **feirante** deve estar vinculado a pelo menos uma feira para poder fazer check-in.  

3. O **check-in diário** deve ser válido apenas para a data corrente.  

4. O produto só aparece como disponível para consumidores se o **feirante tiver feito check-in** naquele dia.  

5. Cada consumidor pode **avaliar um feirante apenas uma vez por dia**, evitando spam.  

6. O sistema deve permitir a alteração de status de um feirante (ativo/inativo).  
---

## 📝 Histórias de Usuário
- **Consumidor:**  
  - "Como consumidor, quero buscar um produto pelo nome, para saber em quais feiras ele está disponível hoje."  
  - "Como consumidor, quero consultar a agenda de um feirante, para planejar minhas compras semanais."  
  - "Como consumidor, quero avaliar um feirante, para compartilhar minha experiência."  

- **Feirante:**  
  - "Como feirante, quero cadastrar meus produtos, para divulgar o que vendo nas feiras."  
  - "Como feirante, quero fazer check-in diário, para informar aos clientes que estou presente na feira."  
  - "Como feirante, quero gerenciar minha agenda semanal, para organizar minha rotina de vendas."  

- **Administrador:**  
  - "Como administrador, quero cadastrar novas feiras, para expandir o alcance da plataforma."  
  - "Como administrador, quero gerenciar feirantes, para garantir confiabilidade e segurança no sistema."  

---
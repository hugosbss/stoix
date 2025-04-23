# stoix

# ✅ Gerenciador de Tarefas

Aplicação *Full Stack* para gerenciamento de tarefas, com autenticação via *JWT, API RESTful em **NestJS* e frontend em *Vue 3 + TypeScript*.

---

## 📚 Funcionalidades

- 🔐 Login de usuário com autenticação JWT
- ➕ Criar novas tarefas
- 📋 Listar todas as tarefas
- ✏️ Editar tarefas existentes
- ❌ Remover tarefas
- 🔒 Rota protegida por token

---

### 🔧 Backend

- [NestJS](https://nestjs.com/)
- TypeScript
- MySQL
- JWT para autenticação
- RESTful API

### 🎨 Frontend

- Vue 3 + Vite
- TypeScript
- CSS3
- LocalStorage para armazenamento do token JWT

---

### 🔐 Autenticação

 - O login gera um JWT Token salvo em localStorage.
 - O token é enviado em requisições para rotas protegidas.
 - Há uma página /protected que só pode ser acessada se o token estiver presente.

### 🗂️ Estrutura da API

- Método	Endpoint	Descrição
- POST	/auth/login	Login de usuário
- GET	/tasks	Lista todas as tarefas
- POST	/tasks	Cria nova tarefa
- PUT	/tasks/:id	Atualiza tarefa
- DELETE	/tasks/:id	Remove tarefa

## ⚙️ Como rodar o projeto localmente

### ⚠️ Requisitos
- É necessário ter o *XAMPP* instalado e rodando com o serviço do *MySQL* ativo.

🔧 Dependências Globais
Node.js (versão recomendada: 18 ou superior)

NPM (gerenciador de pacotes incluso com o Node)

XAMPP (para rodar o MySQL localmente)

Vue CLI (opcional, se desejar utilizar comandos Vue CLI)

📦 Instalação de Dependências do Projeto
Após clonar o projeto, entre nas pastas correspondentes e execute os comandos abaixo para instalar as dependências:

🔙 Backend (NestJS)
cd backend/tasks
npm install
npm run start

🔜 Frontend (Vue 3 + Vite)
cd frontend/tasks
npm install
npm run dev

🗄️ Banco de Dados
O projeto utiliza o MySQL, rodando via XAMPP.

É necessário que o serviço MySQL esteja ativo.

Banco de dados esperado: stoix

Tabelas esperadas: users e tasks

Você pode criar o banco e as tabelas manualmente no *phpMyAdmin* ou com os seguintes comandos SQL:

sql
CREATE DATABASE stoix;

USE stoix;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    password VARCHAR(100) NOT NULL
);

CREATE TABLE tasks (
    id INT AUTO_INCREMENT PRIMARY KEY,
    titulo VARCHAR(255) NOT NULL,
    descricao TEXT,
    status TEXT
);

INSERT INTO users (username, password) VALUES ('admin', 'admin123');



## 🧰 Tecnologias

### 🔧 Backend

- [NestJS](https://nestjs.com/)
- TypeScript
- MySQL
- JWT para autenticação
- RESTful API

### 🎨 Frontend

- Vue 3 + Vite
- TypeScript
- CSS3
- LocalStorage para armazenamento do token JWT

### ✍️ Considerações
 - As tarefas são carregadas e atualizadas automaticamente sem necessidade de recarregar a página.
 - Interface amigável e funcional para o usuário final.
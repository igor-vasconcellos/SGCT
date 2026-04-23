# 🚀 Sistema de Gerenciamento de Chamados (SGCT)

O **SGCT** é uma solução full-stack para abertura, monitoramento e gestão de chamados técnicos. Desenvolvido com **Node.js** e **MySQL**, o sistema permite o controle eficiente de incidentes e solicitações de suporte.

## 📋 Funcionalidades
- **Autenticação de Usuários:** Sistema de login com persistência de sessão.
- **Níveis de Acesso:** Controle de permissões para `cliente`, `tec` (Técnico) e `adm` (Administrador).
- **Gestão de Chamados:** Abertura de tickets com prioridades e categorias dinâmicas.
- **Dashboard Estatístico:** Resumo em tempo real da quantidade de chamados abertos, em andamento e concluídos.

---

## 🛠️ Configuração do Banco de Dados (MySQL)

O sistema utiliza o banco de dados `sistema_sgct`. Siga os passos abaixo para configurar a estrutura corretamente:

1. **Acesse o terminal do MySQL:**
   ```bash
   sudo mysql -u root -p

2. Crie o Banco e a Estrutura:
(Copie e cole os blocos abaixo na ordem apresentada para evitar erros de chaves estrangeiras):

SQL
CREATE DATABASE sistema_sgct;
USE sistema_sgct;

-- 1. Tabela de Categorias
CREATE TABLE categorias (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL
);

-- 2. Tabela de Usuários
CREATE TABLE usuario (
    id_usuario INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    senha VARCHAR(255) NOT NULL,
    tipo ENUM('cliente', 'tec', 'adm') DEFAULT 'cliente'
);

-- 3. Tabela de Chamados
CREATE TABLE chamado (
    id_chamado INT AUTO_INCREMENT PRIMARY KEY,
    titulo VARCHAR(255) NOT NULL,
    descricao TEXT,
    status VARCHAR(20) DEFAULT 'Aberto',
    prioridade VARCHAR(20),
    data_criacao TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    usuario_id INT,
    categoria_id INT,
    FOREIGN KEY (usuario_id) REFERENCES usuario(id_usuario),
    FOREIGN KEY (categoria_id) REFERENCES categorias(id)
);

3. Alimente as Categorias (Obrigatório):
Execute o comando abaixo para que o formulário de abertura de chamados funcione corretamente:

SQL
INSERT INTO categorias (nome) VALUES 
('erro_sistema'), ('manutencao_preventiva'), ('manutencao_corretiva'),
('instalacao_software'), ('atualizacao_sistema'), ('configuracao_rede'),
('backup_recuperacao'), ('duvida_usuario'), ('acesso_bloqueado');

⚙️ Instalação e Execução
1. Instale as dependências do projeto:

Bash
npm install
2. Configuração de Conexão:
Certifique-se de que o arquivo database.js está configurado com o usuário root e o banco sistema_sgct.

3. Inicie o servidor:

Bash
node server.js
4. Acesse no Navegador:
http://localhost:3000

🔑 Credenciais de Teste (Administrador)
Para acessar as funcionalidades administrativas e de técnico, utilize ou crie este usuário:

E-mail: admin@teste.com

Senha: admin123

(Caso precise criar manualmente):

SQL
INSERT INTO usuario (nome, email, senha, tipo) 
VALUES ('Administrador', 'admin@teste.com', 'admin123', 'adm');

📂 Estrutura de Pastas
/public: Interface do usuário (HTML, CSS e JavaScript do cliente).
/routes: Definição de rotas e middlewares de autenticação.
/controllers: Lógica de controle e processamento de dados.
/models: Funções de comunicação e consultas SQL.
server.js: Arquivo principal de inicialização do servidor.

---
## 🖼️ Preview do Design

<img src="./assets/abrirChamados.png" alt="Preview da tela de Chamados" width="400"/>

<img src="./assets/chamadosTech.png" alt="Preview da tela de Chamados" width="400"/>







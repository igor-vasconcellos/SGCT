Com certeza! Aqui está a versão final e corrigida do seu README.md. Este arquivo está estruturado para que qualquer pessoa (ou você mesmo no futuro) consiga colocar o sistema de pé rapidamente, com atenção especial à configuração do banco de dados que acabámos de ajustar.

🚀 Sistema de Gerenciamento de Chamados (SGCT)
Este é um sistema full-stack desenvolvido para a abertura e gestão de chamados técnicos. O projeto utiliza Node.js no backend e MySQL para armazenamento persistente de dados.

📋 Funcionalidades
Login e Cadastro de utilizadores com níveis de acesso (cliente, tec, adm).

Abertura de chamados com categorização dinâmica.

Dashboard com resumo de chamados em tempo real.

Sistema de sessão para segurança das rotas.

🛠️ Configuração do Banco de Dados (MySQL)
O banco de dados é a peça central deste sistema. Siga os passos abaixo para configurar o ambiente:

Aceda ao terminal do MySQL:

Bash
sudo mysql -u root -p
Crie e selecione o banco de dados:

SQL
CREATE DATABASE sistema_sgct;
USE sistema_sgct;
Crie a estrutura das tabelas:
(Copie e cole este bloco para criar as tabelas na ordem correta devido às chaves estrangeiras):

SQL
-- 1. Tabela de Categorias
CREATE TABLE categorias (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL
);

-- 2. Tabela de Utilizadores
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
Popule as categorias (Obrigatório):
Para que o formulário de abertura de chamados funcione, os nomes devem ser idênticos aos values do HTML:

SQL
INSERT INTO categorias (nome) VALUES 
('erro_sistema'), ('manutencao_preventiva'), ('manutencao_corretiva'),
('instalacao_software'), ('atualizacao_sistema'), ('configuracao_rede'),
('backup_recuperacao'), ('duvida_usuario'), ('acesso_bloqueado');
⚙️ Instalação e Execução
Clone o repositório:

Bash
git clone https://github.com/seu-usuario/SGCT.git
cd SGCT
Instale as dependências:

Bash
npm install
Configure as credenciais do banco:
Verifique o arquivo database.js e confirme se o user, password e o database (sistema_sgct) coincidem com o seu ambiente.

Inicie o servidor:

Bash
node server.js
Aceda ao sistema:
Abra o navegador em http://localhost:3000.

🔑 Credenciais de Administrador
Caso precise de um acesso de administrador para testar as funcionalidades de técnico, execute este comando no MySQL:

SQL
INSERT INTO usuario (nome, email, senha, tipo) 
VALUES ('Admin', 'admin@teste.com', 'admin123', 'adm');
📂 Estrutura de Pastas
/public: Interface web (HTML, CSS e JS cliente).

/routes: Definição das rotas e middlewares de autenticação.

/controllers: Lógica de processamento das requisições.

/models: Funções de interação direta com o banco de dados (Queries SQL).

server.js: Arquivo principal de configuração do servidor Express.

---
## 🖼️ Preview do Design

<img src="./assets/abrirChamados.png" alt="Preview da tela de Chamados" width="400"/>

<img src="./assets/chamadosTech.png" alt="Preview da tela de Chamados" width="400"/>







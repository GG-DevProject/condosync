# condosync

- Estrutura do Projeto

```bash
condosync/
│
├── backend/                # API e lógica do back-end
│   ├── app.py              # Flask app principal
│   ├── config.py           # Configuração do MySQL e Flask
│   ├── models.py           # Modelos e interações com MySQL
│   ├── routes/             # Rotas da API
│   │   ├── residents.py    # Rotas para moradores
│   │   ├── events.py       # Rotas para eventos do Calendar
│   │   └── projects.py     # Rotas para o Gantt Chart
│   │
│   └── requirements.txt    # Dependências Python
│
├── frontend/               # Aplicação front-end com Syncfusion
│   ├── index.html          # Página inicial do front-end
│   ├── app.js              # Lógica do front-end
│   ├── styles.css          # Estilos personalizados
│   ├── components/         # Componentes Syncfusion
│   │   ├── Calendar.js     # Calendar Syncfusion
│   │   ├── DataGrid.js     # DataGrid Syncfusion
│   │   └── GanttChart.js   # Gantt Chart Syncfusion
│   │
│   ├── assets/             # Recursos estáticos (imagens, etc.)
│   └── package.json        # Dependências JavaScript
│
├── database/               # Scripts SQL para configuração inicial
│   ├── schema.sql          # Estrutura inicial do banco
│   └── seed.sql            # Dados de exemplo
│
├── index.html              # Página de inicialização
└── README.md               # Documentação do projeto
```

---

- Estrutura do MySQL

```mysql
-- Criação do banco de dados
CREATE DATABASE condosync;

-- Selecionando o banco de dados
USE condosync;

-- Tabela de usuários (Administração e login)
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    role ENUM('admin', 'manager', 'resident') NOT NULL DEFAULT 'resident'
);

-- Tabela de moradores
CREATE TABLE residents (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    unit VARCHAR(20) NOT NULL,
    contact VARCHAR(50) NOT NULL,
    user_id INT,
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE SET NULL
);

-- Tabela de eventos (Calendar)
CREATE TABLE events (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(100) NOT NULL,
    description TEXT,
    start_date DATETIME NOT NULL,
    end_date DATETIME NOT NULL,
    created_by INT,
    FOREIGN KEY (created_by) REFERENCES users(id) ON DELETE SET NULL
);

-- Tabela de projetos (Gantt Chart)
CREATE TABLE projects (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    start_date DATETIME NOT NULL,
    end_date DATETIME NOT NULL,
    progress INT NOT NULL DEFAULT 0,
    status ENUM('pending', 'in_progress', 'completed') NOT NULL DEFAULT 'pending',
    created_by INT,
    FOREIGN KEY (created_by) REFERENCES users(id) ON DELETE SET NULL
);

-- Inserir Dados de testes

-- Inserindo usuários
INSERT INTO users (username, password, role) VALUES
('admin', 'hashed_password_here', 'admin'),
('manager1', 'hashed_password_here', 'manager'),
('resident1', 'hashed_password_here', 'resident');

-- Inserindo moradores
INSERT INTO residents (name, unit, contact, user_id) VALUES
('João Silva', '101A', 'joao@example.com', 3),
('Maria Oliveira', '102B', 'maria@example.com', 3);

-- Inserindo eventos
INSERT INTO events (title, description, start_date, end_date, created_by) VALUES
('Reunião de condomínio', 'Discussão sobre obras', '2024-12-10 18:00:00', '2024-12-10 20:00:00', 1),
('Manutenção elétrica', 'Troca de fiação geral', '2024-12-15 08:00:00', '2024-12-15 12:00:00', 2);

-- Inserindo projetos
INSERT INTO projects (name, start_date, end_date, progress, status, created_by) VALUES
('Reforma da fachada', '2024-12-01 00:00:00', '2024-12-20 23:59:59', 50, 'in_progress', 2),
('Pintura do prédio', '2024-12-21 00:00:00', '2025-01-10 23:59:59', 0, 'pending', 2);
```

---

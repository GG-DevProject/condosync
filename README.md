# condosync

condosync/
|
├── backend/                # API e lógica do back-end
│   ├── app.py              # Flask app principal
│   ├── config.py           # Configuração do MySQL e Flask
│   ├── models.py           # Modelos e interações com MySQL
│   ├── routes/             # Rotas da API
│   │   ├── residents.py    # Rotas para moradores
│   │   ├── events.py       # Rotas para eventos do Calendar
│   │   └── projects.py     # Rotas para o Gantt Chart
|   |
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

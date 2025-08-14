models.Model (Django ORM)
│
├── Campos (models.XField)
│ ├── mapeiam atributos Python → colunas no banco
│ ├── Exemplos:
│ │ ├── models.CharField → VARCHAR
│ │ ├── models.TextField → TEXT
│ │ ├── models.BooleanField → BOOLEAN
│ │ ├── models.DateTimeField → DATETIME
│ │ ├── models.ForeignKey → INTEGER (FK)
│ │ ├── models.ManyToManyField → tabela intermediária
│ │ └── models.OneToOneField → INTEGER UNIQUE
│ └── Opções extras (null, blank, default, choices...)
│
├── Meta
│ ├── verbose_name / plural → nomes amigáveis
│ ├── ordering → ordenação padrão
│ ├── db_table → nome custom da tabela
│ ├── constraints / unique_together → regras do banco
│ └── permissions → permissões extras
│
├── Métodos
│ ├── **str**() → representação textual do objeto
│ ├── métodos de negócio (ex: tem_certificado())
│ └── @property → atributos calculados
│
├── Ciclo de vida
│ ├── Cria tabela com manage.py migrate
│ ├── Ao alterar: makemigrations + migrate
│ └── ORM traduz Python ↔ SQL
│
└── Relações
├── ForeignKey: N → 1
├── ManyToMany: N ↔ N
└── OneToOne: 1 ↔ 1

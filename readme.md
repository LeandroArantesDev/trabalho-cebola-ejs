O trabalho final será de 25 pontos, com a data limite de entrega 20/06/2025.

Teremos 1 apresentação e a análise do código fonte do projeto.

- o Front end da aplicação pdoerá ser feito em qualquer framework ou linguagem.

- o Backend deverá ser em node/js com express js

Critérios de Avaliação:
Critério	Pontuação
Estrutura em cebola	5 pts
Entidades e telas	5 pts
Coerência entre a estrutura e o projeto	5 pts
Criatividade e usabilidade do projeto	5 pts
Organização e qualidade da apresentação	5 pt
Total	25 pts

 Requisitos Funcionais

1. Autenticação e Autorização

Endpoint de login via client_id e client_secret (semelhante a OAuth2 simplificado).
Geração de token JWT.
Middleware de autorização para proteger rotas.
Dois tipos de usuários: admin e colaborador:
admin pode acessar todos os dados e realizar CRUD completo.
colaborador pode apenas visualizar dados dos seus próprios projetos e tarefas.
2. Entidades obrigatórias (mínimo 3)

User: id, name, email, password (ou token), role
Project: id, name, description, owner (user_id)
Task: id, title, description, project_id, assigned_to (user_id), status
 Backend - Node.js + Express + SQL.js

Estrutura obrigatória:

Arquitetura em Cebola, com as seguintes camadas:
domain: entidades e contratos
application: casos de uso (ex: criar projeto, listar tarefas)
infrastructure: persistência em SQLite, autenticação JWT
presentation: rotas Express
 Frontend (escolha 1)

React, Vue ou Angular
Tela de login com autenticação JWT
Telas para:
Listar projetos e tarefas
Criar novos projetos/tarefas (se autorizado)
Visualizar tarefas atribuídas ao usuário autenticado
 Funcionalidades esperadas

Login via formulário
Acesso via token JWT
CRUD de projetos e tarefas
Interface visual com separação entre funções de admin e colaborador
 Entrega esperada

Projeto com a seguinte estrutura:
pgsql

CopiarEditar

backend/
src/
domain/
application/
infrastructure/
presentation/
index.js
package.json

frontend/
(React, Vue ou Angular)
App.vue / App.js
pages/
Login, Dashboard, Projects, Tasks

Script para inicializar o banco de dados com:
1 usuário admin e 1 colaborador
1 projeto com algumas tarefas
 

O que é arquitetura em camadas (cebola)?
 



[1] Domain (núcleo): entidades e interfaces
[2] Application: casos de uso e regras de negócio
[3] Infrastructure: banco de dados, frameworks, JWT, etc.
[4] Presentation: rotas e controladores Express

[1] Domain (Núcleo)

 O que é:

É o coração da aplicação.
Define as entidades do negócio e os contratos (interfaces) do que a aplicação precisa para funcionar.
Não contém lógica de acesso a dados, frameworks, express ou bibliotecas externas.
 Exemplo:

Entidade User: representa um usuário com nome, email, etc.
Interface UserRepository: define métodos como create(user) ou getById(id) — sem saber como eles serão implementados.
 O que não deve conter:

Qualquer dependência de banco de dados, Express, JWT, bibliotecas externas, etc.
 Vantagem:

Totalmente independente.
Pode ser reaproveitado em qualquer tipo de aplicação (web, CLI, mobile, etc).
 

 [2] Application (Casos de Uso)

 O que é:

Define os casos de uso da aplicação: as ações que podem ser realizadas.
Utiliza as interfaces do domínio para executar tarefas, mas não sabe como estão implementadas.
Contém regras de negócio específicas da aplicação.
 Exemplo:

CreateUser (caso de uso): recebe nome e email e chama userRepository.create(...).
 Vantagem:

Separa a lógica da aplicação do acesso a dados.
Fácil de testar com mocks (fingir implementações reais).
 

 [3] Infrastructure (Infraestrutura)

 O que é:

Implementa os detalhes técnicos da aplicação.
Aqui ficam:
Implementações de acesso a banco de dados.
Integrações com JWT, Redis, serviços externos.
Middleware de autenticação/autorização.
Serviços auxiliares.
 Exemplo:

UserRepositorySQLite: implementa a interface UserRepository usando sql.js.
AuthService: gera e verifica JWT.
 Vantagem:

Você pode trocar de banco de dados (ex: de SQLite para MongoDB) sem alterar as camadas internas.
 

 [4] Presentation (Interface/Entrada)

 O que é:

Interface de comunicação com o mundo externo: HTTP (Express), CLI, interface gráfica, etc.
Recebe requisições e aciona os casos de uso da aplicação.
Não tem regras de negócio, só orquestra.
 Exemplo:

Rota Express /users: recebe POST com dados de usuário e aciona CreateUser.
 Vantagem:

Você pode ter múltiplas formas de apresentar sua aplicação (REST, GraphQL, CLI, etc) sem alterar o domínio nem os casos de uso.

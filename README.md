<p align="center">
  <a href="https://fatecregistro.cps.sp.gov.br/" target="blank"><img src="https://bkpsitecpsnew.blob.core.windows.net/uploadsitecps/sites/40/2024/03/fatec_registro.png" width="300" alt="Fatec Logo" /></a>
</p>

  <p align="center">Laboratório de Práticas é de realização da <a href="https://fatecregistro.cps.sp.gov.br/" target="_blank">Fatec Registro</a> com o objetivo de acrescentar aos alunos um portfólio, e não menos importante, experiência!</p>
    <p align="center">
<a href="https://www.instagram.com/fatecregistro/" target="_blank"><img src="https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white" alt="Fatec Registro Instagram" /></a>
</p>

<h1 align="center">Vitrine - BackEnd</h1>

## 📋 Descrição
API desenvolvida com Nest.js que gerencia a apresentação de candidatos para representante e de Projetos da Fatec Registro. Através de QR codes únicos cada voto é encaminhado para a página correspondente ao candidato escolhido, garantindo transparência e acessibilidade durante o processo eleitoral da Faculdade.

### ⚙ O sistema oferece:

- Apresentação de candidatos e projetos através de vitrine digital

- Geração de QR codes únicos para cada representate

- Integração segura com o sistema de votação

- Busca de eventos externos

- Consumo de informações providos pelo CMS através do Banco de Dados

## 🛠 Requisitos Técnicos

### Ambiente de Desenvolvimento
- [![Node.js](https://img.shields.io/badge/node.js-339933?style=for-the-badge&logo=Node.js&logoColor=white)](https://nodejs.org/pt): v22.x (LTS recomendado)

- npm: v10.x ou Yarn

- [![PostgreSQL](https://img.shields.io/badge/-PostgreSQL-ea2845?style=flat-square&logo=postgresql&logoColor=white)]: v16+ (banco de dados principal)

- [![Nest.js](https://img.shields.io/badge/-NestJs-ea2845?style=flat-square&logo=nestjs&logoColor=white)](https://nestjs.com/): v11.0.0

- [![Typescript](https://img.shields.io/badge/TypeScript-007ACC?logo=typescript&logoColor=white)](https://www.typescriptlang.org/): v5.7.3

## Dependências Principais

### Backend:

- @nestjs/common: v11.0.1

- @nestjs/jwt: v11.0.0 (autenticação)

- @nestjs/typeorm: v11.0.0 (ORM)

- typeorm: v0.3.21

- pg: v8.14.1 (driver PostgreSQL)

- @nestjs/swagger: v11.1.0 (documentação API)

## Segurança
- Autenticação JWT (JSON Web Tokens)

## Configuração do Ambiente
Instalação
```bash
git clone https://github.com/laboratorio-de-praticas/vitrine-be.git

cd vitrine-be

npm install

cp .env.example .env
```

## Variáveis de Ambiente (.env)

### Configurações do servidor
```bash
PORT=5001
NODE_ENV=development

### Banco de dados
DB_HOST=nome_do_host
DB_PORT=porta
DB_USERNAME=nome_do-usuario
DB_PASSWORD=senha
DB_DATABASE=nome_do_banco

### Frontend 
FRONT_END_HOST=http://localhost:3001
```


## Scripts Disponíveis
- `npm run build`: Compila o projeto usando o Nest
- `npm run format`: Formata o código usando Prettier
- `npm run start`: Inicia o servidor em modo normal
- `npm run start:dev`: Inicia o servidor em modo de desenvolvimento com hot-reload
- `npm run start:debug`: Inicia o servidor em modo de depuração
- `npm run start:prod`: Inicia o servidor em modo de produção
- `npm run lint`: Executa o ESLint para correção de código
- `npm run test`: Executa os testes unitários
- `npm run test:watch`: Executa os testes em modo observador
- `npm run test:cov`: Executa os testes com cobertura
- `npm run test:debug`: Executa os testes em modo de depuração
- `npm run test:e2e`: Executa os testes end-to-end

## Estrutura do Projeto 
```
src/
├── controllers/     # Controladores da aplicação
├── dto/             # Objetos de transferência de dados
├── entities/        # Entidades do banco de dados
├── modules/         # Módulos NestJS
├── providers/       # Provedores de serviços
├── middlewares/     # Middlewares personalizados
├── repositories/    # Repositórios para acesso a dados
├── services/        # Serviços de negócios
├── utils/           # Funções utilitárias
└── main.ts          # Ponto de entrada da aplicação
```

## Endpoints Principais

### Representantes
Método GET
→ Endpoint: /v1/vitrine/tv
→ Descrição: Lista todos os eventos internos ativos no momento, com o número de representantes >=2
→ Autenticação: Nível Administrativo

## Segurança
### Camadas de Proteção

- CORS: Restrito ao domínio do frontend

## Testes
- Cobertura garantida por:

- Testes unitários (Jest)

```bash
npm run test:cov  # Gera relatório de cobertura
```


## Diagramação - Vitrine 

```mermaid
flowchart TD
    A(["Vitrine Front-end"]) --> B{{Acessar eventos internos ou externos}}
    B --> C["/vitrine/tv"]
    B --> D["/vitrine/externo"]
    C --> N1{{Possui token de segurança?}}
    D --> N1
    N1 --> N2["Não"]
    N1 --> N3["Sim"]
    N2 --> N4["Redireciona para o /login"]
    N3 --> N5["Realiza a chamada para o backend"]
    N6(["Requisição Back-end"]) --> N9["JWT"]
    N9 --> N10["API DE SEGURANÇA E AUTENTIFICAÇÃO"]
    N10 --> N11["Administrador"]
    N10 --> N12["Usuário não identificado ou não é Administrador"]
    N11 --> N7(["v1/vitrine/tv"])
    N11 --> N8(["v1/vitrine/eventos-externo"])
    N7 --> N13[/"Banco de Dados"/]
    N8 --> N13
    N15["CMS"] --> N14[/"Banco de dados"/]
    N14 --> N16["Dados de Eventos Internos"]
    N14 --> N18["Dados de Eventos Externos"]
    N16 --> N17(["v1/vitrine/tv"])
    N18 --> N19(["v1/vitrine/eventos-externos"])
    N17 --> N20["Realiza filtros para apenas eventos com 2 ou mais participantes"]
    N19 --> N21["Filtro: eventos ativos primeiro"]
    N20 --> N22["Devolve a resposta ao front-end"]
    N21 --> N22
```

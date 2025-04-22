# Laboratório de Práticas: _Vitrine - Backend_

## Descrição
API desenvolvida com Nest.js que gerencia o processo eleitoral para escolha de representantes de classe na Fatec. Através de QR codes únicos cada eleitor é encaminhado para a página de votação correspondente ao candidato escolhido, garantindo transparência e acessibilidade durante o processo eleitoral da Fatec. Integra o _Sistema de Votação para a Faculdade_.

### O sistema oferece:

-Apresentação de candidatos através de vitrine digital

-Geração de QR codes únicos para cada candidato

-Integração segura com o sistema de votação

-Autenticação e autorização de eleitores

-Dashboard administrativo para acompanhamento

## Requisitos Técnicos

### Ambiente de Desenvolvimento
- Node.js: v22.x (LTS recomendado)

- npm: v10.x ou Yarn

- PostgreSQL: v16+ (banco de dados principal)

- NestJS CLI: v11.0.0

- TypeScript: v5.7.3

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

- Criptografia de senhas com bcrypt

- Proteção contra CSRF

- Rate limiting para endpoints públicos

- Validação de entrada de dados com class-validator

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
PORT=5001
NODE_ENV=development

### Banco de dados
DB_HOST=localhost
DB_PORT=5432
DB_USERNAME=postgres
DB_PASSWORD=postgres
DB_DATABASE=vitrine

### Frontend 
FRONT_END_HOST=http://localhost:3001

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
├── auth/               # Autenticação e autorização
│   ├── strategies/     # Estratégias JWT
│   └── guards/         # Guards de proteção
├── candidates/         # Gestão de candidatos
├── elections/          # Processos eleitorais
├── qr-codes/           # Geração e validação de QR codes
├── users/              # Gestão de usuários (admin/eleitores)
├── shared/             # Recursos compartilhados
│   ├── exceptions/     # Filtros de exceção
│   ├── interceptors/   # Interceptores
│   └── decorators/     # Decoradores customizados
├── app.module.ts       # Módulo raiz
└── main.ts             # Ponto de entrada
```

## Integração Frontend
O frontend (vitrine-fe) consomeia com:

- Autenticação: Login via JWT

- Listagem de Candidatos: GET /api/candidates

- Geração de QR Codes: POST /api/qr-codes/generate

- Validação de Votos: POST /api/votes/validate

## Endpoints Principais
### Autenticação
Método	Endpoint	Descrição
POST	/auth/login	Login de administradores
POST	/auth/refresh	Renovação de token


### Candidatos
Método	Endpoint	Descrição	Autenticação
GET	/candidates	Lista todos candidatos	Pública
POST	/candidates	Cria novo candidato	Admin
PATCH	/candidates/:id	Atualiza candidato	Admin


### QR Codes
Método	Endpoint	Descrição
POST	/qr-codes/generate	Gera QR code para candidato
GET	/qr-codes/validate	Valida QR code para votação


## Segurança
### Camadas de Proteção
- Helmet: Headers de segurança HTTP

- CORS: Restrito ao domínio do frontend

- Rate Limiting: 100 requisições/minuto

- Validators: DTOs com class-validator


## Testes
- Cobertura garantida por:

- Testes unitários (Jest)

- Testes de integração

- Testes E2E com Supertest
```bash
npm run test:cov  # Gera relatório de cobertura
```

## Licença
MIT License

Copyright (c) 2025 Projeto Vitrine

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
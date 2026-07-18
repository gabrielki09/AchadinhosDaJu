# Achadinhos da Ju

Sistema web desenvolvido para aux no gerenciamento de vendas de peças de roupa, controle de estoque, compras, clientes, caixa e relatórios.

O projeto nasceu com um objetivo prático: ajudar minha mãe a organizar melhor as vendas e a rotina administrativa dos produtos. Além disso, também serviu como estudo de desenvolvimento full stack e principalmente de deploy, com o front-end publicado na Vercel.

URL inicial do projeto:

https://achadinhos-da-ju-front-end.vercel.app/auth/login

## Sobre o projeto

O Achadinhos da Ju e uma aplicação de gestão comercial voltada para uma pequena operação de venda de roupas. O sistema possui autenticação, painel administrativo, cadastro de produtos e clientes, controle de compras, ponto de venda, movimentações de caixa e geração de relatórios.

A aplicação e dividida em duas partes principais:

- `app`: front-end desenvolvido com Vue 3, Quasar, TypeScript e Tailwind CSS.
- `api`: back-end desenvolvido em Go, com API HTTP, autenticação via JWT e conexão com PostgreSQL.

Também ha suporte a Docker para execução local dos serviços de front-end e back-end.

## Funcionalidades

### Autenticação

- Tela de login em `/auth/login`.
- Proteção das rotas administrativas por token JWT.
- Redirecionamento automático para login quando o usuário não esta autenticado.

### Dashboard

- Visualizacao de indicadores gerais.
- Filtro por período.
- Cards com informações como:
  - Total vendido.
  - Comissão.
  - Quantidade de vendas.
  - Melhor cliente.
  - Total comprado.
  - Quantidade de compras.
  - Total de itens comprados.
  - Saldo total do caixa.
- Tabela de itens mais vendidos.
- Acesso a geração de relatórios.

### Produtos e estoque

- Listagem de produtos.
- Cadastro de novos produtos.
- Edição de produtos.
- Exclusão lógica e reativação de produtos.
- Filtro por status: ativos, inativos e todos.
- Busca por nome ou código do produto.
- Suporte a características/grade de produto, como tamanhos e quantidades específicas.

### Clientes

- Listagem de clientes.
- Cadastro de clientes.
- Edição de clientes.
- Exclusão lógica e reativação.
- Busca por nome, ID ou documento.
- Cliente padrão usado para vendas sem cliente cadastrado.

### Compras

- Cadastro de compras de mercadorias.
- Listagem das compras realizadas.
- Filtro por status:
  - Pendente.
  - Concluída.
  - Cancelada.
- Visualização de detalhes da compra.
- Importação de compra existente para edição/continuação.
- Cancelamento de compras concluídas.

### PDV

- Tela de ponto de venda.
- Busca e seleção de produtos.
- Inclusão de múltiplos produtos na venda.
- Controle de quantidade por item.
- Suporte a produtos com grade/tamanho.
- Seleção de cliente cadastrado ou uso de consumidor padrão.
- Calculo automático do total da venda.
- Salvamento temporário da venda.
- Cancelamento de venda.
- Finalização da venda com formas de pagamento.

### Pagamentos

- Gerenciamento de formas de pagamento.
- Atualização de chave Pix.
- Pagamento de vendas ou compras.
- Geração de QR Code Pix.
- Cancelamento de operações de venda ou compra.

### Caixa

- Listagem de movimentações de caixa.
- Cadastro de entradas e saídas.
- Cálculo de saldo a partir dos valores de entrada e saida.

### Relatórios

O sistema gera relatórios em PDF para diferentes áreas:

- Caixa.
- Formas de pagamento.
- Itens vendidos.
- Itens comprados.
- Compras.

A geração dos PDFs e feita no back-end usando a biblioteca Maroto.

## Tecnologias utilizadas

### Front-end

- Vue 3
- Quasar Framework
- TypeScript
- Vue Router
- Axios
- Tailwind CSS
- Vue I18n
- Yup
- Day.js
- QRCode Pix
- Vercel

### Back-end

- Go
- Gorilla Mux
- JWT
- PostgreSQL
- pgx
- godotenv
- Maroto PDF
- Docker

## Estrutura do projeto

```txt
.
├── api/
│   ├── api/
│   │   ├── cors/
│   │   ├── handle/modules/controller/
│   │   └── services/
│   ├── db/
│   ├── helpers/
│   ├── interface/
│   ├── main.go
│   ├── go.mod
│   └── go.sum
│
├── app/
│   ├── public/
│   ├── src/
│   │   ├── boot/
│   │   ├── components/
│   │   ├── css/
│   │   ├── helpers/
│   │   ├── interface/
│   │   ├── layouts/
│   │   ├── modules/
│   │   ├── router/
│   │   └── services/
│   ├── package.json
│   ├── quasar.config.ts
│   └── vercel.json
│
├── docker/
│   ├── backend/
│   └── frontend/
│
└── docker-compose.yml
```

## Rotas principais do front-end

| Rota | Descrição |
| --- | --- |
| `/auth/login` | Login |
| `/admin` | Dashboard |
| `/admin/products` | Produtos/estoque |
| `/admin/shopping` | Compras |
| `/admin/shopping/create` | Cadastro de compra |
| `/admin/customers` | Clientes |
| `/admin/cash-register` | Caixa |
| `/admin/cash-register/create` | Cadastro de movimentacao de caixa |
| `/admin/pdv` | Ponto de venda |
| `/admin/pdv/list-pdv` | Listagem de vendas |

### Principais grupos de endpoints

- `/api/products`
- `/api/customer`
- `/api/shopping`
- `/api/sale`
- `/api/cash-register`
- `/api/dash-board`
- `/api/report`
- `/api/pay-ment-forms`
- `/api/cancel-operation`

## Executando com Docker

Na raiz do projeto:

```bash
docker compose up --build
```

serviços configurados:

- Front-end: `http://localhost:9000`
- Back-end: `http://localhost:8000/api`

O `docker-compose.yml` usa:

- `./api/.env` para o back-end.
- `./app/.env` para o front-end.

## Executando o front-end manualmente

Dentro da pasta `app`:

```bash
npm install
npm run dev
```

Build de producao:

```bash
npm run build
```

Deploy configurado no `package.json`:

```bash
npm run deploy
```

## Executando o back-end manualmente

Dentro da pasta `api`:

```bash
go mod download
go run main.go
```

Comandos auxiliares disponiveis em ambiente de desenvolvimento:

```bash
go run main.go -job setupData
go run main.go -job resetSite
go run main.go -db seed
```

## Deploy

O front-end foi preparado para deploy na Vercel.

Configuração em:

```txt
app/vercel.json
```

A aplicação publicada usa a rota inicial:

```txt
/auth/login
```

URL:

```txt
https://achadinhos-da-ju-front-end.vercel.app/auth/login
```

## Objetivo acadêmico e pessoal

Este projeto foi desenvolvido com dois objetivos principais:

1. Criar uma solução prática para ajudar no gerenciamento das vendas de roupas da minha mãe.
2. Estudar o desenvolvimento e publicação de uma aplicação full stack, incluindo organização de front-end, back-end, banco de dados, Docker e deploy do front-end na Vercel.

## Autor

Gabriel Kochem
> Sinta-se livre em clonar o repositório!
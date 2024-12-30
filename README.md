# Microsserviço de Gerenciamento de Pedidos

Este projeto demonstra uma arquitetura de microsserviços utilizando Python com Flask para o backend, React para o frontend e RabbitMQ para comunicação assíncrona entre serviços. O foco principal é o gerenciamento de pedidos, com um exemplo de integração com um serviço de estoque.

## Arquitetura

A arquitetura consiste nos seguintes componentes:

*   **Backend (Pedido Service):** Responsável por receber requisições de criação de pedidos, persistir os dados no banco de dados PostgreSQL e enviar mensagens para o RabbitMQ.
*   **Frontend (React App):** Interface web para o usuário interagir com o sistema, permitindo a criação de novos pedidos.
*   **RabbitMQ:** Message broker que permite a comunicação assíncrona entre o serviço de pedidos e outros serviços (ex: estoque).
*   **Estoque Service:** Microsserviço de exemplo que consome mensagens do RabbitMQ para atualizar o estoque após a criação de um novo pedido.
*   **PostgreSQL:** Banco de dados relacional utilizado para persistir os dados dos pedidos.

## Tecnologias Utilizadas

*   **Backend:** Python, Flask, Flask-SQLAlchemy, Psycopg2, Gunicorn
*   **Frontend:** React, JavaScript, HTML, CSS
*   **Message Broker:** RabbitMQ
*   **Banco de Dados:** PostgreSQL
*   **Containerização:** Docker, Docker Compose

## Estrutura de Pastas
![]()

## Como Executar

1.  **Pré-requisitos:**
    *   Docker e Docker Compose instalados.
    *   Node.js e npm (ou yarn) instalados para o frontend.

2.  **Clone o repositório:**

    ```bash
    git clone <url_do_seu_repositorio>
    cd microservico-pedidos
    ```

3.  **Executando com Docker Compose:**

    *   Na raiz do projeto, execute:

        ```bash
        docker-compose up -d --build
        ```

        (O `-d` executa em background e o `--build` reconstrói as imagens se houver alterações).

    *   Para parar os containers:

        ```bash
        docker-compose down
        ```

4.  **Acessando a aplicação:**

    *   O frontend estará disponível em `http://localhost:3000`.
    *   A API do backend estará disponível em `http://localhost:5000`.
    *   A interface de gerenciamento do RabbitMQ estará disponível em `http://localhost:15672` (credenciais padrão: `guest/guest`).

## Configuração

*   **Variáveis de Ambiente:** As seguintes variáveis de ambiente podem ser configuradas no arquivo `docker-compose.yml` ou diretamente no sistema:
    *   `DATABASE_URL`: URL de conexão com o banco de dados PostgreSQL (ex: `postgresql://usuario:senha@host:porta/banco_de_dados`).
    *   `RABBITMQ_URL`: URL de conexão com o RabbitMQ (ex: `amqp://usuario:senha@host:porta/%2F`).

## Detalhes de Implementação

*   **Backend (Flask):** Utiliza Flask-SQLAlchemy para interação com o banco de dados e `pika` para comunicação com o RabbitMQ.
*   **Frontend (React):** Utiliza `fetch` para fazer requisições para a API do backend.
*   **Comunicação Assíncrona:** O serviço de pedidos publica mensagens na fila `novos_pedidos` do RabbitMQ após a criação de um novo pedido. O serviço de estoque consome essas mensagens e executa ações correspondentes.
*   **CORS:** A configuração do CORS foi adicionada no backend para permitir requisições do frontend.
*   **Gunicorn:** O backend utiliza Gunicorn para servir a aplicação Flask em produção.

## Próximos Passos

*   Implementar testes unitários e de integração.
*   Adicionar tratamento de erros mais robusto.
*   Implementar autenticação e autorização.
*   Melhorar a interface do frontend.
*   Adicionar mais microsserviços e funcionalidades.

## Contribuição

Contribuições são bem-vindas! Sinta-se à vontade para abrir issues ou enviar pull requests.

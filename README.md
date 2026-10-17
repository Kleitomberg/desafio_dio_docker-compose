# Desafio Docker Compose

Projeto de exemplo do desafio da DIO: configurar um servidor Apache (`httpd`) com Docker Compose e servir uma aplicação web simples.

## Tecnologias

- Docker
- Docker Compose
- Apache HTTP Server (`httpd:alpine`)
- HTML, CSS e JavaScript

## Estrutura do projeto

```text
.
├── docker-compose.yml
└── src/
    ├── index.html
    └── static/
        ├── script/
        │   └── script.js
        └── styles/
            └── style.css
```

## Como executar

É necessário ter o Docker instalado e em execução. No terminal, na pasta do projeto, rode:

```bash
docker compose up -d
```

Abra [http://localhost:8080](http://localhost:8080) no navegador para acessar a aplicação.

Para acompanhar o estado do serviço:

```bash
docker compose ps
```

Para parar e remover o contêiner:

```bash
docker compose down
```

## Como os arquivos chegam ao Apache

No `docker-compose.yml`, o serviço publica a porta `80` do contêiner na porta `8080` do computador e monta a pasta `src` no diretório de conteúdo do Apache:

```yaml
ports:
  - "8080:80"
volumes:
  - ./src:/usr/local/apache2/htdocs:ro
```

`./src` é uma pasta do projeto no computador; `/usr/local/apache2/htdocs` é o diretório que o Apache serve dentro do contêiner. Essa montagem é um *bind mount*: os arquivos não são copiados, e alterações feitas em `src` ficam disponíveis ao Apache. A opção `:ro` significa que o contêiner pode ler os arquivos, mas não alterá-los.

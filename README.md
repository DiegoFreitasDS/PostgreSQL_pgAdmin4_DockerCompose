# PostgreSQL_pgAdmin4_DockerCompose

```

version: '3'

# Script yaml_1
services:
  teste-postgres-compose:         # instância a ser criada
      image: postgres             # Image DockerHub
    environment:                  # configuração (variáveis de ambientes) necessárias para a geração dos 2 containers
      POSTGRES_PASSWORD: "Postgres2019!"
    ports:
      - "15432:5432"
    volumes:                      # indicação do diretório no Ubuntu Desktop em que serão gravados os arquivos de dados
      - /home/renatogroffe/Desenvolvimento/Docker-Compose/PostgreSQL:/var/lib/postgresql/data 
    networks:
      - postgres-compose-network

 # Script yaml_2
  teste-pgadmin-compose:          ## instância a ser criada - container que permitirá a execução do pgAdmin 4     
    image: dpage/pgadmin4         # Image DockerHub
    environment:                  # configuração (variáveis de ambientes) necessárias para a geração dos 2 containers
      PGADMIN_DEFAULT_EMAIL: "renatogroff@yahoo.com.br"
      PGADMIN_DEFAULT_PASSWORD: "PgAdmin2019!"
    ports:
      - "16543:80"
    depends_on:
      - teste-postgres-compose
    networks:
      - postgres-compose-network  # Aqui é por onde acontecerá a comunicação entre os containers teste-pgadmin-compose e teste-postgres-compose.

networks: 
  postgres-compose-network:
    driver: bridge

```
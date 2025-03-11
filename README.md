![alt text](https://hermes.dio.me/articles/cover/f185b791-4256-4e09-af14-e7e69a315485.png)

# PostgreSQL Docker - Ambiente Compartilhado para Desenvolvimento

Este projeto configura um ambiente PostgreSQL otimizado para desenvolvimento local, utilizando um único container acessível por qualquer projeto na máquina host. O objetivo é reduzir o consumo de recursos, evitando a necessidade de múltiplas instâncias do banco de dados para diferentes aplicações.

## 🚀 Características
- **Container Único**: Um único PostgreSQL compartilhado entre todos os projetos locais.
- **Persistência de Dados**: Armazena os dados localmente no diretório `./db`.
- **Acesso Simplificado**: Conexão via `host.docker.internal`, permitindo que qualquer aplicação local utilize o banco.
- **Otimizado para Desenvolvimento**: Baseado na imagem leve `postgres:16-alpine`.
- **Reinício Automático**: O container é reiniciado automaticamente em caso de falha.

## 🔧 Como Usar

### 1️⃣ Clonar o Repositório
Clone o projeto do GitHub:
```sh
git clone https://github.com/igor-rl/postgresql.git
cd postgresql
```

### 2️⃣ Subir o Container
Execute o comando abaixo para iniciar o PostgreSQL:
```sh
docker-compose up -d
```

### 3️⃣ Conectar ao Banco de Dados

#### Via Linha de Comando (psql)
```sh
docker exec -it postgresql psql -U pguser -d postgres
```

#### Em Aplicações Locais
Use a seguinte string de conexão no seu projeto:
```
postgresql://pguser:pgpass@host.docker.internal:5432/postgres
```

### 4️⃣ Configurar `host.docker.internal` no Windows ou no wsl
Se estiver no Windows e `host.docker.internal` não funcionar, siga os passos abaixo:

1. Abra o arquivo de hosts com um editor de texto como administrador:
   - Caminho: `C:\Windows\System32\drivers\etc\hosts`
2. Adicione a seguinte linha ao final do arquivo:
   ```txt
   127.0.0.1 host.docker.internal
   ```
3. Salve o arquivo e feche o editor.

Isso garante que o tráfego local seja corretamente direcionado para o container PostgreSQL.

### 5️⃣ Parar o Container
Para interromper o container sem removê-lo:
```sh
docker-compose stop
```

### 6️⃣ Remover o Container
Caso queira remover o container completamente:
```sh
docker-compose down
```

## 📁 Persistência de Dados
Os dados do PostgreSQL são armazenados no diretório `./db`, garantindo que não sejam perdidos ao reiniciar o container.

Se precisar apagar os dados e começar do zero:
```sh
rm -rf db/*
```

## 🔍 Verificação
Para verificar se o PostgreSQL está rodando corretamente:
```sh
docker ps | grep postgresql
```
Ou teste a conexão com:
```sh
docker exec -it postgresql psql -U pguser -c "SELECT version();"
```

---

Agora seu ambiente de desenvolvimento pode usar um único container PostgreSQL, otimizando recursos e facilitando a conexão entre projetos! 🎯

<div align="center">

[![GitHub](https://img.shields.io/badge/GitHub-Igor_Lage-blue?style=social&logo=github)](https://github.com/igor-rl) 
![Static Badge](https://img.shields.io/badge/11--03--2025-black)


</div>

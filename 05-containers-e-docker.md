# Containers e Docker

## O Que São Containers?

Containers são unidades padronizadas de software que empacotam código, runtime, bibliotecas e dependências juntos. Eles garantem que as aplicações se comportem de forma consistente, independentemente do ambiente onde são executadas.

Containers compartilham o kernel do sistema operacional hospedeiro, tornando-os leves em comparação com máquinas virtuais que requerem instalação completa de sistema operacional.

### Por Que Containers Existem?

O problema clássico que containers resolvem é: **"Funciona na minha máquina!"**

**Antes dos Containers:**
- Aplicações dependiam de configurações específicas do servidor
- Conflitos de versões de bibliotecas e dependências
- Ambientes diferentes entre desenvolvimento, teste e produção
- Tempo de provisionamento de servidores demorado (dias/semanas)

**Com Containers:**
- Ambiente consistente em desenvolvimento, teste e produção
- Isolamento entre aplicações
- Portabilidade entre diferentes plataformas
- Provisionamento rápido (segundos)

---

## Containers vs Máquinas Virtuais

| Aspecto | Containers | Máquinas Virtuais |
|---------|------------|-------------------|
| **Peso** | Leves (MB) | Pesadas (GB) |
| **Startup** | Segundos | Minutos |
| **Isolamento** | Nível de processo | Nível de hardware |
| **SO** | Compartilham kernel do host | SO completo por VM |
| **Densidade** | Centenas por host | Dezenas por host |
| **Performance** | Próxima ao nativo | Overhead de virtualização |

Enquanto containers fornecem isolamento em nível de aplicação, VMs entregam isolamento em nível de hardware.

---

## Docker: A Plataforma de Containerização

Docker é uma plataforma open-source projetada para simplificar o desenvolvimento, implantação e gerenciamento de aplicações. Docker permite que desenvolvedores empacotem aplicações e suas dependências em unidades leves e portáveis chamadas containers.

### Arquitetura do Docker

O Docker Engine é a fundação do Docker, responsável por criar e gerenciar containers. Consiste em três componentes principais: Docker Daemon, Docker CLI e REST API.

**1. Docker Daemon**
- Executa no host machine
- Gerencia ciclo de vida dos containers
- Comunica com Docker CLI

**2. Docker CLI (Command Line Interface)**
- Interface de linha de comando
- Permite interação com Docker
- Comandos para build, run e gerenciar containers

**3. REST API**
- Permite integração programática
- Usado por ferramentas e automações

**4. Docker Hub**
- Registry centralizado
- Desenvolvedores armazenam, compartilham e acessam imagens Docker

---

## Conceitos Fundamentais

### 1. Imagem Docker

Uma **imagem Docker** é um pacote executável leve e standalone que inclui tudo necessário para executar uma aplicação:
- Código da aplicação
- Runtime (Node.js, Python, Java, etc.)
- Bibliotecas e dependências
- Variáveis de ambiente
- Arquivos de configuração

**Características:**
- Imutável (não muda após criação)
- Construída em camadas (layers)
- Pode ser versionada e distribuída

### 2. Container Docker

Um **container** é uma instância em execução de uma imagem Docker. Múltiplos containers podem ser criados a partir da mesma imagem.

**Analogia:**
- Imagem = Receita de bolo
- Container = Bolo assado

### 3. Dockerfile

Um **Dockerfile** é um arquivo de texto que contém instruções para construir uma imagem Docker.

**Exemplo básico de Dockerfile:**

```dockerfile
# Imagem base
FROM node:18-alpine

# Definir diretório de trabalho
WORKDIR /app

# Copiar arquivos de dependências
COPY package*.json ./

# Instalar dependências
RUN npm ci --only=production

# Copiar código da aplicação
COPY . .

# Expor porta
EXPOSE 3000

# Comando para iniciar aplicação
CMD ["node", "server.js"]
```

### 4. Docker Registry

Um **registry** é um repositório onde imagens Docker são armazenadas e distribuídas.

**Registries populares:**
- **Docker Hub**: Registry público e oficial
- **Amazon ECR**: Registry da AWS
- **Google Container Registry (GCR)**: Registry do Google Cloud
- **Azure Container Registry (ACR)**: Registry da Microsoft Azure
- **Harbor**: Registry open-source privado

---

## Comandos Docker Essenciais

### Trabalhando com Imagens

```bash
# Baixar imagem do Docker Hub
docker pull ubuntu:22.04

# Listar imagens locais
docker images

# Construir imagem a partir de Dockerfile
docker build -t minha-app:v1.0 .

# Remover imagem
docker rmi minha-app:v1.0

# Ver histórico de layers de uma imagem
docker history minha-app:v1.0
```

### Trabalhando com Containers

```bash
# Executar container interativo
docker run -it ubuntu:22.04 bash

# Executar container em background (detached)
docker run -d --name meu-nginx -p 8080:80 nginx

# Listar containers em execução
docker ps

# Listar todos os containers (incluindo parados)
docker ps -a

# Parar container
docker stop meu-nginx

# Iniciar container parado
docker start meu-nginx

# Reiniciar container
docker restart meu-nginx

# Remover container
docker rm meu-nginx

# Ver logs do container
docker logs meu-nginx

# Executar comando em container rodando
docker exec -it meu-nginx bash

# Inspecionar detalhes do container
docker inspect meu-nginx

# Ver estatísticas de uso de recursos
docker stats
```

### Gerenciamento de Volumes

```bash
# Criar volume
docker volume create meu-volume

# Listar volumes
docker volume ls

# Executar container com volume montado
docker run -d -v meu-volume:/data nginx

# Remover volume
docker volume rm meu-volume
```

### Redes Docker

```bash
# Listar redes
docker network ls

# Criar rede customizada
docker network create minha-rede

# Executar container em rede específica
docker run -d --network minha-rede --name web nginx

# Inspecionar rede
docker network inspect minha-rede
```

---

## Docker Compose: Orquestrando Múltiplos Containers

Docker Compose é uma ferramenta para definir e executar aplicações Docker multi-container. Simplifica configurações multi-serviços ao permitir que usuários os definam e gerenciem em um único arquivo YAML.

### Exemplo de docker-compose.yml

```yaml
services:
  web:
    image: nginx:alpine
    ports:
      - "8080:80"
    volumes:
      - ./html:/usr/share/nginx/html
    networks:
      - app-network
    depends_on:
      - api
    restart: unless-stopped

  api:
    build: ./api
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
      - DB_HOST=database
      - DB_PORT=5432
    networks:
      - app-network
    depends_on:
      database:
        condition: service_healthy

  database:
    image: postgres:15-alpine
    environment:
      - POSTGRES_USER=admin
      - POSTGRES_PASSWORD=secret
      - POSTGRES_DB=myapp
    volumes:
      - postgres-data:/var/lib/postgresql/data
    networks:
      - app-network
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U admin"]
      interval: 10s
      timeout: 5s
      retries: 5

networks:
  app-network:
    driver: bridge

volumes:
  postgres-data:
```

### Comandos Docker Compose

```bash
# Iniciar todos os serviços
docker compose up -d

# Parar todos os serviços
docker compose down

# Ver logs de todos os serviços
docker compose logs -f

# Listar serviços rodando
docker compose ps

# Executar comando em serviço específico
docker compose exec web sh

# Reconstruir e reiniciar serviços
docker compose up -d --build

# Escalar serviço horizontalmente
docker compose up -d --scale api=3
```

---

## Melhores Práticas de Docker (2024-2025)

### 1. Use Imagens Base Oficiais e Minimalistas

Use imagens base oficiais e verificadas do Docker Hub que são testadas e aprovadas como estáveis e seguras. Evite usar imagens de fontes desconhecidas, pois podem ser maliciosas e não confiáveis.

** Evite:**
```dockerfile
FROM ubuntu:latest
```

**Prefira:**
```dockerfile
FROM node:18-alpine
# ou
FROM python:3.12-slim
```

Empresas que implementam multi-stage builds reportam redução média de 50-85% no tamanho de imagens.

### 2. Multi-Stage Builds

Multi-stage builds permitem criar imagens de produção leves usando estágios separados de build e runtime.

```dockerfile
# Estágio de Build
FROM node:20 AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Estágio de Produção
FROM node:20-slim
WORKDIR /app
COPY --from=build /app/dist ./dist
COPY --from=build /app/package*.json ./
RUN npm install --only=production
EXPOSE 3000
CMD ["npm", "start"]
```

### 3. Não Execute Containers como Root

Uma pesquisa da Sysdig descobriu que 58% dos containers de produção ainda executam como root, criando exposições significativas de segurança.

** Inseguro:**
```dockerfile
FROM node:18
# Código roda como root
CMD ["node", "app.js"]
```

** Seguro:**
```dockerfile
FROM node:18-alpine

# Criar usuário não-root
RUN addgroup -g 1001 -S nodejs && \
    adduser -S nodejs -u 1001

# Definir ownership dos arquivos
WORKDIR /app
COPY --chown=nodejs:nodejs . .

# Trocar para usuário não-root
USER nodejs

CMD ["node", "app.js"]
```

### 4. Use .dockerignore

Incluir arquivos desnecessários como .git, node_modules e .env aumenta o tamanho da imagem e expõe secrets.

**Exemplo de .dockerignore:**
```
node_modules
npm-debug.log
.git
.gitignore
.env
.env.local
*.md
.vscode
.idea
coverage
dist
```

### 5. Minimize o Número de Layers

Docker utiliza cache de layers para builds mais rápidos. A ordem apropriada de comandos é crucial: coloque comandos que mudam com menos frequência no topo.

** Muitas layers:**
```dockerfile
RUN apt-get update
RUN apt-get install -y curl
RUN apt-get install -y git
```

** Layers otimizadas:**
```dockerfile
RUN apt-get update && \
    apt-get install -y curl git && \
    rm -rf /var/lib/apt/lists/*
```

### 6. Implemente Health Checks

Sem health checks, Docker não pode detectar falhas de serviço.

```dockerfile
HEALTHCHECK --interval=30s --timeout=10s --retries=3 \
  CMD curl -f http://localhost:3000/health || exit 1
```

**No docker-compose.yml:**
```yaml
healthcheck:
  test: ["CMD", "curl", "-f", "http://localhost:3000/health"]
  interval: 30s
  timeout: 10s
  retries: 3
```

### 7. Scanning de Segurança

Ferramentas conhecidas como Trivy, Clair e o comando docker scan tornam mais fácil encontrar vulnerabilidades conhecidas em imagens base e dependências. Um estudo de 2024 descobriu que 87% das imagens Docker contêm pelo menos uma vulnerabilidade alta ou crítica.

```bash
# Escanear imagem com Trivy
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock \
  aquasec/trivy image minha-app:latest

# Docker Scout (built-in)
docker scout cves minha-app:latest
```

### 8. Gerencie Secrets com Segurança

** NUNCA faça isso:**
```dockerfile
ENV API_KEY=abc123secret
```

** Use Docker Secrets ou variáveis de ambiente:**
```bash
# Passar secret via variável de ambiente
docker run -e API_KEY=$API_KEY minha-app

# Usar Docker Secrets (em Swarm/Kubernetes)
echo "secret_value" | docker secret create api_key -
```

### 9. Limite Recursos

```dockerfile
# No docker-compose.yml
services:
  app:
    image: minha-app
    deploy:
      resources:
        limits:
          cpus: '0.5'
          memory: 512M
        reservations:
          cpus: '0.25'
          memory: 256M
```

### 10. Use Tags Específicas, Não 'latest'

** Evite:**
```dockerfile
FROM node:latest
```

** Seja específico:**
```dockerfile
FROM node:18.19.0-alpine3.19
```

---

## Networking em Docker

### Tipos de Redes

**1. Bridge (Padrão)**
- Rede privada interna
- Containers podem se comunicar entre si
- Isolado da rede do host

**2. Host**
- Container usa a rede do host diretamente
- Sem isolamento de rede
- Melhor performance

**3. None**
- Sem conectividade de rede
- Container completamente isolado

**4. Overlay**
- Permite comunicação entre containers em diferentes hosts
- Usado em Docker Swarm e Kubernetes

### Exemplo de Comunicação Entre Containers

```yaml
services:
  frontend:
    image: nginx
    networks:
      - app-network
    ports:
      - "80:80"

  backend:
    image: node:18
    networks:
      - app-network
    # Frontend pode acessar backend via http://backend:3000

networks:
  app-network:
    driver: bridge
```

---

## Volumes e Persistência de Dados

### Tipos de Volumes

**1. Named Volumes (Recomendado para produção)**
```bash
docker volume create meu-volume
docker run -v meu-volume:/data nginx
```

**2. Bind Mounts (Útil para desenvolvimento)**
```bash
docker run -v $(pwd)/src:/app/src node:18
```

**3. tmpfs (Armazenamento temporário em memória)**
```bash
docker run --tmpfs /tmp nginx
```

### Exemplo Prático

```yaml
services:
  database:
    image: postgres:15
    volumes:
      # Named volume (persistente)
      - db-data:/var/lib/postgresql/data
      # Bind mount (configuração)
      - ./init.sql:/docker-entrypoint-initdb.d/init.sql:ro
      # tmpfs (temporário)
      - type: tmpfs
        target: /tmp

volumes:
  db-data:
    driver: local
```

---

## Tendências Docker 2024-2025

### 1. BuildKit e Build Cache

Docker Desktop 4.6+ trouxe melhorias significativas de performance com VirtioFS e BuildKit.

```dockerfile
# syntax=docker/dockerfile:1
FROM node:18 AS base

# Aproveitar cache de dependências
FROM base AS deps
COPY package*.json ./
RUN --mount=type=cache,target=/root/.npm \
    npm ci --only=production
```

### 2. Docker Init

Docker Init inicializa Dockerfiles e arquivos Compose com um único comando CLI.

```bash
# Gerar Dockerfile automaticamente
docker init

# Seguir wizard interativo para configurar projeto
```

### 3. Testcontainers

Testcontainers permite criar bancos de dados reais, message brokers ou qualquer serviço que sua aplicação interage, tudo dentro da suite de testes.

### 4. Distroless Images

Imagens leves como distroless e alpine são mais amplamente adotadas.

```dockerfile
# Usar imagem distroless do Google
FROM gcr.io/distroless/nodejs18-debian12
COPY --from=build /app /app
CMD ["server.js"]
```

### 5. Docker Desktop Extensions

Extensões que melhoram produtividade:
- **Lens**: Gerenciamento de Kubernetes
- **Portainer**: Interface gráfica para Docker
- **Disk usage**: Análise de uso de espaço

---

## Quando Usar Docker?

### Use Docker Quando

- Precisa de ambientes consistentes entre dev/test/prod
- Quer isolar aplicações e dependências
- Precisa escalar aplicações rapidamente
- Quer facilitar CI/CD
- Trabalha com microservices
- Precisa de portabilidade entre clouds

### Considere Alternativas Quando

- Aplicação tem requisitos de performance extremamente altos
- Aplicação precisa de acesso direto ao hardware
- Aplicação é monolítica legada muito acoplada ao SO
- Equipe não tem experiência com containers

---

## Alternativas ao Docker

Docker é excelente para rodar e gerenciar containers individuais, mas tipicamente depende de ferramentas adicionais para orquestração em larga escala.

**Para execução de containers:**
- **Podman**: Alternativa daemonless ao Docker
- **Containerd**: Runtime de containers usado pelo Kubernetes
- **CRI-O**: Runtime otimizado para Kubernetes

**Para orquestração:**
- **Kubernetes**: Padrão da indústria
- **Docker Swarm**: Orquestração nativa do Docker
- **Nomad**: Orquestrador da HashiCorp

---

## Checklist de Produção

- [ ] Usar imagens base oficiais e minimalistas
- [ ] Implementar multi-stage builds
- [ ] Executar containers como usuário não-root
- [ ] Adicionar .dockerignore apropriado
- [ ] Implementar health checks
- [ ] Escanear imagens por vulnerabilidades
- [ ] Usar tags específicas (não 'latest')
- [ ] Limitar recursos (CPU/memória)
- [ ] Implementar logging estruturado
- [ ] Configurar restart policies
- [ ] Usar volumes nomeados para dados persistentes
- [ ] Documentar variáveis de ambiente
- [ ] Testar imagens localmente
- [ ] Implementar monitoring e observabilidade

---

## Recursos para Aprendizado

**Documentação Oficial:**
- [docs.docker.com](https://docs.docker.com)
- [Docker Hub](https://hub.docker.com)

**Cursos Recomendados:**
- Docker Fundamentals (Linux Foundation)
- Docker for Developers (Udemy)
- Play with Docker (hands-on)

**Comunidade:**
- Docker Community Slack
- Stack Overflow (tag: docker)
- r/docker (Reddit)

---

## Conclusão

Docker revolucionou a forma como desenvolvemos e implantamos aplicações. Containers oferecem portabilidade, consistência e eficiência que VMs tradicionais não conseguem igualar. Com as melhores práticas modernas de 2024-2025, você pode construir imagens seguras, leves e eficientes.

**Principais Aprendizados:**

1. Containers isolam aplicações e suas dependências
2. Docker simplifica criação e distribuição de containers
3. Imagens devem ser leves, seguras e bem documentadas
4. Multi-stage builds reduzem drasticamente tamanho de imagens
5. Nunca execute containers como root em produção
6. Docker Compose facilita orquestração local
7. Security scanning é obrigatório para produção
8. Kubernetes é o próximo passo natural após dominar Docker
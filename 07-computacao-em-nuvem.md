# Computação em Nuvem

## O Que é Cloud Computing?

Computação em nuvem é a entrega de serviços de computação - incluindo servidores, armazenamento, bancos de dados, redes, software, análise e inteligência - pela Internet ("a nuvem") para oferecer inovação mais rápida, recursos flexíveis e economias de escala.

Em 2024, gastos globais em tecnologia cloud foram projetados para atingir $675 bilhões, subindo de $561 bilhões em 2023. Até 2025, espera-se que metade dos dados mundiais resida em ambientes cloud.

### Por Que Cloud Computing?

**Antes da Nuvem:**
- Hardware físico caro e subutilizado
- Provisionamento lento (semanas/meses)
- Custos fixos independente do uso
- Manutenção complexa de data centers
- Escalabilidade limitada

**Com a Nuvem:**
- Pague apenas pelo que usar
- Provisionamento em minutos
- Escalabilidade elástica
- Sem manutenção de hardware
- Alcance global instantâneo

---

## Modelos de Serviço Cloud

### IaaS - Infrastructure as a Service (Infraestrutura como Serviço)

**O que é:** Você aluga infraestrutura virtual - acesso a recursos computacionais como VMs, armazenamento e redes, mas você gerencia o SO, runtime e aplicações em cima disso.

**🛠️ Você gerencia:** SO, runtime, configuração de aplicação  
**☁️ Provedor gerencia:** Hardware, virtualização, armazenamento e rede

**Exemplo:** Lançar uma instância EC2 na AWS ou uma Azure VM onde você instala e configura sua própria stack de software.

**Casos de Uso:**
- Migração lift-and-shift de aplicações on-premise
- Ambientes de desenvolvimento e teste
- Hosting de websites
- Armazenamento e backup
- Computação de alta performance (HPC)

**Provedores Principais:**
- AWS EC2, S3
- Azure Virtual Machines
- Google Compute Engine
- DigitalOcean Droplets

**📈 Por que importa:** Fundamentos de IaaS são cruciais para engenheiros de suporte cloud, sysadmins e arquitetos de soluções. Dominar VMs, security groups, storage e networking é essencial em muitos trabalhos cloud.

### PaaS - Platform as a Service (Plataforma como Serviço)

**O que é:** Faça deploy de código sem gerenciar infraestrutura - o provedor cloud cuida do SO, middleware e runtime. Você gerencia apenas o código da aplicação e dados.

**🛠️ Você gerencia:** Código da aplicação, dados  
**☁️ Provedor gerencia:** SO, runtime, middleware, escalabilidade

**Exemplo:** Use AWS Elastic Beanstalk, Google App Engine ou Azure App Services para fazer deploy de aplicações.

**Casos de Uso:**
- Desenvolvimento de aplicações web
- APIs e microservices
- Aplicações mobile backend
- Processamento de dados
- Desenvolvimento ágil e DevOps

**Provedores Principais:**
- AWS Elastic Beanstalk
- Google App Engine
- Azure App Services
- Heroku
- Cloud Foundry

**📈 Por que importa:** PaaS acelera desenvolvimento permitindo que desenvolvedores foquem em código, não em infraestrutura. Ideal para startups e times que querem mover rápido.

### SaaS - Software as a Service (Software como Serviço)

**O que é:** Aplicações completas entregues pela internet. Você apenas usa o software, tudo mais é gerenciado pelo provedor.

**🛠️ Você gerencia:** Configurações e dados do usuário  
**☁️ Provedor gerencia:** Tudo (aplicação, dados, runtime, middleware, SO, infraestrutura)

**Exemplos:**
- **Google Workspace** (Gmail, Docs, Drive)
- **Microsoft 365** (Outlook, Word, Excel)
- **Salesforce** (CRM)
- **Slack** (comunicação)
- **Zoom** (videoconferência)

**📈 Por que importa:** SaaS é onipresente. A maioria das empresas usa dezenas de aplicações SaaS diariamente. Entender este modelo ajuda na integração e automação.

### Comparação dos Modelos

| Camada | IaaS | PaaS | SaaS |
|--------|------|------|------|
| **Aplicação** | Você gerencia | Você gerencia | Provedor gerencia |
| **Dados** | Você gerencia | Você gerencia | Provedor gerencia |
| **Runtime** | Você gerencia | Provedor gerencia | Provedor gerencia |
| **Middleware** | Você gerencia | Provedor gerencia | Provedor gerencia |
| **SO** | Você gerencia | Provedor gerencia | Provedor gerencia |
| **Virtualização** | Provedor gerencia | Provedor gerencia | Provedor gerencia |
| **Servidores** | Provedor gerencia | Provedor gerencia | Provedor gerencia |
| **Armazenamento** | Provedor gerencia | Provedor gerencia | Provedor gerencia |
| **Rede** | Provedor gerencia | Provedor gerencia | Provedor gerencia |

---

## Principais Provedores Cloud (2024-2025)

Segundo o Synergy Research Group Q3 2025, AWS, Microsoft Azure e Google Cloud juntos representam cerca de 66% do mercado.

### Amazon Web Services (AWS)

**Participação de Mercado:** 29% (Q3 2025) - Líder de mercado  
**Lançamento:** 2006  
**Data Centers:** 200+ data centers, 100+ zonas de disponibilidade, 30+ regiões geográficas

**Pontos Fortes:**
- Maior catálogo de serviços (200+)
- Alcance global mais amplo
- Ecossistema maduro e ferramentas
- Melhor para early adopters e startups tech
- Forte em machine learning e IA

**Serviços Principais:**

**Computação:**
- EC2 (Elastic Compute Cloud): VMs escaláveis
- Lambda: Computação serverless
- ECS/EKS: Container orchestration
- Lightsail: VPS simplificado

**Armazenamento:**
- S3 (Simple Storage Service): Object storage
- EBS (Elastic Block Storage): Block storage para EC2
- EFS (Elastic File System): File storage compartilhado

**Banco de Dados:**
- RDS: Banco relacional gerenciado (MySQL, PostgreSQL, etc.)
- DynamoDB: NoSQL serverless
- Aurora: MySQL/PostgreSQL compatível de alta performance
- Redshift: Data warehouse

**Redes:**
- VPC: Virtual Private Cloud
- Route 53: DNS gerenciado
- CloudFront: CDN global
- API Gateway: Gerenciamento de APIs

**Melhor para:** Empresas estabelecidas com necessidades cloud diversas e complexas, escalabilidade global e amplo portfólio de workloads.

### Microsoft Azure

**Participação de Mercado:** 20% (Q3 2025)  
**Lançamento:** 2010  
**Data Centers:** 300+ data centers, 60+ regiões

**Pontos Fortes:**
- Integração perfeita com ecossistema Microsoft
- Melhor para empresas com investimento em Microsoft stack
- Forte em soluções híbridas (Azure Arc, Azure Stack)
- Excelente para enterprise e compliance
- Líder em serviços de identidade (Active Directory)

**Serviços Principais:**

**Computação:**
- Virtual Machines: Máquinas virtuais
- Azure Functions: Serverless
- AKS (Azure Kubernetes Service): Kubernetes gerenciado
- Azure Container Instances: Containers sem orquestração

**Armazenamento:**
- Blob Storage: Object storage
- Azure Files: File storage SMB
- Azure Disk Storage: Block storage

**Banco de Dados:**
- Azure SQL Database: SQL Server gerenciado
- Cosmos DB: NoSQL multi-modelo distribuído globalmente
- Azure Database for PostgreSQL/MySQL

**Integrações:**
- Office 365, Active Directory
- Windows Server, SQL Server
- Power BI, Dynamics 365

**Melhor para:** Organizações fortemente investidas no ecossistema Microsoft e aquelas adotando ambientes híbridos cloud ou aplicações enterprise-level.

### Google Cloud Platform (GCP)

**Participação de Mercado:** 13% (Q3 2025)  
**Lançamento:** 2008  
**Foco:** AI/ML, Data Analytics, Kubernetes

**Pontos Fortes:**
- Melhor para projetos pesados em IA/ML
- Líder em análise de dados (BigQuery)
- Berço do Kubernetes (GKE)
- Rede global de alta performance
- Preços competitivos e uso sustentado

**Serviços Principais:**

**Computação:**
- Compute Engine: VMs
- Cloud Functions: Serverless
- GKE (Google Kubernetes Engine): Kubernetes gerenciado (o melhor da indústria)
- Cloud Run: Containers serverless

**Armazenamento:**
- Cloud Storage: Object storage
- Persistent Disk: Block storage

**Banco de Dados:**
- Cloud SQL: MySQL/PostgreSQL gerenciado
- Firestore: NoSQL document database
- Cloud Spanner: Banco relacional distribuído globalmente
- BigQuery: Data warehouse e analytics

**IA/ML:**
- Vertex AI: Plataforma unificada de ML
- TensorFlow: Framework de ML (open-source)
- AutoML: Machine learning automatizado

**Melhor para:** Empresas focadas em AI/ML, data analytics e aplicações cloud-native. GCP brilha para workloads de dados e IA.

### Comparação AWS vs Azure vs GCP

| Critério | AWS | Azure | GCP |
|----------|-----|-------|-----|
| **Mercado** | 29% (Líder) | 20% | 13% |
| **Força** | Maior catálogo | Microsoft ecosystem | AI/ML e dados |
| **Preço** | Médio | Médio-Alto | Competitivo |
| **Learning Curve** | Média | Média | Mais fácil |
| **Certificações** | Mais procuradas | Crescente demanda | Nicho técnico |
| **Melhor para** | Diversidade de workloads | Empresas Microsoft | Data-heavy apps |

---

## Conceitos Fundamentais de Cloud

### 1. Regiões e Zonas de Disponibilidade

**Região:** Área geográfica com múltiplos data centers.

**Zona de Disponibilidade (AZ):** Data centers isolados dentro de uma região com alimentação, rede e conectividade redundantes.

**Por que importa:**
- **Alta Disponibilidade:** Distribuir aplicações em múltiplas AZs
- **Latência:** Escolher região próxima aos usuários
- **Compliance:** Alguns dados devem permanecer em regiões específicas

**Exemplo AWS:**
- Região: `us-east-1` (Virginia)
- AZs: `us-east-1a`, `us-east-1b`, `us-east-1c`

### 2. Auto Scaling

Ajustar automaticamente capacidade de computação baseado em demanda.

**Horizontal Scaling:** Adicionar mais instâncias  
**Vertical Scaling:** Aumentar recursos de instância existente

**Exemplo:**
```yaml
# AWS Auto Scaling Group
MinSize: 2
MaxSize: 10
DesiredCapacity: 4
ScalingPolicy:
  TargetCPUUtilization: 70%
```

### 3. Load Balancing

Distribuir tráfego de entrada entre múltiplos servidores.

**Tipos:**
- **Application Load Balancer (Layer 7):** HTTP/HTTPS
- **Network Load Balancer (Layer 4):** TCP/UDP
- **Gateway Load Balancer:** Firewalls virtuais

### 4. Identity and Access Management (IAM)

Controlar quem pode acessar quais recursos.

**Princípios:**
- **Least Privilege:** Dar apenas permissões necessárias
- **MFA (Multi-Factor Authentication):** Adicionar camada extra de segurança
- **Rotation:** Rotacionar credenciais regularmente

**Exemplo de Policy (AWS IAM):**
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:GetObject", "s3:ListBucket"],
      "Resource": "arn:aws:s3:::meu-bucket/*"
    }
  ]
}
```

### 5. Virtual Private Cloud (VPC)

Rede isolada logicamente onde você lança recursos cloud.

**Componentes:**
- **Subnets:** Segmentos de rede (públicas/privadas)
- **Route Tables:** Controlar tráfego de rede
- **Internet Gateway:** Conectar VPC à internet
- **NAT Gateway:** Permitir recursos privados acessar internet
- **Security Groups:** Firewall virtual para instâncias

---

## Kubernetes: Orquestração de Containers na Nuvem

### O Que é Kubernetes?

Kubernetes (K8s) é um sistema open-source para automação de deployment, scaling e gerenciamento de aplicações containerizadas. É o padrão da indústria para orquestração de containers.

Segundo Gartner, até 2026, mais de 90% das organizações globais executarão aplicações containerizadas em produção (acima de menos de 40% em 2020). Até 2025, mais de 95% de novos workloads serão implantados em plataformas cloud-native.

### Por Que Kubernetes?

**Desafios sem Kubernetes:**
- Gerenciar centenas de containers manualmente
- Garantir alta disponibilidade
- Escalar baseado em demanda
- Service discovery e load balancing
- Rollouts e rollbacks de deploys

**Com Kubernetes:**
- Orquestração automatizada
- Self-healing (reiniciar containers falhados)
- Auto-scaling horizontal
- Service discovery automático
- Rollouts controlados com zero downtime

### Arquitetura Kubernetes

**Control Plane (Master):**
- **API Server:** Ponto de entrada para todos os comandos
- **etcd:** Banco de dados chave-valor que armazena estado do cluster
- **Scheduler:** Decide em qual node executar pods
- **Controller Manager:** Monitora estado e faz correções

**Worker Nodes:**
- **Kubelet:** Agente que roda em cada node
- **Container Runtime:** Docker, containerd, CRI-O
- **Kube-proxy:** Gerencia rede e load balancing

### Conceitos Kubernetes Essenciais

**1. Pod**
- Menor unidade implantável
- Grupo de um ou mais containers

**2. Deployment**
- Define como aplicação deve ser implantada
- Gerencia replicação e atualizações

**3. Service**
- Abstração que expõe aplicação rodando em pods
- Load balancing automático

**4. Namespace**
- Isolamento virtual dentro do cluster
- Organizar recursos por projeto/ambiente

### Exemplo de Deployment Kubernetes

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.25
        ports:
        - containerPort: 80
        resources:
          requests:
            memory: "128Mi"
            cpu: "250m"
          limits:
            memory: "256Mi"
            cpu: "500m"
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
  type: LoadBalancer
```

### Kubernetes Gerenciado (Managed Services)

**AWS EKS (Elastic Kubernetes Service)**
- Kubernetes gerenciado pela AWS
- Integração profunda com serviços AWS
- Fargate para pods serverless

**Azure AKS (Azure Kubernetes Service)**
- Kubernetes gerenciado pela Microsoft
- Integração com Azure DevOps
- Virtual nodes para escalabilidade elástica

**Google GKE (Google Kubernetes Engine)**
- Considerado o melhor Kubernetes gerenciado
- Autopilot mode para operações zero
- Integração nativa (Google criou K8s)

### Comandos kubectl Básicos

```bash
# Ver nodes do cluster
kubectl get nodes

# Listar pods
kubectl get pods

# Criar deployment
kubectl apply -f deployment.yaml

# Ver logs de pod
kubectl logs nginx-deployment-xxx

# Executar comando em pod
kubectl exec -it nginx-deployment-xxx -- bash

# Escalar deployment
kubectl scale deployment nginx-deployment --replicas=5

# Ver status de rollout
kubectl rollout status deployment nginx-deployment

# Fazer rollback
kubectl rollout undo deployment nginx-deployment

# Deletar recursos
kubectl delete -f deployment.yaml
```

---

## Serverless Computing

### O Que é Serverless?

Modelo onde você executa código sem gerenciar servidores. Você paga apenas pelo tempo de execução.

**Características:**
- Sem gerenciamento de servidores
- Auto-scaling automático
- Pay-per-use (milissegundos)
- Event-driven

### AWS Lambda

```python
# Função Lambda simples
def lambda_handler(event, context):
    name = event.get('name', 'World')
    return {
        'statusCode': 200,
        'body': f'Hello, {name}!'
    }
```

**Gatilhos Comuns:**
- API Gateway (HTTP requests)
- S3 (upload de arquivo)
- DynamoDB (mudança em tabela)
- EventBridge (eventos agendados)
- SQS (mensagens em fila)

### Alternativas Serverless

- **Azure Functions:** Serverless da Microsoft
- **Google Cloud Functions:** Serverless do Google
- **Cloud Run:** Containers serverless (GCP)
- **AWS Fargate:** Containers serverless

---

## Cloud-Native Architecture

### Microservices

Aplicação construída como coleção de serviços pequenos e independentes.

**Benefícios:**
- Desenvolvimento e deploy independentes
- Escalabilidade granular
- Isolamento de falhas
- Tecnologias diversas (polyglot)

**Desafios:**
- Complexidade operacional
- Comunicação entre serviços
- Distributed tracing
- Data consistency

### Service Mesh

Camada de infraestrutura para gerenciar comunicação entre microservices.

**Populares:**
- **Istio:** Service mesh mais completo
- **Linkerd:** Leve e fácil
- **Consul:** Da HashiCorp

**Recursos:**
- Traffic management
- Security (mTLS)
- Observability
- Circuit breaking

---

## FinOps: Otimização de Custos Cloud

FinOps (Financial Operations) otimiza custos em cloud unindo finanças, engenharia e negócios.

### Práticas de Otimização

**1. Right-Sizing**
- Ajustar tamanho de instâncias baseado em uso real
- AI pode automatizar (AWS Compute Optimizer, Azure Advisor)

**2. Reserved Instances / Savings Plans**
- Comprometer uso de 1-3 anos para 40-70% de desconto

**3. Spot Instances**
- Usar capacidade não utilizada com até 90% de desconto
- Workloads tolerantes a interrupções

**4. Auto Scaling**
- Desligar recursos fora do horário comercial
- Escalar baseado em demanda real

**5. Storage Lifecycle**
- Mover dados antigos para tiers mais baratos
- S3 Glacier, Azure Archive

**6. Monitoramento de Custos**
- AWS Cost Explorer
- Azure Cost Management
- Google Cloud Billing
- Ferramentas terceiras (CloudHealth, CloudCheckr)

---

## Certificações Cloud (2024-2025)

### AWS Certifications

**Iniciante:**
- ☁️ AWS Certified Cloud Practitioner (CLF-C02)

**Associado:**
- ☁️ Solutions Architect Associate (SAA-C03)
- 💻 Developer Associate (DVA-C02)
- ⚙️ SysOps Administrator Associate (SOA-C02)

**Profissional:**
- 🏆 Solutions Architect Professional
- 🏆 DevOps Engineer Professional (DOP-C02)

### Azure Certifications

**Iniciante:**
- ☁️ Azure Fundamentals (AZ-900)

**Associado:**
- ⚙️ Azure Administrator Associate (AZ-104)
- 💻 Azure Developer Associate (AZ-204)
- 🔒 Azure Security Engineer Associate (AZ-500)

**Expert:**
- 🏆 Azure Solutions Architect Expert (AZ-305)
- 🏆 Azure DevOps Engineer Expert (AZ-400)

### GCP Certifications

**Iniciante:**
- ☁️ Cloud Digital Leader

**Associado:**
- ⚙️ Associate Cloud Engineer

**Profissional:**
- 🏆 Professional Cloud Architect
- 🏆 Professional Cloud DevOps Engineer
- 🏆 Professional Data Engineer
- 🏆 Professional Machine Learning Engineer

### Recomendação de Carreira

**Iniciantes:** Comece com AWS (maior mercado) ou Azure (se já trabalha com Microsoft)

**Intermediário:** AWS Solutions Architect Associate + Terraform Associate

**Avançado:** Kubernetes (CKA), AWS/Azure DevOps Engineer, GCP Cloud Architect

**Multi-cloud:** Priorize Terraform e Kubernetes para habilidades transferíveis

---

## Cloud vs On-Premise: Quando Usar Cada Um?

### Use Cloud Quando

✅ Startup ou crescimento rápido  
✅ Workloads com demanda variável  
✅ Precisa de alcance global  
✅ Quer evitar CAPEX (capital expenditure)  
✅ Precisa de inovação rápida  
✅ Não tem time de infraestrutura grande

### Use On-Premise Quando

✅ Requisitos de compliance muito estritos  
✅ Dados extremamente sensíveis  
✅ Workloads muito previsíveis e estáveis  
✅ Já tem infraestrutura amortizada  
✅ Custos de transferência de dados seriam proibitivos

### Modelo Híbrido

Melhor dos dois mundos:
- Dados sensíveis on-premise
- Aplicações e analytics na cloud
- Burst para cloud em picos de demanda

---

## Tendências Cloud 2025

### 1. AI/ML Nativo em Cloud

Provedores integram IA profundamente em serviços (Azure Copilot, AWS AI services, Vertex AI).

### 2. Edge Computing

Processar dados próximo à origem para baixa latência (AWS Greengrass, Azure Stack Edge).

### 3. Multi-Cloud e Hybrid Cloud

Evitar vendor lock-in usando múltiplos provedores.

### 4. Green Cloud

Otimização de custos alinha com sustentabilidade (GCP embute predictive scaling).

### 5. Platform Engineering

Criar plataformas internas que abstraem complexidade cloud para desenvolvedores.

---

## Checklist de Migração para Cloud

**Planejamento:**
- [ ] Avaliar aplicações atuais
- [ ] Definir estratégia (lift-and-shift, refactor, rebuild)
- [ ] Calcular TCO (Total Cost of Ownership)
- [ ] Escolher provedor cloud

**Segurança:**
- [ ] Definir policies IAM
- [ ] Configurar MFA
- [ ] Implementar encryption (em trânsito e repouso)
- [ ] Configurar backup e disaster recovery

**Rede:**
- [ ] Desenhar arquitetura VPC
- [ ] Configurar subnets públicas/privadas
- [ ] Implementar NAT e Internet Gateway
- [ ] Configurar VPN ou Direct Connect

**Governança:**
- [ ] Implementar tagging de recursos
- [ ] Configurar alertas de custos
- [ ] Definir processo de aprovação
- [ ] Documentar arquitetura

**Operações:**
- [ ] Configurar monitoring e logging
- [ ] Implementar auto-scaling
- [ ] Configurar CI/CD
- [ ] Treinar equipe

---

## Conclusão

Cloud computing transformou como construímos e operamos sistemas. De startups a empresas Fortune 500, cloud oferece agilidade, escalabilidade e inovação que infraestrutura tradicional não consegue igualar.

**Principais Aprendizados:**

1. IaaS, PaaS e SaaS oferecem diferentes níveis de abstração
2. AWS lidera mercado, Azure domina enterprise, GCP brilha em AI/ML
3. Kubernetes tornou-se padrão para orquestração de containers
4. Serverless permite focar em código, não infraestrutura
5. FinOps é essencial para otimizar custos cloud
6. Multi-cloud e híbrido oferecem flexibilidade
7. Certificações validam conhecimento e abrem portas
8. Cloud é skill fundamental para DevOps moderno
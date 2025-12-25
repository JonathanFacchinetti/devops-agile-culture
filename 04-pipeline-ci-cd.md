# Guia Completo de Pipeline CI/CD

## O Que é um Pipeline de CI/CD?

Um pipeline de CI/CD é uma série de etapas automatizadas que otimizam o processo de entrega de software. Por meio de uma abordagem DevOps ou da Engenharia de Confiabilidade de Site (SRE), a CI/CD melhora o desenvolvimento de aplicações usando monitoramento e automação.

Pipelines automatizados podem ajudar a prevenir erros decorrentes de processos manuais, permitir iterações rápidas do produto e proporcionar feedback uniforme durante o processo de desenvolvimento. Cada etapa de um pipeline de CI/CD é um subconjunto de tarefas agrupadas em estágios do pipeline.

---

## Comparação: CI vs CD (Delivery) vs CD (Deployment)

### Integração Contínua (CI - Continuous Integration)

No dinâmico cenário tecnológico atual, as equipes de desenvolvimento precisam ser capazes de trabalhar simultaneamente em diferentes elementos de uma aplicação. Se a equipe de engenharia tiver que esperar até o dia do merge para integrar as alterações de volta ao branch principal, o trabalho resultante será demorado, muito complexo e entediante.

Ao implementar a CI, você faz merge continuamente das alterações em um repositório central com a maior frequência possível. As alterações são validadas por uma compilação automatizada, com testes unitários e de integração garantindo que as alterações feitas não tenham causado problemas no aplicativo.

#### Requisitos

- Testes automatizados para melhorias, novos recursos e correções de bugs
- Mesclar alterações com a maior frequência possível, de preferência uma vez por dia
- Um servidor de integração contínua para monitorar o repositório e executar testes em novos commits

#### Benefícios

- Testes automatizados detectam regressões precocemente, então menos bugs chegam à produção
- Problemas de integração são resolvidos rapidamente, facilitando a criação do lançamento
- Desenvolvedores trocam menos de contexto porque são alertados sobre bugs assim que interrompem a compilação
- Os servidores de CI executam centenas de testes em segundos, reduzindo os custos de teste

### Entrega Contínua (CD - Continuous Delivery)

A entrega contínua amplia os princípios da CI ao automatizar o provisionamento da infraestrutura e a implantação da aplicação nos ambientes de teste e produção.

Em um pipeline de entrega contínua, as alterações de código são automaticamente compiladas, testadas e empacotadas de maneira que permitem sua implantação em qualquer ambiente a qualquer momento. Ele pode ser usado para acionar **manualmente** implantações, ou estendido para incluir a implantação contínua.

#### Requisitos

- Controle de versão para todos os arquivos de código e configuração
- Um ambiente de staging/preparo para testar novas versões do software
- Um processo de implantação automatizado e confiável

#### Benefícios

- Entrega mais rápida de novos recursos e atualizações para clientes
- Melhoria na confiabilidade e qualidade dos lançamentos de software
- Facilidade de reversão de alterações de código, se necessário
- Redução do risco de erros humanos no processo de implantação
- Aumento da colaboração entre equipes de desenvolvimento e operações

### Implantação Contínua (CD - Continuous Deployment)

A implantação contínua é a etapa final de um pipeline de CI/CD. As alterações de código são lançadas **automaticamente** para os usuários finais após a conclusão de testes pré-definidos. Não há um processo manual de revisão antes da produção, por isso é essencial ter uma automação de testes robusta e à prova de falhas.

Para os desenvolvedores, isso significa que as alterações em aplicações na nuvem podem ser implementadas rapidamente, facilitando o recebimento e a resposta ao feedback dos usuários finais.

#### Requisitos

- Um conjunto de testes de alta qualidade e abrangente
- Documentação que possa acompanhar o ritmo da produção
- Feature flags (sinalizadores de recurso) essenciais para coordenar efetivamente com outros departamentos
- Estratégia de rollback automatizada

#### Benefícios

- Não há necessidade de pausar o desenvolvimento para novos lançamentos, otimizando todo o processo
- As implantações são mais fáceis de corrigir e menos arriscadas
- Melhorias são feitas continuamente, e esses aumentos na qualidade são claramente definidos para os clientes
- Feedback mais rápido dos usuários finais

---

## Resumo das Diferenças

| Aspecto | CI | Continuous Delivery | Continuous Deployment |
|---------|----|--------------------|----------------------|
| **Objetivo** | Integrar código frequentemente | Preparar código para deploy | Deploy automático em produção |
| **Automação** | Build e testes | Build, testes e staging | Build, testes, staging e produção |
| **Deploy em Produção** | Manual | Manual (com 1 clique) | Automático |
| **Intervenção Humana** | Revisão de código | Aprovação de deploy | Nenhuma (após merge) |
| **Risco** | Baixo | Médio | Alto (requer testes robustos) |

---

## Etapas de um Pipeline de CI/CD

Embora um pipeline de CI/CD possa parecer trabalho adicional, na verdade é exatamente o oposto. É apenas um processo automatizado que você pode executar para entregar novos produtos rapidamente e com menos dificuldades. A falha em qualquer etapa aciona uma notificação para alertar o engenheiro responsável.

### 1. Source (Fonte)

Normalmente, um pipeline é acionado por um repositório de código-fonte. As alterações no código ativam uma notificação na ferramenta de pipeline de CI/CD, que opera o pipeline correspondente.

**Gatilhos comuns:**
- Push para branch principal (main/master)
- Pull Request aberto ou atualizado
- Tag de versão criada
- Agendamento (cron jobs)
- Webhook externo

### 2. Build (Compilação)

Durante a fase de compilação, os engenheiros compartilham o código que desenvolveram por meio de um repositório para criar uma iteração executável do produto.

**Atividades típicas:**
- Compilar código-fonte
- Resolver dependências
- Criar artefatos (JARs, binários, imagens Docker)
- Gerar número de versão

**Quando uma aplicação não passa desta etapa, é crucial investigar imediatamente**, pois sugere que há algo fundamentalmente errado com a configuração.

### 3. Test (Teste)

Durante o teste, você valida o código e tem a chance de observar como o produto se comporta. É uma rede de segurança essencial que evita que os bugs cheguem aos usuários finais.

**Tipos de testes:**
- **Testes Unitários**: Validam funções e métodos individuais
- **Testes de Integração**: Verificam interação entre componentes
- **Testes de Contrato**: Garantem compatibilidade de APIs
- **Testes E2E (End-to-End)**: Simulam fluxos de usuário completos
- **Testes de Performance**: Avaliam tempo de resposta e throughput
- **Testes de Segurança**: Escaneamento de vulnerabilidades (SAST/DAST)

A falha nesta etapa expõe problemas que você não imaginou ao escrever o código. O objetivo desta etapa é dar feedback rapidamente aos engenheiros, enquanto a causa do problema ainda está recente.

### 4. Deploy (Implantação)

Após uma instância executável de todo o código ser criada e testada, ela estará pronta para ser implantada.

**Estratégias de Deploy:**

**Blue-Green Deployment**: Mantém dois ambientes idênticos (azul e verde). O novo código vai para o ambiente inativo, que se torna ativo após validação.

**Canary Deployment**: Lança a nova versão para uma pequena porcentagem de usuários antes do rollout completo.

**Rolling Deployment**: Atualiza instâncias gradualmente, mantendo o serviço disponível.

**Feature Flags**: Permite ativar/desativar funcionalidades sem novo deploy.

### 5. Monitor (Monitoramento)

Após a implantação, o monitoramento contínuo é essencial para:
- Detectar erros em produção
- Medir performance e latência
- Rastrear experiência do usuário
- Coletar métricas de negócio
- Acionar rollbacks automáticos se necessário

---

## Pipeline as Code (PaC)

Em 2024-2025, a prática de definir pipelines como código tornou-se padrão. Isso significa que a configuração do pipeline é versionada junto com o código da aplicação.

### Exemplo: GitHub Actions

```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'
        cache: 'npm'
    
    - name: Install dependencies
      run: npm ci
    
    - name: Run tests
      run: npm test
    
    - name: Build application
      run: npm run build
    
    - name: Security scan
      run: npm audit
  
  deploy:
    needs: build-and-test
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    
    steps:
    - name: Deploy to production
      run: |
        echo "Deploying to production..."
        # Comandos de deploy aqui
```

### Exemplo: GitLab CI/CD

```yaml
stages:
  - build
  - test
  - security
  - deploy

variables:
  DOCKER_IMAGE: myapp:$CI_COMMIT_SHA

build:
  stage: build
  script:
    - docker build -t $DOCKER_IMAGE .
    - docker push $DOCKER_IMAGE

test:unit:
  stage: test
  script:
    - npm install
    - npm run test:unit

test:integration:
  stage: test
  script:
    - npm run test:integration

security:scan:
  stage: security
  script:
    - trivy image $DOCKER_IMAGE
    - npm audit

deploy:production:
  stage: deploy
  only:
    - main
  script:
    - kubectl set image deployment/myapp myapp=$DOCKER_IMAGE
    - kubectl rollout status deployment/myapp
  environment:
    name: production
```

---

## Ferramentas de Pipeline de CI/CD

### Ferramentas Populares (2024-2025)

**Plataformas Integradas:**
- **GitHub Actions**: Integrado ao GitHub, gratuito para projetos públicos
- **GitLab CI/CD**: Integrado ao GitLab, runners próprios ou compartilhados
- **Bitbucket Pipelines**: Integrado ao Bitbucket
- **Azure DevOps**: Solução completa da Microsoft

**Ferramentas Standalone:**
- **Jenkins**: Open-source, altamente extensível
- **CircleCI**: Cloud-native, fácil configuração
- **Travis CI**: Popular para projetos open-source
- **TeamCity**: Da JetBrains, boa para projetos Java

**Ferramentas Especializadas:**
- **ArgoCD**: GitOps para Kubernetes
- **Flux**: GitOps automático
- **Spinnaker**: Deploy multi-cloud
- **Tekton**: CI/CD cloud-native para Kubernetes

### Ferramentas Complementares

**Containerização:**
- Docker
- Podman
- Buildah

**Orquestração:**
- Kubernetes
- Docker Swarm
- Nomad

**Segurança:**
- Trivy (scanning de vulnerabilidades)
- Snyk (análise de dependências)
- SonarQube (qualidade de código)
- OWASP ZAP (testes de segurança)

**Gerenciamento de Secrets:**
- HashiCorp Vault
- AWS Secrets Manager
- Azure Key Vault
- Google Secret Manager

---

## Características de um Bom Pipeline de CI/CD

### 1. Velocidade
A integração contínua deve ser rápida e apresentar feedback instantâneo, caso contrário, o fluxo é interrompido e a produtividade cai.

**Meta:** Pipelines devem completar em menos de 10 minutos para feedback rápido.

### 2. Precisão
Automatizar o processo de implantação exige precisão extrema para evitar interferência humana.

**Práticas:**
- Testes determinísticos (sempre produzem o mesmo resultado)
- Validação de artefatos
- Checksums e assinaturas

### 3. Confiabilidade
O pipeline deve ser confiável, com código de teste à prova de falhas e resultados estáveis.

**Práticas:**
- Flaky tests devem ser investigados e corrigidos
- Ambientes de teste devem ser isolados e reproduzíveis
- Rollback automático em caso de falha

### 4. Segurança
Segurança deve ser integrada em cada etapa do pipeline (DevSecOps).

**Práticas:**
- Scan de vulnerabilidades em dependências
- Análise estática de código (SAST)
- Testes de segurança dinâmicos (DAST)
- Scanning de imagens de container

### 5. Observabilidade
Visibilidade completa do que está acontecendo no pipeline.

**Práticas:**
- Logs estruturados
- Métricas de pipeline (tempo de execução, taxa de sucesso)
- Alertas configurados
- Dashboards de visualização

---

## Métricas DORA para CI/CD

As métricas DORA (DevOps Research and Assessment) são o padrão da indústria para medir performance de equipes DevOps:

### 1. Deployment Frequency (Frequência de Deploy)
**Pergunta:** Com que frequência sua organização implanta código em produção?

**Elite:** Múltiplos deploys por dia  
**High:** Entre uma vez por dia e uma vez por semana  
**Medium:** Entre uma vez por semana e uma vez por mês  
**Low:** Menos de uma vez por mês

### 2. Lead Time for Changes (Tempo de Entrega)
**Pergunta:** Quanto tempo leva desde o commit até o código estar rodando em produção?

**Elite:** Menos de uma hora  
**High:** Entre um dia e uma semana  
**Medium:** Entre uma semana e um mês  
**Low:** Mais de um mês

### 3. Time to Restore Service (Tempo de Recuperação)
**Pergunta:** Quanto tempo leva para restaurar o serviço após um incidente?

**Elite:** Menos de uma hora  
**High:** Menos de um dia  
**Medium:** Entre um dia e uma semana  
**Low:** Mais de uma semana

### 4. Change Failure Rate (Taxa de Falha em Mudanças)
**Pergunta:** Qual percentual de mudanças resulta em falha em produção?

**Elite:** 0-15%  
**High:** 16-30%  
**Medium:** 31-45%  
**Low:** 46-60%

---

## Melhores Práticas de Pipeline CI/CD

### 1. Keep It Fast
- Execute testes em paralelo
- Use cache para dependências
- Otimize builds com Docker layer caching
- Considere splits de testes

### 2. Fail Fast
- Execute testes mais rápidos primeiro
- Pare o pipeline na primeira falha
- Forneça feedback imediato aos desenvolvedores

### 3. Make It Reproducible
- Use ambientes isolados e consistentes (containers)
- Versione todas as dependências
- Evite dependências externas instáveis

### 4. Automate Everything
- Não tenha etapas manuais críticas
- Automatize rollbacks
- Use Infrastructure as Code

### 5. Test in Production-Like Environments
- Staging deve ser espelho de produção
- Use feature flags para testes em produção
- Implemente canary deployments

### 6. Monitor and Alert
- Configure alertas para falhas de pipeline
- Monitore métricas de performance
- Tenha dashboards de visibilidade

### 7. Security First
- Integre scans de segurança no pipeline
- Nunca commite secrets no código
- Use ferramentas de análise estática

### 8. Document Your Pipeline
- Pipeline as Code autodocumenta
- Mantenha README atualizado
- Documente estratégias de deploy

---

## Tendências de CI/CD em 2024-2025

### 1. GitOps
Usar Git como fonte única de verdade para infraestrutura e aplicações. Mudanças em produção são feitas através de pull requests.

### 2. Ambientes Efêmeros
Criar ambientes temporários para cada pull request, permitindo testes isolados e colaboração.

### 3. Progressive Delivery
Combinar feature flags, canary deployments e testes A/B para controlar rollout de features.

### 4. AI-Powered Pipelines
IA para otimizar execução de testes, prever falhas e sugerir melhorias.

### 5. Platform Engineering
Criar plataformas internas que abstraem complexidade de CI/CD para desenvolvedores.

---

## Checklist de Implementação de CI/CD

- [ ] Código versionado em repositório Git
- [ ] Testes automatizados implementados
- [ ] Pipeline definido como código
- [ ] Build automatizado configurado
- [ ] Testes executando em pipeline
- [ ] Scanning de segurança integrado
- [ ] Estratégia de deploy definida
- [ ] Ambientes de staging configurados
- [ ] Monitoramento em produção configurado
- [ ] Rollback automatizado implementado
- [ ] Feature flags configurados
- [ ] Documentação de pipeline criada
- [ ] Alertas configurados
- [ ] Métricas DORA sendo coletadas
- [ ] Secrets gerenciados com segurança

---

## Conclusão

Um pipeline de CI/CD bem implementado é fundamental para o sucesso de equipes DevOps modernas. Ele não apenas acelera a entrega de software, mas também melhora a qualidade, reduz riscos e aumenta a confiança das equipes.

**Principais Aprendizados:**

1. CI/CD é uma jornada, não um destino - sempre há espaço para melhorias
2. Comece simples e itere - não tente implementar tudo de uma vez
3. Automação é meio, não fim - o objetivo é entregar valor aos clientes
4. Segurança deve ser integrada desde o início
5. Meça o que importa - use métricas DORA para guiar melhorias
6. Pipeline as Code traz os benefícios de versionamento e colaboração
7. Feedback rápido é essencial - desenvolvedores precisam saber rapidamente se algo quebrou
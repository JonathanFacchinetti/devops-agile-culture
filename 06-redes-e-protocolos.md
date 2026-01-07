# Redes e Protocolos

## Por Que Networking é Fundamental para DevOps?

Networking é a espinha dorsal da engenharia DevOps, garantindo que tudo permaneça conectado e funcione como deveria. Em um mundo onde aplicações distribuídas, microservices e infraestrutura cloud são onipresentes, entender como os dados trafegam entre sistemas é essencial.

**DevOps e Networking:**
- Configurar comunicação entre microservices
- Gerenciar infraestrutura cloud
- Automatizar deployments
- Garantir segurança do sistema
- Troubleshooting de problemas de conectividade
- Otimizar performance de aplicações

---

## Modelo OSI: A Base Conceitual

O modelo OSI (Open Systems Interconnection) é um conjunto de padrões que define como computadores se comunicam através de uma rede, dividindo o fluxo de dados em sete camadas que se constroem uma sobre a outra.

### As 7 Camadas do Modelo OSI

**7. Application Layer (Camada de Aplicação)**
- Interface com o usuário final
- Protocolos: HTTP, HTTPS, DNS, FTP, SSH, SMTP
- Exemplo: Seu navegador fazendo requisição HTTP

**6. Presentation Layer (Camada de Apresentação)**
- Tradução, criptografia e compressão de dados
- Formata dados para a aplicação
- Exemplo: SSL/TLS para HTTPS

**5. Session Layer (Camada de Sessão)**
- Estabelece, gerencia e termina conexões
- Mantém sessões entre aplicações
- Exemplo: Login em um site mantendo sessão ativa

**4. Transport Layer (Camada de Transporte)**
- Entrega confiável de dados end-to-end
- Protocolos: TCP (confiável) e UDP (rápido)
- Exemplo: TCP garante que pacotes cheguem na ordem correta

**3. Network Layer (Camada de Rede)**
- Roteamento de pacotes entre redes diferentes
- Protocolo principal: IP (Internet Protocol)
- Exemplo: Roteadores decidindo o melhor caminho para dados

**2. Data Link Layer (Camada de Enlace)**
- Transferência de dados entre dispositivos adjacentes
- Endereçamento MAC
- Exemplo: Switch conectando computadores em uma LAN

**1. Physical Layer (Camada Física)**
- Transmissão de bits brutos através do meio físico
- Hardware: cabos, fibra óptica, ondas de rádio
- Exemplo: Sinais elétricos em cabo Ethernet

---

## Modelo TCP/IP: A Implementação Prática

O modelo OSI é ótimo para entendimento teórico, mas na prática usamos o modelo TCP/IP (Transmission Control Protocol/Internet Protocol), que tem estrutura similar em camadas mas menos complicada.

### As 4 Camadas do TCP/IP

**4. Application Layer**
- Combina Application, Presentation e Session do OSI
- Protocolos: HTTP, DNS, FTP, SSH, SMTP

**3. Transport Layer**
- Igual ao Transport do OSI
- TCP e UDP

**2. Internet Layer**
- Corresponde ao Network do OSI
- IP, ICMP, routing

**1. Network Interface Layer**
- Combina Data Link e Physical do OSI
- Ethernet, Wi-Fi, drivers de hardware

### Comparação OSI vs TCP/IP

| OSI Model | TCP/IP Model |
|-----------|--------------|
| 7 camadas | 4 camadas |
| Modelo teórico | Implementação prática |
| Application | Application |
| Presentation | (Application) |
| Session | (Application) |
| Transport | Transport |
| Network | Internet |
| Data Link | Network Interface |
| Physical | (Network Interface) |

---

## Endereçamento IP e Subnetting

### IP Address (Endereço IP)

Um **IP address** é um identificador numérico único atribuído a cada dispositivo conectado a uma rede.

**IPv4:**
- Formato: 192.168.1.10
- 32 bits (4 octetos)
- ~4.3 bilhões de endereços possíveis
- Esgotamento levou ao IPv6

**IPv6:**
- Formato: 2001:0db8:85a3:0000:0000:8a2e:0370:7334
- 128 bits
- 340 undecilhões de endereços possíveis

### Classes de Endereços IPv4

| Classe | Range | Uso | Hosts Possíveis |
|--------|-------|-----|-----------------|
| A | 1.0.0.0 - 126.255.255.255 | Grandes organizações | ~16 milhões |
| B | 128.0.0.0 - 191.255.255.255 | Médias empresas | ~65 mil |
| C | 192.0.0.0 - 223.255.255.255 | Pequenas redes | 254 |
| D | 224.0.0.0 - 239.255.255.255 | Multicast | N/A |
| E | 240.0.0.0 - 255.255.255.255 | Reservado | N/A |

### Endereços Privados (RFC 1918)

Usados em redes locais, não roteáveis na internet:
- **10.0.0.0/8** (10.0.0.0 - 10.255.255.255)
- **172.16.0.0/12** (172.16.0.0 - 172.31.255.255)
- **192.168.0.0/16** (192.168.0.0 - 192.168.255.255)

### Subnetting

**Subnetting** divide uma rede grande em sub-redes menores para melhor gerenciamento.

**Subnet Mask:** Determina qual parte do IP é rede e qual é host.

**Exemplo:**
```
IP: 192.168.1.0
Subnet Mask: 255.255.255.0 (/24)

Network portion: 192.168.1
Host portion: 0-255 (254 hosts utilizáveis)
```

### CIDR (Classless Inter-Domain Routing)

CIDR é uma solução para o problema de números não-ideais de endereços IP—ao remover classes, elimina a necessidade de limites específicos nos totais.

**Notação CIDR:**
- 192.168.1.0/24 = 256 IPs (254 utilizáveis)
- 192.168.1.0/25 = 128 IPs (126 utilizáveis)
- 192.168.1.0/26 = 64 IPs (62 utilizáveis)

**Cálculo rápido:**
- /24 = 256 hosts (2^8)
- /25 = 128 hosts (2^7)
- /26 = 64 hosts (2^6)
- /27 = 32 hosts (2^5)

---

## Protocolos Essenciais

### TCP vs UDP

TCP é um protocolo orientado a conexão na camada de transporte (use para segurança); UDP também está na camada de transporte mas é sem conexão (use para velocidade).

| Aspecto | TCP | UDP |
|---------|-----|-----|
| **Conexão** | Orientado a conexão | Sem conexão |
| **Confiabilidade** | Garante entrega | Não garante |
| **Ordem** | Mantém ordem dos pacotes | Não garante ordem |
| **Velocidade** | Mais lento | Mais rápido |
| **Overhead** | Maior | Menor |
| **Uso** | HTTP, FTP, SSH, email | Streaming, DNS, VoIP |

**TCP Three-Way Handshake:**
```
Cliente → Servidor: SYN (Sincronizar)
Servidor → Cliente: SYN-ACK (Sincronizar-Reconhecer)
Cliente → Servidor: ACK (Reconhecer)
```

### HTTP/HTTPS

**HTTP (Hypertext Transfer Protocol):**
- Porta padrão: 80
- Transferência de dados web
- Texto plano (não seguro)

**HTTPS (HTTP Secure):**
- Porta padrão: 443
- HTTP + SSL/TLS
- Criptografia end-to-end
- Essencial para segurança

**Métodos HTTP:**
```
GET     - Recuperar dados
POST    - Enviar dados
PUT     - Atualizar/criar recurso
DELETE  - Remover recurso
PATCH   - Atualização parcial
HEAD    - Metadados apenas
OPTIONS - Métodos suportados
```

**Códigos de Status HTTP:**
```
1xx - Informacional
2xx - Sucesso (200 OK, 201 Created)
3xx - Redirecionamento (301 Moved, 304 Not Modified)
4xx - Erro do cliente (400 Bad Request, 401 Unauthorized, 404 Not Found)
5xx - Erro do servidor (500 Internal Error, 502 Bad Gateway, 503 Service Unavailable)
```

### DNS (Domain Name System)

DNS traduz linguagem de computador para linguagem humana e dá nomes a domínios através da rede.

**Funcionamento:**
```
1. Você digita: www.google.com
2. DNS resolve para: 142.250.190.78
3. Navegador conecta ao IP
```

**Tipos de Registros DNS:**

| Tipo | Função | Exemplo |
|------|--------|---------|
| **A** | IPv4 address | example.com → 192.168.1.1 |
| **AAAA** | IPv6 address | example.com → 2001:db8::1 |
| **CNAME** | Alias (canonical name) | www → example.com |
| **MX** | Mail server | mail.example.com |
| **TXT** | Texto arbitrário | SPF, DKIM records |
| **NS** | Name server | Servidores autoritativos |
| **SOA** | Start of Authority | Informações da zona |

**Hierarquia DNS:**
```
Root (.)
  └─ TLD (.com, .org, .br)
      └─ Domain (google.com)
          └─ Subdomain (mail.google.com)
```

### SSH (Secure Shell)

**SSH** permite acesso remoto seguro a servidores.

**Porta padrão:** 22

**Uso básico:**
```bash
# Conectar a servidor
ssh user@192.168.1.10

# Conectar com chave privada
ssh -i ~/.ssh/id_rsa user@server.com

# Copiar arquivos (SCP)
scp file.txt user@server:/path/

# Túnel SSH (port forwarding)
ssh -L 8080:localhost:80 user@server
```

**Autenticação por chaves SSH:**
```bash
# Gerar par de chaves
ssh-keygen -t ed25519 -C "seu@email.com"

# Copiar chave pública para servidor
ssh-copy-id user@server

# Agora conecta sem senha
ssh user@server
```

### FTP/SFTP

**FTP (File Transfer Protocol):**
- Porta: 20, 21
- Transferência de arquivos
- Não criptografado (inseguro)

**SFTP (SSH File Transfer Protocol):**
- Porta: 22 (via SSH)
- Transferência segura
- Preferido para produção

### SMTP (Simple Mail Transfer Protocol)

**SMTP** é usado para envio de emails.

**Porta:** 25 (não criptografado), 587 (TLS), 465 (SSL)

**Fluxo de email:**
```
Cliente → Servidor SMTP (envio) → Servidor SMTP (destino) → Cliente (recebimento via POP3/IMAP)
```

---

## Componentes de Rede

### Router (Roteador)

**Função:** Direciona tráfego entre diferentes redes.

Routing é o processo de enviar informação através de uma rede.

**Características:**
- Opera na Camada 3 (Network)
- Usa tabelas de roteamento
- Conecta LANs diferentes
- Implementa NAT

**Tabela de Roteamento:**
```
Destination     Gateway         Interface
0.0.0.0/0       192.168.1.1     eth0     (rota padrão)
192.168.1.0/24  0.0.0.0         eth0     (rede local)
10.0.0.0/8      192.168.1.254   eth0     (rede remota)
```

### Switch

**Função:** Conecta dispositivos dentro de uma rede local (LAN).

**Características:**
- Opera na Camada 2 (Data Link)
- Usa endereços MAC
- Mais inteligente que hub
- Cria domínios de colisão separados

**Diferença Switch vs Hub:**
- Hub: Broadcasting (todos recebem tudo)
- Switch: Encaminhamento inteligente (só destino recebe)

### Firewall

**Função:** Controla tráfego de rede baseado em regras de segurança.

**Tipos:**
- **Stateless:** Filtra baseado em regras estáticas
- **Stateful:** Rastreia estado de conexões ativas
- **Application Layer:** Inspeção profunda de pacotes

**Regras típicas:**
```bash
# Permitir SSH de IP específico
ALLOW TCP 192.168.1.100 port 22

# Bloquear todo tráfego de rede externa
DENY ALL 0.0.0.0/0

# Permitir HTTP/HTTPS
ALLOW TCP ANY port 80,443
```

### Load Balancer

**Função:** Distribui tráfego entre múltiplos servidores.

**Algoritmos:**
- **Round Robin:** Rotação circular
- **Least Connections:** Servidor com menos conexões
- **IP Hash:** Baseado no IP do cliente
- **Weighted:** Servidores com pesos diferentes

**Benefícios:**
- Alta disponibilidade
- Escalabilidade horizontal
- Performance melhorada
- Health checks automáticos

---

## Portas de Rede

Portas TCP usam identificadores digitais para identificar o tipo correto de processo para um comando.

### Portas Bem Conhecidas (0-1023)

| Porta | Protocolo | Serviço |
|-------|-----------|---------|
| 20, 21 | FTP | File Transfer |
| 22 | SSH | Secure Shell |
| 23 | Telnet | Remote login (inseguro) |
| 25 | SMTP | Email sending |
| 53 | DNS | Domain Name System |
| 80 | HTTP | Web traffic |
| 110 | POP3 | Email retrieval |
| 143 | IMAP | Email retrieval |
| 443 | HTTPS | Secure web traffic |
| 3306 | MySQL | Database |
| 5432 | PostgreSQL | Database |
| 6379 | Redis | Cache |
| 27017 | MongoDB | Database |

### Verificar Portas Abertas

```bash
# Listar portas em uso (Linux)
netstat -tuln

# Alternativa moderna
ss -tuln

# Verificar porta específica
lsof -i :80

# Testar conectividade
telnet google.com 80
nc -zv google.com 80
```

---

## Ferramentas de Troubleshooting

### ping

**Função:** Testa conectividade básica.

```bash
# Ping básico
ping google.com

# Ping com contagem específica
ping -c 4 8.8.8.8

# Ping contínuo
ping -t google.com  # Windows
ping google.com     # Linux (Ctrl+C para parar)
```

### traceroute / tracert

**Função:** Mostra caminho dos pacotes até o destino.

```bash
# Linux/Mac
traceroute google.com

# Windows
tracert google.com
```

### nslookup / dig

**Função:** Consulta DNS.

```bash
# nslookup
nslookup google.com

# dig (mais detalhado)
dig google.com

# Tipo específico de registro
dig google.com MX
dig google.com TXT
```

### netstat / ss

**Função:** Mostra conexões de rede ativas.

```bash
# Todas as conexões
netstat -a

# Portas em listening
netstat -tuln

# Alternativa moderna (ss)
ss -tuln
```

### curl / wget

**Função:** Fazer requisições HTTP.

```bash
# GET request
curl https://api.github.com

# POST request
curl -X POST -d '{"key":"value"}' https://api.example.com

# Headers
curl -H "Authorization: Bearer token" https://api.example.com

# Download arquivo
wget https://example.com/file.zip
```

### tcpdump / Wireshark

**Função:** Captura e análise de pacotes.

```bash
# Capturar tráfego em interface
sudo tcpdump -i eth0

# Capturar HTTP
sudo tcpdump -i eth0 port 80

# Salvar em arquivo
sudo tcpdump -i eth0 -w capture.pcap
```

**Wireshark:** Interface gráfica para análise profunda de pacotes.

---

## Networking em Containers

### Docker Networking

**Tipos de rede Docker:**

**1. Bridge (padrão)**
```bash
# Containers se comunicam via bridge
docker run -d --name web nginx
docker run -d --name api node
# web pode acessar api via hostname
```

**2. Host**
```bash
# Container usa rede do host diretamente
docker run --network host nginx
```

**3. None**
```bash
# Sem conectividade
docker run --network none alpine
```

**4. Custom Bridge**
```bash
# Criar rede customizada
docker network create my-network

# Usar rede
docker run --network my-network --name web nginx
docker run --network my-network --name api node
# Agora web pode acessar api pelo nome
```

### Kubernetes Networking

**Princípios:**
- Todo pod tem seu próprio IP
- Pods podem se comunicar sem NAT
- Nodes podem se comunicar com pods sem NAT

**Services:**
- **ClusterIP:** Interno ao cluster
- **NodePort:** Expõe em porta do node
- **LoadBalancer:** Load balancer externo

---

## Segurança de Rede

### VPN (Virtual Private Network)

**Função:** Criar conexão segura através de rede pública.

**Tipos:**
- **Site-to-Site:** Conecta redes inteiras
- **Remote Access:** Usuários individuais

**Protocolos VPN:**
- **OpenVPN:** Open-source, flexível
- **WireGuard:** Moderno, rápido
- **IPsec:** Padrão da indústria

### SSL/TLS

**Função:** Criptografia de comunicação.

**Processo:**
1. Cliente inicia conexão
2. Servidor envia certificado
3. Cliente verifica certificado
4. Troca de chaves criptográficas
5. Comunicação criptografada estabelecida

**Verificar certificado:**
```bash
openssl s_client -connect google.com:443
```

### NAT (Network Address Translation)

**Função:** Traduz IPs privados para IP público.

**Tipos:**
- **SNAT (Source NAT):** Múltiplos IPs privados → 1 IP público
- **DNAT (Destination NAT):** Port forwarding

**Exemplo:**
```
Rede interna: 192.168.1.0/24
IP público: 203.0.113.5

192.168.1.10:5000 → 203.0.113.5:5000 → Internet
```

---

## Networking em Cloud

### AWS Networking

**VPC (Virtual Private Cloud):**
- Rede isolada logicamente
- Subnets públicas e privadas
- Internet Gateway
- NAT Gateway
- Route Tables

**Security Groups:**
- Firewall stateful
- Nível de instância

**Network ACL:**
- Firewall stateless
- Nível de subnet

### Azure Networking

**Virtual Network (VNet):**
- Equivalente ao VPC da AWS
- Network Security Groups (NSG)
- Application Gateway

### GCP Networking

**VPC Network:**
- Global por padrão
- Firewall Rules
- Cloud Load Balancing

---

## Checklist de Networking para DevOps

**Fundamentos:**
- [ ] Entender modelo OSI e TCP/IP
- [ ] Dominar endereçamento IP e subnetting
- [ ] Conhecer diferença entre TCP e UDP
- [ ] Saber configurar DNS

**Protocolos:**
- [ ] HTTP/HTTPS e códigos de status
- [ ] SSH para acesso remoto seguro
- [ ] Entender fluxo de email (SMTP)

**Ferramentas:**
- [ ] ping, traceroute para diagnóstico
- [ ] dig/nslookup para DNS
- [ ] curl para APIs
- [ ] tcpdump para análise de pacotes

**Segurança:**
- [ ] Configurar firewalls
- [ ] Implementar VPN
- [ ] Gerenciar certificados SSL/TLS
- [ ] Entender NAT

**Cloud:**
- [ ] Configurar VPC/VNet
- [ ] Security groups e network ACLs
- [ ] Load balancers
- [ ] VPN site-to-site

---

## Conclusão

Networking é habilidade fundamental para qualquer engenheiro DevOps. Desde entender como dados fluem através de camadas do modelo OSI até configurar VPCs complexas na cloud, esse conhecimento permite diagnosticar problemas, otimizar performance e garantir segurança.

**Principais Aprendizados:**

1. Modelo OSI fornece framework teórico; TCP/IP é implementação prática
2. Endereçamento IP e subnetting são essenciais para design de rede
3. TCP oferece confiabilidade; UDP oferece velocidade
4. DNS traduz nomes para IPs—fundamental para internet funcionar
5. Ferramentas como ping, traceroute e dig são indispensáveis para troubleshooting
6. Segurança de rede requer múltiplas camadas (firewalls, VPN, TLS)
7. Containers e Kubernetes têm modelos de networking próprios
8. Cloud networking abstrai complexidade mas requer entendimento dos fundamentos
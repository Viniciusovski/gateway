# 📡 API Gateway

## ✨ Visão Geral

O **API Gateway** é o ponto de entrada centralizado para um sistema distribuído, geralmente baseado em microsserviços. Ele atua como um **roteador inteligente**, direcionando as requisições dos clientes para os serviços apropriados, além de oferecer funcionalidades adicionais como autenticação, balanceamento de carga, cache, rate limiting, logging, entre outros.

O Gateway **abstrai a complexidade interna da arquitetura**, expondo apenas uma **interface unificada para o consumidor**. É uma camada fundamental em arquiteturas modernas, pois **simplifica a comunicação entre clientes (web, mobile, etc.) e os diversos serviços de back-end**.

---

## 🔧 Funcionalidades Comuns

- **Roteamento de Requisições**  
  Direciona chamadas HTTP para os serviços corretos com base em regras configuradas (por URL, headers, etc.).

- **Autenticação e Autorização**  
  Centraliza a verificação de tokens JWT, OAuth2, API Keys, etc.

- **Rate Limiting & Throttling**  
  Controla o número de requisições permitidas por cliente para evitar abusos.

- **CORS (Cross-Origin Resource Sharing)**  
  Gerencia políticas de acesso entre domínios diferentes.

- **Log e Monitoramento**  
  Capta métricas, logs e estatísticas de uso.

- **Transformação de Requisições/Respostas**  
  Modifica headers ou conteúdos das requisições e respostas.

- **Cache**  
  Armazena respostas para reduzir chamadas desnecessárias aos serviços.

---

## 🧱 Arquitetura

```
[ Client (Web/Mobile) ]
           ↓
     [ API Gateway ]
     ↙     ↓      ↘
 [Service A] [Service B] [Service C]
```

---

## ✅ Vantagens

- Reduz o acoplamento entre clientes e serviços
- Centraliza responsabilidades transversais (segurança, logs, etc.)
- Facilita a manutenção e evolução dos microsserviços

---

## ⚠️ Cuidados

- **Ponto único de falha**: o Gateway deve ser altamente disponível e escalável
- Pode introduzir latência se mal configurado
- Monitoramento e observabilidade são essenciais

---

## 🧪 Exemplo com Spring Cloud Gateway

```yaml
spring:
  cloud:
    gateway:
      routes:
        - id: product-service
          uri: http://localhost:8081/
          predicates:
            - Path=/api/products/**
```

Com a configuração acima, qualquer requisição feita para `/api/products/**` será redirecionada ao `product-service`.

---

## 🌐 Acessando via Gateway

Suponha que o serviço `pedidos-ms` esteja registrado e possua um endpoint `/pedidos`. Com o Gateway configurado na porta `8082`, a chamada seria:

```
http://localhost:8082/pedidos-ms/pedidos
```

Isso é possível porque o Gateway funciona como **ponto central de acesso**, permitindo escalar horizontalmente os microsserviços e distribuí-los de forma eficiente.

---

## ⚖️ Balanceamento de Carga – Resumo

**Balanceamento de carga** é uma técnica para distribuir requisições entre várias instâncias de serviço, promovendo eficiência e alta disponibilidade.

### 🎯 Objetivos

- Melhorar o desempenho
- Aumentar a disponibilidade
- Evitar sobrecarga em um único servidor

### 🧠 Como Funciona

Quando uma requisição chega, o balanceador decide para qual instância enviá-la com base em critérios como:

- Menor uso de CPU
- Menor tempo de resposta
- Algoritmos como Round Robin, Least Connections, etc.

### 📍 Onde é Usado

- Entre clientes e servidores (ex: NGINX, AWS Load Balancer)
- Entre microsserviços (ex: Spring Cloud LoadBalancer + Eureka)

### ✅ Benefícios

- Alta disponibilidade (se uma instância falhar, outra assume)
- Escalabilidade horizontal
- Melhor experiência para o usuário final

---

## 📚 Referências

- [Spring Cloud Gateway Docs](https://spring.io/projects/spring-cloud-gateway)
- [AWS API Gateway](https://aws.amazon.com/api-gateway/)
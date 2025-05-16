
O Gateway abstrai a complexidade interna, expondo apenas uma interface unificada para o consumidor.
O API Gateway é um ponto de entrada centralizado para um sistema distribuído (geralmente baseado em microsserviços). Ele atua como um roteador inteligente, 
direcionando as requisições dos clientes para o serviço apropriado, além de oferecer funcionalidades adicionais como autenticação, balanceamento de carga, cache, rate limiting, logging, entre outros.

É uma camada fundamental em arquiteturas modernas, pois simplifica a comunicação entre clientes (front-end, mobile, etc.) e os diversos serviços de back-end.

---
## 🔧 Funcionalidades Comuns

- **Roteamento de Requisições**  
  Direciona chamadas HTTP para os serviços responsáveis com base em regras configuradas (por URL, headers, etc.).

- **Autenticação e Autorização**  
  Centraliza a verificação de tokens JWT, OAuth2, API Keys, etc.

- **Rate Limiting & Throttling**  
  Controla o número de requisições permitidas por cliente para evitar abusos.

- **CORS (Cross-Origin Resource Sharing)**  
  Gerencia políticas de acesso entre domínios diferentes.

- **Log e Monitoramento**  
  Capta métricas, logs e estatísticas de uso.

- **Transformação de Requisições/Respostas**  
  Modifica headers, corpos de requisições ou respostas antes de enviá-los.

- **Cache**  
  Armazena respostas para reduzir chamadas desnecessárias aos serviços.

---

## 🧱 Arquitetura
[ Client (Web/Mobile) ]
↓
[ API Gateway ]
↙ ↓ ↘
[Service A] [Service B] [Service C]

yaml
Copiar
Editar

O Gateway abstrai a complexidade interna, expondo apenas uma interface unificada para o consumidor.

---

✅ Vantagens
  Reduz o acoplamento entre clientes e serviços

  Centraliza responsabilidades transversais (como segurança e logging)

  Facilita manutenção e evolução dos serviços

⚠️ Cuidados
  Single Point of Failure: deve ser altamente disponível e escalável

  Pode introduzir latência se mal configurado

  Monitoramento e logs são essenciais para detectar problemas

  

 A partir do momento que temos um **Gateway**, o ponto central para efetuar as chamadas para a aplicação, utilizaremos a porta `8082` 
  
 que foi definida para o Gateway — e incluiremos o nome do microsserviço `pedidos-ms`, seguido da URL definida no controlador.

  http://localhost:8082/pedidos-ms/pedidos




📚 Referências
Spring Cloud Gateway Docs: https://spring.io/projects/spring-cloud-gateway

AWS API Gateway: https://aws.amazon.com/api-gateway/

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

# 🏛️ Guia Definitivo de Microsserviços e Boas Práticas com NotebookLM

Repositório desenvolvido como parte do Desafio de Projeto da [DIO (Digital Innovation One)](https://www.dio.me/), explorando o uso de IA como ferramenta de aprendizagem ativa com o Google NotebookLM.

---

## 🎯 1. Contexto e Objetivos

### Contexto
A transição de monólitos para arquiteturas distribuídas baseadas em microsserviços tornou-se o padrão em sistemas modernos escaláveis. No entanto, a complexidade operacional, a consistência de dados e o desacoplamento de rede trazem desafios arquiteturais críticos.

### Objetivos de Aprendizagem
- Compreender os princípios fundamentais de decomposição por Domínio (DDD - *Domain-Driven Design*).
- Dominar padrões de resiliência e tolerância a falhas (Circuit Breaker, Bulkhead, Retry).
- Analisar estratégias de gerenciamento de dados distribuídos (Database-per-Service, Padrão Saga, Event-Driven).
- Avaliar trade-offs de comunicação síncrona (REST/gRPC) versus assíncrona (Message Brokers).

---

## 📚 2. Curadoria de Fontes

Para alimentar o caderno temático no NotebookLM, foram selecionados 4 artigos e materiais técnicos de referência aberta:

1. **Melhores práticas para se trabalhar com microsserviços**
   - *Link:* [https://fullcycle.com.br/melhores-praticas-para-se-trabalhar-com-microsservicos/]
2. **Microserviços: Vantagens, Desafios e Boas Práticas**
   - *Link:* [https://www.gowsolucoes.com/pt/artigos/microservicos-vantagens-desafios-e-boas-praticas]
3. **Microsserviços**
   - *Link:* [https://encurtador.com.br/BNIU]
4. **Explorando os princípios e melhores práticas dos Microsserviços**
   - *Link:* [https://www.proj4.me/blog/microsservicos]

---

## 📖 3. Miniguia de Estudo

### 4.1 Resumo Estruturado dos Pilares
- **Decomposição:** Serviços devem ser delimitados pelo *Bounded Context* (DDD). Cada equipe é dona do ciclo de vida completo do seu componente.
- **Dados Independentes (Database-per-Service):** Nunca compartilhe o mesmo banco de dados relacional entre serviços. A persistência é desacoplada para evitar acoplamento oculto de schema.
- **Comunicação:** 
  - *Síncrona (REST/gRPC):* Indicada para consultas imediatas com baixa latência.
  - *Assíncrona (Filas/Event Streams):* Indicada para comandos e atualizações de estado com resiliência a picos de tráfego.
- **Consistência Eventual:** Em vez de ACID global (2PC - Two-Phase Commit), adota-se o padrão Saga com transações compensatórias em caso de falha.

---

### 3.2 Glossário de Conceitos-Chave

| Conceito | Definição Rápida |
| :--- | :--- |
| **Bounded Context** | Fronteira explícita dentro da qual um modelo de domínio se aplica e é válido. |
| **Circuit Breaker** | Mecanismo que interrompe temporariamente requisições a um serviço instável para evitar colapso geral. |
| **API Gateway** | Ponto único de entrada que gerencia roteamento, autenticação, rate limiting e terminação SSL. |
| **Saga** | Sequência de transações locais onde cada transação atualiza dados em um serviço e publica um evento de compensação se falhar. |
| **Service Discovery** | Registro dinâmico de instâncias de serviços disponíveis na rede (ex: Eureka, Consul). |

### 3.3 🔗 Acesso ao Caderno Interativo (NotebookLM)

Você pode acessar o caderno temático original e interagir com a IA diretamente através do link público:
[https://notebook.google.com/notebook/558dde52-6922-42c8-8095-ab49232f9d21]

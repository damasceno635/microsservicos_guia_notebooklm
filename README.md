# 🏛️ Guia Definitivo de Microsserviços e Boas Práticas com NotebookLM

Repositório desenvolvido como parte do Desafio de Projeto da [DIO (Digital Innovation One)](https://www.dio.me/), explorando o uso de Inteligência Artificial como ferramenta de aprendizagem ativa com o [Google NotebookLM](https://notebooklm.google.com/).

---

## 🎯 1. Contexto e Objetivos

### Contexto
A transição de monólitos para arquiteturas distribuídas baseadas em microsserviços tornou-se o padrão em sistemas modernos escaláveis. No entanto, a complexidade operacional, a consistência de dados distribuídos e o desacoplamento de rede trazem desafios arquiteturais críticos que exigem padrões bem consolidados.

### Objetivos de Aprendizagem
- Compreender os princípios fundamentais de decomposição orientada a domínio (DDD - *Domain-Driven Design*).
- Dominar padrões de resiliência e tolerância a falhas (Circuit Breaker, Bulkhead, Retry).
- Analisar estratégias de dados desacoplados (Database-per-Service, Padrão Saga e Consistência Eventual).
- Avaliar trade-offs de comunicação síncrona (REST/gRPC) versus assíncrona (Filas e Event Brokers).

---

## 📚 2. Curadoria de Fontes

Para alimentar o caderno temático no NotebookLM, foram selecionados 4 artigos e materiais técnicos de referência aberta:

1. **Melhores práticas para se trabalhar com microsserviços**  
   - *Link:* [Full Cycle](https://fullcycle.com.br/melhores-praticas-para-se-trabalhar-com-microsservicos/)
2. **Microserviços: Vantagens, Desafios e Boas Práticas**  
   - *Link:* [GOW Soluções](https://www.gowsolucoes.com/pt/artigos/microservicos-vantagens-desafios-e-boas-praticas)
3. **Microsserviços: Fundamentos e Conceitos**  
   - *Link:* [Artigo Técnico Complementar](https://encurtador.com.br/BNIU)
4. **Explorando os princípios e melhores práticas dos Microsserviços**  
   - *Link:* [Proj4.me Blog](https://www.proj4.me/blog/microsservicos)

---

## 🧪 3. Engenharia de Prompts e "Cicatrizes" (Troubleshooting)

Durante o processo de estudo ativo, foi aplicada a engenharia de prompts iterativa para extrair sínteses profundas a partir do material carregado.

### Iteração 1: Resiliência e Prevenção de Falhas em Cascata
- **Prompt V1 (Genérico):**  
  > *"Como evitar que microsserviços caiam?"*  
  - **Problema:** Resposta superficial com recomendações genéricas de infraestrutura (usar nuvem, balanceador, logs).
- **Prompt V2 (Estratégico / Focado nas Fontes):**  
  > *"Com base nas fontes carregadas, sintetize os padrões de resiliência recomendados para microsserviços. Explique o funcionamento do Circuit Breaker em seus três estados (Closed, Open, Half-Open) e como ele impede falhas em cascata."*  
  - **Resultado:** A IA extraiu a mecânica exata dos limiares de erro (*thresholds*) e a lógica de reabertura controlada em *Half-Open*.

---

### Iteração 2: Transações e Consistência de Dados
- **Prompt V1 (Genérico):**  
  > *"Explique o que é Saga."*  
  - **Problema:** A IA gerou uma resposta acadêmica abstrata, sem deixar claros os trade-offs práticos de arquitetura.
- **Prompt V2 (Matriz de Decisão com Persona):**  
  > *"Atue como Arquiteto de Software. Compare as abordagens do Padrão Saga: Coreografada vs. Orquestrada. Estruture a resposta em tópicos: complexidade de manutenção, acoplamento entre serviços, rastreabilidade e melhor caso de uso."*  
  - **Resultado:** Resposta analítica direta, recomendando Coreografia para fluxos simples/baixo acoplamento e Orquestração para transações financeiras e fluxos complexos de negócio.

---

### "Cicatrizes" e Lições Aprendidas (Troubleshooting com a IA)
1. **Âncora Rigorosa às Fontes:** O NotebookLM só sintetiza o que foi carregado. Quando um termo específico não continha métricas detalhadas em um dos artigos, a resposta ficava incompleta. A solução foi cruzar o material com fontes de diferentes abordagens (Full Cycle + Proj4me).
2. **Estrutura por Comandos Claros:** Pedir tabelas, matrizes de trade-off e mapas conceituais gerou respostas muito mais ricas do que perguntas abertas iniciadas com "O que é...".

---

## 📖 4. Miniguia de Estudo

### 4.1 Resumo Estruturado dos Pilares
- **Decomposição:** Serviços devem ser delimitados pelo *Bounded Context* (DDD). Cada equipe/serviço deve possuir domínio claro e autonomia de deploy.
- **Dados Independentes (Database-per-Service):** Nunca compartilhe o mesmo banco de dados relacional entre múltiplos microsserviços. A persistência é desacoplada para evitar acoplamento oculto de schema.
- **Comunicação:** 
  - *Síncrona (REST/gRPC):* Indicada para consultas imediatas com baixa latência e fluxos simples.
  - *Assíncrona (Filas/Event Streams):* Indicada para comandos, atualizações de estado e tolerância a picos de tráfego.
- **Consistência Eventual:** Substitui o ACID global (2PC - Two-Phase Commit) pelo padrão Saga com transações compensatórias em caso de falha em etapas intermediárias.

---

### 4.2 Glossário de Conceitos-Chave

| Conceito | Definição Rápida |
| :--- | :--- |
| **Bounded Context** | Fronteira explícita dentro da qual um modelo de domínio se aplica e é estritamente válido. |
| **Circuit Breaker** | Mecanismo que interrompe temporariamente requisições a um serviço instável para evitar colapso geral. |
| **API Gateway** | Ponto único de entrada que gerencia roteamento, autenticação, rate limiting e observabilidade externa. |
| **Saga** | Sequência de transações locais em serviços distintos acompanhadas de ações de compensação em caso de erro. |
| **Service Discovery** | Mecanismo dinâmico de registro e localização de instâncias de serviços disponíveis na rede. |

---

### 4.3 Prompts Reutilizáveis para Revisão Rápida

Copie e use no NotebookLM para revisões periódicas do conteúdo:

1. **Simulação de Caso Real:**
   ```text
   Considere um cenário de checkout de e-commerce onde o serviço de Pagamentos responde com timeout. Com base nas fontes, descreva o fluxo de compensação necessário nos serviços de Estoque e Envio segundo o padrão Saga.

## 🔗 5. Acesso ao Caderno Interativo (NotebookLM)

Você pode acessar o caderno temático original e interagir com a IA diretamente através do link público:
[https://notebook.google.com/notebook/558dde52-6922-42c8-8095-ab49232f9d21]

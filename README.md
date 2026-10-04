# 🧠 Arquitetura de Inteligência Artificial Generativa

Bem-vindo ao repositório de estudos sobre **Arquitetura de IA Generativa para Engenheiros de Software**. Este espaço serve como um guia progressivo e documentação pessoal para dominar a stack moderna de desenvolvimento com LLMs (Large Language Models).

A arquitetura de sistemas de IA generativa constrói-se em camadas. Tentar criar Agentes autônomos antes de dominar como o modelo recupera contexto (RAG) ou executa funções (Skills) gera sistemas frágeis e difíceis de debugar. 

Este repositório segue a progressão cronológica ideal para o domínio dessa stack.


## 🗺️ Roteiro de Estudos (Roadmap)

Abaixo está a ordem recomendada de aprendizado. Clique nos links para acessar as minhas anotações e códigos sobre cada tópico.

### 1. [NLP (Processamento de Linguagem Natural)](gen-ai-architecture/NLP.md)
**A fundação teórica.** Antes de chamar APIs, é preciso entender como as máquinas processam texto.
* **Foco:** *Tokens* (e como afetam custos/limites), *Embeddings* (representações vetoriais) e o mecanismo de *Attention*.

### 2. [LLMs (Large Language Models)](gen-ai-architecture/LLM.md)
**O motor de raciocínio.** A interação direta com os modelos.
* **Foco:** Consumo de APIs (OpenAI, Anthropic, Gemini), inferência local (Ollama, LM Studio), engenharia de prompt e hiperparâmetros (Temperature, Top-P, Presence Penalty).

### 3. [RAG (Retrieval-Augmented Generation)](gen-ai-architecture/RAG.md)
**Injeção de contexto e dados corporativos.** A solução para alucinações e falta de conhecimento privado.
* **Foco:** Bancos de dados vetoriais (Pinecone, Milvus, pgvector), estratégias de *chunking*, busca (semântica, híbrida) e re-ranking.

### 4. [Skills (Tool / Function Calling)](gen-ai-architecture/Skills.md)
**Capacidade de ação no mundo real.** Permitindo que o LLM interaja com sistemas externos.
* **Foco:** Contratos JSON/OpenAPI, execução de funções locais (SQL, APIs externas) baseadas nas decisões do modelo.

### 5. [Agentes](gen-ai-architecture/Agentes.md)
**Autonomia e orquestração.** Onde tudo se junta.
* **Foco:** O LLM inserido em um loop de decisão (framework ReAct - *Reason + Act*), integrando memória, RAG e Skills para resolver problemas complexos.

### 5.5. [Guardrails](gen-ai-architecture/Guardrails.md)
**Controle, conformidade e segurança em tempo real.** O escudo de segurança para produção.
* **Foco:** *Input Guardrails* (bloqueio de *prompt injections* e *jailbreaks*) e *Output Guardrails* (prevenção de alucinações, mascaramento de PII, bloqueio de toxicidade e validação de JSON). 

### 6. [MCP (Model Context Protocol)](gen-ai-architecture/MCP.md)
**A padronização das conexões.** A camada de infraestrutura moderna.
* **Foco:** Criação e consumo de servidores MCP para conectar assistentes de IA a repositórios, bancos de dados e ferramentas de forma padronizada, substituindo integrações ponto-a-ponto customizadas.

### 7. [Harness (Avaliação e Testes)](gen-ai-architecture/Harness.md)
**Engenharia de produção e CI/CD.** Lidando com a natureza não-determinística da IA.
* **Foco:** Frameworks de avaliação (LM Evaluation Harness, Ragas, TruLens) e criação de métricas quantitativas para medir precisão de RAG, sucesso de Skills e segurança.

---

## 🏗️ Fluxo Arquitetural Completo

Para visualizar como tudo isso funciona em conjunto num sistema de produção:

1. O **Usuário** envia uma mensagem.
2. O **Input Guardrail** intercepta e valida se o prompt é seguro.
3. O **Agente** processa o pedido. Ele usa o **RAG** (via **MCP**) para buscar contexto e executa **Skills** para ações externas.
4. O modelo (LLM) gera a resposta bruta.
5. O **Output Guardrail** verifica se a resposta não é tóxica, alucinada ou se vaza dados.
6. O **Usuário** recebe a resposta final processada.
7. O sistema inteiro é continuamente avaliado pela camada de **Harness**.

---
*Repositório mantido por [Eng. Idelfrides Jorge/@idelfrides] - Em construção 🚀*
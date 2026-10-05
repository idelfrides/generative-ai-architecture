# 📚 Processamento de Linguagem Natural (NLP)

O **Processamento de Linguagem Natural (NLP)** é a subárea da Inteligência Artificial dedicada a dar aos computadores a capacidade de entender, interpretar e gerar a linguagem humana de forma valiosa. 

Para um Engenheiro de Software trabalhando com GenAI, entender a evolução do NLP não é apenas história institucional; é essencial para compreender *por que* os LLMs atuais funcionam da maneira que funcionam, e por que conceitos como **Tokens** e **Embeddings** são a base de tudo o que construiremos (como RAG e Agentes).



## 📈 A Evolução do NLP: Das Regras aos Transformers

A jornada para chegarmos ao ChatGPT e sistemas similares levou décadas de pesquisa e mudança de paradigmas.

### 1. Sistemas Baseados em Regras (Anos 1950 - 1980)
No início, a compreensão de texto era feita através de regras criadas manualmente por linguistas e programadores (Expressões Regulares, gramáticas formais).
* **Como funcionava:** `SE palavra == "olá" ENTÃO responda "Oi!"`
* **Limitação:** A linguagem humana é ambígua, cheia de gírias e sarcasmo. É impossível mapear todas as regras em `if/else`.
* **Exemplo Clássico:** **ELIZA** (1966), o primeiro "chatbot" psicoterapeuta.

### 2. NLP Estatístico e Machine Learning (Anos 1990 - 2010)
Os computadores ficaram mais rápidos, e começamos a usar estatística em vez de regras fixas. 
* **Como funcionava:** Modelos como *Bag of Words (BoW)* e *TF-IDF* contavam a frequência das palavras para classificar textos. Algoritmos clássicos como Naive Bayes e SVM dominavam.
* **Limitação:** Esses modelos perdiam a **ordem** e o **contexto** das palavras. Para o computador, "O cachorro mordeu o homem" e "O homem mordeu o cachorro" eram vetores quase idênticos.

### 3. Deep Learning e Redes Neurais Recorrentes (2010 - 2017)
A revolução das Redes Neurais. Aqui nascem os **Word Embeddings** (como Word2Vec e GloVe) e o uso de RNNs (Recurrent Neural Networks) e LSTMs.
* **Como funcionava:** O texto passou a ser processado de forma sequencial (palavra por palavra). Os modelos começaram a entender a "memória" de curto prazo de uma frase.
* **Limitação:** O processamento sequencial era lento, difícil de paralelizar em GPUs e, em textos muito longos, o modelo "esquecia" o que estava no início (o problema de *vanishing gradient*).

### 4. A Revolução dos Transformers e LLMs (2017 - Presente)
O marco zero da GenAI moderna. Em 2017, o Google publicou o artigo *"Attention is All You Need"*, introduzindo a arquitetura **Transformer**.
* **Como funciona:** Substituiu a leitura sequencial pelo mecanismo de **Self-Attention**. O modelo analisa todas as palavras de uma vez e calcula matematicamente quais partes da frase merecem mais "atenção" para entender o contexto global.
* **Resultado:** Treinamento altamente paralelizável (ideal para GPUs) e o nascimento dos Large Language Models (LLMs) como GPT, BERT e LLaMA.

<!-- 
![Linha do Tempo Evolutiva do NLP](https://via.placeholder.com/800x200?text=Evolucao+do+NLP:+Regras+->+Estatistica+->+Deep+Learning+->+Transformers) 
-->


## ⏰ Ilustração da Linha do Tempo Evolutiva do NLP

<p align="center">
    <img src="https://raw.githubusercontent.com/idelfrides/portfolio-assets/main/images/understanding_NLP.jpeg" alt="Understanding NLP image ilustration" width="800" title="Understanding NLP"/>
</p>


## 🔑 Conceitos Fundamentais para GenAI

Se você vai construir aplicações com IA Generativa, estes são os três pilares que você manipulará diariamente.

### 1. Tokens e Tokenização
LLMs não leem letras ou palavras; eles leem **Tokens**. Um token pode ser uma palavra inteira, uma sílaba ou apenas uma letra. 
* **Regra de ouro:** 1 Token $\approx$ 0.75 palavras (em inglês). Em português, o modelo costuma quebrar mais as palavras, gastando mais tokens.
* **Impacto na Arquitetura:** As APIs (OpenAI, Anthropic) cobram por token. O limite de "memória" do modelo é medido em tokens (Context Window).

#### 💻 Exemplo Prático: Contando Tokens (Python)
*Usando a biblioteca `tiktoken` da OpenAI.*

```python
import tiktoken

# Carrega o codificador usado pelo GPT-4
enc = tiktoken.encoding_for_model("gpt-4")

texto = "Engenharia de software com IA generativa"
tokens = enc.encode(texto)

print(f"Texto original: '{texto}'")
print(f"Total de Tokens: {len(tokens)}")
print(f"IDs dos tokens: {tokens}")

# Decodificando para ver como o modelo enxergou os pedaços
for token_id in tokens:
    print(f"{token_id} -> {enc.decode([token_id])}")
```

### 2. Embeddings (Vetorização Semântica)
O processo de transformar texto em arrays numéricos (vetores) onde a **distância entre os números representa a similaridade de significado**. 
* **O truque mágico:** A famosa equação matemática de embeddings: `Vetor(Rei) - Vetor(Homem) + Vetor(Mulher) ≈ Vetor(Rainha)`.
* **Impacto na Arquitetura:** Embeddings são o coração do **RAG**. Usamos embeddings para converter os documentos da nossa empresa e armazená-los em um banco de dados vetorial.

![Visualização de Word Embeddings em espaço 3D](https://via.placeholder.com/800x400?text=Representacao+Visual+de+Embeddings+em+Espaco+Vetorial)

#### 💻 Exemplo Prático: Gerando Embeddings
```python
from openai import OpenAI

client = OpenAI(api_key="SUA_API_KEY")

resposta = client.embeddings.create(
    input="Arquitetura de software e bancos de dados",
    model="text-embedding-3-small"
)

# O resultado será uma lista de floats (ex: 1536 dimensões)
vetor = resposta.data[0].embedding
print(f"Dimensões do vetor: {len(vetor)}")
print(f"Primeiros 5 valores: {vetor[:5]}")
```

### 3. O Mecanismo de Attention (Atenção)
É o mecanismo que permite ao Transformer avaliar a importância de cada palavra da frase em relação às outras.
* **Exemplo:** Na frase *"O banco do parque estava quebrado, então fui ao banco sacar dinheiro"*. O mecanismo de atenção percebe que no primeiro caso "banco" relaciona-se com "parque" e "sentar", e no segundo caso com "sacar" e "dinheiro".



## 🎯 Conclusão e Próximos Passos
Dominar NLP teoricamente nos prepara para a próxima camada: lidar com **LLMs (Large Language Models)** na prática. Agora que entendemos que textos viram **tokens**, processados via **attention** após serem convertidos por **embeddings**, estamos prontos para explorar engenharia de prompt, hiperparâmetros de inferência e consumo de APIs.

➡️ **Próximo Estudo:** [LLMs (Large Language Models)](./LLM.md)
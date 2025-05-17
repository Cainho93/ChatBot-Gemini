# 🤖 Seu Assistente Financeiro Multifacetado: Consulta, Educação e Simulação! 🏦

[![Python Version](https://img.shields.io/badge/python-3.9%2B-blue.svg)](https://python.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) **Domine suas finanças com um chatbot inteligente que oferece consultoria, educação e simulações de investimento personalizadas e ajustadas pela inflação!**

Este projeto é um chatbot financeiro avançado desenvolvido em Python, utilizando o Google Agent Development Kit (ADK) e o poder dos modelos de linguagem Gemini da Google. Ele se destaca por sua arquitetura com **três agentes especializados**, projetados para fornecer uma experiência financeira completa e interativa:

* **Consultoria e Educação Financeira Detalhada:** Com o `ConsultorFinanceiro`.
* **Suporte Ágil para Processos e Dúvidas Operacionais:** Com o `SuporteOperacional`.
* **Simulações de Investimento Avançadas:** Com o `SimuladorFinanceiro`, capaz de buscar taxas de mercado e apresentar resultados ajustados pela inflação, com opção de download dos detalhes.

---

## ✨ Funcionalidades Principais

* **🧠 Arquitetura Multiagente Especializada:**
    * **`ConsultorFinanceiro`**: Seu guru para um vasto leque de informações. Ele cobre:
        * **Produtos e Mercado**: Análise detalhada de investimentos (CDB, LCI/LCA, Ações, Fundos, Tesouro Direto), empréstimos, seguros, etc. Comparações, taxas, riscos e tendências de mercado.
        * **Educação Financeira**: Explicações claras sobre conceitos financeiros (inflação, Selic, CDI, juros compostos), dicas de orçamento pessoal, estratégias para economizar e sair de dívidas.
    * **`SuporteOperacional`**: Seu ponto de contato para resolver dúvidas processuais e técnicas, como:
        * Processos bancários (abertura/encerramento de contas).
        * Gerenciamento de cartões, transações (PIX, TED, boletos).
        * Suporte técnico básico para acesso a apps e sites bancários.
    * **`SimuladorFinanceiro`**: Um agente dedicado que interage com você para:
        * Coletar dados para simulações de investimento (valor inicial, aportes mensais, taxa de juros nominal anual, período em anos e **taxa de inflação anual esperada**).
        * Utilizar o `Google Search` para buscar taxas de mercado atuais (Selic, CDI, projeções de inflação) caso você solicite, sempre pedindo sua confirmação antes de usar.
* **💹 Simulador de Investimentos Detalhado (Ajustado pela Inflação):**
    * Receba projeções do seu investimento considerando o **poder de compra futuro em termos de hoje**.
    * Resultados apresentados de forma textual e clara, incluindo valor final real e total nominal investido.
    * **📄 Download dos Resultados:** Em ambientes como o Google Colab, você pode baixar um arquivo `.txt` com os detalhes completos da sua simulação.
* **🔍 Busca Inteligente de Informações:** Os agentes `ConsultorFinanceiro` e `SimuladorFinanceiro` utilizam o `Google Search` para fornecer dados atualizados.
* **🗣️ Interação e Contexto Aprimorados:**
    * Reconhece uma ampla variedade de saudações e frases de encerramento (incluindo gírias e formas coloquiais).
    * Lógica de roteamento por palavras-chave (com tratamento para variações e falta de acentos) para direcionar sua pergunta ao especialista correto.
    * Gerenciamento de contexto para manter a fluidez da conversa, incluindo:
        * Prioridade para continuar diálogos em andamento com o `SimuladorFinanceiro` durante a coleta de dados.
        * Capacidade de responder a perguntas de acompanhamento sobre os resultados de uma simulação recém-realizada diretamente pelo sistema.
        * Passagem de contexto básico (última pergunta e resumo da resposta) ao trocar de agente em perguntas de follow-up.
* **🛡️ Foco na Informação Segura e Responsável:**
    * Inclui disclaimers claros informando que o chatbot fornece informações gerais e educativas, não constituindo aconselhamento financeiro personalizado.

---

## 💡 Como Funciona? A Arquitetura

1.  **Interface com o Usuário**: Interação via console.
2.  **Pré-processamento**: Saudações e frases de encerramento são tratadas diretamente.
3.  **Roteamento por Palavras-Chave**: Um sistema de pontuação baseado em palavras-chave (com robustez a variações de acentuação) direciona a pergunta ao agente mais adequado (`ConsultorFinanceiro`, `SuporteOperacional`, ou `SimuladorFinanceiro`), com lógicas de prioridade para continuidade e pedidos explícitos.
4.  **Interação com Agentes (ADK)**: A pergunta (com possível contexto) é enviada ao agente escolhido (instâncias de modelos Gemini com instruções específicas).
5.  **Execução de Simulações**:
    * O `SimuladorFinanceiro` coleta os 5 parâmetros necessários, podendo usar `Google Search` para taxas de mercado (com confirmação do usuário).
    * Retorna um comando interno `ACAO_SIMULAR:{{...}}`.
    * O código Python principal intercepta esta ação, chama a função `simular_investimento_juros_compostos` (que calcula o valor final real, ajustado pela inflação), e apresenta os resultados textualmente.
    * No Colab, um arquivo `.txt` é oferecido para download.
6.  **Respostas e Continuidade**: As respostas dos agentes ou os resultados da simulação são exibidos, e o sistema armazena informações da última interação para contexto.

---

## 🛠️ Tecnologias Utilizadas

* **Python 3.9+**
* **Google Agent Development Kit (`google-adk`)**
* **Google Generative AI SDK (`google-generativeai`)**
    * Modelos Gemini (ex: `gemini-2.5-pro-preview-03-25`, `gemini-2.0-flash-001`)
* **Google Search** (como ferramenta dos agentes)
* **IPython.display** (`Markdown`, `display` - para formatação da saída no Colab/Jupyter)
* **google.colab.files** (para a funcionalidade de download no Colab)
* Bibliotecas padrão Python: `json`, `re`, `datetime`, `os`, `sys`, `io`.

---

## 🚀 Como Executar?

Este projeto é ideal para ser executado em um ambiente como o Google Colab.

### Pré-requisitos

* Uma conta Google.
* Uma Chave de API válida do Google AI Studio ou do Google Cloud com a API "Generative Language" habilitada.

### Configuração

1.  **Clone o Repositório (se o projeto estiver no GitHub):**
    ```bash
    git clone [URL_DO_SEU_REPOSITORIO_AQUI]
    cd [NOME_DO_SEU_REPOSITORIO]
    ```
2.  **Instale as Dependências (em uma célula no início do seu Notebook Colab):**
    ```python
    !pip install -q google-adk google-generativeai
    ```
3.  **Configure sua Chave API no Google Colab:**
    * No menu à esquerda do Colab, clique no ícone de chave (🔑 Secrets).
    * Crie um novo "Secret" com o nome `GOOGLE_API_KEY`.
    * Cole a sua chave de API como o valor do secret.
    * Certifique-se de que a opção "Notebook access" (Acesso ao notebook) esteja marcada.
    * O script principal tentará carregar esta chave automaticamente.

### Executando o Chatbot

Após a configuração, execute a célula principal do seu notebook Python que contém todo o código do chatbot. Ele começará com a mensagem de boas-vindas e um prompt para você digitar sua pergunta.

---

## 💬 Exemplos de Interação

**Usuário:** `bora de simulação`
**Chatbot (ConsultorFinanceiro):** `🤖 Nosso SimuladorFinanceiro pode te ajudar com isso. Gostaria de fazer uma simulação agora?`
**Usuário:** `sim`
**Chatbot (SimuladorFinanceiro):** `🤖 Ok! Direcionando para o SimuladorFinanceiro para iniciar a simulação... Qual o valor inicial que você já possui para investir?`
**Usuário (para Simulador):** `1000 iniciais, 500 de aporte, use a selic como taxa e a inflação atual durante um periodo de 10 anos`
**Chatbot (SimuladorFinanceiro):** (Interage para confirmar Selic e inflação encontradas via busca, e os outros parâmetros) ...
`Entendido! Com os dados confirmados: valor inicial R$1000.00, aporte mensal R$500.00, taxa de juros nominal anual X.XX% (0.XX), período de 10.0 anos, e inflação anual esperada Y.YY% (0.YY).`
`ACAO_SIMULAR:{{...}}`
**(Sistema então exibe os resultados textuais da simulação ajustada pela inflação e oferece o download do arquivo .txt)**

**Usuário:** `qual foi o lucro real disso?`
**Chatbot:** (Calcula e exibe o lucro real baseado nos resultados da última simulação) `Analisando os resultados da sua última simulação: ... Seu Lucro/Rendimento Real ... foi de: R$ ZZZ,ZZ`

---

## 🔮 Próximos Passos & Ideias Futuras

* **Roteamento por LLM:** Implementar um roteador de intenções usando um LLM para um direcionamento ainda mais inteligente e flexível (substituindo o sistema de keywords).
* **Gráficos Visuais:** Reintroduzir gráficos (ex: com `matplotlib` no Colab ou bibliotecas web como Plotly/Chart.js se migrar para uma aplicação web).
* **Mais Tipos de Simulação:** Financiamentos (SAC/Price), projeção detalhada para aposentadoria, etc.
* **Interface de Usuário:** Desenvolver uma interface web ou integrar com plataformas de mensagens.

---

## 📜 Licença

Este projeto está licenciado sob a Licença MIT. (Sugestão: Crie um arquivo `LICENSE` no seu repositório com o texto da licença MIT se desejar).

---

**Dica Extra:** Adicione um GIF curto no topo do seu README mostrando o chatbot em ação (especialmente a simulação e a interação com os diferentes agentes). Isso pode aumentar muito o engajamento de quem visita seu repositório!

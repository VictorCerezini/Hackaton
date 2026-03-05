# PROJETO: MODELAGEM DE AMEAÇAS UTILIZANDO IA

# **1\. Visão Geral**

O objetivo desta solução é automatizar a análise de segurança de diagramas de arquitetura de software. Utilizando Inteligência Artificial Multimodal (Visão \+ Linguagem), o sistema identifica componentes, fluxos de dados e aplica a metodologia STRIDE para gerar um relatório detalhado de riscos e mitigações, atendendo aos requisitos de MVP solicitados pela FIAP Software Security.

# **2\. Pilha Tecnológica (Stack)**

* **Motor de IA:** Google Gemini 1.5 Flash (Modelo Multimodal de alta performance)  
* **Linguagem:** Python 3.10+  
* **Bibliotecas de Visão:** PIL (Pillow) para processamento de imagens  
* **Integração:** google-generativeai para comunicação com o LLM  
* **Tratamento de Dados:** json e re (Regex) para extração de dados estruturados  
* **Ambiente:** Google Colab

# **3\. Fluxo de Desenvolvimento e Execução**

O desenvolvimento foi estruturado em um pipeline de cinco etapas fundamentais:

1. **Configuração e Ingestão de Dados:** O sistema solicita uma chave de API segura e permite o upload de diagramas complexos em formatos PNG ou JPG.  
2. **Processamento Multimodal (Visão Computacional):** Utilizamos In-Context Learning para que o modelo interprete semântica visual sem necessidade de treinamento manual (Fine-tuning), permitindo reconhecer ícones de nuvem (Azure, AWS) e fluxos de dados.  
3. **Engenharia de Prompt e Análise STRIDE:** Desenvolvimento de um prompt sistêmico que força a IA a classificar cada componente nas categorias STRIDE: Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service e Elevation of Privilege.  
4. **Extração Robusta de JSON:** Implementação de um parser com expressões regulares para garantir que a resposta da IA seja convertida em dados estruturados, eliminando ruídos de texto ou markdown.  
5. **Geração do Relatório Final:** O sistema renderiza um relatório técnico detalhando o risco específico de cada componente e a contramedida (Mitigação) recomendada.

# **4\. Arquitetura da Solução (Fluxo Lógico)**

A solução segue o seguinte fluxo lógico: Entrada do Diagrama \-\> Processamento Multimodal (Gemini) \-\> Extração via Prompt Engineering \-\> Parser de JSON \-\> Relatório Final Estruturado.

    graph LR  
    A\[Imagem do Diagrama\] \--\> B\[Gemini 1.5 Flash API\]

    C\[Prompt Estruturado\] \--\> B

    B \--\> D{Parser JSON}

    D \--\>|Sucesso| E\[Relatório STRIDE Formatado\]

    D \--\>|Erro| F\[Fallback/Regex Cleanup\]

    F \--\> E

# **5\. Metodologia de Análise (STRIDE)**

A IA correlaciona os componentes identificados com ameaças reais baseadas em contexto:

* Componentes de Identidade (ex: Entra ID): Foco em Spoofing e Acesso não autorizado.  
* Gateways e APIs: Foco em Negação de Serviço (DoS) e Manipulação (Tampering).  
* Conexões (Setas): Foco em Vazamento de Dados (Information Disclosure) através de interceptação de tráfego.

# **6\. Considerações sobre o Treinamento do Modelo**

Para atender aos requisitos do projeto de 'treinamento', a solução adota o estado da arte com Zero-Shot Prompting em modelos de fundação. Essa abordagem substitui o treinamento estático de Redes Neurais tradicionais por uma IA Multimodal que já possui conhecimento prévio de segurança defensiva, sendo capaz de aprender o contexto do diagrama específico via instruções contidas no prompt.

# **7\. Conclusão**

O MVP demonstrou alta eficácia ao reduzir o tempo de uma modelagem de ameaças manual de horas para segundos. A solução fornece uma base sólida de segurança, permitindo que arquitetos foquem na correção das vulnerabilidades identificadas pela IA desde o início do ciclo de vida do software (Security by Design).


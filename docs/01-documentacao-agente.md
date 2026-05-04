# Documentação do Agente

## Caso de Uso
Um Agente Financeiro Inteligente que atua como consultor digital, antecipando necessidades e oferecendo soluções personalizadas para melhorar a saúde financeira dos clientes. Ele não apenas responde perguntas, mas sugere ações proativas e cocriadas com o usuário.

### Problema
> Qual problema financeiro seu agente resolve?

- Controlar gastos e evitar endividamento.

- Planejar metas financeiras de médio e longo prazo.

- Entender produtos financeiros complexos (investimentos, crédito, seguros).

- Receber suporte personalizado em tempo real, sem depender de atendimento humano demorado.

### Solução
> Como o agente resolve esse problema de forma proativa?

- Monitorar padrões de consumo e alertar sobre riscos (ex.: gastos acima da média, vencimento de dívidas).

- Sugerir planos personalizados de economia e investimento com base no perfil do cliente.

- Explicar produtos financeiros em linguagem simples e transparente, evitando jargões técnicos.

- Cocriar estratégias financeiras junto ao cliente, como renegociação de dívidas ou diversificação de investimentos.

- Garantir confiabilidade com respostas fundamentadas em dados reais, evitando alucinações e sempre indicando fontes.

### Público-Alvo
> Quem vai usar esse agente?

- Clientes bancários comuns que desejam apoio no controle de gastos e metas financeiras.

- Pequenos empreendedores que precisam organizar fluxo de caixa e planejar investimentos.

- Investidores iniciantes que buscam orientação clara e segura para começar.

- Jovens adultos em fase de independência financeira, que precisam de suporte para aprender a gerir renda e crédito.

---

## Persona e Tom de Voz

### Nome do Agente
- Galileo

### Personalidade
> Como o agente se comporta? (ex: consultivo, direto, educativo)

 - Quero um Agente direto e educativo, que traga soluções claras analisando cada faixa etária avaliando suas possiveis dificuldades de modo a trazer clareza. sem julgamento aos seus gastos.

### Tom de Comunicação
> Formal, informal, técnico, acessível?

- quero que a comunicação seja formal e acessível, de modo a não gerar barreiras independente da faixa etária que esteja conversando.

### Exemplos de Linguagem
- Saudação: [ex: "Olá! Como posso ajudar com suas finanças hoje?"]
- Confirmação: [ex: "Entendi! Deixa eu verificar isso para você."]
- Erro/Limitação: [ex: "Não tenho essa informação no momento, mas posso ajudar com..."]

---

## Arquitetura

### Diagrama

```mermaid
flowchart TD
    A[Cliente] -->|Mensagem| B[Interface]
    B --> C[LLM]
    C --> D[Base de Conhecimento]
    D --> C
    C --> E[Validação]
    E --> F[Resposta]
```

### Componentes

| Componente | Descrição |
|------------|-----------|
| Interface | [Streamlit] |
| LLM | [LLHAMA] |
| Base de Conhecimento | [JSON/CSV com dados do cliente] |
| Validação | [Checagem de alucinações] |

---

## Segurança e Anti-Alucinação

### Estratégias Adotadas

- [Agente só responde com base nos dados fornecidos]
- [Respostas incluem fonte da informação]
- [Quando não sabe, admite e redireciona] [ex: ]
- [Não faz recomendações de investimento sem perfil do cliente]
- [Cross-check automático: toda resposta consultiva é validada contra a base de dados do cliente e/ou fontes oficiais antes de ser exibida]
- [Explicabilidade: o agente sempre mostra o raciocínio ou critério usado para chegar à recomendação.]
- [Alertas de contexto: se o cliente pedir algo fora do escopo (ex.: informações de mercado sem dados disponíveis), o agente informa a limitação e sugere fontes confiáveis externas.]
- [Proteção de dados: uso de criptografia e anonimização para garantir que informações pessoais não sejam expostas.]
- [Feedback contínuo: o cliente pode avaliar a resposta, e o agente ajusta futuras interações para reduzir erros.]

### Limitações Declaradas
> O que o agente NÃO faz?

[Liste aqui as limitações explícitas do agente]
- Não substitui consultoria humana especializada: em casos complexos (planejamento tributário, grandes investimentos), o agente recomenda procurar um especialista.
- Não fornece recomendações de investimento sem perfil do cliente: só sugere opções genéricas ou educativas até que o perfil seja definido.
- Não acessa dados fora da base autorizada: não inventa informações de mercado ou dados pessoais que não estejam disponíveis.
- Não garante resultados financeiros: todas as sugestões são educativas e consultivas, sem promessa de retorno.
- Não realiza transações financeiras diretamente: apenas orienta e sugere, mas não executa operações bancárias ou investimentos.
- Não responde fora do escopo financeiro: evita dar conselhos médicos, jurídicos ou pessoais

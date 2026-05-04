# Base de Conhecimento

## Dados Utilizados

Descreva se usou os arquivos da pasta `data`, por exemplo:

| Arquivo | Formato | Utilização no Agente |
|---------|---------|---------------------|
| `historico_atendimento.csv` | CSV | Contextualizar interações anteriores |
| `perfil_investidor.json` | JSON | Personalizar recomendações |
| `produtos_financeiros.json` | JSON | Sugerir produtos adequados ao perfil |
| `transacoes.csv` | CSV | Analisar padrão de gastos do cliente |

> [!TIP]
> **Quer um dataset mais robusto?** Você pode utilizar datasets públicos do [Hugging Face](https://huggingface.co/datasets) relacionados a finanças, desde que sejam adequados ao contexto do desafio.

---

## Adaptações nos Dados

- Normalização: padronização de categorias de gastos (ex.: lazer, alimentação, transporte).

- Enriquecimento: inclusão de campos extras como objetivos financeiros (ex.: viagem, compra de imóvel).

- Anonimização: remoção de dados sensíveis para testes e prototipagem.

- Simulação: criação de perfis fictícios para demonstrar diferentes faixas etárias e perfis de risco.

---

## Estratégia de Integração

### Como os dados são carregados?
> Descreva como seu agente acessa a base de conhecimento.

- Carregamento inicial: os arquivos JSON/CSV são carregados no início da sessão.

- Consulta dinâmica: o agente acessa os dados conforme a interação do usuário, sem sobrecarregar o prompt.

- Contextualização no prompt: apenas informações relevantes são inseridas no contexto da resposta (ex.: últimas transações ou perfil de investidor).

- Validação cruzada: antes de sugerir qualquer ação, o agente compara os dados do cliente com regras pré-definidas (ex.: não recomendar investimento sem perfil).

### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?

Dados do Cliente:
- Nome: João Silva
- Perfil: Moderado
- Saldo disponível: R$ 5.000

Últimas transações:
- 01/11: Supermercado - R$ 450
- 03/11: Streaming - R$ 55
- 05/11: Restaurante - R$ 120

Objetivo: Guardar R$ 10.000 em 12 meses para viagem internacional.


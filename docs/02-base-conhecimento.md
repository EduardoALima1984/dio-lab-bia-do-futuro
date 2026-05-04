# Base de Conhecimento

## Dados Utilizados

Descreva se usou os arquivos da pasta `data`, por exemplo:

| Arquivo | Formato | Para que serve no Galileo |
|---------|---------|---------------------|
| `historico_atendimento.csv` | CSV | Contextualizar interações anteriores - Dando continuidade aos atendimentos anteriores |
| `perfil_investidor.json` | JSON | Personalizar recomendações sobre as dúvidas e aprendizado do cliente |
| `produtos_financeiros.json` | JSON | Sugerir produtos adequados ao perfil |
| `transacoes.csv` | CSV | Analisar padrão de gastos do cliente e usar essas informações de forma didática |


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

import pandas as pd
import json

# --- Carregamento inicial ---
# CSVs e JSONs são carregados no início da sessão
historico = pd.read_csv("data/historico_atendimento.csv")
transacoes = pd.read_csv("data/transacoes.csv")

with open("data/perfil_investidor.json", "r", encoding="utf-8") as f:
    perfil = json.load(f)

with open("data/produtos_financeiros.json", "r", encoding="utf-8") as f:
    produtos = json.load(f)

# --- Consulta dinâmica ---
# Exemplo: buscar últimas transações do cliente
ultimas_transacoes = transacoes.tail(5)

# --- Contextualização no prompt ---
# Apenas informações relevantes são inseridas no contexto
contexto = {
    "nome": perfil["nome"],
    "perfil_investidor": perfil["perfil_investidor"],
    "objetivo_principal": perfil["objetivo_principal"],
    "saldo_disponivel": perfil["patrimonio_total"],
    "ultimas_transacoes": ultimas_transacoes.to_dict(orient="records")
}

# --- Validação cruzada ---
# Exemplo: não recomendar produtos fora do perfil
def recomendar_produtos(perfil, produtos):
    recomendados = []
    for p in produtos:
        if perfil["perfil_investidor"] == "moderado" and p["risco"] in ["baixo", "medio"]:
            recomendados.append(p)
    return recomendados

produtos_recomendados = recomendar_produtos(perfil, produtos)

# --- Exemplo de saída ---
print("Contexto montado para o agente:")
print(json.dumps(contexto, indent=2, ensure_ascii=False))

print("\nProdutos recomendados para o perfil moderado:")
for p in produtos_recomendados:
    print(f"- {p['nome']} ({p['categoria']}, risco {p['risco']})")

### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?
- Os dados não são todos carregados no system prompt.
- O agente acessa a base de conhecimento dinamicamente, conforme a interação.
- Apenas informações relevantes e recentes são inseridas no prompt (ex.: últimas transações, perfil do investidor, metas).
- Isso garante que o modelo não fique sobrecarregado e que as respostas sejam contextuais e confiáveis.
- Antes de sugerir qualquer ação, há uma validação cruzada com regras pré-definidas (ex.: não recomendar investimento sem perfil).

Exemplo de atendimento:
Dados do Cliente:
- Nome: João Silva
- Perfil: Moderado
- Saldo disponível: R$ 5.000

Últimas transações:
- 01/11: Supermercado - R$ 450
- 03/11: Streaming - R$ 55
- 05/11: Restaurante - R$ 120

Objetivo: Guardar R$ 10.000 em 12 meses para viagem internacional.


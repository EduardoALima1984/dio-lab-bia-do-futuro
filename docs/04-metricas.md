# Avaliação e Métricas

## Como Avaliar seu Agente

A avaliação pode ser feita de duas formas complementares:

1. **Testes estruturados:** Você define perguntas e respostas esperadas;
2. **Feedback real:** Pessoas testam o agente e dão notas.

---

## Métricas de Qualidade

| Métrica | O que avalia | Exemplo de teste |
|---------|--------------|------------------|
| **Assertividade** | O agente respondeu o que foi perguntado? | Perguntar o saldo e receber o valor correto |
| **Segurança** | O agente evitou inventar informações? | Perguntar algo fora do contexto e ele admitir que não sabe |
| **Coerência** | A resposta faz sentido para o perfil do cliente? | Sugerir investimento conservador para cliente conservador |


---

Teste 1: Consulta de gastos
- **Pergunta:** "Quanto gastei com alimentação?"
- **Resposta esperada:** Valor baseado no `transacoes.csv`
- **Resultado:** [x] Correto  [ ] Incorreto

Teste 2: Recomendação de produto
- **Pergunta:** "Qual investimento você recomenda para mim?"
- **Resposta esperada:** Produto compatível com o perfil do cliente
- **Resultado:** [x] Correto  [ ] Incorreto

Teste 3: Pergunta fora do escopo
- **Pergunta:** "Qual a previsão do tempo?"
- **Resposta esperada:** Agente informa que só trata de finanças
- **Resultado:** [x] Correto  [ ] Incorreto

Teste 4: Informação inexistente
- **Pergunta:** "Quanto rende o produto XYZ?"
- **Resposta esperada:** Agente admite não ter essa informação
- **Resultado:** [x] Correto  [ ] Incorreto

---

## Resultados

Após os testes, registre suas conclusões:

**O que funcionou bem:**
✅ Fallback local: o agente responde mesmo sem o Ollama ativo, usando dados do CSV/JSON.

✅ Contexto personalizado: o Galileo usa nome, perfil e histórico para dar respostas contextualizadas.

✅ Respostas fora do escopo: ele se mantém no tema financeiro e responde com elegância.

✅ Mensagens de erro amigáveis: quando o servidor não responde, o app mostra aviso claro sem travar.

✅ Comando exit: encerra a sessão de forma limpa e intuitiva.

**O que pode melhorar:**
⚙️ Memória persistente: salvar histórico de conversas para manter contexto entre sessões.

⚙️ Análises proativas: permitir que o agente gere insights mensais automaticamente (ex.: resumo de gastos).

⚙️ Interface visual: adicionar cores ou ícones nos balões de chat para diferenciar usuário e assistente.

⚙️ Expansão de escopo: incluir perguntas sobre planejamento financeiro, metas e simulações de investimento.

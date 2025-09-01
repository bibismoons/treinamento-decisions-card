# Exercício 106: Percentual de Contas Inativas por Mais de 90 Dias

## 📝 Pergunta

Calcule o percentual de contas que não fazem compras há mais de 90 dias sobre o total de contas cadastradas. Use a maior data de venda da base como referência.

Mostre: `total_contas_cadastradas`, `contas_sem_compras_90_dias`, `percentual_contas_sem_compras_90_dias`.

## 🎯 Objetivo

Demanda estratégica para medir a taxa de dormência da base de clientes e avaliar a necessidade de campanhas de reativação.

## 💡 Contexto de Negócio

Este KPI ajuda a entender a saúde da base ativa e pode indicar problemas na experiência do cliente ou na competitividade dos produtos.

## 💡 Dica Importante

Use `(SELECT MAX(dt_venda) FROM decisionscard.t_venda) - INTERVAL '90 days'` para calcular a data limite.

---

## ✍️ Sua Resposta

```sql


```

---

## 📋 Critérios de Avaliação

- [ ] Query executa sem erros
- [ ] Usa data máxima da base como referência
- [ ] Identifica contas sem compras corretamente
- [ ] Calcula percentual sobre total cadastrado
- [ ] Apresenta os três valores solicitados


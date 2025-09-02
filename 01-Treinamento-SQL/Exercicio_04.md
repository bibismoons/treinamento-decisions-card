# Exercício 4: Top 5 Vendas por Valor

## 📝 Pergunta

Encontre as 5 vendas (`t_venda`) de maior valor da base de dados. Mostre os campos `id_venda`, `id_cliente`, `vl_venda` e `dt_venda`. Ordene do maior valor para o menor.

## 🎯 Objetivo

Praticar:
- Ordenação decrescente (DESC)
- Limitação de resultados com LIMIT
- Trabalho com campos numéricos e de data
- Identificação de registros extremos (top N)

## 💡 Dica

Para ordenar do maior para o menor, use ORDER BY campo DESC.

---

## ✍️ Sua Resposta

```sql

select id_venda,
       id_cliente,
       vl_venda,
       dt_venda
from t_venda
order by vl_venda desc
limit 5;

```

---

## 📋 Critérios de Avaliação

- [x] Query executa sem erros
- [x] Retorna exatamente 5 registros
- [x] Ordenação decrescente por valor
- [x] Campos corretos são exibidos
- [x] Mostra as vendas de maior valor


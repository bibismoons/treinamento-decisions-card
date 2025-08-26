# Exercício 112: Ranking dos Clientes por Quantidade/Valor de Compras

## 📝 Pergunta

Crie um ranking dos top 50 clientes por valor de compras. Mostre:

- `posicao` (ranking)
- `id_cliente`
- `nm_cliente`
- `qtd_compras` (número de vendas ativas)
- `valor_total` (soma das vendas)
- `ticket_medio` (valor médio por compra)
- `primeira_compra` (data da primeira compra)
- `ultima_compra` (data da última compra)
- `dias_cliente` (dias entre primeira e última compra)
- `frequencia_compra` (compras por mês em média)

Considere apenas vendas ativas e ordene por valor total decrescente.

## 🎯 Objetivo

Demanda comercial para identificar clientes VIP e personalizar estratégias de relacionamento.

## 💡 Contexto de Negócio

Conhecer os melhores clientes permite criar programas de fidelidade e ações comerciais direcionadas para maximizar o lifetime value.

---

## ✍️ Sua Resposta

```sql
--Tentativa 1:
select 
    c.id_cliente,
    c.nm_cliente,
    tv.vl_venda
from t_cliente c
join t_venda tv on tv.id_cliente = c.id_cliente
where c.id_cliente in (
    select sum(vl_venda) 
    from t_venda)
order by tv.vl_venda desc;

with compras as (
    select 
        v.id_cliente,
        count(v.id_venda) as qtd_compras,
        sum(v.vl_venda) as valor_total,
        avg(v.vl_venda) as ticket_medio,
        min(v.dt_venda) as primeira_compra,
        max(v.dt_venda) as ultima_compra
    from t_venda v
    where v.fl_status_venda = 'A'
    group by v.id_cliente
),
metricas as (
    select
        c.id_cliente,
        c.nm_cliente,
        cmp.qtd_compras,
        cmp.valor_total,
        cmp.ticket_medio,
        cmp.primeira_compra,
        cmp.ultima_compra,
        extract(day from cmp.ultima_compra - cmp.primeira_compra) as dias_cliente,
        case 
            when extract(month from age(cmp.ultima_compra, cmp.primeira_compra)) = 0 
                and extract(year from age(cmp.ultima_compra, cmp.primeira_compra)) = 0 
            then cmp.qtd_compras
            else round(cmp.qtd_compras::numeric / 
                    ((extract(year from age(cmp.ultima_compra, cmp.primeira_compra)) * 12) 
                    + extract(month from age(cmp.ultima_compra, cmp.primeira_compra))), 2)
        end as frequencia_compra
    from t_cliente c
    join compras cmp on c.id_cliente = cmp.id_cliente
),
ranking as (
    select 
        row_number() over (order by m.valor_total desc) as posicao, m.*
    from metricas m
)
select *
from ranking
where posicao <= 50
order by posicao;

```

---

## 📋 Critérios de Avaliação

- [ ] Query executa sem erros
- [ ] Ranking correto (ROW_NUMBER)
- [ ] Todas as métricas calculadas
- [ ] Cálculo de frequência de compra
- [ ] Limitação aos top 50


# Exercício 104: Contas sem Compras há Mais de 90 Dias

## 📝 Pergunta

Identifique quantas contas não fizeram compras há mais de 90 dias. Considere a maior data de venda existente na base como referência e contas que têm `fl_status_conta = 'A'`.

## 🎯 Objetivo

Demanda da área de retenção para identificar clientes em risco de churn e criar campanhas de reativação.

## 💡 Contexto de Negócio

Clientes inativos por muito tempo têm alta probabilidade de cancelamento. Identificá-los permite ações proativas de retenção.

## 💡 Dica Importante

Como a base não é atualizada há muito tempo, use `(SELECT MAX(dt_venda) FROM decisionscard.t_venda)` como data de referência ao invés de CURRENT_DATE.

---

## ✍️ Sua Resposta

```sql
--Tentativa 1:
select c.id_cliente as "total de contas sem compras há +90d"
    from t_cliente c
        where id_cliente in (
            select distinct id_cliente
                from t_venda
                    where dt_venda <= (
                        select max(dt_venda) 
                        from t_venda
                    ) - interval '90 day'
		)
        and c.fl_status_conta = 'A';

--Tentativa 2:
select id_cliente
    from t_cliente
        where fl_status_conta = 'A'
        and id_cliente not in (
            select c.id_cliente
--                 max(v.dt_venda)
                from t_venda v,
                     t_cliente c
                    where v.id_cliente = c.id_cliente
                    and c.fl_status_conta = 'A'
                    and v.dt_venda >= (select max(dt_venda) - interval '90 day' from t_venda)
--                  group by c.id_cliente
        );

--Tentativa 3:
with parametros as (
    select max(dt_venda) as data_referencia
        from t_venda
),

ultima_compra as (
    select 
        c.id_cliente,
        max(v.dt_venda) as dt_ultima_compra
        from t_cliente c
            join t_venda v 
            on c.id_cliente = v.id_cliente
            where c.fl_status_conta = 'A'
        group by c.id_cliente
)

select count(*) as "total de contas sem compras há +90d"
    from ultima_compra uc
        cross join parametros p
        where uc.dt_ultima_compra <= p.data_referencia - interval '90 days';

with parametros as (
    select max(dt_venda) as data_referencia
    from t_venda
),

clientes_90d as (
    select distinct c.id_cliente
        from t_cliente c
            join t_venda v 
            on c.id_cliente = v.id_cliente
        cross join parametros p
        where c.fl_status_conta = 'A'
        and v.dt_venda between (p.data_referencia - interval '90 days') and p.data_referencia
)

select count(*) as "total de contas sem compras há +90d"
    from clientes_90d;

select count(*) as "total de contas sem compras há +90d"
    from (
        select 
            c.id_cliente,
            max(v.dt_venda) as ultima_venda
            from t_cliente c
                join t_venda v 
                on c.id_cliente = v.id_cliente
                where c.fl_status_conta = 'A'
            group by c.id_cliente
    ) sub

where sub.ultima_venda <= (
    (select max(dt_venda) from t_venda) - interval '90 days'
);

```

---

## 📋 Critérios de Avaliação

- [ ] Query executa sem erros
- [ ] Usa maior data da base como referência
- [ ] Calcula diferença de 90 dias corretamente
- [ ] Considera apenas contas ativas
- [ ] Identifica última compra por cliente


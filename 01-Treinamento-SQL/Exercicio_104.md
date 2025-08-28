# Exercício 104: Contas sem Compras há Mais de 90 Dias

## 📝 Pergunta

Identifique quantas contas não fizeram compras há mais de 90 dias. Considere a maior data de venda existente na base como referência.

## 🎯 Objetivo

Demanda da área de retenção para identificar clientes em risco de churn e criar campanhas de reativação.

## 💡 Contexto de Negócio

Clientes inativos por muito tempo têm alta probabilidade de cancelamento. Identificá-los permite ações proativas de retenção.

## 💡 Dica Importante

Como a base não é atualizada há muito tempo, use `(SELECT MAX(dt_venda) FROM decisionscard.t_venda)` como data de referência ao invés de CURRENT_DATE.

---

## ✍️ Sua Resposta

```sql

--Opção 1:
select 
    count(distinct c.id_cliente) as "total de contas sem compras há +90d"
from 
    t_cliente c
where 
    id_cliente not in (
	    select 
	        distinct id_cliente
	    from 
	        t_venda
	    where 
	        dt_venda >= (
		        select 
                    max(dt_venda) 
		        from 
                    t_venda
	        ) - interval '90 day'
    ); 
    		  		
--Opção 2:
select
	count(id_cliente)
from
	t_cliente
where 
    id_cliente not in (
	    select
		    c.id_cliente
	    from
		    t_venda v,
		    t_cliente c
	    where
		    v.id_cliente = c.id_cliente
		    and v.dt_venda >= (select max(dt_venda) - interval '90 day' from t_venda)
);

```

---

## 📋 Critérios de Avaliação

- [ ] Query executa sem erros
- [ ] Usa maior data da base como referência
- [ ] Calcula diferença de 90 dias corretamente
- [ ] Identifica última compra por cliente


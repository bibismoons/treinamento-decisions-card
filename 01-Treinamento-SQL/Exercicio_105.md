# Exercício 105: Percentual de Contas Bloqueadas

## 📝 Pergunta

Calcule o percentual de contas bloqueadas em relação ao total de contas cadastradas. Considere como bloqueadas as contas que possuem pelo menos um registro ativo na tabela `t_bloqueio_cliente` (`fl_liberado = 'N'`).

Mostre o resultado como: `total_contas`, `contas_bloqueadas`, `percentual_bloqueadas`.

## 🎯 Objetivo

Demanda da área de risco para monitorar a saúde da carteira de clientes e identificar tendências de bloqueios.

## 💡 Contexto de Negócio

Alto percentual de bloqueios pode indicar problemas na política de crédito ou deterioração da qualidade da carteira.

---

## ✍️ Sua Resposta

```sql
--Tentativa 1:
with total_contas as (
    select count(*) as total
    from t_cliente
),
contas_bloqueadas as (
    select count(distinct b.id_cliente) as bloqueadas
    from t_bloqueio_cliente b
    where b.fl_liberado = 'N'
)
select 
    t.total as total_contas,
    cb.bloqueadas as contas_bloqueadas,
    round((cb.bloqueadas::numeric / t.total) * 100, 2) as percentual_bloqueadas
from total_contas t
cross join contas_bloqueadas cb;

```

---

## 📋 Critérios de Avaliação

- [ ] Query executa sem erros
- [ ] Conta total de contas corretamente
- [ ] Identifica contas com bloqueio ativo
- [ ] Calcula percentual corretamente
- [ ] Apresenta os três valores solicitados


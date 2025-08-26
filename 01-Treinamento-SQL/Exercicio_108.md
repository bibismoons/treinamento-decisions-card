# Exercício 108: Distribuição de Contas por Origem Comercial

## 📝 Pergunta

Analise a distribuição de contas por origem comercial. Mostre:

- `nm_fantasia` (nome da rede/origem)
- `quantidade_contas` (número de contas originadas)
- `percentual_total` (% sobre total de contas)
- `contas_ativas` (quantas estão ativas)
- `taxa_ativacao` (% de ativas sobre total da origem)

Considere apenas origens que geraram pelo menos 10 contas. Ordene por quantidade decrescente.

## 🎯 Objetivo

Demanda comercial para avaliar a performance dos canais de aquisição e otimizar investimentos em parcerias.

## 💡 Contexto de Negócio

Identificar quais origens comerciais geram mais clientes e qual a qualidade desses clientes (taxa de ativação) é crucial para estratégia comercial.

---

## ✍️ Sua Resposta

```sql
--Tentativa 1:
with total as (
    select count(*) as total_contas
    from t_cliente
)
select 
    r.nm_fantasia,
    count(distinct c.id_cliente) as quantidade_contas,
    round((count(distinct c.id_cliente)::numeric / t.total_contas) * 100, 2) as percentual_total,
    count(distinct case when c.fl_status_conta = 'A' then c.id_cliente end) as contas_ativas,
    round((count(distinct case when c.fl_status_conta = 'A' then c.id_cliente end)::numeric / count(distinct c.id_cliente)) * 100, 2) as taxa_ativacao
from t_cliente c
join t_venda v on c.id_cliente = v.id_cliente
join t_rede r on v.id_rede = r.id_rede
cross join total t
group by r.nm_fantasia, t.total_contas
having count(distinct c.id_cliente) >= 10
order by quantidade_contas desc;

```

---

## 📋 Critérios de Avaliação

- [ ] Query executa sem erros
- [ ] JOIN entre cliente e rede (origem)
- [ ] Calcula métricas por origem
- [ ] Filtra origens com 10+ contas
- [ ] Calcula taxa de ativação corretamente


# Exercício 107: Distribuição de Contas por Situação

## 📝 Pergunta

Crie um relatório mostrando a quantidade e percentual de contas por situação. Mostre:

- `situacao` (descrição da situação)
- `quantidade` (número de contas)
- `percentual` (% sobre o total)

Considere as situações baseadas no `fl_status_conta` e `fl_status_analise`:
- "Ativa": fl_status_conta = 'A'
- "Inativa": fl_status_conta = 'I' 
- "Pendente Análise": fl_status_analise = 'P'
- "Rejeitada": fl_status_analise = 'R'

Ordene por quantidade decrescente.

## 🎯 Objetivo

Demanda operacional para acompanhar a distribuição da carteira por status e identificar gargalos no processo.

## 💡 Contexto de Negócio

Este relatório ajuda a identificar problemas no funil de aprovação e monitorar a saúde operacional da carteira.

---

## ✍️ Sua Resposta

```sql
select td.vl_dominio as "Situação da conta",
       td.cd_dominio as "Status da conta",
       count(c.id_cliente) as "Quantidade de contas por situação",
       round((count(c.id_cliente) * 100.0 / nullif(total.total_contas, 0)), 2) as Percentual
from t_dominio td
left join t_cliente c on td.cd_dominio = c.fl_status_conta 
          and td.nm_dominio = 'FL_STATUS_CONTA'
cross join (
    select count(*) as total_contas
    from t_cliente
) as total
where td.nm_dominio = 'FL_STATUS_CONTA'
group by td.vl_dominio,
         td.cd_dominio,
         total.total_contas 
order by Percentual desc nulls last;

```

---

## 📋 Critérios de Avaliação

- [x] Query executa sem erros
- [x] Categoriza situações corretamente
- [x] Calcula quantidade por situação
- [x] Calcula percentual sobre total
- [x] Ordenação por quantidade decrescente


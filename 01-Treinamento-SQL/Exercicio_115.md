# Exercício 115: Quantidade de Cartões por Tipo de Bloqueio

## 📝 Pergunta

Analise os cartões bloqueados por tipo de bloqueio. Mostre:

- `ds_tipo_bloqueio_cartao` (descrição do tipo de bloqueio)
- `quantidade_cartoes` (número de cartões com este tipo de bloqueio)
- `percentual_total_bloqueios` (% sobre total de bloqueios)

Considere apenas bloqueios ativos (`fl_ativo = 'S'`) e faça JOIN com a tabela de tipos de bloqueio para obter a descrição. Ordene por quantidade decrescente.

## 🎯 Objetivo

Demanda de risco para entender os principais motivos de bloqueio de cartões e otimizar políticas.

## 💡 Contexto de Negócio

Identificar os tipos de bloqueio mais frequentes ajuda a melhorar processos e reduzir bloqueios desnecessários.

---

## ✍️ Sua Resposta

```sql
--Tentativa 1 errada:
select count(fl_status_cartao) as from t_cartao;

select
	count(bc.id_cartao),
	tbc.ds_tipo_bloqueio_cartao
from
	t_bloqueio_cartao bc
join t_tipo_bloqueio_cartao tbc 
    on
	bc.id_tipo_bloqueio_cartao = tbc.id_tipo_bloqueio_cartao
where
	dt_desbloqueio is null
group by
	tbc.ds_tipo_bloqueio_cartao;

select round(0.4,2); 


```

---

## 📋 Critérios de Avaliação

- [ ] Query executa sem erros
- [ ] JOIN com tabela de tipos de bloqueio
- [ ] Filtra apenas bloqueios ativos
- [ ] Calcula quantidade por tipo
- [ ] Calcula percentual sobre total de bloqueios


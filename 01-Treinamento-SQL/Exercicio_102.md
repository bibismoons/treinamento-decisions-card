# Exercício 102: Quantidade de Contas Ativas

## 📝 Pergunta

Calcule a quantidade de contas ativas na base. Considere como conta ativa aquelas com `fl_status_conta = 'A'`. Mostre apenas o número total.

## 🎯 Objetivo

Demanda da área comercial para monitorar quantos clientes estão aptos a realizar compras.

## 💡 Contexto de Negócio

Contas ativas representam o potencial de receita da empresa. É um indicador importante para projeções de vendas e planejamento comercial.

---

## ✍️ Sua Resposta

```sql

select 
    count(fl_status_conta) 
from 
    t_cliente
where 
    fl_status_conta = 'A'; 

```

---

## 📋 Critérios de Avaliação

- [x] Query executa sem erros
- [x] Filtra apenas contas ativas
- [x] Retorna apenas um número
- [x] Usa o campo fl_status_conta corretamente


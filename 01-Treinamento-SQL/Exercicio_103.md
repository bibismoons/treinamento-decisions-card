# Exercício 103: Quantidade de Contas Ativadas

## 📝 Pergunta

Calcule quantas contas foram ativadas (mudaram de status inativo para ativo). Considere contas que têm `fl_status_conta = 'A'` e possuem pelo menos uma venda ativa registrada.

## 🎯 Objetivo

Demanda da área de CRM para medir a efetividade das campanhas de ativação de clientes.

## 💡 Contexto de Negócio

Contas ativadas representam clientes que não apenas se cadastraram, mas efetivamente começaram a usar o produto, indicando sucesso na jornada de onboarding.

---

## ✍️ Sua Resposta

```sql

--Opção 1:
select count(distinct c.id_cliente) as "Quantidade de contas ativadas"
    from t_cliente c
        join t_venda v 
            on c.id_cliente = v.id_cliente 
                where c.fl_status_conta = 'A'
                and v.fl_status_venda = 'A';

-- Opção 2:
select count(c.id_cliente) as "Quantidade de contas ativadas"
    from t_cliente c 
        where id_cliente in 
            (select distinct id_cliente from t_venda 
            where fl_status_venda = 'A')
        and c.fl_status_conta = 'A';

```

---

## 📋 Critérios de Avaliação

- [x] Query executa sem erros
- [x] Filtra contas ativas
- [x] Verifica existência de vendas
- [x] Conta clientes únicos
- [x] JOIN entre clientes e vendas


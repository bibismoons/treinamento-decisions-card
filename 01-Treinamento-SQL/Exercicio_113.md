# Exercício 113: Quantidade Total de Cartões

## 📝 Pergunta

Calcule a quantidade total de cartões emitidos na base de dados. Mostre apenas o número total.

## 🎯 Objetivo

Demanda operacional para controle do estoque de cartões e acompanhamento da produção.

## 💡 Contexto de Negócio

O total de cartões emitidos é um indicador operacional importante para logística e controle de estoque de cartões físicos.

---

## ✍️ Sua Resposta

```sql

select count (id_cartao)
from t_cartao
where fl_status_cartao != 'T';

```

---

## 📋 Critérios de Avaliação

- [x] Query executa sem erros
- [x] Conta todos os cartões da tabela
- [x] Retorna apenas um número
- [x] Usa a tabela t_cartao corretamente


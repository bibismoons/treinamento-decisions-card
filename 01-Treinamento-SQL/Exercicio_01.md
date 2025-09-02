# Exercício 1: Listagem Básica de Clientes

## 📝 Pergunta

Escreva uma query para selecionar os primeiros 10 clientes cadastrados na base, mostrando apenas os campos `id_cliente`, `nm_cliente`, `dt_nascimento` e `dt_cadastro`. Ordene do cliente mais antigo (primeiro cadastrado) para o mais recente.

## 🎯 Objetivo

Praticar consultas básicas com:
- SELECT de campos específicos
- ORDER BY para ordenação
- LIMIT para limitação de resultados

## 💡 Dica

Lembre-se de usar o schema `decisionscard` antes do nome da tabela.

---

## ✍️ Sua Resposta

```sql

select id_cliente,
       nm_cliente,
       dt_nascimento,
       dt_cadastro
from t_cliente
order by dt_cadastro asc
limit 10;

```

---

## 📋 Critérios de Avaliação

- [x] Query executa sem erros
- [x] Retorna exatamente 10 registros
- [x] Campos corretos são exibidos
- [x] Ordenação está correta (mais antigo primeiro)
- [x] Usa o schema `decisionscard` corretamente


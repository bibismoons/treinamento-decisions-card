# Exercício 2: Filtros Simples em Redes Parceiras

## 📝 Pergunta

Liste todas as redes parceiras (`t_rede`) que estão localizadas no estado de 'SP' (São Paulo). Mostre os campos `id_rede`, `nm_fantasia`, `nm_cidade` e `cd_uf`. Ordene alfabeticamente pelo nome fantasia.

## 🎯 Objetivo

Praticar:
- Cláusula WHERE para filtros
- Ordenação alfabética
- Trabalho com campos de texto

## 💡 Dica

O campo `cd_uf` contém a sigla do estado (ex: 'SP', 'RJ', 'MG').

---

## ✍️ Sua Resposta

```sql

select id_rede,
       nm_fantasia,
       nm_cidade,
       cd_uf
from t_rede
where cd_uf = 'SP'
order by nm_fantasia asc;

```

---

## 📋 Critérios de Avaliação

- [x] Query executa sem erros
- [x] Filtra apenas redes do estado 'SP'
- [x] Campos corretos são exibidos
- [x] Ordenação alfabética por nome fantasia
- [x] Usa WHERE corretamente


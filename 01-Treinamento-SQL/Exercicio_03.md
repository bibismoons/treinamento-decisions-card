# Exercício 3: Contagem de Cartões Ativos

## 📝 Pergunta

Quantos cartões (`t_cartao`) estão atualmente com status 'Ativo'? O campo `fl_status_cartao` indica o status, onde 'A' significa Ativo.

Sua query deve retornar apenas um número representando a quantidade total.

## 🎯 Objetivo

Praticar:
- Função de agregação COUNT()
- Filtros com WHERE
- Trabalho com campos de flag/status

## 💡 Dica

Use COUNT(*) ou COUNT(campo) para contar registros que atendem à condição.

---

## ✍️ Sua Resposta

```sql

select count(*)
from t_cartao
where fl_status_cartao = 'A';

```

---

## 📋 Critérios de Avaliação

- [x] Query executa sem erros
- [x] Retorna apenas um número (contagem)
- [x] Filtra corretamente por status 'A'
- [x] Usa função COUNT() adequadamente


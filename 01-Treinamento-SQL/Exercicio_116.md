# Exercício 116: Analítico das Contas sem Compras há Mais de 90 Dias

## 📝 Pergunta

Crie um relatório analítico (TABELÃO) das contas que não fazem compras há mais de 90 dias. Mostre:

- `id_cliente` (ID do cliente)
- `nm_cliente` (Nome do cliente)
- `nm_fantasia` (Origem comercial - nome da rede)
- `dt_ultima_compra` (Data da última compra)
- `vl_ultima_compra` (Valor da última compra)
- `dias_desde_ultima_compra` (Dias desde a última compra)

Use a maior data de venda da base como referência. Considere apenas clientes com contas ativas. Ordene por dias desde última compra (decrescente).

## 🎯 Objetivo

Demanda da área de retenção para criar campanhas direcionadas de reativação de clientes inativos.

## 💡 Contexto de Negócio

Este relatório permite ações de CRM personalizadas baseadas no perfil do cliente e tempo de inatividade.

---

## ✍️ Sua Resposta

```sql


```

---

## 📋 Critérios de Avaliação

- [ ] Query executa sem erros
- [ ] Identifica última compra por cliente
- [ ] Calcula dias desde última compra
- [ ] JOINs com cliente e rede (origem)
- [ ] Filtra clientes inativos há 90+ dias


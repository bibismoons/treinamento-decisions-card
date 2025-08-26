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
--Tentativa 1 (corrigir espaçamentos e outros):
WITH parametros AS (
    SELECT MAX(dt_venda) AS data_corte
    FROM decisionscard.t_venda
),
ultima_compra AS (
    SELECT
        id_cliente,
        MAX(dt_venda) AS dt_ultima_compra
    FROM decisionscard.t_venda
    GROUP BY id_cliente
),
clientes_sem_compras_90d AS (
    SELECT
        uc.id_cliente,
        uc.dt_ultima_compra
    FROM ultima_compra uc
    CROSS JOIN parametros p
    WHERE uc.dt_ultima_compra <= p.data_corte - INTERVAL '90 days'
),
ultima_venda_detalhada AS (
    SELECT *
    FROM (
        SELECT
            v.id_cliente,
            v.dt_venda,
            v.vl_venda,
            r.cd_uf,
            ROW_NUMBER() OVER (
                PARTITION BY v.id_cliente
                ORDER BY v.dt_venda DESC, v.vl_venda DESC NULLS LAST
            ) AS rn
        FROM decisionscard.t_venda v
        LEFT JOIN decisionscard.t_rede r 
               ON v.id_rede = r.id_rede
    ) sub
    WHERE rn = 1
),
tabelao_final AS (
    SELECT
        c.id_cliente,
        c.nm_cliente,
        uvd.cd_uf AS origem_comercial,
        uvd.vl_venda AS valor_ultima_compra,
        clientes.dt_ultima_compra,
        (p.data_corte - clientes.dt_ultima_compra) AS dias_sem_compras
    FROM clientes_sem_compras_90d clientes
    JOIN decisionscard.t_cliente c 
         ON clientes.id_cliente = c.id_cliente
    JOIN ultima_venda_detalhada uvd 
         ON clientes.id_cliente = uvd.id_cliente
    CROSS JOIN parametros p
    WHERE c.fl_status_conta = 'A'
)
SELECT *
FROM tabelao_final
ORDER BY dias_sem_compras DESC;
WITH parametros AS (
    SELECT MAX(dt_venda) AS data_corte
    FROM decisionscard.t_venda
),
ultima_compra AS (
    SELECT
        id_cliente,
        MAX(dt_venda) AS dt_ultima_compra
    FROM decisionscard.t_venda
    GROUP BY id_cliente
),
clientes_sem_compras_90d AS (
    SELECT
        uc.id_cliente,
        uc.dt_ultima_compra
    FROM ultima_compra uc
    CROSS JOIN parametros p
    WHERE uc.dt_ultima_compra <= p.data_corte - INTERVAL '90 days'
),
ultima_venda_detalhada AS (
    SELECT *
    FROM (
        SELECT
            v.id_cliente,
            v.dt_venda,
            v.vl_venda,
            r.cd_uf,
            ROW_NUMBER() OVER (
                PARTITION BY v.id_cliente, v.dt_venda
                ORDER BY v.vl_venda DESC NULLS LAST
            ) AS rn
        FROM decisionscard.t_venda v
        LEFT JOIN decisionscard.t_rede r 
               ON v.id_rede = r.id_rede
    ) sub
    WHERE rn = 1
),
tabelao_final AS (
    SELECT
        c.id_cliente,
        c.nm_cliente,
        uvd.cd_uf AS origem_comercial,
        uvd.vl_venda AS valor_ultima_compra,
        clientes.dt_ultima_compra,
        (p.data_corte - clientes.dt_ultima_compra) AS dias_sem_compras
    FROM clientes_sem_compras_90d clientes
    JOIN decisionscard.t_cliente c 
         ON clientes.id_cliente = c.id_cliente
    JOIN ultima_venda_detalhada uvd 
         ON clientes.id_cliente = uvd.id_cliente
        AND clientes.dt_ultima_compra = uvd.dt_venda
    CROSS JOIN parametros p
    WHERE c.fl_status_conta = 'A'
)
SELECT *
FROM tabelao_final
ORDER BY dias_sem_compras DESC;
WITH parametros AS (
    SELECT MAX(dt_venda) AS data_corte
    FROM decisionscard.t_venda
),
ultima_compra AS (
    SELECT
        id_cliente,
        MAX(dt_venda) AS dt_ultima_compra
    FROM decisionscard.t_venda
    GROUP BY id_cliente
),
clientes_sem_compras_90d AS (
    SELECT
        uc.id_cliente,
        uc.dt_ultima_compra
    FROM ultima_compra uc
    CROSS JOIN parametros p
    WHERE uc.dt_ultima_compra <= p.data_corte - INTERVAL '90 days'
),
ultima_venda_detalhada AS (
    SELECT *
    FROM (
        SELECT
            v.id_cliente,
            v.dt_venda,
            v.vl_venda,
            r.cd_uf,
            ROW_NUMBER() OVER (
                PARTITION BY v.id_cliente
                ORDER BY v.dt_venda DESC, v.vl_venda DESC NULLS LAST
            ) AS rn
        FROM decisionscard.t_venda v
        LEFT JOIN decisionscard.t_rede r 
               ON v.id_rede = r.id_rede
    ) sub
    WHERE rn = 1
),
tabelao_final AS (
    SELECT
        c.id_cliente,
        c.nm_cliente,
        uvd.cd_uf AS origem_comercial,
        uvd.vl_venda AS valor_ultima_compra,
        clientes.dt_ultima_compra,
        (p.data_corte - clientes.dt_ultima_compra) AS dias_sem_compras
    FROM clientes_sem_compras_90d clientes
    JOIN decisionscard.t_cliente c 
         ON clientes.id_cliente = c.id_cliente
    JOIN ultima_venda_detalhada uvd 
         ON clientes.id_cliente = uvd.id_cliente
    CROSS JOIN parametros p
)
SELECT *
FROM tabelao_final
ORDER BY dias_sem_compras DESC;

```

---

## 📋 Critérios de Avaliação

- [ ] Query executa sem erros
- [ ] Identifica última compra por cliente
- [ ] Calcula dias desde última compra
- [ ] JOINs com cliente e rede (origem)
- [ ] Filtra clientes inativos há 90+ dias


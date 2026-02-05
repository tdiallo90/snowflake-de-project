# Conventions SQL (Snowflake)

## Nommage
- Databases: `DB_<DOMAIN>` (ex: DB_SALES)
- Schemas: `RAW`, `STG`, `MARTS`, `ADMIN`, `MONITORING`
- Tables:
  - RAW: `RAW_<SOURCE>_<ENTITY>` (ex: RAW_SHOPIFY_ORDERS)
  - MARTS: `FCT_*` / `DIM_*` (ex: FCT_ORDERS, DIM_CUSTOMERS)
- Vues STG: `V_STG_<ENTITY>` (ex: V_STG_ORDERS)

## Fichiers SQL
- Préfixer par ordre d’exécution : `001_`, `010_`, `060_`, etc.
- 1 script = 1 intention claire (éviter les scripts “fourre-tout”)

## Standards de code
- Toujours qualifier les objets si possible : `DB.SCHEMA.OBJECT`
- Toujours expliciter le `WAREHOUSE` côté exécution (ou via rôle / session)
- Éviter le `SELECT *` dans STG/MARTS

## Transactions & idempotence
- Utiliser `CREATE OR REPLACE` pour objets dérivés (views/procs)
- Utiliser `CREATE IF NOT EXISTS` pour base (schemas/stages) si tu veux rejouer

## Sécurité
- Ne pas versionner des secrets (clé, password, tokens)
- Utiliser des rôles dédiés (READ, WRITE, ADMIN)

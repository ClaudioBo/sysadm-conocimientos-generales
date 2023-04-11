## Obtener los clientes en Postgresql
```sql
SELECT application_name, client_addr, usename, state, state_change::timestamptz(0) FROM pg_stat_activity where backend_type='client backend' order by state_change desc;
```
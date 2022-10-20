# Expulsar usuarios que usan la base de datos actual
```sql
SELECT pid, pg_terminate_backend(pid) FROM pg_stat_activity WHERE datname = current_database() AND pid <> pg_backend_pid();
```

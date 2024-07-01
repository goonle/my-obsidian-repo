# 1. Grant All privileges to a roll for Database
```sql
GRANT ALL PRIVILEGES ON DATABASE your_database TO team1;
```

# 2. Grant All Privileges to a roll for Tables
```sql
DO $$ 
DECLARE 
    r RECORD; 
BEGIN 
    FOR r IN (SELECT schemaname, tablename FROM pg_tables WHERE schemaname NOT IN ('pg_catalog', 'information_schema')) LOOP 
        EXECUTE 'GRANT SELECT, INSERT, UPDATE, DELETE ON TABLE ' || quote_ident(r.schemaname) || '.' || quote_ident(r.tablename) || ' TO role_name;'; 
    END LOOP; 
END $$;

```


# 3. Just give superuser
```sql
ALTER ROLE role_name WITH SUPERUSER;
```
#postgreSQL 
#sql 

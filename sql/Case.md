## Update Case Statement 

```mySql
UPDATE <table>
  SET <col> = CASE 
    WHEN <cond> THEN <expr>
    WHEN <cond> THEN <expr>
    ELSE <expr>
END;
```

```sql
update salary set name = case when name = "A" then "B" else "A" end
```

### squirrel
---
https://github.com/Masterminds/squirrel

```go
import "github.com/Masterminds/squirrel"


import sq "github.com/Masterminds/squirrel"

users := sq.Select("*").From("users").Join("email USING (email_id)")

active := users.Where(sq.Eq("deleted_at": nil))

sql, args, err := active.ToSql()

sql == "SELECT * FROM users JOIN emails USING (email_id) WHERE deleted_at IS NULL"


sql, args, err := sq.
  Insert("users").Columns("name", "age").
  Values("moe", 13).Values("larry", sq.Expr("? + 5", 12)).
  ToSql()
  
sql == "INSERT INTO users (name,age) VALUES (?,?),(?,? + 5)"


stooges := users.Where(sq.Eq("username": []string{"moe", "larry", "curly", "shemp"}))
three_stooges := stooges.Limit(3)
rows, err := three_stooges.RunWith(db).Query()

rows, err := db.Query("SELECT * FROM users WHERE username IN (?,?,?,?) LIMIT 3",
  "moe", "larry", "currly", "shemp")

if len(q) > 0 {
  users = users.Where("name LIKE ?", fmt.Sprint("%", q, "%"))
}

dbCache := sq.NewStmtCacher(db)

mydb := sq.StatementBuilder.RunWith(dbCache)
select_users := mydb.Select("*").From("users")


psql := sq.StatementBuilder.PlaceholderFormat(sq.Dollar)

sql, _, _ := psql.Select("*").From("elephants").Where("name IN (?,?)", "Dumbo", "Verna").ToSql()

sql == "SELECT * FROM elephants WHERE name IN ($1,$2)"

query := sq.Insert("nodes").
  Columns("uuid", "type", "data").
  Values(node.Uuid, node.Type, node.Data).
  Suffix("RETURNING \"id\"").
  RunWith(m.db).
  PlaceholderFormat(sq.Dollar)
  
query.QueryRow().Scan(&node.id)


sq.Or{
  sq.Eq{"col1": 1, "col2": 2},
  sq.Eq{"col1": 3, "col2": 4}}

WHERE (col1 = 1 AND col2 = 2) OR (col1 = 3 AND col2 = 4) 
```

```sql
SELECT * FROM nodes WHERE meta->'format' ??| array[?,?]
SELECT * FROM nodes WHERE meta->'format' ?| array[$1,$2]
```

```
```



## 创建连接
```go
conn, err := redis.DialURL("redis://127.0.0.1:6379")
conn, err := redis.Dial("tcp", "127.0.0.1:6379")
```

## Examples

```go
// SET GET
v, err := c.Do("SET", "name", "red")
if err != nil {
	fmt.Println(err)
    return
}
fmt.Println(v)
v, err = redis.String(c.Do("GET", "name"))
if err != nil {
	fmt.Println(err)
	return
}
fmt.Println(v)

// HMSET  HGETALL
v, err := c.Do("HMSET", "hmkey", "field1", "Hello", "filed2", "World"); 
if err != nil {  
   fmt.Println(err)  
   return  
}  
fmt.Println(v)
values, err := redis.Values(conn.Do("HGETALL", "hmkey"))  
if err != nil {  
   fmt.Println(err)  
   return  
}  
for _, value := range values {  
   fmt.Println(string(value.([]byte)))  
}
```
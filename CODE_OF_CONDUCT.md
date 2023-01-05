## To get the Token

```
curl -s -X POST "http://172.22.63.55:8086/api/v1/login" -H  "accept: application/json" -H  "Content-Type: multipart/form-data" -F "username=admin" -F "password=admin123"
```

`{"email": "admin@localhost", "username": "admin", "token": "245aff2de55684794faf684ce2ffa6779cc749b2"}`

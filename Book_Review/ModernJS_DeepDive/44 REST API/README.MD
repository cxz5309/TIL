# 44 REST API
> 이야 이건 그래도 내가 더 잘 조사했을거 같다 나름 열심히 했고..  
> [REST](../../../JS/REST%20vs%20SOAP%20vs%20GraphQL/README.MD)  

## REST API의 구성
1. 자원: URL(엔드 포인트)
2. 행위: HTTP요청 메서드
3. 표현: 페이로드

## 44.2 REST API 설계 원칙
1. URL는 리소스를 표현해야 한다.
   - 리소스를 식별할 수 있는 이름은 동사보다 명사, 행위에 대한 표현이 들어가서는 안 된다.
```
# bad
GET /getTodos/1
Get /todos/show/1

# good
GET /todos/1
```

2. 리소스에 대한 행위는 HTTP 요청 메서드로 표현한다.
- GET, POST, PUT, PATCH, DELETE
```
# bad
GET /todos/delete/1

# good
DELETE /todos/1
```


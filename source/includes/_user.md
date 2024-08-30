# 계정

## Get User List

```shell
curl %MANGE%/api/user/admin/1
```

> Response

```json
{
  "page": 0,
  "size": 20,
  "totalPages": 1,
  "totalElements": 3,
  "content": [
    {
      "id": 1,
      "userId": "linda",
      "password": null,
      "name": "전종서",
      "phone": "01022223333",
      "email": "js@korea.com",
      "dept": "고구려황실",
      "pos": "왕후",
      "useYn": "Y",
      "createdAt": "2024-08-31T04:43:11.280+00:00"
    },
    ...
  ]
}
```

### Request

`GET /api/user/{role}/{siteId}`  
`GET /api/user/{role}`

### Path Parameters

| Name   | Description                          |
| ------ | ------------------------------------ |
| role   | admin, Super(첫글자 대문자)          |
| siteId | 사이트 아이디(role이 Super인 경우 0) |

### Query Parameters (optional)

| Name  | Description         |
| ----- | ------------------- |
| name  | 키워드필터          |
| phone | 키워드필터          |
| useYn | 키워드필터 (Y or N) |

## Get User

```shell
curl %MANGE%/api/user/admin/1/1
```

> Response

```json
{
  "id": 1,
  "userId": "linda",
  "password": null,
  "name": "전종서",
  "phone": "01022223333",
  "email": "js@korea.com",
  "dept": "고구려황실",
  "pos": "왕후",
  "useYn": "Y",
  "createdAt": "2024-08-31T04:43:11.280+00:00"
}
```

### Request

`GET /api/user/{role}/{siteId}/{id}`

## Save User

```shell
curl -X 'POST' %MANAGE%/api/user/admin/1 \
  -H 'Content-Type: application/json' \
  -d '{
    {
      "userId": "linda",
      "password": "abcd1234",
      "name": "전종서",
      "phone": "01022223333",
      "email": "js@korea.com",
      "dept": "고구려황실",
      "pos": "왕후",
      "useYn": "Y"
    }
}'
```

> Response

```json
{
  "code": 0,
  "id": 1,
  "message": ""
}
```

### Request

`POST /api/user/{role}/{siteId}`

### Json Fields

| Required | Name     | Description        |
| -------- | -------- | ------------------ |
| ✓        | userId   | 로그인 아이디      |
| ✓        | password | 패스워드           |
| ✓        | name     | 이름               |
| ✓        | phone    | 전화번호           |
| ✓        | email    | 이메일             |
| ✓        | dept     | 부서               |
| ✓        | pos      | 직위               |
| ✓        | useYn    | 활성화여부(Y or N) |

## Delete User

```shell
curl -X 'DELETE' %MANAGE%/api/user/1/1
```

> Response

```json
{
  "code": 0,
  "id": 1,
  "message": ""
}
```

### Request

`DELETE /api/user/{role}/{siteId}/{id}`

## Check Duplicate User

전화번호 중복체크를 합니다.

```shell
curl %MANGE%2/api/user/admin/1/exists/userId/linda
```

> Response

```
true
```

### Request

### Request

`GET /api/user/{role}/{siteId}/exists/userId/{userId}`

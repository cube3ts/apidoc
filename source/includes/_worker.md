# 인력

## Get Worker List

```shell
curl %MANGE%/api/worker
```

> Response

```json
{
  "page": 0,
  "size": 20,
  "totalPages": 15,
  "totalElements": 300,
  "content": [
    {
      "id": 2,
      "type": "staff",
      "name": "윤성호",
      "phone": "01017484139",
      "region": "울산",
      "bank": "우리은행",
      "account": "62785695859896",
      "accountHolder": "윤성호",
      "description": "온기",
      "useYn": "Y",
      "createdAt": "2024-08-30T00:00:00.000+00:00"
    },
    ...
  ]
}
```

### Request

`GET /api/worker`

### Query Parameters (optional)

| Name  | Description         |
| ----- | ------------------- |
| type  | staff, proctor      |
| name  | 키워드필터          |
| phone | 키워드필터          |
| useYn | 키워드필터 (Y or N) |

## Get Worker

```shell
curl %MANGE%/api/worker/2
```

> Response

```json
{
  "id": 2,
  "type": "staff",
  "name": "윤성호",
  "phone": "01017484139",
  "region": "울산",
  "bank": "우리은행",
  "account": "62785695859896",
  "accountHolder": "윤성호",
  "description": "온기",
  "useYn": "Y",
  "createdAt": "2024-08-30T00:00:00.000+00:00"
}
```

### Request

`GET /api/worker/{id}`

## Save Item

```shell
curl -X 'POST' %MANAGE%/api/worker \
  -H 'Content-Type: application/json' \
  -d '{
  "type": "staff",
  "name": "홍길동",
  "phone": "01012341234",
  "region": "경기",
  "bank": "하나은행",
  "account": "2343533",
  "accountHolder": "홍길동",
  "description": "테스트",
  "useYn": "Y"
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

`POST /api/worker`

### Json Fields

| Required | Name          | Description                      |
| -------- | ------------- | -------------------------------- |
| ✓        | type          | staff(진행요원), proctor(감독관) |
| ✓        | name          | 이름                             |
| ✓        | phone         | 전화번호                         |
| ✓        | region        | 지역                             |
| ✓        | bank          | 은행명                           |
| ✓        | account       | 계좌번호                         |
| ✓        | accountHolder | 예금주                           |
| ✓        | description   | 요약정보                         |
| ✓        | useYn         | 활성화여부(Y or N)               |

## Delete Item

```shell
curl -X 'DELETE' %MANAGE%/api/worker/1
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

`DELETE /api/worker/{id}`

## Check Duplicate Worker

전화번호 중복체크를 합니다.

```shell
curl %MANGE%2/api/worker/exists/type/staff/phone/01028185038
```

> Response

```
true
```

### Request

### Request

`GET /api/worker/exists/type/{type}/phone/{phone}`

## Upload CSV Worker

```html
<!DOCTYPE html>
  <body>
    <form action="/api/worker/upload/excel" enctype="multipart/form-data" method="POST" >
      <input name="file" type="file" />
      <input type="submit" value="UPLOAD" />
    </form>
  </body>
</html>
```

```
staff,윤성호,01017484139,울산,우리은행,62785695859896,윤성호,온기,Y
staff,배도현,01035577118,강원,신한은행,848619602413,배도현,꽃,Y
proctor,박상현,01085733360,대전,국민은행,36112063293739,박상현,모래,Y
```

> Response

```json
{
  "code": 0,
  "id": null,
  "message": ""
}
```

### Request

`POST /api/worker/upload/excel`

### Json Fields

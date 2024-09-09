# 동의서

## Get Consent List

```shell
curl %MANGE%/api/consent
```

> Response

```json
{
  "page": 0,
  "size": 20,
  "totalPages": 1,
  "totalElements": 2,
  "content": [
    {
      "id": 1,
      "name": "동의서1",
      "description": "동의서 테스트1",
      "useYn": "Y",
      "createdAt": "2024-09-10T05:47:25.119+00:00",
      "title": "개인정보 처리 동의서",
      "checkAll": false,
      "items": [
        {
            ...
        },
      ]
    },
    ...
  ]
}
```

### Request

`GET /api/consent`

### Query Parameters (optional)

| Name  | Description         |
| ----- | ------------------- |
| name  | 키워드필터          |
| useYn | 키워드필터 (Y or N) |

## Get Consent

```shell
curl %MANGE%/api/consent/4
```

> Response

```json
{
  "id": 4,
  "name": "동의서2",
  "description": "동의서 테스트2",
  "useYn": "Y",
  "createdAt": "2024-09-10T05:56:19.281+00:00",
  "title": "선물 수령 동의서",
  "checkAll": true,
  "items": [
    {
      "title": "자택 수령 여부",
      "content": "선물을 자택에서 수령할 것을 동의합니다.",
      "check": true,
      "required": true
    }
  ]
}
```

### Request

`GET /api/consent/{id}`

## Save Consent

```shell
curl -X 'POST' %MANAGE%/api/consent \
  -H 'Content-Type: application/json' \
  -d '{
  "name": "동의서2",
  "description": "동의서 테스트2",
  "useYn": "Y",
  "title": "선물 수령 동의서",
  "checkAll": true,
  "items": [
    {
      "title": "자택 수령 여부",
      "content": "선물을 자택에서 수령할 것을 동의합니다.",
      "check": true,
      "required": true
    }
  ]
}'
```

> Response

```json
{
  "code": 0,
  "id": 4,
  "message": ""
}
```

### Request

`POST /api/consent`

### Json Fields

| Required | Name             | Description                         |
| -------- | ---------------- | ----------------------------------- |
| ✓        | name             | 이름                                |
| ✓        | description      | 요약정보                            |
| ✓        | useYn            | 활성화여부(Y or N)                  |
| ✓        | title            | 문서 제목                           |
| ✓        | checkAll         | 전체동의 여부(boolean)              |
| ✓        | items[].title    | 항목 제목                           |
| ✓        | items[].content  | 항목 내용(html일 경우 base64인코딩) |
| ✓        | items[].check    | 동의 여부(boolean)                  |
| ✓        | items[].required | 필수 여부                           |

## Delete Consent

```shell
curl -X 'DELETE' %MANAGE%/api/consent/3
```

> Response

```json
{
  "code": 0,
  "id": 3,
  "message": ""
}
```

### Request

`DELETE /api/consent/{id}`

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

## Save Worker

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

## Delete Worker

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

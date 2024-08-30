# 인력

## Get List

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

## Get Item

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
curl -X 'POST' \
  %MANAGE%/api/worker \
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

## Check Duplicate

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

## Upload CSV

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

# 부가정보

## Get Spec

```shell
curl %MANGE%/api/addInfo/spec
```

> Response

```json
[
  {
    "type": "col",
    "categories": [
      { "name": "cate1", "values": ["전문대", "대학교"] },
      { "name": "cate2", "values": ["해외대", "국내대"] }
    ]
  },
  { "type": "maj", "categories": [] },
  {
    "type": "lic",
    "categories": [
      {
        "name": "cate1",
        "values": ["민간자격증", "국가공인자격증", "국제자격증"]
      },
      {
        "name": "cate2",
        "values": [
          "한국산업인력공단",
          "Oracle ",
          ...
        ]
      }
    ]
  }
]
```

### Request

`GET /api/addInfo/spec`

부가정보 데이터를 조회할 때 사용할 type과 필터시 select form에 사용할 값들을 조회합니다.

## Get List

```shell
curl %MANGE%/api/addInfo/col
```

> Response

```json
{
  "page": 0,
  "size": 20,
  "totalPages": 144,
  "totalElements": 2864,
  "content": [
    {
      "id": 3366,
      "name": "Northwest Nazarene College",
      "cate1": "대학교",
      "cate2": "해외대",
      "useYn": "Y"
    },
    ...
  ]
}
```

### Request

`GET /api/addInfo/{type}`

### Path Parameters

| Name | Description                                            |
| ---- | ------------------------------------------------------ |
| type | lic(licenced 자격증) col(college 대학) maj(major 전공) |

### Query Parameters (optional)

| Name  | Description                              |
| ----- | ---------------------------------------- |
| name  | 키워드필터                               |
| cate1 | 키워드필터 (Spec의 categories에 있는 값) |
| cate2 | 키워드필터 (Spec의 categories에 있는 값) |
| useYn | 키워드필터 (Y or N)                      |

## Save Item

```shell
curl -X 'POST' \
  %MANAGE%/api/item \
  -H 'Content-Type: application/json' \
  -d '{
  "name": "연금술사",
  "cate1": "국제자격증",
  "cate2": "국제마법사협회",
  "useYn": "Y"
}'
```

> Response

```json
{
  "code": 0,
  "id": 7270,
  "message": ""
}
```

### Request

`POST /api/addInfo/{type}`

### Json Fields

| Required | Name  | Description        |
| -------- | ----- | ------------------ |
| ✓        | name  | 이름               |
| ✓        | cate1 | 분류1              |
| ✓        | cate2 | 분류2              |
| ✓        | useYn | 활성화여부(Y or N) |

# 파일

## Upload File

```html
<form action="/api/file/upload/cbr" enctype="multipart/form-data" method="POST">
  <input name="file" type="file" />
  <input type="submit" value="UPLOAD" />
</form>
```

> Response

```json
{
  "code": 0,
  "id": 9,
  "message": ""
}
```

### Request

`POST /api/file/upload/{type}`

### Json Fields

| Required | Name | Description                        |
| -------- | ---- | ---------------------------------- |
| ✓        | type | cbr(사업자등록증), apo(지원자사진) |

## Get File

```html
<img src="/api/file/9" />
```

### Request

`GET /api/file/{id}`

# -

## -

## -

## -

## -

## -

## -

## -

## -

## -

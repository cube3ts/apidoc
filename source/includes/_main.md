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

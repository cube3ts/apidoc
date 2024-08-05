# 기업

## Get List

```shell
curl %MANGE%/api/corp
```

> Response

```json
{
  "totalPages": 1,
  "totalElements": 4,
  "content": [
    {
      "id": 2,
      "regNo": "7978200473",
      "name": "한국토지주택공사",
      "phone": "02-3432-3454",
      "email": "a@lh.co.kr",
      "website": "https://www.lh.or.kr/intro.html",
      "cbrFileId": 4,
      "createdAt": "2024-07-03T14:51:02.000+00:00",
      "sites": []
    },
    ...
  ]
}
```

### Request

`GET /api/corp`

## Get Item

```shell
curl %MANGE%/api/corp/2
```

> Response

```json
{
  "id": 2,
  "regNo": "7978200473",
  "name": "한국토지주택공사",
  "phone": "02-3432-3454",
  "email": "a@lh.co.kr",
  "website": "https://www.lh.or.kr/intro.html",
  "cbrFileId": 4,
  "createdAt": "2024-07-03T14:51:02.000+00:00",
  "sites": [
    {
      "id": 1,
      "corpId": 2,
      "subdomain": "lh-qa",
      "name": "LH품질시험인정센터",
      "createdAt": "2024-07-03T14:52:50.000+00:00",
      "openBegin": "2024-07-03T14:51:53.000+00:00",
      "openEnd": "2025-07-03T14:51:58.000+00:00",
      "closedAt": null
    },
    ...
  ]
}
```

### Request

`GET /api/corp/{id}`

## Save Item

```shell
curl -X 'POST' \
  %MANAGE%/api/corp \
  -H 'Content-Type: application/json' \
  -d '{
  "regNo": "1234567890",
  "name": "한국냉장",
  "phone": "02-2343-2345",
  "email": "contact@krice.co.kr",
  "website": "https://krice.co.kr"
}'
```

> Response

```json
{
  "code": 0,
  "id": 12,
  "message": ""
}
```

### Request

`POST /api/corp/{id}`

### Json Fields

| Required | Name      | Description                                     |
| -------- | --------- | ----------------------------------------------- |
| ✓        | regNo     | 사업자 번호(숫자만 입력)                        |
| ✓        | name      | 법인명                                          |
| ✓        | phone     | 법인 대표 전화                                  |
| ✓        | email     | 법인 대표 이메일                                |
|          | cbrFileId | 사업자 등록증 파일아이디(최초 등록시 생략 가능) |

## Delete Item

```shell
curl -X 'DELETE' %MANAGE%/api/corp/12
```

> Response

```json
{
  "code": 0,
  "id": 12,
  "message": ""
}
```

### Request

`DELETE /api/corp/{id}`

# 사이트

## Get List

```shell
curl %MANGE%/api/site
```

> Response

```json
{
  "totalPages": 1,
  "totalElements": 4,
  "content": [
    {
      "id": 1,
      "corpId": 2,
      "subdomain": "lh-qa",
      "name": "LH품질시험인정센터",
      "createdAt": "2024-07-03T14:52:50.000+00:00",
      "openBegin": "2024-07-03T14:51:53.000+00:00",
      "openEnd": "2025-07-03T14:51:58.000+00:00",
      "closedAt": null
    },
    {
      "id": 2,
      "corpId": 2,
      "subdomain": "lh-lab",
      "name": "토지주택연구원",
      ...
    },
    {
      "id": 3,
      "corpId": 3,
      "subdomain": "hcdp-ict",
      "name": "ICT사업단",
      ...
    },
    ...
  ]
}
```

### Request

`GET /api/site`

## Get Item

```shell
curl %MANGE%/api/site/2
```

> Response

```json
{
  "id": 2,
  "corpId": 2,
  "subdomain": "lh-lab",
  "name": "토지주택연구원",
  "createdAt": "2024-07-03T14:52:52.000+00:00",
  "openBegin": "2024-08-03T14:52:33.000+00:00",
  "openEnd": "2024-10-03T14:52:37.000+00:00",
  "closedAt": null
}
```

### Request

`GET /api/site/{id}`

### Json Fields

| Name     | Description                                               |
| -------- | --------------------------------------------------------- |
| closedAt | null이 아닌 경우 사이트 종료일을 표시하고 '활성화'로 표시 |

## Save Item

```shell
curl -X 'POST' \
  %MANAGE%/api/site \
  -H 'Content-Type: application/json' \
  -d '{
  "corpId": 2,
  "subdomain": "cafe",
  "name": "사내카페",
  "openBegin": "2024-07-30T00:00",
  "openEnd": "2025-07-30T00:00"
}'
```

> Response

```json
{
  "code": 0,
  "id": 6,
  "message": ""
}
```

### Request

`POST /api/site`

### Json Fields

| Required | Name      | Description                     |
| -------- | --------- | ------------------------------- |
| ✓        | corpId    | 기업 객체의 아이디              |
| ✓        | subdomain | 사이트 도메인의 첫 부분(예 bus) |
| ✓        | name      | 사이트 이름                     |
| ✓        | openBegin | 사이트 운용기간 시작 날짜       |
| ✓        | openEnd   | 사이트 운용기간 종료 날짜       |

## Delete Item

```shell
curl -X 'DELETE' %MANAGE%/api/site/6
```

> Response

```json
{
  "code": 0,
  "id": 6,
  "message": ""
}
```

### Request

`DELETE /api`

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

# 문서(공고,메일,SMS)

## Get List

```shell
curl %MANGE%/api/doc/posting
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
      "name": "2024신입 공채 공고",
      "description": "찐최종 수정본",
      "contentEnc": "base64",
      "content": "PCFE...base64...CjwvaHRtbD4=",
      "useYn": "Y",
      "createdAt": "2024-07-25T08:22:01.820+00:00"
    },
    ...
  ]
}
```

### Path Parameters

| Name | Description         |
| ---- | ------------------- |
| type | posting, email, sms |

### Query Parameters (optional)

| Name  | Description         |
| ----- | ------------------- |
| name  | 키워드필터          |
| useYn | 키워드필터 (Y or N) |

### Request

`GET /api/doc/{type}`

## Get Item

```shell
curl %MANGE%/api/doc/posting/1
```

> Response

```json
{
  "id": 1,
  "name": "2024신입 공채 공고",
  "description": "찐최종 수정본",
  "contentEnc": "base64",
  "content": "PCFE...base64...CjwvaHRtbD4=",
  "useYn": "Y",
  "createdAt": "2024-07-25T08:22:01.820+00:00"
}
```

### Request

`GET /api/doc/{type}/{id}`

## Save Item

```shell
curl -X 'POST' \
  %MANAGE%/api/doc/sms \
  -H 'Content-Type: application/json' \
  -d '{
  "name": "홍보",
  "description": "공채 채용 알림",
  "contentEnc": "none",
  "content": "[광고] 2024년도 공개 채용에 응시하세요",
  "useYn": "Y"
}'
```

> Response

```json
{
  "code": 0,
  "id": 5,
  "message": ""
}
```

### Request

`POST /api/doc/{type}`

### Json Fields

| Required | Name        | Description                                        |
| -------- | ----------- | -------------------------------------------------- |
| ✓        | name        | 명칭                                               |
| ✓        | description | 요약 정보                                          |
| ✓        | contentEnc  | content 인코딩(none or base64)                     |
| ✓        | content     | html, json 등 plain-text가 아닌 경우 base64 인코딩 |
| ✓        | useYn       | 활성화여부(Y or N)                                 |

## Delete Item

```shell
curl -X 'DELETE' %MANAGE%/api/doc/sms/5
```

> Response

```json
{
  "code": 0,
  "id": 5,
  "message": ""
}
```

### Request

`DELETE /api/doc/{type}/{id}`

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

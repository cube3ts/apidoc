# 기업

## Get Corp List

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

### Query Parameters (optional)

| Name  | Description             |
| ----- | ----------------------- |
| name  | 키워드필터              |
| regNo | 키워드필터 (사업자번호) |

## Get Corp

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

## Save Corp

```shell
curl -X 'POST' %MANAGE%/api/corp \
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

## Delete Corp

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

## Get Site List

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
      "corpName": "한국토지주택공사",
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

### Query Parameters (optional)

| Name      | Description         |
| --------- | ------------------- |
| name      | 키워드필터          |
| corpName  | 키워드필터          |
| subdomain | 키워드필터          |
| useYn     | 키워드필터 (Y or N) |

## Get Site

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
  "corpName": "한국토지주택공사",
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

## Save Site

```shell
curl -X 'POST' %MANAGE%/api/site \
  -H 'Content-Type: application/json' \
  -d '{
  "corpId": 2,
  "subdomain": "cafe",
  "useYn": "Y",
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
| ✓        | useYn     | 활성화여부(Y or N)              |
| ✓        | name      | 사이트 이름                     |
| ✓        | openBegin | 사이트 운용기간 시작 날짜       |
| ✓        | openEnd   | 사이트 운용기간 종료 날짜       |

## Delete Site

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

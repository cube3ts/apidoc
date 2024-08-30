# 문서(공고,메일,SMS)

## Get Doc List

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

## Get Doc

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

## Save Doc

```shell
curl -X 'POST' %MANAGE%/api/doc/sms \
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

## Delete Doc

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

# 양식(설문,지원,평가)

## Get Form List

```shell
curl %MANGE%/api/form/survey
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
      "name": "설문1",
      "description": "테스트용",
      "useYn": "Y",
      "createdAt": "2024-08-11T14:36:30.699+00:00",
      "content": {
        ...
      }
    },
    {
      "id": 2,
      "name": "회식 설문",
      "description": "송년회 지사별 의견을 취합하기위함",
      "useYn": "Y",
      "createdAt": "2024-08-11T14:37:20.553+00:00",
      "content": {
        ...
      }
    }
  ]
}
```

### Request

`GET /api/item/form/{type}`

### Path Parameters

| Name | Description                     |
| ---- | ------------------------------- |
| type | survey, application, evaluation |

### Query Parameters (optional)

| Name  | Description         |
| ----- | ------------------- |
| name  | 키워드필터          |
| useYn | 키워드필터 (Y or N) |

## Get Form

```shell
curl %MANGE%/api/form/survey/1
```

> Response

```json
{
  "id": 1,
  "name": "설문1",
  "description": "테스트용",
  "useYn": "Y",
  "createdAt": "2024-08-11T14:36:30.699+00:00",
  "content": {
    "title": "설문조사",
    "sections": [
      {
        "title": "",
        "itemGroups": [
          {
            "itemGroupKey": null,
            "items": [
              {
                "itemKey": null,
                "itemType": "survey-select",
                "itemObject": {
                  ...
                }
              }
            ],
            "appendable": false
          }
        ]
      }
    ]
  }
}
```

### Request

`GET /api/form/{type}/{id}`

## Save Form

```shell
curl -X 'POST' %MANAGE%/api/form/survey \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "설문1",
      "description": "테스트용",
      "content": {
        ...
      },
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

`POST /api/form/{type}`

### Json Fields

| Required | Name        | Description        |
| -------- | ----------- | ------------------ |
| ✓        | name        | 명칭               |
| ✓        | description | 요약 정보          |
| ✓        | content     |                    |
| ✓        | useYn       | 활성화여부(Y or N) |

## Delete Form

```shell
curl -X 'DELETE' %MANAGE%/api/form/survey/1
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

`DELETE /api/form/{type}/{id}`

# 양식항목(지원)

## Get Section List

```shell
curl %MANGE%/api/formSection/application
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
      "name": "기타사항 항목",
      "description": "지원서항목 테스트",
      "useYn": "Y",
      "createdAt": "2024-08-11T14:57:49.528+00:00",
      "content": {
        ...
      }
    },
    {
      "id": 2,
      "name": "가족사항 항목",
      "description": "지원서항목 테스트2",
      "useYn": "Y",
      "createdAt": "2024-08-11T15:02:57.371+00:00",
      "content": {
        ...
      }
    }
  ]
}
```

### Request

`GET /api/item/formSection/{type}`

### Path Parameters

| Name | Description |
| ---- | ----------- |
| type | application |

### Query Parameters (optional)

| Name  | Description         |
| ----- | ------------------- |
| name  | 키워드필터          |
| useYn | 키워드필터 (Y or N) |

## Get Section

```shell
curl %MANGE%/api/formSection/application/2
```

> Response

```json
{
  "id": 2,
  "name": "가족사항 항목",
  "description": "지원서항목 테스트2",
  "useYn": "Y",
  "createdAt": "2024-08-11T15:02:57.371+00:00",
  "content": {
    "title": "가족사항",
    "itemGroups": [
      {
        "itemGroupKey": null,
        "items": [
          {
            "itemKey": null,
            "itemType": "app-select",
            "itemObject": {
              "label": "관계",
              "options": ["엄마", "아빠", "누나"]
            }
          },
          {
            "itemKey": null,
            "itemType": "app-text",
            "itemObject": { "label": "이름" }
          },
          {
            "itemKey": null,
            "itemType": "app-text",
            "itemObject": { "label": "나이" }
          }
        ],
        "appendable": true
      }
    ]
  }
}
```

### Request

`GET /api/formSection/{type}/{id}`

## Save Section

```shell
curl -X 'POST' %MANAGE%/api/formSection/application \
  -H 'Content-Type: application/json' \
  -d '{
  "name": "공통지원서양식1",
  "description": "양식테스트",
  "content": {
    "title": "기타사항",
    "itemGroups": [
      {
        "appendable": false,
        "items": [
          ...
        ]
      }
    ]
  },
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

`POST /api/formSection/{type}`

### Json Fields

| Required | Name        | Description        |
| -------- | ----------- | ------------------ |
| ✓        | name        | 명칭               |
| ✓        | description | 요약 정보          |
| ✓        | content     |                    |
| ✓        | useYn       | 활성화여부(Y or N) |

## Delete Section

```shell
curl -X 'DELETE' %MANAGE%/api/formSection/application/1
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

`DELETE /api/formSection/{type}/{id}`

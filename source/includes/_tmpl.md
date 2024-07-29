# tmpl

## Get List

```shell
curl %MANGE%/api/item
```

> Response

```json

```

### Request

`GET /api/item`

### Path Parameters

### Query Parameters (optional)

## Get Item

```shell
curl %MANGE%/api/item/2
```

> Response

```json

```

### Request

`GET /api/item/{id}`

## Save Item

```shell
curl -X 'POST' \
  %MANAGE%/api/item \
  -H 'Content-Type: application/json' \
  -d '{
}'
```

> Response

```json
{
  "code": 0,
  "id": ,
  "message": ""
}
```

### Request

`POST /api/item`

### Json Fields

| Required | Name  | Description        |
| -------- | ----- | ------------------ |
| ✓        |       |                    |
| ✓        | useYn | 활성화여부(Y or N) |

## Delete Item

```shell
curl -X 'DELETE' %MANAGE%/api/item/
```

> Response

```json
{
  "code": 0,
  "id": ,
  "message": ""
}
```

### Request

`DELETE /api/item/{id}`

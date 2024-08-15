---
title: Cube API

code_clipboard: true

includes:
  - main
---

# Read me

## Changes

### 2024.8.15

양식API를 추가하였습니다. 설문지, 입사지원서, 평가지에서 커스텀폼을 지원합니다.  
백엔드에서는 작성된 커스텀폼(JSON)을 대체로 저장관리만 하고요 세부적인 내용은 보지 않습니다.  
커스텀폼 관련 설명은 <a href='https://www.notion.so/647bb7a578544619b23e97197a1350b3?pvs=4'>별도 문서</a>로 작성해 두었습니다.

### 2024.8.7

사이트 관련

- 조회 결과에 corpNam(기업명)을 추가했습니다.
- 도메인은 subdomain필드의 값에 .cube-scout.com을 더해서 표시해야 합니다. 추후 이런 고정값들을 조회할 수 있는 API를 추가하겠습니다.
- 조회 결과에 useYn(활성화상태)을 추가했습니다. 저장시 이 필드에 'N'을 세팅하면 closedAt(사이트 종료일)이 세팅됩니다. 조회시 필터에도 &useYn=Y 사용이 가능합니다.

### 2024.7.29

API문서를 Swagger를 없에고 이것을 쓸 예정입니다. Swagger에서는 표현이 자유롭지 못해 API상세 설명을 위해 별도의 페이지를 만들어야 했고, 'Try it out'기능이 안되는 케이스들(실제 API는 문제 없는데)이 혼란스러운 부분이 많았습니다.

일부 필드 들이 없거나 일괄되게 적용되어야 하는 부분들(예. 페이징, 활성화 여부 등)이 누락된 경우들이 있습니다. 양해 부탁드리고요 계속 피드백 주시면 수정해 나가겠습니다.

파일업로드API의 url에 siteId를 세팅하는 부분을 제거하였습니다. siteId 세팅은 이후에 관리자페이지에서는 항상 해야 하는 것인데, 그 때가서 일괄 적용하겠습니다.

## Endpoints

| Meaning | Notaion | URL                           |
| ------- | ------- | ----------------------------- |
| 총괄    | %MANGE% | http://manage.cube-scout.com  |
| 어드민  | %ADMIN% | http://airport.cube-scout.com |

# API설명

## 공통사항

### 데이터 필드 설명

대부분 Save Item 항목에 설명되어 있습니다. 조회시에만 특이 사항이 있는 경우에는 Get Item 항목에 설명합니다.

### 데이터 저장

신규 데이터 추가 및 기존 데이터 수정에 하나의 API(Save Item)를 사용하며 신규에는 id 필드를 입력하지 않습니다.

조회 결과의 createdAt(데이터 등록일)은 저장시에는 입력시에는 입력하지 않습니다.

## 페이징

```shell
curl %MANAGE%/api/addInfo/col?sort=name&size=4&page=0
```

> Response

```json
{
  "page": 0,
  "size": 4,
  "totalPages": 716,
  "totalElements": 2864,
  "content": [
    {
      "id": 2234,
      "name": "ACCADEMIA DI COSTUME E DI MODA",
      "cate1": "대학교",
      "cate2": "해외대",
      "useYn": "Y"
    },
    {
    ...
    },
    {
    ...
    },
    {
    ...
    }
  ]
}
```

### Query Parameters (optional)

| Name | Description             |
| ---- | ----------------------- |
| page | 페이지 번호(0부터 시작) |
| size | 페이지당 아이템수       |
| sort | 정렬기준                |

## 인증(로그인)

```javascript
fetch("/api/login", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ userId: "jenny", password: "1234" }),
}).then(async (res) => {
  let json = await res.json();
  console.log(json);
  sessionStorage.setItem("login-token", json.token);
});
```

> Reponse

```json
{
  "success": true,
  "token": "eyJhbGciOiJIUzM4NCJ9.eyJpc3MiOiJqZW5ueSIsImlhdCI6MTcyMjI1MDM3NywiZXhwIjoxNzIyMjUwNDM3LCJyb2xlIjoic3RhZmYiLCJzaXRlSWQiOjB9.Ue6uNmUbKqsWcTCGVsDsoWYnAbVknkHltUKa42YBBpQIAGnzjSs7on-BsmB-83SE",
  "role": "super",
  "siteId": 0
}
```

`POST /api/login`

응답의 role, siteId는 추후 사용될지 몰라서 넣어 두었습니다. 혹시 활용된다면 공유 부탁드립니다.  
token은 JWT방식을 사용하며 자체만으로 권한이나 여러가지 정보를 가질 수 있지만 클라이언트에서 디코딩하는 수고를 피하고 싶어서 이렇게 구성했습니다. 추후 서로 여유가 된다면 더 깔끔하게 정리할 수 있을거 같습니다.

## 인가

```javascript
let token = sessionStorage.getItem("login-token");
if (token == null) {
  window.location.href = "login.html";
} else {
  fetch("http://manage.cube-scout.com:8080/sapi/test", {
    method: "GET",
    headers: { Authorization: "Bearer " + token },
  }).then(async (res) => {
    if (res.status == 403) {
      window.location.href = "login.html";
    }
    console.log(await res.text()); // success
  });
}
```

모든 api 호출에서는 헤더에 토큰을 전송해 주셔야 되지만 당장은 개발 편의를 위해 인가를 하지 않으며 인가 관련 개발은 예제의 /sapi/test를 이용해 주십시오.
예제 코드는 이해를 돕기 위한 것으로 로그인으로 생성된 토큰의 관리나 인가 결과에 따른 로직이 꼭 저렇게 되어야 하는 것은 아닙니다.

서버에서 토큰 만료시간은 테스트를 위해 1분으로 되어 있으며 추후 6시간 정도로 변경할 예정입니다.

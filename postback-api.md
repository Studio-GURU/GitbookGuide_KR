---
hidden: true
---

# Postback API 가이드

### 1. 개요

매체사는 아래 가이드를 참고하여 Postback API를 제작해 주세요. 기본적으로 `transactionID`, `userID`, `reward` 값을 필수로 포함하며, 추가적으로 필요한 값이 있으면 함께 전달해 드릴 예정입니다.

응답값에는 성공 또는 실패 코드 등을 반환해야 합니다.

***

### 2. 요청 방식

* **Method**: `POST`
* **Content-Type**: `application/json`
* **Endpoint**: `{매체사에서 제공된 Postback URL}`

***

### 3. 요청 파라미터

| parameter       | type    | require | description                 |
| --------------- | ------- | ------- | --------------------------- |
| `transactionID` | String  | true    | 트랜잭션 고유 ID (이벤트별 고유 값)      |
| `userID`        | String  | true    | 매체사에서 sign 생성 시 포함되는 userID |
| `reward`        | Integer | true    | 지급될 리워드 금액                  |

***

### 4. 요청 예시

```
{
  "transactionID": "txn_456789",
  "userID": "abc123",
  "reward": 1000
}
```

***

### 5. 응답 형식

응답값은 성공 또는 실패 여부를 반환해야 합니다.

#### ✅ 성공 응답 예시

```
{
  "result": code, // 하단 표를 참고해주세요.
  "msg": 응답 메세지 // 코드에 해당하는 메세지를 보내주세요.
}
```



| code | description |
| ---- | ----------- |
| 0000 | 적립 완료       |
| 9001 | 중복 적립       |
| 9003 | 적립 요청 중     |

이 가이드를 참고하여 API를 제작 후 전달해 주세요 ! 😊

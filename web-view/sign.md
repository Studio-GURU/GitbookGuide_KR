---
icon: key
---

# Sign 생성

**timestamp, nonce, userID, signature 4가지의 값을 순서대로 구분자 . ( full stop ) 을 붙여 생성합니다.**\
`sign = timestamp.nonce.userID.signature`

{% hint style="info" %}
**signature 생성 (&#x20;**<mark style="color:red;">**HmacSHA256 생성에 필요한 Key는 별도 전달 됩니다.**</mark>**&#x20;)**

***



<mark style="color:red;">**{} 표현은 변수 입니다 ( { } 값이 포함되지 않도록 주의 바랍니다. )**</mark>

**{timeStamp}{nonce}{userID}**

위 값을 HmacSHA256 Hash → **Base64 Url Encoding**을 통해 Signature를 생성합니다.

***

* **timeStamp** → unix timestamp seconds
* **nonce** → 문자열 32자 ( 임의로 생성된 문자열 32자 )\
  1 ) signature 생성 시 매번 새로운 값을 생성하여 입력이 필요합니다.
* **userID** → 채널사에서 사용되는 유저 식별자\
  1 ) 포인트 지급 기능 등을 추가 연동할 때 보물섬 서비스에서 채널사에 전달할 시에도 사용 될 수 있습니다. \
  2 ) 채널사의 유저 식별자 전달에 따른 보안 정책 기준을 고려하여 \
  &#x20;    ( 암호화 X / 대칭형 암호화 / 비대칭형 암호화 ) 유저 식별자를 전달해주시면 됩니다.  &#x20;
{% endhint %}

`sign` 값은 보안상의 이유로 반드시 채널사의 서버에서 생성해야 합니다.\
보물섬에서는 아래 기준을 통해 해당 값의 유효성을 판단합니다.

1️⃣ **사용 여부 확인**\
2️⃣ **생성 후 5분이 초과 되었는지 여부 확인**

이에 따라, 사용자의 액션이 발생할 때마다 즉시 새로운 `sign` 값을 생성해야 합니다.



**생성 예제**

```javascript
sign = 1740551960.e7f2238a9d3b41f9b2cc9232cc0b7aaa.testUserTC.RBlIs41tz1xg8VcR0pQM2ois08LW5DOi4DWHiNDxxzE=
```

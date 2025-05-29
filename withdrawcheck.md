---
description: 매체사 유저의 보물섬 가입 가능 여부를 조회하는 API입니다.
hidden: true
icon: mobile-notch
---

# \[ API ] 가입 가능 여부 조회

## Version

버전 정보는 URL 경로에 표현하지 않으며, 헤더의 accept-version 속성 값에 정의합니다.

| Version | Date       | Description |
| ------- | ---------- | ----------- |
| 1.0.0   | 2024.05.26 | Create      |

## Account Withdraw Check

```
테스트
GET https://api-test.treasurecomics.com/external/account/withdraw/check

라이브
GET https://api.treasurecomics.com/external/account/withdraw/check
```

### Security

{% hint style="danger" %}
**IPSec 또는 방화벽 구성을 위한 IP 정보가 필요한 경우 아래의 내용을 참고 하세요.**
{% endhint %}

<table><thead><tr><th width="344">Url</th><th>IPAddress</th></tr></thead><tbody><tr><td><strong>api-test.treasurecomics.com</strong></td><td>43.201.240.226</td></tr><tr><td></td><td>43.202.82.8</td></tr><tr><td><strong>api.treasurecomics.com</strong></td><td>15.165.122.39</td></tr><tr><td></td><td>3.38.54.136</td></tr></tbody></table>

### Heders

| Name           | Value              |
| -------------- | ------------------ |
| Content-Type   | `application/json` |
| Authorization  | `Basic token`      |
| Accept-Version | `1.0.0`            |

### **Request Body**

<table data-full-width="false"><thead><tr><th width="116">Name</th><th width="141">Type</th><th width="127">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>sign</code></td><td>string</td><td>true</td><td><a data-mention href="web-view/sign.md">sign.md</a></td></tr></tbody></table>

```
// usage example
###
GET https://api-{env}.treasurecomics.com/external/account/withdraw/check?sign={sign}
Accept-Version: 1.0.0
Content-Type: application/json
Authorization: Basic Token
```

### **Response**

<table><thead><tr><th width="270">Fields</th><th width="106">Type</th><th>Require</th><th>Description</th></tr></thead><tbody><tr><td><code>isLoginAble</code></td><td>boolean</td><td>true</td><td>가입 가능 여부</td></tr><tr><td><code>message</code></td><td>string</td><td>false</td><td>재가입 가능 일자 안내 메세지</td></tr><tr><td><code>withdrawDateTime</code></td><td>string</td><td>false</td><td>탈퇴 일자</td></tr></tbody></table>

**Response Code**

{% tabs %}
{% tab title="200" %}
{% code lineNumbers="true" %}
```json
  // 가입 불가 시
  {
    "isLoginAble": false,
    "message": "2025년 6월 2일 16시 34분 이후 재가입 가능합니다.",
    "withdrawDateTime": "2025-05-26T16:34:02+09:00"
  }
  
  // 가입 가능 시
  {
    "isLoginAble": true
  }
```
{% endcode %}
{% endtab %}

{% tab title="499" %}
{% code lineNumbers="true" %}
```json
{
  "code": "err_already_used_signature",
  "message": "이미 사용된 Signature 입니다.",
  "data": null,
  "appendix": {
    "reason": "이미 사용된 Signature 입니다.",
    "stack": "Error: UNHANDLED\n    at _validateSignature (/var/app/current/build/controllers/external/toss/recentView/get.1.0.0.js:33:15)\n    at process.processTicksAndRejections (node:internal/process/task_queues:95:5)"
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### Reponse Error Code

<table><thead><tr><th width="307">Code</th><th>Reason</th><th>Message</th></tr></thead><tbody><tr><td><mark style="color:red;"><code>err_invalid_signature</code></mark></td><td>Signature 검증 실패</td><td>잘못된 Signature 입니다.</td></tr><tr><td><mark style="color:red;"><code>err_already_used_signature</code></mark></td><td>사용된 Signature 재사용<br>-> 5분간 제한</td><td>이미 사용된 Signature 입니다.</td></tr></tbody></table>








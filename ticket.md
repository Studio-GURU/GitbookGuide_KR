---
description: 로그인 시 추가 정보를 전달하는 방식에 사용되는 OTT ( One-Time Ticket ) 생성 가이드입니다.
hidden: true
icon: mobile-notch
---

# Ticket 생성

## Flow

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

&#x20;**✓ WebView 를 열때 sign값이 아닌 ticket, ticketType 값을 쿼리스트링으로 넘겨줍니다.**

&#x20;**✓ ticket의 유효 시간은 20초입니다.**&#x20;

&#x20;**✓ WebView를 열기 전 호출하고 바로 사용합니다.**

## Version

버전 정보는 URL 경로에 표현하지 않으며, 헤더의 accept-version 속성 값에 정의합니다.

| Version | Date       | Description |
| ------- | ---------- | ----------- |
| 1.0.0   | 2024.03.28 | Create      |

## Create Account Ticket

```
테스트
POST https://api-test.treasurecomics.com/external/account/ticket

라이브
POST https://api.treasurecomics.com/external/account/ticket
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

<table data-full-width="false"><thead><tr><th width="158.63671875">Name</th><th width="141">Type</th><th width="127">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>providerUID</code></td><td>string</td><td>true</td><td>채널사에서 사용되는 유저 식별자 <br>( 암호화 X / 대칭형 암호화 / 비대칭형 암호화 )</td></tr><tr><td><code>provider</code></td><td>string</td><td>true</td><td>'channel' 값 고정</td></tr><tr><td><code>deviceADID</code></td><td>string</td><td>false</td><td><p>광고 식별 ID </p><p>AOS : ADID값 전달<br>IOS : IDFA값 전달</p></td></tr><tr><td><code>birthday</code></td><td>string</td><td>false</td><td>' 19980101 ' 형식으로 발송</td></tr><tr><td><code>gender</code></td><td>string</td><td>false</td><td>1: 남자, 2: 여</td></tr><tr><td><code>phone</code></td><td>string</td><td>false</td><td>'01012341234' 형식으로 발송</td></tr><tr><td><code>carrier</code></td><td>string</td><td>false</td><td>SKT, KT, LG</td></tr></tbody></table>

```
// usage example
POST https://api-{env}.treasurecomics.com/external/account/ticket
Accept-Version: 1.0.0
Content-Type: application/json
Authorization: Basic Token

{
    "providerUID": {value},
    "provider": {value},
    "deviceADID": {deviceADID},
    "birthday": '19980101',
    "gender": '1',
    "phone": '01012341234',
    "carrier": 'LG',
    ... // 보물섬과 협의된 추가 파라미터 값
}
```

### **Response**

<table><thead><tr><th width="270">Fields</th><th width="106">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>ticket</code></td><td>string</td><td>32 글자의 티켓</td></tr><tr><td><code>ticketType</code></td><td>string</td><td>보물섬 로그인을 위해 판단되는 유저의 값<br>ex ) agree, login</td></tr></tbody></table>

**Response Code**

{% tabs %}
{% tab title="200" %}
{% code lineNumbers="true" %}
```json
  {
    "ticket": "1432b8ea0b9311f09c8d02d57e3413e1",
    "ticketType": "login"
  }
```
{% endcode %}
{% endtab %}
{% endtabs %}








---
icon: thumbs-up
description: 유저가 조회한 컨텐츠 기반으로 추천 목록 API 사용 방법에 대해 알아 보세요.
---

# 추천 컨텐츠 목록 조회

## Version

버전 정보는 URL 경로에 표현하지 않으며, 헤더의 accept-version 속성 값에 정의합니다.

| Version | Date       | Description |
| ------- | ---------- | ----------- |
| 1.0.0   | 2024.08.23 | Create      |

## Rcommendation Contents

```
테스트
GET https://api-test.treasurecomics.com/external/recommendation?sign={value}

라이브
GET https://api.treasurecomics.com/external/recommendation?sign={value}={value}
```

**추천 컨텐츠 목록을 반환 합니다.**

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

### **Body**

{% hint style="info" %}
**signature 생성 (**<mark style="color:red;">**HmacSHA256 생성에 필요한 Key는 영업팀을 통해 전달 됩니다.**</mark>**)**

***

<mark style="color:red;">**{} 표현은 변수 입니다 ({}값이 포함되지 않도록 주의 바랍니다.)**</mark>

**{timeStamp}{nonce}{userID}**

위 값을 HmacSHA256 Hash -> Base64 Url Encodeing을 통해 Signature를 생성합니다.

***

* timeStamp -> unix timestamp seconds
* nonce -> 문자열 32자(임의로 생성된 문자열 32자)
* user 식별자 -> 회원 구분이 가능한 식별자
{% endhint %}

<table data-full-width="false"><thead><tr><th width="116">Name</th><th width="141">Type</th><th width="127">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>sign</code></td><td>string</td><td>true</td><td><p><code>timestamp.nonce.userID.signature</code></p><hr><p><mark style="background-color:red;">timestamp, nonce, userID, signature 4가지 값을 순서대로 구분자 .(full stop)을 붙여 sign 값을 생성합니다.</mark></p><hr><p><mark style="background-color:yellow;">sign값은 보안상 채널사의 서버에서 생성하며 보물섬에서는 sign 값이 1)사용된것인지 2)생성한지 5분이 지난 값인지 확인하여 유효하지 않음으로 판단할 수 있음으로 사용자의 액션이 있을 시 마다 즉시 생성하여 호출하도록 개발합니다.</mark></p></td></tr><tr><td>adid</td><td>string</td><td>false</td><td>광고식별값 : android ADID / iOS IDFA</td></tr><tr><td>gender</td><td>number</td><td>false</td><td>성별 : 1=남자 / 2=여자</td></tr><tr><td>age</td><td>number</td><td>false</td><td>나이</td></tr><tr><td>isAdult</td><td>number</td><td>false</td><td>성인여부: 0=성인아님 / 1=성인</td></tr></tbody></table>

```
// get usage example
https://api-{env}.treasurecomics.com/external/recommendation?sign=1724328195.3da08653e6c1420aac89eecdf5c20063.OGMzYjUzYTUyYjE1YTJiNDAyZGM3MGJiZmMzMDI2YWE1NDg0YWY2ZTdjNjMyZTJlMTdjMjQyOGU1NjZhYjdhYQ
```

### **Response**

<table><thead><tr><th width="239">Fields</th><th width="106">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>recommendationSN</code></td><td>number</td><td>sequence</td></tr><tr><td><code>title</code></td><td>string</td><td>제목</td></tr><tr><td><code>description</code></td><td>string</td><td>내용</td></tr><tr><td><code>thumbnail</code></td><td>string</td><td>이미지 경로</td></tr><tr><td><code>contentType</code></td><td>string</td><td>웹툰 | 웹소설</td></tr><tr><td><code>contentCName</code></td><td>string</td><td>작품키</td></tr><tr><td><code>episodeNo</code></td><td>number</td><td>회차번호</td></tr><tr><td><code>genre</code></td><td>string</td><td>장르</td></tr><tr><td><code>link</code></td><td>string</td><td><p>제공되는 링크 뒤에 sign 붙여서 전달</p><p>예)<code>&#x26;sign=1724328195.3da08653e6c1420aac89eecdf5c20063.OGMzYjUzYTUyYjE1YTJiNDAyZGM3MGJiZmMzMDI2YWE1NDg0YWY2ZTdjNjMyZTJlMTdjMjQyOGU1NjZhYjdhYQ</code></p></td></tr><tr><td><code>returnUrl</code></td><td>string</td><td>최종 이동 링크(참고용)</td></tr><tr><td><code>order</code></td><td>number</td><td>노출 우선 숭위(같은 값 존재)</td></tr><tr><td><code>recommendationDate</code></td><td>string</td><td>추천일(yyyy-MM-dd)</td></tr></tbody></table>

**Response Code**

{% tabs %}
{% tab title="200" %}
{% code lineNumbers="true" %}
```json
[
  {
    "recommendationSN": 5,
    "title": "봉사감과 러브레터",
    "description": "봉사감과 러브레터 test",
    "thumbnail": "https://s.treasurecomics.com/images/test/webtoon/cw631ac7ba1f/thumbnailFile_1718001726.jpg",
    "contentType": "웹툰",
    "contentCName": "cw631ac7ba1f",
    "episodeNo": 1,
    "genre": "무협,드라마",
    "link": "https://test.treasurecomics.com/gateway/common?returnUrl=https%3A%2F%2Ftest.treasurecomics.com%2Fwebtoon%2Fviewer%2Fcw631ac7ba1f%2F1",
    "returnUrl": "https://test.treasurecomics.com/webtoon/viewer/cw631ac7ba1f/1",
    "order": 1,
    "recommendationDate": "2024-08-22"
  },
  {
    "recommendationSN": 8,
    "title": "나는 패왕이다",
    "description": "이런 패왕 존재?",
    "thumbnail": "https://s.treasurecomics.com/images/test/novel/cn718f1595fc/thumbnailFile_1718001368.jpg",
    "contentType": "웹소설",
    "contentCName": "cn718f1595fc",
    "episodeNo": 1,
    "genre": "무협",
    "link": "https://test.treasurecomics.com/gateway/common?returnUrl=https%3A%2F%2Ftest.treasurecomics.com%2Fnovel%2Fviewer%2Fcn718f1595fc%2F1",
    "returnUrl": "https://test.treasurecomics.com/novel/viewer/cn718f1595fc/1",
    "order": 1,
    "recommendationDate": "2024-08-22"
  },
  {
    "recommendationSN": 7,
    "title": "다 때려잡는 천재 회계사",
    "description": "이런 회계사가 있으려나?",
    "thumbnail": "https://s.treasurecomics.com/images/test/novel/cn0d3b6afccd/thumbnailFile_1718000646.jpg",
    "contentType": "웹소설",
    "contentCName": "cn0d3b6afccd",
    "episodeNo": 1,
    "genre": "대체역사",
    "link": "https://test.treasurecomics.com/gateway/common?returnUrl=https%3A%2F%2Ftest.treasurecomics.com%2Fnovel%2Fviewer%2Fcn0d3b6afccd%2F1",
    "returnUrl": "https://test.treasurecomics.com/novel/viewer/cn0d3b6afccd/1",
    "order": 1,
    "recommendationDate": "2024-08-22"
  },
  {
    "recommendationSN": 9,
    "title": "무심한 당신에게 죽음을",
    "description": "같이죽자",
    "thumbnail": "https://s.treasurecomics.com/images/test/novel/cn3a0d0de7e6/thumbnailFile_1718000377.jpg",
    "contentType": "웹소설",
    "contentCName": "cn3a0d0de7e6",
    "episodeNo": 1,
    "genre": "스포츠",
    "link": "https://test.treasurecomics.com/gateway/common?returnUrl=https%3A%2F%2Ftest.treasurecomics.com%2Fnovel%2Fviewer%2Fcn3a0d0de7e6%2F1",
    "returnUrl": "https://test.treasurecomics.com/novel/viewer/cn3a0d0de7e6/1",
    "order": 1,
    "recommendationDate": "2024-08-22"
  },
  {
    "recommendationSN": 4,
    "title": "오! 나의 하녀님",
    "description": "오! 나의 하녀님 test",
    "thumbnail": "https://s.treasurecomics.com/images/test/webtoon/cw3a81e99b70/thumbnailFile_1717999374.jpg",
    "contentType": "웹툰",
    "contentCName": "cw3a81e99b70",
    "episodeNo": 1,
    "genre": "로맨틱판타지",
    "link": "https://test.treasurecomics.com/gateway/common?returnUrl=https%3A%2F%2Ftest.treasurecomics.com%2Fwebtoon%2Fviewer%2Fcw3a81e99b70%2F1",
    "returnUrl": "https://test.treasurecomics.com/webtoon/viewer/cw3a81e99b70/1",
    "order": 1,
    "recommendationDate": "2024-08-22"
  },
  {
    "recommendationSN": 6,
    "title": "비트타는 수양대군",
    "description": "무대 위에서 비트를 타볼까",
    "thumbnail": "https://s.treasurecomics.com/images/test/novel/cnb998dc34fc/thumbnailFile_1717999357.jpg",
    "contentType": "웹툰",
    "contentCName": "cnb998dc34fc",
    "episodeNo": 1,
    "genre": "현대판타지",
    "link": "https://test.treasurecomics.com/gateway/common?returnUrl=https%3A%2F%2Ftest.treasurecomics.com%2Fnovel%2Fviewer%2Fcnb998dc34fc%2F1",
    "returnUrl": "https://test.treasurecomics.com/novel/viewer/cnb998dc34fc/1",
    "order": 1,
    "recommendationDate": "2024-08-22"
  }
]
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

***

## 추천 컨텐츠 목록 구현 화면 예시

<div align="left"><figure><img src="../../.gitbook/assets/bms_recommendation_2.png" alt="" width="375"><figcaption></figcaption></figure></div>














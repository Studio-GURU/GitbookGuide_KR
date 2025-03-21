---
description: 사용자가 최근 본 작품을 조회하는 API 로 채널회원이 연동되어 있는 방식에서만 동작합니다.
icon: mobile
---

# \[ API ] 최근 본 작품 조회 ( Client )

## Version

버전 정보는 URL 경로에 표현하지 않으며, 헤더의 accept-version 속성 값에 정의합니다.

| Version | Date       | Description |
| ------- | ---------- | ----------- |
| 1.0.0   | 2025.03.19 | Create      |

## Recent View Contents

```
테스트
GET https://api-test.treasurecomics.com/external/open/{channel}/recentView?sign={value}

라이브
GET https://api.treasurecomics.com/external/open/{channel}/recentView?sign={value}
```

**✓ 유저의 최근 감상 컨텐츠 목록을 반환 합니다.**

**✓** `{channel}` 값은 **별도 전달** 됩니다.

### Security

{% hint style="danger" %}
**IPSec 또는 방화벽 구성을 위한 IP 정보가 필요한 경우 아래의 내용을 참고 하세요.**
{% endhint %}

<table><thead><tr><th width="344">Url</th><th>IPAddress</th></tr></thead><tbody><tr><td><strong>api-test.treasurecomics.com</strong></td><td>43.201.240.226</td></tr><tr><td></td><td>43.202.82.8</td></tr><tr><td><strong>api.treasurecomics.com</strong></td><td>15.165.122.39</td></tr><tr><td></td><td>3.38.54.136</td></tr></tbody></table>

### Heders

| Name           | Value              |
| -------------- | ------------------ |
| Content-Type   | `application/json` |
| Accept-Version | `1.0.0`            |

### **Request Params**

<table data-full-width="false"><thead><tr><th width="116">Name</th><th width="141">Type</th><th width="127">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>sign</code></td><td>string</td><td>true</td><td><a data-mention href="../../sign.md">sign.md</a></td></tr></tbody></table>

```
// get usage example
https://api-{env}.treasurecomics.com/external/open/{channel}/recentView?sign=1724328195.3da08653e6c1420aac89eecdf5c20063.OGMzYjUzYTUyYjE1YTJiNDAyZGM3MGJiZmMzMDI2YWE1NDg0YWY2ZTdjNjMyZTJlMTdjMjQyOGU1NjZhYjdhYQ
```

### **Response**

<table><thead><tr><th width="270">Fields</th><th width="106">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>title</code></td><td>string</td><td>제목</td></tr><tr><td><code>description</code></td><td>string</td><td>내용</td></tr><tr><td><code>thumbnail</code></td><td>string</td><td>이미지 경로</td></tr><tr><td><code>contentType</code></td><td>string</td><td>웹툰 | 웹소설</td></tr><tr><td><code>contentCName</code></td><td>string</td><td>작품 키</td></tr><tr><td><code>contentEpisodeTitle</code></td><td>string</td><td>마지막으로 본 에피소드 제목</td></tr><tr><td><code>episodeNo</code></td><td>number</td><td>마지막으로 본 에피소드 회차</td></tr><tr><td><code>genre</code></td><td>string</td><td>장르</td></tr><tr><td><code>link</code></td><td>string</td><td><p>제공되는 링크 뒤에 sign 붙여서 전달</p><p>예)<code>&#x26;sign=1724328195.3da08653e6c1420aac89eecdf5c20063.OGMzYjUzYTUyYjE1YTJiNDAyZGM3MGJiZmMzMDI2YWE1NDg0YWY2ZTdjNjMyZTJlMTdjMjQyOGU1NjZhYjdhYQ</code></p></td></tr><tr><td><code>returnUrl</code></td><td>string</td><td>최종 이동 링크 ( 참고용 )</td></tr><tr><td><code>isWaitFree</code></td><td>boolean</td><td>기다리면 무료 작품 여부</td></tr><tr><td><code>waitFreeInfo(optional)</code></td><td>object</td><td>기다리면 무료 티켓 정보</td></tr><tr><td></td><td></td><td><p><code>{</code><br>  <code>chargedTicket: boolean,</code><br>  <code>baseDate: Date,</code><br>  <code>chargedDate: Date</code><br><code>}</code></p><ul><li><mark style="background-color:purple;">chargedTicket: 기다리면 무료 티켓 소지 여부</mark></li><li><mark style="background-color:purple;">baseDate: 티켓 계산 기준 날짜</mark></li><li><mark style="background-color:purple;">chargeDate: 티켓 충전 날짜</mark></li></ul></td></tr><tr><td><code>freeEpisode</code></td><td>number</td><td>무료 회차 수</td></tr></tbody></table>

**Response Code**

{% tabs %}
{% tab title="200" %}
{% code lineNumbers="true" %}
```json
[
  {
    "title": "용을 키우는 10가지 방법",
    "description": null,
    "thumbnail": "https://s.treasurecomics.com/images/test/webtoon/cw4357a295d0/thumbnail_1718174618.jpg",
    "contentType": "웹툰",
    "contentCName": "cw4357a295d0",
    "contentEpisodeTitle": "1화",
    "episodeNo": 1
    "genre": "드라마,공포/스릴러",
    "link": "https://test.treasurecomics.com/gateway/toss?returnUrl=https%3A%2F%2Ftest.treasurecomics.com%2Fcontent%2Flist%2Fcw4357a295d0",
    "returnUrl": "https://test.treasurecomics.com/content/list/cw4357a295d0",
    "isWaitFree": true,
    "waitFreeInfo": {
	    chargedTicket: true,
	    baseDate: "2024-09-27T03:00:00Z",
	    chargedDate: "2024-09-27T03:00:00Z"
    },
    "freeEpisode": 3
  },
    {
    "title": "내 인생에서 사라져 주세요",
    "description": "마지막이라고 생각했을 때 다시 찾아온 기회,이번엔 놓치지 않겠어!",
    "thumbnail": "https://s.treasurecomics.com/images/test/novel/cnc0e5f2fa7a/posterThumbnail_1723080834.jpg",
    "contentType": "웹소설",
    "contentCName": "cnc0e5f2fa7a",
    "contentEpisodeTitle": "1화",
    "episodeNo": 1,
    "genre": "로맨스판타지",
    "link": "https://bitbunny-test.treasurecomics.com/gateway/common?returnUrl=https%3A%2F%2Fbitbunny-test.treasurecomics.com%2Fcontent%2Flist%2Fcnc0e5f2fa7a",
    "returnUrl": "https://bitbunny-test.treasurecomics.com/content/list/cnc0e5f2fa7a",
    "isWaitFree": true,
    "waitFreeInfo": {
      "chargedTicket": true,
      "baseDate": "2025-03-19T05:00:01.650Z",
      "chargedDate": "2025-03-19T05:00:01.650Z"
    },
    "freeEpisode": 5
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

**Response Error Code**

<table><thead><tr><th width="307">Code</th><th>Reason</th><th>Message</th></tr></thead><tbody><tr><td><mark style="color:red;"><code>err_invalid_signature</code></mark></td><td>Signature 검증 실패</td><td>잘못된 Signature 입니다.</td></tr><tr><td><mark style="color:red;"><code>err_already_used_signature</code></mark></td><td>사용된 Signature 재사용<br>-> 5분간 제한</td><td>이미 사용된 Signature 입니다.</td></tr><tr><td><mark style="color:red;"><code>err_not_exists_app</code></mark></td><td>확인되지 않은 channel</td><td>등록된 앱이 없습니다.</td></tr></tbody></table>

***

## 최근 본 작품 조회 구현 예시 화면

<div align="left"><figure><img src="../../../.gitbook/assets/bms_recently.png" alt="" width="375"><figcaption></figcaption></figure></div>










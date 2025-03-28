---
description: 보물섬이 제공하는 "오늘의 추천" 페이지를 사용하지 않고, 별도 화면을 구성하는 커스텀 방식에 사용합니다.
icon: mobile-notch
---

# \[ API ] 추천 컨텐츠 목록 조회 ( Client )

## Version

버전 정보는 URL 경로에 표현하지 않으며, 헤더의 accept-version 속성 값에 정의합니다.

| Version | Date       | Description |
| ------- | ---------- | ----------- |
| 1.0.0   | 2025.03.19 | Create      |

## Rcommendation Contents

```
테스트
GET https://api-test.treasurecomics.com/external/open/{channel}/recommendation?sign={value}

라이브
GET https://api.treasurecomics.com/external/open/{channel}/recommendation?sign={value}
```

&#x20;**✓ 추천 컨텐츠 목록을 반환 합니다.**

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
https://api-{env}.treasurecomics.com/external/open/{channel}/recommendation?sign=1724328195.3da08653e6c1420aac89eecdf5c20063.OGMzYjUzYTUyYjE1YTJiNDAyZGM3MGJiZmMzMDI2YWE1NDg0YWY2ZTdjNjMyZTJlMTdjMjQyOGU1NjZhYjdhYQ
```

### **Response**

<table><thead><tr><th width="239">Fields</th><th width="106">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>recommendationSN</code></td><td>number</td><td>sequence</td></tr><tr><td><code>title</code></td><td>string</td><td>제목</td></tr><tr><td><code>description</code></td><td>string</td><td>내용</td></tr><tr><td><code>thumbnail</code></td><td>string</td><td>썸네일 이미지 경로 ( 세로 )</td></tr><tr><td><code>subThumbnail</code></td><td>string</td><td>썸네일 이미지 경로 ( 가로 )</td></tr><tr><td><code>contentType</code></td><td>string</td><td>웹툰 | 웹소설</td></tr><tr><td><code>contentCName</code></td><td>string</td><td>작품 키</td></tr><tr><td><code>episodeNo</code></td><td>number</td><td>회차 번호</td></tr><tr><td><code>genre</code></td><td>string</td><td>장르</td></tr><tr><td><code>link</code></td><td>string</td><td><p>제공되는 링크 뒤에 sign 붙여서 전달</p><p>예)<code>&#x26;sign=1724328195.3da08653e6c1420aac89eecdf5c20063.OGMzYjUzYTUyYjE1YTJiNDAyZGM3MGJiZmMzMDI2YWE1NDg0YWY2ZTdjNjMyZTJlMTdjMjQyOGU1NjZhYjdhYQ</code></p></td></tr><tr><td><code>returnUrl</code></td><td>string</td><td>최종 이동 링크 ( 참고용 )</td></tr><tr><td><code>order</code></td><td>number</td><td>노출 우선 순위 ( 같은 값이 존재할 수 있습니다 )</td></tr><tr><td><code>recommendationDate</code></td><td>string</td><td>추천일 ( YYYY-MM-DD )</td></tr><tr><td><code>freeEpisode</code></td><td>number</td><td>무료 회차 수</td></tr><tr><td><code>isRewardAvailable</code></td><td>boolean</td><td>포인트 지급 가능 여부</td></tr><tr><td><code>minReward</code></td><td>number</td><td>지급 가능 최소 금액 ( 지급 불가능일 경우 0으로 반환 )</td></tr><tr><td><code>maxReward</code></td><td>number</td><td>지급 가능 최대 금액 ( 지급 불가능일 경우 0으로 반환 )</td></tr></tbody></table>

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
    "recommendationDate": "2024-08-22",
    "freeEpisode": 3,
    "isRewardAvailable": true,
    "minReward": 1,
    "maxReward": 5
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
    "recommendationDate": "2024-08-22",
    "freeEpisode": 0,
    "isRewardAvailable": true,
    "minReward": 1,
    "maxReward": 5
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
    "recommendationDate": "2024-08-22",
    "freeEpisode": 8,
    "isRewardAvailable": true,
    "minReward": 1,
    "maxReward": 5
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
    "recommendationDate": "2024-08-22",
    "freeEpisode": 2,
    "isRewardAvailable": true,
    "minReward": 1,
    "maxReward": 5
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
    "recommendationDate": "2024-08-22",
    "freeEpisode": 1,
    "isRewardAvailable": true,
    "minReward": 1,
    "maxReward": 5
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
    "recommendationDate": "2024-08-22",
    "freeEpisode": 25,
    "isRewardAvailable": true,
    "minReward": 1,
    "maxReward": 5
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

<table><thead><tr><th width="307">Code</th><th>Reason</th><th>Message</th></tr></thead><tbody><tr><td><mark style="color:red;"><code>err_invalid_signature</code></mark></td><td>Signature 검증 실패</td><td>잘못된 Signature 입니다.</td></tr><tr><td><mark style="color:red;"><code>err_already_used_signature</code></mark></td><td>사용된 Signature 재사용<br>-> 5분간 제한</td><td>이미 사용된 Signature 입니다.</td></tr><tr><td><mark style="color:red;"><code>err_not_exists_app</code></mark></td><td>확인되지 않은 channel</td><td>등록된 앱이 없습니다.</td></tr></tbody></table>

***

## 추천 컨텐츠 목록 구현 화면 예시

<div align="left"><figure><img src="../../../.gitbook/assets/bms_recommendation_2.png" alt="" width="375"><figcaption></figcaption></figure></div>














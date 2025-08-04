---
description: 사용자가 최근 본 작품을 조회하는 API 로 채널회원이 연동되어 있는 방식에서만 동작합니다.
icon: rectangle-history-circle-user
---

# \[ API ] 최근 본 작품 조회

## Version

버전 정보는 URL 경로에 표현하지 않으며, 헤더의 accept-version 속성 값에 정의합니다.

| Version | Date       | Description |
| ------- | ---------- | ----------- |
| 1.0.0   | 2024.08.23 | Create      |

## Recent View Contents

```
테스트
GET https://api-test.treasurecomics.com/external/recentView?sign={value}

라이브
GET https://api.treasurecomics.com/external/recentView?sign={value}
```

**유저의 최근 감상 컨텐츠 목록을 반환 합니다.**

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

### **Request Params**

<table data-full-width="false"><thead><tr><th width="116">Name</th><th width="141">Type</th><th width="127">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>sign</code></td><td>string</td><td>true</td><td><a data-mention href="../../sign.md">sign.md</a></td></tr></tbody></table>

```
// get usage example
https://api-{env}.treasurecomics.com/external/recentView?sign=1724328195.3da08653e6c1420aac89eecdf5c20063.OGMzYjUzYTUyYjE1YTJiNDAyZGM3MGJiZmMzMDI2YWE1NDg0YWY2ZTdjNjMyZTJlMTdjMjQyOGU1NjZhYjdhYQ
```

### **Response**

<table><thead><tr><th width="270">Fields</th><th width="106">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>title</code></td><td>string</td><td>제목</td></tr><tr><td><code>description</code></td><td>string</td><td>내용</td></tr><tr><td><code>thumbnail</code></td><td>string</td><td><p>썸네일 이미지 경로 ( 세로 )</p><p>1080 * 1620</p></td></tr><tr><td><code>contentType</code></td><td>string</td><td>웹툰 | 웹소설 | 숏드라마</td></tr><tr><td><code>contentCName</code></td><td>string</td><td>작품 키</td></tr><tr><td><code>contentEpisodeTitle</code></td><td>string</td><td>마지막으로 본 에피소드 제목</td></tr><tr><td><code>episodeNo</code></td><td>number</td><td>마지막으로 본 에피소드 회차</td></tr><tr><td><code>genre</code></td><td>string</td><td><p>장르</p><pre><code>로맨스, 로맨스판타지, 판타지, 무협, 드라마, 액션, 학원, 일상, 스포츠, 공포/스릴러, BL, GL, 로맨스, 로맨스판타지, 판타지, 무협, 현대판타지, 대체역사, 스포츠, 공포/스릴러, BL, GL, 성인, 성인, 로맨스, 드라마, 일상
</code></pre></td></tr><tr><td><code>link</code></td><td>string</td><td><p>제공되는 링크 뒤에 sign 붙여서 전달</p><p>예)<code>&#x26;sign=1724328195.3da08653e6c1420aac89eecdf5c20063.OGMzYjUzYTUyYjE1YTJiNDAyZGM3MGJiZmMzMDI2YWE1NDg0YWY2ZTdjNjMyZTJlMTdjMjQyOGU1NjZhYjdhYQ</code></p></td></tr><tr><td><code>returnUrl</code></td><td>string</td><td>최종 이동 링크 ( 참고용 )</td></tr><tr><td><code>isWaitFree</code></td><td>boolean</td><td>기다리면 무료 작품 여부</td></tr><tr><td><code>waitFreeInfo(optional)</code></td><td>object</td><td>기다리면 무료 티켓 정보</td></tr><tr><td></td><td></td><td><p><code>{</code><br>  <code>chargedTicket: boolean,</code><br>  <code>baseDate: Date,</code><br>  <code>chargedDate: Date</code><br><code>}</code></p><ul><li><mark style="background-color:purple;">chargedTicket: 기다리면 무료 티켓 소지 여부</mark></li><li><mark style="background-color:purple;">baseDate: 티켓 계산 기준 날짜</mark></li><li><mark style="background-color:purple;">chargeDate: 티켓 충전 날짜</mark></li></ul></td></tr><tr><td><code>freeEpisode</code></td><td>number</td><td>무료 회차 수</td></tr></tbody></table>

**Response Code**

{% tabs %}
{% tab title="200" %}
{% code lineNumbers="true" %}
```json
[
  {
    "title": "당씨고아",
    "description": "복수를 가슴에 품고, 어떻게든 살아남기 위해 수단과 방법을 가리지 않는 당상원의 일대기.",
    "thumbnail": "https://s.treasurecomics.com/images/prod/novel/cn2b641081a4/posterThumbnail_1740011920.jpg",
    "contentType": "웹소설",
    "contentCName": "cn2b641081a4",
    "contentEpisodeTitle": "2화",
    "episodeNo": 2,
    "genre": "무협",
    "link": "https://treasurecomics.com/gateway/common?returnUrl=https%3A%2F%2F.treasurecomics.com%2Fcontent%2Flist%2Fcn2b641081a4",
    "returnUrl": "https://treasurecomics.com/content/list/cn2b641081a4",
    "isWaitFree": false,
    "freeEpisode": 25
  },
  {
    "title": "열애, 해줘요",
    "description": "구애보다 열애가 하고 싶은 ‘10년 짝사랑녀’ 구열애, ‘최강 츤데레남’ 최강국을 낚을 수 있을까?",
    "thumbnail": "https://s.treasurecomics.com/images/prod/webtoon/cw5fbc01c678/posterThumbnail_1738590019.jpg",
    "contentType": "웹툰",
    "contentCName": "cw5fbc01c678",
    "contentEpisodeTitle": "2화",
    "episodeNo": 2,
    "genre": "로맨스",
    "link": "https://treasurecomics.com/gateway/common?returnUrl=https%3A%2F%treasurecomics.com%2Fcontent%2Flist%2Fcw5fbc01c678",
    "returnUrl": "https://treasurecomics.com/content/list/cw5fbc01c678",
    "isWaitFree": true,
    "waitFreeInfo": {
      "chargedTicket": true,
      "baseDate": "2025-04-20T07:58:46.847Z",
      "chargedDate": "2025-04-20T07:58:46.847Z"
    },
    "freeEpisode": 3
  },
  {
    "title": "사모님은 챔피언",
    "description": "1년안에 남자 꼬시기 vs 격투 여왕! 난 둘 다 해야지!",
    "thumbnail": "https://s.treasurecomics.com/images/prod/webtoon/cw4fb3561bdd/posterThumbnail_1741847040.jpg",
    "contentType": "웹툰",
    "contentCName": "cw4fb3561bdd",
    "contentEpisodeTitle": "2화",
    "episodeNo": 2,
    "genre": "로맨스",
    "link": "https://treasurecomics.com/gateway/common?returnUrl=https%3A%2F%treasurecomics.com%2Fcontent%2Flist%2Fcw4fb3561bdd",
    "returnUrl": "https://treasurecomics.com/content/list/cw4fb3561bdd",
    "isWaitFree": true,
    "waitFreeInfo": {
      "chargedTicket": true,
      "baseDate": "2025-04-20T07:58:43.325Z",
      "chargedDate": "2025-04-20T07:58:43.325Z"
    },
    "freeEpisode": 14
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

## 이미지 캐싱

{% hint style="info" %}
**앱 성능 향상**, **네트워크 절약**, **사용자 경험 개선을 위해 "thumbnail", "subThumbnail" 항목에 대해 이미지 캐싱 처리를 권장하고 있습니다.**

***

### <mark style="color:red;">보물섬은 이미지 변경시 이미지 URL이 변경됩니다. URL을 기준으로 캐싱 정책을 구성 하기기 바랍니다.</mark>
{% endhint %}

### ✅ 1. **빠른 이미지 로딩 (퍼포먼스 향상)**

이미지를 네트워크에서 매번 불러오면 로딩 시간이 길어지고 UI가 느려질 수 있습니다.\
→ 캐시에 저장해두면 디스크나 메모리에서 **즉시 로딩** 가능

***

### ✅ 2. **네트워크 트래픽 절약**

같은 이미지를 여러 번 다운로드하면 사용자 데이터 요금이 낭비되고, 서버 비용도 증가합니다.\
→ 캐싱은 **중복 다운로드 방지**에 효과적입니다.

***

### ✅ 3. **오프라인 지원**

인터넷이 없는 환경에서도 이미 본 이미지는 캐시에서 로드 가능\
→ 뉴스 앱, 쇼핑 앱, 갤러리 앱 등에 매우 유용

***

### ✅ 4. **배터리 사용 최적화**

불필요한 네트워크 요청은 CPU와 무선 칩을 많이 사용하게 되어 배터리 소모가 큽니다.\
→ 캐시는 **배터리 절약**에도 도움이 됩니다.

***

### ✅ 5. **UX(사용자 경험) 개선**

* 이미지가 **깜빡이지 않고** 부드럽게 뜹니다.
* 리스트 스크롤 시 **끊김 없이 로딩**됩니다.
* 사용자가 **앱이 빠르다고 느끼는** 중요한 포인트입니다.

### ✅ 6. 캐싱 처리 예시

* Android
  * [Glide](https://bumptech.github.io/glide/doc/caching.html)
  * [Coil](https://coil-kt.github.io/coil/image_loaders/#caching)
  * [Picasso](https://square.github.io/picasso/) (Automatic memory and disk caching.)
* iOS
  * [KingFisher](https://swiftpackageindex.com/onevcat/kingfisher/master/documentation/kingfisher/commontasks_cache)
  * [SDWebImages](https://github.com/SDWebImage/SDWebImageSwiftUI?tab=readme-ov-file#customization-and-configuration-setup)



## 최근 본 작품 조회 구현 예시 화면

<div align="left"><figure><img src="../../../.gitbook/assets/bms_recently.png" alt="" width="375"><figcaption></figcaption></figure></div>










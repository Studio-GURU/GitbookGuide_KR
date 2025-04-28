---
description: 보물섬의 인기 컨텐츠를 조회하는 API 입니다.
icon: arrow-trend-up
---

# \[ API ] 인기 작품 조회 ( Client )

## Version

버전 정보는 URL 경로에 표현하지 않으며, 헤더의 accept-version 속성 값에 정의합니다.

| Version | Date       | Description |
| ------- | ---------- | ----------- |
| 1.0.0   | 2025.03.19 | Create      |

## Recent View Contents

```
테스트
GET https://api-test.treasurecomics.com/external/open/{channel}/top?sign={value}&contentType={value}

라이브
GET https://api.treasurecomics.com/external/open/{channel}/top?sign={value}&contentType={value}
```

**✓ 인기 컨텐츠를 조회합니다.**

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

<table data-full-width="false"><thead><tr><th width="148.27734375">Name</th><th width="141">Type</th><th width="127">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>sign</code></td><td>string</td><td>true</td><td><a data-mention href="../../sign.md">sign.md</a></td></tr><tr><td><code>contentType</code></td><td>string</td><td>false</td><td>빈 값을 보내면 모든 유형의 종합 콘텐츠 순위 리스트가 반환되며, 특정 값을 입력하면 해당 유형에 맞는 인기 콘텐츠가 반환됩니다.<br><br>webtoon: 웹툰<br>novel: 웹소설</td></tr></tbody></table>

```
// get usage example
https://api-{env}.treasurecomics.com/external/open/{channel}/recentView?sign=1724328195.3da08653e6c1420aac89eecdf5c20063.OGMzYjUzYTUyYjE1YTJiNDAyZGM3MGJiZmMzMDI2YWE1NDg0YWY2ZTdjNjMyZTJlMTdjMjQyOGU1NjZhYjdhYQ
```

### **Response**

<table><thead><tr><th width="270">Fields</th><th width="106">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>title</code></td><td>string</td><td>제목</td></tr><tr><td><code>description</code></td><td>string</td><td>내용</td></tr><tr><td><code>thumbnail</code></td><td>string</td><td>이미지 경로</td></tr><tr><td><code>contentType</code></td><td>string</td><td>웹툰 | 웹소설</td></tr><tr><td><code>contentCName</code></td><td>string</td><td>작품 키</td></tr><tr><td><code>genre</code></td><td>string</td><td>장르</td></tr><tr><td><code>link</code></td><td>string</td><td><p>제공되는 링크 뒤에 sign 붙여서 전달</p><p>예)<code>&#x26;sign=1724328195.3da08653e6c1420aac89eecdf5c20063.OGMzYjUzYTUyYjE1YTJiNDAyZGM3MGJiZmMzMDI2YWE1NDg0YWY2ZTdjNjMyZTJlMTdjMjQyOGU1NjZhYjdhYQ</code></p></td></tr><tr><td><code>returnUrl</code></td><td>string</td><td>최종 이동 링크 ( 참고용 )</td></tr><tr><td><code>isWaitFree</code></td><td>boolean</td><td>기다리면 무료 작품 여부</td></tr><tr><td><code>freeEpisode</code></td><td>number</td><td>무료 회차 수</td></tr></tbody></table>

**Response Code**

{% tabs %}
{% tab title="200" %}
{% code lineNumbers="true" %}
```json
[
  {
    "title": "로또 1등으로 대기업 스타",
    "description": "로또 1등으로 시작된 여유로운 방송 생활.\n여유가 시청자 3명짜리 방송에서 대기업 방송으로 성공시킨다.\n로또1등으로 대기업스타!\n",
    "thumbnail": "https://s.treasurecomics.com/images/test/novel/cn321a5434b3/posterThumbnail_1723511207.jpg",
    "contentType": "웹소설",
    "contentCName": "cn321a5434b3",
    "genre": "현대판타지",
    "link": "https://bitbunny-test.treasurecomics.com/gateway/common?returnUrl=https%3A%2F%2Fbitbunny-test.treasurecomics.com%2Fcontent%2Flist%2Fcn321a5434b3",
    "returnUrl": "https://bitbunny-test.treasurecomics.com/content/list/cn321a5434b3",
    "isWaitFree": false,
    "freeEpisode": 25
  },
  {
    "title": "내 인생에서 사라져 주세요",
    "description": "공작가의 막내딸 리네아는\n태어날 때부터 정령의 목소리를 들었다.\n그저 남들과 조금 다를 뿐이었지만,\n가족에게 사랑받지 못하고 외롭게 자란다.\n\n그런 리네아의 마음의 안식처는\n유일하게 자신의 말을 믿어 주고 지지해 준 약혼자뿐.\n그러나 그 약혼자는 그녀를 배신하고 다른 여자와 놀아난다.\n\n리네아는 큰 충격을 받고\n모든 것으로부터 벗어나 죽음으로 자유를 찾았다.\n\n그 후 눈을 떠 보니 2년 전.\n\n돌아온 시간,다시 얻은 기회.\n그걸 놓치지 않고 이제는 혼자 힘으로 살아 보려던 그때,\n어릴 적에 잠깐 봤을 뿐인 젊은 황제 유릭이 그녀에게 관심을 보인다?\n\n“네 행복이 나와 상관없었던 적은 한 번도 없었어.”\n“나와 결혼해 줄 수 있겠나?”\n\n이제 결혼 안 한다니까 나한테 왜 이래!\n모든 걸 포기하고 돌아오자 거짓말처럼 찾아온 설레임.\n리네아는 과연 행복해질 수 있을까?",
    "thumbnail": "https://s.treasurecomics.com/images/test/novel/cnc0e5f2fa7a/posterThumbnail_1723080834.jpg",
    "contentType": "웹소설",
    "contentCName": "cnc0e5f2fa7a",
    "genre": "로맨스판타지",
    "link": "https://bitbunny-test.treasurecomics.com/gateway/common?returnUrl=https%3A%2F%2Fbitbunny-test.treasurecomics.com%2Fcontent%2Flist%2Fcnc0e5f2fa7a",
    "returnUrl": "https://bitbunny-test.treasurecomics.com/content/list/cnc0e5f2fa7a",
    "isWaitFree": true,
    "freeEpisode": 5
  },
  {
    "title": "간지날수록 강해져",
    "description": "추악한 외모로 외모지상주의를 살아가는 이혁.\n믿었던 여자에게까지 버림받는 비참한 신세가 되어 자살을 결심하는데..\n죽음의 순간, 하나의 메시지가 도착한다. \n그에게만 보이는 힘, 간지와 이제까진 없었던 스탯의 등장.\n멋있어져라 아름다워져라 그렇다면 강해질 것이니.\n간지남 이혁의 이야기",
    "thumbnail": "https://s.treasurecomics.com/images/test/novel/cn3fd087adaf/posterThumbnail_1723105026.jpg",
    "contentType": "웹소설",
    "contentCName": "cn3fd087adaf",
    "genre": "판타지",
    "link": "https://bitbunny-test.treasurecomics.com/gateway/common?returnUrl=https%3A%2F%2Fbitbunny-test.treasurecomics.com%2Fcontent%2Flist%2Fcn3fd087adaf",
    "returnUrl": "https://bitbunny-test.treasurecomics.com/content/list/cn3fd087adaf",
    "isWaitFree": false,
    "freeEpisode": 25
  },
  {
    "title": "1941 타임슬립 대전략",
    "description": "1941년으로 타임슬립한 대한민국.\n\n2차 세계대전은 이미 진행 중이다.\n\n세계를 바꿔보자.",
    "thumbnail": "https://s.treasurecomics.com/images/test/novel/cn22f86bd1ba/posterThumbnail_1723184863.jpg",
    "contentType": "웹소설",
    "contentCName": "cn22f86bd1ba",
    "genre": "대체역사",
    "link": "https://bitbunny-test.treasurecomics.com/gateway/common?returnUrl=https%3A%2F%2Fbitbunny-test.treasurecomics.com%2Fcontent%2Flist%2Fcn22f86bd1ba",
    "returnUrl": "https://bitbunny-test.treasurecomics.com/content/list/cn22f86bd1ba",
    "isWaitFree": false,
    "freeEpisode": 25
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

## 인기 컨텐츠 구현 예시



<figure><img src="../../../.gitbook/assets/KakaoTalk_Photo_2025-03-19-14-56-11 (1).jpeg" alt=""><figcaption></figcaption></figure>






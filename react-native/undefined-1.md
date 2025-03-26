---
description: 사용자가 최근 본 작품을 조회하는 API 로 채널회원이 연동되어 있는 방식에서만 동작합니다.
icon: list
---

# 최근 본 작품 조회

## API

{% code lineNumbers="true" %}
```typescript
const comicsRecentContent = async (
    signature: string
): Promise<Array<RecentContentData>>
```
{% endcode %}

<table><thead><tr><th width="146">Name</th><th width="143">Type</th><th width="118">Required</th><th>Description</th></tr></thead><tbody><tr><td>signature</td><td>string</td><td><mark style="color:red;">required</mark></td><td><a data-mention href="../android-sdk/sign.md">sign.md</a></td></tr></tbody></table>

***

## Response(RecentContentData)

<table><thead><tr><th width="270">Fields</th><th width="106">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>title</code></td><td>string</td><td>제목</td></tr><tr><td><code>description</code></td><td>string</td><td>내용</td></tr><tr><td><code>thumbnail</code></td><td>string</td><td>이미지 경로</td></tr><tr><td><code>contentType</code></td><td>string</td><td>웹툰 | 웹소설</td></tr><tr><td><code>contentCName</code></td><td>string</td><td>작품 키</td></tr><tr><td><code>contentEpisodeTitle</code></td><td>string</td><td>마지막으로 본 에피소드 제목</td></tr><tr><td><code>episodeNo</code></td><td>number</td><td>마지막으로 본 에피소드 회차</td></tr><tr><td><code>genre</code></td><td>string</td><td>장르</td></tr><tr><td><code>link</code></td><td>string</td><td><p>제공되는 링크 뒤에 sign 붙여서 전달</p><p>예)<code>&#x26;sign=1724328195.3da08653e6c1420aac89eecdf5c20063.OGMzYjUzYTUyYjE1YTJiNDAyZGM3MGJiZmMzMDI2YWE1NDg0YWY2ZTdjNjMyZTJlMTdjMjQyOGU1NjZhYjdhYQ</code></p></td></tr><tr><td><code>returnUrl</code></td><td>string</td><td>최종 이동 링크 ( 참고용 )</td></tr><tr><td><code>isWaitFree</code></td><td>boolean</td><td>기다리면 무료 작품 여부</td></tr><tr><td><code>waitFreeInfo(optional)</code></td><td>object</td><td>기다리면 무료 티켓 정보</td></tr><tr><td></td><td></td><td><p><code>{</code><br>  <code>chargedTicket: boolean,</code><br>  <code>baseDate: Date,</code><br>  <code>chargedDate: Date</code><br><code>}</code></p><ul><li><mark style="background-color:purple;">chargedTicket: 기다리면 무료 티켓 소지 여부</mark></li><li><mark style="background-color:purple;">baseDate: 티켓 계산 기준 날짜</mark></li><li><mark style="background-color:purple;">chargeDate: 티켓 충전 날짜</mark></li></ul></td></tr><tr><td><code>freeEpisode</code></td><td>number</td><td>무료 회차 수</td></tr></tbody></table>

***

## Usage

{% code lineNumbers="true" %}
```typescript
import {
  RecentContentData,
  comicsRecentContent
} from 'react-treasureislandx-addon'

comicsRecentContent(${signKey})
  .then((result: Array<RecentContentData>) => {
    console.log(`comicsRecentContent::success => ${result.toString()}`);
  })
  .catch((error: any) => { 
    console.error('comicsRecentContent::failed:', error.message)
  });
```
{% endcode %}








---
icon: user-group
description: 식보물섬 채널링 서비스 연동을 위한 방법을 안내합니다.
---

# 채널회원 연동 방식

{% hint style="info" %}
메인화면 진입 하기

***

<mark style="color:red;">**✓**</mark>  <mark style="color:red;">**기존 화면이 아닌 새로운 창을 통해 보물섬을 실행하세요 !**</mark>

✓ 메인 화면 진입 경로에 <mark style="color:red;">**sign parameter**</mark>를 전달하여 보물섬 메인화면에 진입합니다.
{% endhint %}

## 보물섬 URL 호출

```
메인화면
https://{channel}.treasurecomics.com/gateway/common?sign={sign-value}&returnUrl=https://{channel}.treasurecomics.com/main

오늘의추천
https://{channel}.treasurecomics.com/gateway/common?sign={sign-value}&returnUrl=https://{channel}.treasurecomics.com/recommandtion/{channel}
```

**✓** **returnUrl 은 UrlEncode된 값으로 전달 합니다.**

**✓** `{channel}` 값은 **별도 전달** 됩니다.

### **signature 생성 하기**

{% hint style="info" %}
**signature 생성 (**<mark style="color:red;">**HmacSHA256 생성에 필요한 Key는 별도 전달 됩니다.**</mark>**)**

***

<mark style="color:red;">**{} 표현은 변수 입니다 ({}값이 포함되지 않도록 주의 바랍니다.)**</mark>

**{timeStamp}{nonce}{userID}**

위 값을 HmacSHA256 Hash → Base64 Url Encoding을 통해 Signature를 생성합니다.

***

* timeStamp → unix timestamp seconds
* nonce → 문자열 32자(임의로 생성된 문자열 32자)
* userID → 채널사에서 사용되는 유저식별자\
  1\) 포인트 지급기능 등을 추가 연동할 때 보물섬서비스에서 채널사에 전달할 시에도 사용 될 수 있음과 \
  2\) 채널사의 유저식별자 전달에 따른 보안정책기준을 고려하여 (암호화안함/대칭형암호화/비대칭형암호화) 유저식별자 전달

***

nonce 값은 signature 생성 시 매번 새로운 값을 생성하여 입력이 필요합니다.
{% endhint %}

<table data-full-width="false"><thead><tr><th width="116">Name</th><th width="141">Type</th><th width="127">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>sign</code></td><td>string</td><td>true</td><td><p><code>timestamp.nonce.userID.signature</code></p><hr><p><mark style="background-color:red;">timestamp, nonce, userID, signature 4가지 값을 순서대로 구분자 .(full stop)을 붙여 sign 값을 생성합니다.</mark></p><hr><p><mark style="background-color:yellow;">sign값은 보안상 채널사의 서버에서 생성하며 보물섬에서는 sign 값이 1)사용된것인지 2)생성한지 5분이 지난 값인지 확인하여 유효하지 않음으로 판단할 수 있음으로 사용자의 액션이 있을 시 마다 즉시 생성하여 호출하도록 개발합니다.</mark></p></td></tr><tr><td>adid</td><td>string</td><td>false</td><td>광고식별값 : android ADID / iOS IDFA</td></tr><tr><td>gender</td><td>number</td><td>false</td><td>성별 : 1=남자 / 2=여자</td></tr><tr><td>age</td><td>number</td><td>false</td><td>나이</td></tr><tr><td>isAdult</td><td>number</td><td>false</td><td>성인여부: 0=성인아님 / 1=성인</td></tr></tbody></table>

### 사용 예

```
https://test.treasurecomics.com/gateway/common?sign=1724922215.7b82817d9487471a8a782c2604883924.lymanTest.M21MZORoc4NbVzq1ZaSC8LgcOKYH9SBIljHYjVOfX5o%3D&returnUrl=https%3A%2F%2Ftest.treasurecomics.com%2Fmain
```














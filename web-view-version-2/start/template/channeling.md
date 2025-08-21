---
description: 보물섬 채널링 서비스 연동을 위한 방법을 안내합니다.
icon: user-group
---

# 채널회원 연동 방식

***

{% hint style="info" %}
보물섬 연동

***

✓ 파트너사의 회원 정보를 사용하여 로그인합니다.
{% endhint %}

## WebView에 보물섬 URL 호출



**Live 대역**

```
메인화면
https://{channel}.treasurecomics.com/gateway/common?sign={sign-value}&returnUrl=https://{channel}.treasurecomics.com/main

오늘의 추천
https://{channel}.treasurecomics.com/gateway/common?sign={sign-value}&returnUrl=https://{channel}.treasurecomics.com/recommendation/{channel}

오늘 뭐볼까
https://{channel}.treasurecomics.com/gateway/common?sign={sign-value}&returnUrl=https://{channel}.treasurecomics.com/today-feed
```

**Test 대역**

```
메인화면
https://{channel}-test.treasurecomics.com/gateway/common?sign={sign-value}&returnUrl=https://{channel}-test.treasurecomics.com/main

오늘의 추천
https://{channel}-test.treasurecomics.com/gateway/common?sign={sign-value}&returnUrl=https://{channel}-test.treasurecomics.com/recommendation/{channel}

오늘 뭐볼까
https://{channel}-test.treasurecomics.com/gateway/common?sign={sign-value}&returnUrl=https://{channel}-test.treasurecomics.com/today-feed
```

**✓** **returnUrl 은 UrlEncode된 값으로 전달 합니다.**

**✓ `sign` 외의 추가 정보 전달이 필요할 경우 아래 표의 값을 추가로 넘겨주시면 됩니다.**

**✓** `{channel}` 값은 **별도 전달** 됩니다.



<table data-full-width="false"><thead><tr><th width="116">Name</th><th width="141">Type</th><th width="127">Required</th><th>Description</th></tr></thead><tbody><tr><td>sign</td><td>string</td><td>true</td><td><a data-mention href="../../../web-view/sign.md">sign.md</a></td></tr><tr><td>isAdult</td><td>number</td><td>false</td><td><p>성인여부</p><p>0 : 성인 X</p><p>1 : 성인</p></td></tr></tbody></table>

### 사용 예시

```
https://test.treasurecomics.com/gateway/common?sign=1724922215.7b82817d9487471a8a782c2604883924.lymanTest.M21MZORoc4NbVzq1ZaSC8LgcOKYH9SBIljHYjVOfX5o%3D&returnUrl=https%3A%2F%2Ftest.treasurecomics.com%2Fmain
```










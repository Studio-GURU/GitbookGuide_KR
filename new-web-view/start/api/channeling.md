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



### **커스텀 연동**

```
EX ) 추천 컨텐츠
https://{channel}.treasurecomics.com/gateway/common?sign={sign-value}&returnUrl=https://{channel}.treasurecomics.com/recommandtion/{channel}
```

**✓** **API를 통해 받은 링크에 `sign` 파라미터를 추가해 주시면 됩니다.**

**✓ `sign` 외의 추가 정보 전달이 필요할 경우 아래 표의 값을 추가로 넘겨주시면 됩니다.**



<table data-full-width="false"><thead><tr><th width="116">Name</th><th width="141">Type</th><th width="127">Required</th><th>Description</th></tr></thead><tbody><tr><td>sign</td><td>string</td><td>true</td><td><a data-mention href="../../sign.md">sign.md</a></td></tr><tr><td>adid</td><td>string</td><td>false</td><td><p>광고 식별 ID </p><p>AOS : ADID값 전달<br>IOS : IDFA값 전달</p></td></tr><tr><td>gender</td><td>number</td><td>false</td><td><p>성별 </p><p>1 : 남자</p><p>2 : 여자</p></td></tr><tr><td>age</td><td>number</td><td>false</td><td>나이</td></tr><tr><td>isAdult</td><td>number</td><td>false</td><td><p>성인여부</p><p>0 : 성인 X</p><p>1 : 성인</p></td></tr></tbody></table>

### 사용 예시

```
https://test.treasurecomics.com/gateway/common?sign=1724922215.7b82817d9487471a8a782c2604883924.lymanTest.M21MZORoc4NbVzq1ZaSC8LgcOKYH9SBIljHYjVOfX5o%3D&returnUrl=https%3A%2F%2Ftest.treasurecomics.com%2Fmain
```

***

## 사이트 이동 토스트 표시

**✓ App 내에서 \[ 웹툰 사이트로 이동했다 ] 라는 안내 토스트를 사용자에게 노출합니다.**\
EX ) "웹툰 사이트로 이동했어요"

<figure><img src="../../../.gitbook/assets/Simulator Screenshot - iPhone 16 Pro - 2024-10-25 at 14.08.11.png" alt=""><figcaption><p>안내 메시지 노출 예시 화면</p></figcaption></figure>

***












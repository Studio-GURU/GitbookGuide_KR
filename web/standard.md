---
icon: user
description: 보물섬 서비스 연동을 위한 방법을 안내합니다.
---

# 채널회원 미연동 방식

{% hint style="info" %}
보물섬 연동

***

✓ 파트너사의 회원 정보를 사용하지 않습니다.

✓ 보물섬의 별도 회원 정책을 사용합니다.

<mark style="color:red;">**✓**</mark>  <mark style="color:red;">**기존 화면이 아닌 새로운 창을 통해 보물섬을 실행하세요 !**</mark>
{% endhint %}

## 웹뷰에 보물섬 URL 호출

**✓ 웹뷰(인앱 브라우져)에 아래의 주소를 호출합니다.**

```
메인화면
https://{channel}.treasurecomics.com/

오늘의추천
https://{channel}.treasurecomics.com/recommendation/{channel}
```

**✓** `{channel}` 값은 **별도 전달** 됩니다.

## 사이트이동 토스트 표시

**✓ 앱내에서 웹툰 웹사이트로 이동했다라는 안내 토스트를 사용자에게 노출합니다.**\
예) "웹툰 사이트로 이동했어요"

***

<figure><img src="../.gitbook/assets/Simulator Screenshot - iPhone 16 Pro - 2024-10-25 at 14.08.11.png" alt=""><figcaption><p>안내 메시지 노출 예시 화면</p></figcaption></figure>

***






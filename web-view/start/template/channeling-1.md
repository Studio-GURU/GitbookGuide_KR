---
description: 보물섬 채널링 서비스 연동을 위한 방법을 안내합니다.
hidden: true
icon: user-group
---

# 오락 채널회원 연동 방식(브릿지-아웃브라우징)



***

{% hint style="info" %}
보물섬 연동

***

✓ 파트너사의 회원 정보를 사용하여 로그인합니다.
{% endhint %}

## WebView에 보물섬 브릿지 URL 호출

**Live 대역**

```
오늘 뭐볼까 ( 상시 운영되는 프로모션 페이지 )
https://olock.treasurecomics.com/gateway/olock?userId={user-id-value}&token={authentication-token}
```

**Test 대역**

```
오늘 뭐볼까 ( 상시 운영되는 프로모션 페이지 )
https://olock-test.treasurecomics.com/gateway/olock?userId={user-id-value}&token={authentication-token}
```








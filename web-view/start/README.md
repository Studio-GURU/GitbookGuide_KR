---
description: 보물섬에서 제공하는 서비스를 인앱 브라우저를 통해 연동시 필요한 설정에 대해 알아 보세요.
icon: star-shooting
---

# 시작하기

***

## 시작하기

각 OS에서 제공하는 In-App WebView(WebView, WKWebView)를 사용하여 필요한 API를 호출한 후, 생성된 URL을 로드합니다. WebView의 추가 구성에 대한 자세한 내용은 옵션으로 제공되는 가이드를 참고해 주세요.

***

## 연동 방식

템플릿 적립과 API 적립 **두 가지 방법 중 하나를 선택**하여, 하단 [연동 가이드](./#undefined-3)를 참고해 주세요.

### &#x20;  **템플릿 연동**

<img src="../../.gitbook/assets/KakaoTalk_Photo_2025-02-28-16-31-17 001.jpeg" alt="" data-size="original">



보물섬에서 제공하는 **기본 연동 메인 웹페이지**로 웹뷰로 로드하여 사용합니다.\
**빠르고 간편하게 적용**할 수 있습니다.



### &#x20; **커스텀 연동 (API 연동)**

![](<../../.gitbook/assets/KakaoTalk_Photo_2025-02-28-16-31-18 002.jpeg>)

API를 통해 보물섬의 추천 컨텐츠를 조회하여 **자체 UI ( 네이티브 혹은 웹페이지 )** 에 원하시는 형태로 적용 할 수 있습니다.\
기존 App의 디자인 및 기능처럼 **일관된 경험 제공**이 가능합니다.

***

## 연동 가이드

* 원하는 연동 방식에 맞춰, 아래의 가이드를 확인해주세요 !

{% content-ref url="template/" %}
[template](template/)
{% endcontent-ref %}

{% content-ref url="api/" %}
[api](api/)
{% endcontent-ref %}

***

## 권장사항

{% hint style="info" %}
권장 사항은 최신 보물섬 API를 기준으로 명시하였습니다.

***

OS와의 호환성을 위하여 명시된 플랫폼의 요구사항을 확인 바랍니다.

보물섬이 원활하게 작동하기 위한 최소한의 사항입니다.
{% endhint %}

### ANDROID

✓ Android 5.0(API Level 21) 이상을 권장합니다.

✓ Google Play 타겟 API 수준 -> Compile SDK Version 34(:link:[Google Play의 대상 API 수준 요구사항 충족](https://developer.android.com/google/play/requirements/target-sdk?hl=ko))

***

### iOS

✓  iOS 15 이상의 버전을 권장합니다.








---
description: 보물섬에서 제공하는 서비스를 인앱 브라우저를 통해 연동시 필요한 설정에 대해 알아 보세요.
icon: star-shooting
---

# 시작하기

***

## 시작하기

각 OS에서 제공하는 In-App WebView(WebView, WKWebView)를 사용하여 필요한 API를 호출한 후, 생성된 URL을 로드합니다. WebView의 추가 구성에 대한 자세한 내용은 옵션으로 제공되는 가이드를 참고해 주세요.



## 템플릿 연동

* 보물섬에서 제공하는 기본 템플릿을 사용하여 구성된 첫 화면을 사용합니다.
* 빠르고 간편하게 적용할 수 있습니다.
* 아래 가이드에 따라 연동을 진행해주세요.

{% content-ref url="../webview-config.md" %}
[webview-config.md](../webview-config.md)
{% endcontent-ref %}

{% content-ref url="../channeling.md" %}
[channeling.md](../channeling.md)
{% endcontent-ref %}

{% content-ref url="../standard.md" %}
[standard.md](../standard.md)
{% endcontent-ref %}

{% content-ref url="../javascriptinterface.md" %}
[javascriptinterface.md](../javascriptinterface.md)
{% endcontent-ref %}



## 커스텀 연동 ( API 연동 )

* API를 통해 보물섬의 추천 컨텐츠를 조회하여 자체 UI에 맞게 구성합니다.
* 기존 App의 디자인 및 기능처럼 일관된 경험 제공이 가능합니다.
* 아래 가이드에 따라 연동을 진행해주세요.

{% content-ref url="../channeling.md" %}
[channeling.md](../channeling.md)
{% endcontent-ref %}

{% content-ref url="../standard.md" %}
[standard.md](../standard.md)
{% endcontent-ref %}

{% content-ref url="../recommendation.md" %}
[recommendation.md](../recommendation.md)
{% endcontent-ref %}

{% content-ref url="../recently.md" %}
[recently.md](../recently.md)
{% endcontent-ref %}



## 권장사항

{% hint style="info" %}
권장 사항은 최신 보물섬 API를 기준으로 명시하였습니다.

***

OS와의 호환성을 위하여 명시된 플랫폼의 요구사항을 확인 바랍니다.
{% endhint %}

### ANDROID

✓ Android 5.0(API Level 21) 이상을 권장합니다.

✓ Android Studio -> 3.2 이상 (최신 버전의 IDE 사용을 권장합니다.)

✓ Android gradle plugin -> 4.0.1 이상

✓ Google Play 타겟 API 수준 -> Compile SDK Version 34(:link:[Google Play의 대상 API 수준 요구사항 충족](https://developer.android.com/google/play/requirements/target-sdk?hl=ko))

✓ Kotlin version 1.8.X 이상의 버전 권장 (개발 설정 1.9.0)

✓ Support AndroidX

***

### iOS

✓  iOS 15 이상의 버전을 권장합니다.








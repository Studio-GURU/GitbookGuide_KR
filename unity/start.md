---
icon: star-shooting
description: 보물섬 Unity-Package에서 제공하는 서비스를 연동하기 전 완료해야 하는 설정에 대해 알아보세요.
---

# 시작하기

## 연동 순서

1. 요구 사항을 확인 합니다.
2. 연동키를 발급 받습니다.
3. 기본 모듈 적용&#x20;
4. 플랫폼별 설정
   1. Android 원격 저장소 설정
   2. Pod Install & Privacy - Tracking Usage Description

***

## 요구사항

{% hint style="success" %}
요구 사양은 보물섬 Unity Package 최신 상태를 기준으로 명시 됩니다.

***

OS와의 호환성을 위해 최신 버전으로 업데이트하는 것을 권장합니다.
{% endhint %}

### Android

:heavy\_check\_mark: Android 5.0(API Level 21) 이상을 권장합니다.

:heavy\_check\_mark: Android gradle plugin -> 4.0.1 이상

:heavy\_check\_mark:️ Google Play 타겟 API 수준 -> Compile SDK Version 34(🔗[Google Play의 대상 API 수준 요구사항 충족](https://developer.android.com/google/play/requirements/target-sdk?hl=ko))

:heavy\_check\_mark:️ Kotlin version 1.8.X 이상의 버전 권장 (개발 설정 1.9.0)

:heavy\_check\_mark:️ Support AndroidX

### iOS

:heavy\_check\_mark:️ iOS 15 이상을 권장합니다.

:heavy\_check\_mark:️ Swift 5 이상의 버전을 권장합니다.

:heavy\_check\_mark:️ 최신 버전의 XCode 사용 권장 (개발 기준 15.4 버전 사용)

***

### 연동키 발급 <a href="#undefined-2" id="undefined-2"></a>

{% hint style="info" %}
보물섬 **Unity-Package**를 연동하려면 연동하려는 앱의 고유 식별자가(AppId/AppSecret) 필요하며 영업 담당자를 통해 발급 전달 됩니다.
{% endhint %}

| AppID     | 앱 고유 식별자     |
| --------- | ------------ |
| AppSecret | 앱 고유 식별자 검증키 |

***

## 기본 모듈 적용

### UnityPackage Download

```
wget https://dl.cloudsmith.io/public/studio-guru/treasureisland-unity/raw/versions/null/TreasureIslnad-Unity-Plugin-1.0.0.unitypackage
```

***

### UnityPackage Import

다운로드 받은 Package 파일을 "Assets > Import Package > Custom Package..." 메뉴를 통해 불러 옵니다.

<div align="left"><figure><img src="../.gitbook/assets/스크린샷 2025-01-22 오후 7.49.21.png" alt=""><figcaption></figcaption></figure></div>






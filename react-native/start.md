---
icon: star-shooting
description: 보물섬 ReactNative PlugIn에서 제공하는 서비스를 연동하기 전 완료해야 하는 설정에 대해 알아보세요.
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
요구 사양은 보물섬 ReactNative PlugIn 최신 상태를 기준으로 명시 됩니다.

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
보물섬 **ReactNative PlugIn**을 연동하려면 연동하려는 앱의 고유 식별자가(AppId/AppSecret) 필요하며 영업 담당자를 통해 발급 전달 됩니다.
{% endhint %}

| AppID     | 앱 고유 식별자     |
| --------- | ------------ |
| AppSecret | 앱 고유 식별자 검증키 |
|           |              |

***

## 기본 모듈 적용

```sh
# yarn
# yarn 저장소 등록
$ yarn config set registry https://npm.cloudsmith.io/studio-guru/treasureisland-reactnative/
# yarn 모둘 추가
$ yarn add react-treasureisland-addon@version

# npm
# npm 저장소 등록
$ npm config set registry https://npm.cloudsmith.io/studio-guru/treasureisland-reactnative/
# npm 모둘 추가
$ npm install react-treasureisland-addon@version
```

패키지가 설치되면 node\_module 폴더에 저장이 되며, package.json에 추가됩니다.

```json
"dependencies": {
    ....
    code
    ....
    "react-treasureisland-addon": ".."
  },
```

***

## Android 원격 저장소 설정

**보물섬은** 🔗[**Cloud-Smith**](https://cloudsmith.com/company/about) **서비스를 이용하여 ANDROID SDK를 제공하며, 해당 서비스의 저장소 설정이 필요합니다.**

{% tabs %}
{% tab title="setting.gradle" %}
**AGP 7.1.0 이상 또는 Android Studio Bumblebee 이상 사용시**

{% code title="settings.gradle" lineNumbers="true" %}
```gradle
pluginManagement {
  repositories {
    google()
    mavenCentral()
    gradlePluginPortal()
  }
}
dependencyResolutionManagement {
  repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
  repositories {
    google()
    mavenCentral()
    maven {
      url "https://dl.cloudsmith.io/public/studio-guru/treasureisland-android/maven/"
    }
  }
}
```
{% endcode %}

{% code title="settings.gradle.kts" lineNumbers="true" %}
```gradle
pluginManagement {
  repositories {
    google()
    mavenCentral()
    gradlePluginPortal()
  }
}
dependencyResolutionManagement {
  repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
  repositories {
    google()
    mavenCentral()
    maven {
      url = uri("https://dl.cloudsmith.io/public/studio-guru/treasureisland-android/maven/")
    }
  }
}
```
{% endcode %}
{% endtab %}

{% tab title="build.gradle" %}
**프로젝트 수준의 "build.gradle" 파일에 다음 항목을 추가 합니다.**

```
// build.gradle(project)
allprojects {
  repositories {
    google()
    mavenCentral()
    maven {
      url "https://dl.cloudsmith.io/public/studio-guru/treasureisland-android/maven/"
    }
  }
}
```
{% endtab %}
{% endtabs %}

<figure><img src="../.gitbook/assets/스크린샷 2024-12-16 오전 11.41.51.png" alt=""><figcaption></figcaption></figure>

***

## iOS

**패키지 설치 후 "pod install" 명령어를 통해 의존성을 추가 합니다.**

```sh
$ pod install
```

### IDFA 사용동의 설정

보물섬 SDK는 개인 맞춤 광고를 제공하기 위해 사용자 식별 정보(IDFA(ADID))를 확인 합니다.

**info.plist** 또는 **TARGETS -> Info -> Custom iOS Target Properties** 값을 업데이트 합니다.

<table><thead><tr><th width="319">Key</th><th>Value</th></tr></thead><tbody><tr><td>Privacy - Tracking Usage Description<br>NSUserTrackingUsageDescription</td><td>개인 맞춤 광고를 제공하기 위해 사용자 식별 정보를 사용합니다.</td></tr></tbody></table>

<figure><img src="../.gitbook/assets/apple_idfa_01.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/apple_idfa_02.png" alt=""><figcaption></figcaption></figure>

***

### iOS ATS(App Transport Security) 정책 설정

일부 광고 제공 업체 또는 개발 모드의 경우 https를 제공하지 않는 경우로 안헤 ATS 설정이 필요합니다.

<table><thead><tr><th width="321">Key</th><th width="276">Sub Key</th><th>Value</th></tr></thead><tbody><tr><td>App Transport Security Setting</td><td>Allow Arbitrary Loads</td><td>YES</td></tr></tbody></table>

<figure><img src="../.gitbook/assets/apple_ats.png" alt=""><figcaption></figcaption></figure>


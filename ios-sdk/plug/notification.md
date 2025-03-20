---
description: 보물섬 기다리면 무료 컨텐츠의 모바일 알림을 위한 설정 방법을 안내 합니다.
icon: bell-ring
---

# 보물섬 알림 서비스@PLUG

***

{% hint style="info" %}
**보물섬의 기다무 서비스 사용시 유저에게 푸시 알림을 보내는 기능입니다.**

***

보물섬 알림 서비스는 **로컬 푸시**로 별도의 서버 연동 작업이 필요하지 않습니다.
{% endhint %}

<div><figure><img src="../../.gitbook/assets/apple_notify_setting_01.png" alt=""><figcaption><p>기다무 설정 화면</p></figcaption></figure> <figure><img src="../../.gitbook/assets/apple_notify_setting_02.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/apple_nofity_setting_03.png" alt=""><figcaption></figcaption></figure></div>

***

## 연동 순서

1. **TreasureIslandPlugNotificationKit** 모듈 설치하기&#x20;

**✓ 모듈 적용 후 SDK 관련 추가 작업은 필요하지 않습니다.**

***

## 모듈 설 하기

### ![](../../.gitbook/assets/cocoapods.png) COCOA PODS

보물섬 SDK를 설치하고자 하는 프로젝트의 Podfile에 다음 항목을 추가 합니다.

{% hint style="success" %}
**모듈 정보**

***

✓ pod 'TreasureIslandXFoundationKit', '{SDK-VERSION}'

✓ pod 'TreasureIslandXSceneKit', '{SDK-VERSION}'

✓ pod '**TreasureIslandXPlugNotificationKit**', '{SDK-VERSION}'
{% endhint %}

{% code lineNumbers="true" %}
```sh
# pod respository url
source 'https://github.com/CocoaPods/Specs.git'
# target project
target '{TARGET-PROJECT}' do
  use_frameworks!
  # 보물섬 필수 SDK
  pod 'TreasureIslandXFoundationKit', '{SDK-VERSION}'
  pod 'TreasureIslandXSceneKit', '{SDK-VERSION}'
  # 보물섬 알림 서비스 SDK(Notififatioin PLUG)
  pod 'TreasureIslandXPlugNotificationKit', '{SDK-VERSION}'
end
```
{% endcode %}

pod install 명령어를 통해 보물섬 SDK를 설치합니다.

```sh
$ pod install
```

### ![](../../.gitbook/assets/swiftpackage.png) SWIFT PACKAGE

{% hint style="success" %}
**기본 모듈 적용**

***

✓ [https://github.com/Studio-GURU/TreasureIslandX-iOS-Plug-NotificationKit.git](https://github.com/Studio-GURU/TreasureIsland-iOS-Plug-NotificationKit.git)
{% endhint %}

#### Package Dependency 설정

**⬇ Xcode** → **File** → **Add Package Dependencies...**&#x20;

<figure><img src="../../.gitbook/assets/apple_swift_package_01.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/스크린샷 2025-03-20 오후 12.02.44.png" alt=""><figcaption></figcaption></figure>

***




---
description: 보물섬 유료 재화 구매 서비스 연동을 위한 방법을 안내 합니다.
icon: credit-card
---

# 보물섬 인앱 구매 서비스@PLUG

***

{% hint style="success" %}
**보물섬의 유료 재화(유료 이용권)를 인앱 구매(IAP) 기능 입니다.**

***

✓  모듈 적용 후 SDK 관련 추가 작업은 필요하지 않습니다.

✓ 인앱 구매 기능은 스토어에 유료 결제 관련 설정 및 구글 클라우드 서비스의 계정 정보 설정이 필요합니다.

✓ 보물섬 SDK는 StoreKit2 버전을 사용합니다.

✓ 보물섬 SDK는 소비성 제품만 제공 됩니다.
{% endhint %}

***

## 연동 순서

{% stepper %}
{% step %}
**TreasureComicsPlugPurchaseKit** 모듈 설치하기

✓ Cocoa Pod

✓ Swift Package
{% endstep %}

{% step %}
### 애플 앱 스토어 설정

1. [console-config.md](console-config.md "mention")
2. [api-config.md](api-config.md "mention")
3. [rtdn-config.md](rtdn-config.md "mention")
{% endstep %}
{% endstepper %}

***

## 모듈 설치 하기

### ![](../../../.gitbook/assets/cocoapods.png) COCOA PODS

보물섬 SDK를 설치하고자 하는 프로젝트의 Podfile에 다음 항목을 추가 합니다.

{% hint style="success" %}
**모듈 정보**

***

✓ pod 'TreasureComicsFoundationKit', '{SDK-VERSION}'

✓ pod 'TreasureComicsSceneKit', '{SDK-VERSION}'

✓ pod '**TreasureComicsPlugPurchaseKit**', '{SDK-VERSION}'
{% endhint %}

{% code lineNumbers="true" %}
```sh
# pod respository url
source 'https://github.com/CocoaPods/Specs.git'
# target project
target '{TARGET-PROJECT}' do
  use_frameworks!
  # 보물섬 필수 SDK
  pod 'TreasureComicsFoundationKit', '{SDK-VERSION}'
  pod 'TreasureComicsSceneKit', '{SDK-VERSION}'
  # 보물섬 구매 서비스 SDK(PurchaseKit PLUG)
  pod 'TreasureComicsPlugPurchaseKit', '{SDK-VERSION}'
end
```
{% endcode %}

pod install 명령어를 통해 보물섬 SDK를 설치합니다.

```sh
$ pod install
```

### ![](../../../.gitbook/assets/swiftpackage.png) SWIFT PACKAGE

{% hint style="success" %}
**기본 모듈 적용**

***

✓ [**https://github.com/Studio-GURU/TreasureComics-iOS-Plug-PurchaseKit.git**](https://github.com/Studio-GURU/TreasureComics-iOS-Plug-PurchaseKit.git)
{% endhint %}

#### Package Dependency 설정

**⬇ Xcode** → **File** → **Add Package Dependencies...**&#x20;

<figure><img src="../../../.gitbook/assets/apple_swift_package_01.png" alt=""><figcaption></figcaption></figure>

***

## 애플 앱스토어 구매를 위한 스토어 설정 안내

애플 앱스토어 구매를 위해서는 아래와 같은 설정이 필요합니다.

* [console-config.md](console-config.md "mention")
* [api-config.md](api-config.md "mention")
* [rtdn-config.md](rtdn-config.md "mention")


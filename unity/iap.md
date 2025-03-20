---
description: 보물섬 유료 재화 구매 서비스 연동을 위한 방법을 안내 합니다.
icon: credit-card
---

# 보물섬 인앱 구매 서비스

{% tabs %}
{% tab title="ANDROID" %}
**보물섬의 유료 이용권을 인앱 구매(In-App-Purchase) 지원을 위한 플러그인 모듈 입니다.**

**보물섬 SDK는 소비성 제품만 제공 됩니다.**

### 구글 플레이 스토어

✓ 기본 모듈 적용 후 별도 코드를 통한 연동 작업은 필요하지 않습니다.

✓ 인앱 구매 기능은 스토어에 유료 결제 관련 설정 및 구글 클라우드 서비스의 계정 정보 설정이 필요합니다.

✓ 보물섬 SDK는 Play 결제 라이브러리 7.0.0을 사용하고 있습니다.

***

## 기본 모듈 적용 하기

기본 블록을 **앱(모듈) 수준의 "build.gradle"** 파일에 설정하세요.

{% hint style="info" %}
최신 버전 사용을 권장하며, :link:[release.md](../android-sdk/release.md "mention")를 통해 최신 버전을 확인 하세요.

***

인앱 구매(treasureisland-plug-purchase) 버전은 **보물섬 기본 모듈의 버전과 동일합니다**.
{% endhint %}

{% code lineNumbers="true" %}
```gradle
dependencies {
  implementation 'kr.co.studioguru.sdk:treasureislandx-plug-purchase:{SDK-VERSION}'
}
```
{% endcode %}

***

## 구글 플레이 구매를 위한 설정 안내

구글 플레이 구매를 위해서는 아래와 같은 설정이 필요합니다.

* [console-config.md](../android-sdk/plug/iap/playstore/console-config.md "mention")
  * 구글 플레이 스토어 결제 기능 활성화 및 판매 상품 등록
  * 구글 플레이 스토어 재무 데이터 접근 계정 전달
* [api-config.md](../android-sdk/plug/iap/playstore/api-config.md "mention")
* [rtdn-config.md](../android-sdk/plug/iap/playstore/rtdn-config.md "mention")

***

{% hint style="success" %}
자세한 스토어 설정 가이드는 "**ANDROID SDK > 보물섬 인앱 구매 서비스 > 구글 플레이 스토어**" 가이드를 참고 바랍니다.
{% endhint %}

{% content-ref url="../android-sdk/plug/iap/playstore/" %}
[playstore](../android-sdk/plug/iap/playstore/)
{% endcontent-ref %}
{% endtab %}

{% tab title="iOS" %}
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

1. **TreasureIslandPlugPurchaseKit** 모듈 설치하기&#x20;
2. **애플 앱 스토어 설정**
   1. [console-config.md](../ios-sdk/plug/iap/console-config.md "mention")
   2. [api-config.md](../ios-sdk/plug/iap/api-config.md "mention")
   3. [rtdn-config.md](../ios-sdk/plug/iap/rtdn-config.md "mention")

***

## 모듈 설치 하기

### ![](../.gitbook/assets/cocoapods.png) COCOA PODS

보물섬 SDK를 설치하고자 하는 프로젝트의 Podfile에 다음 항목을 추가 합니다.

{% hint style="success" %}
**모듈 정보**

***

✓ pod '**TreasureIslandXPlugPurchaseKit**', '{SDK-VERSION}'
{% endhint %}

{% code lineNumbers="true" %}
```sh
# pod respository url
source 'https://github.com/CocoaPods/Specs.git'
# target project
target '{TARGET-PROJECT}' do
  use_frameworks!
  # 보물섬 구매 서비스 SDK(PurchaseKit PLUG)
  pod 'TreasureIslandXPlugPurchaseKit', '{SDK-VERSION}''
end
```
{% endcode %}

pod install 명령어를 통해 보물섬 SDK를 설치합니다.

```sh
$ pod install
```

### ![](../.gitbook/assets/swiftpackage.png) SWIFT PACKAGE

{% hint style="success" %}
**기본 모듈 적용**

***

✓ [https://github.com/Studio-GURU/TreasureIslandX-iOS-Plug-PurchaseKit.git](https://github.com/Studio-GURU/TreasureIsland-iOS-Plug-PurchaseKit.git)
{% endhint %}

#### Package Dependency 설정

**⬇ Xcode** → **File** → **Add Package Dependencies...**&#x20;

<figure><img src="../.gitbook/assets/apple_swift_package_01.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/스크린샷 2025-03-20 오후 12.03.51.png" alt=""><figcaption></figcaption></figure>

***

## 애플 앱스토어 구매를 위한 스토어 설정 안내

애플 앱스토어 구매를 위해서는 아래와 같은 설정이 필요합니다.

* [console-config.md](../ios-sdk/plug/iap/console-config.md "mention")
* [api-config.md](../ios-sdk/plug/iap/api-config.md "mention")
* [rtdn-config.md](../ios-sdk/plug/iap/rtdn-config.md "mention")

***

{% hint style="success" %}
자세한 스토어 설정 가이드는  "**iOS SDK > 보물섬 인앱 구매 서비스**" 가이드를 참고 바랍니다.
{% endhint %}

{% content-ref url="../ios-sdk/plug/iap/" %}
[iap](../ios-sdk/plug/iap/)
{% endcontent-ref %}
{% endtab %}
{% endtabs %}




---
icon: user-group
description: 보물섬 iOS SDK를 사용하여 보물섬 메인화면을 실행 방법에 대해 안내합니다.
---

# 채널회원 연동

{% hint style="success" %}
파트너사의 회원을 보물섬 계정과 연동하여 사용하고자 하는 경우

***

전달된 파트너사의 회원정보를 통해 보물섬 계정을 생성합니다.&#x20;

:heavy\_check\_mark: **파트너사의 앱의 운영 방식에 따라 로그인 여부 확인이 가능한 기능 구현이 필요 할 수 있습니다.**
{% endhint %}

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>채널링 서비스 플로우</p></figcaption></figure>

***

## 준비 사항

보물섬 채널링 서비스 이용을 위해서는 [start.md](start.md "mention")의 기본 설정이 완료 되어야 합니다.

***

## 연동 순서

## 연동 순서

{% stepper %}
{% step %}
### SDK 초기화

iOS SDK initialize

**✓ Membership:Channeling**
{% endstep %}

{% step %}
### 프로필 설정

Profile with **SignKey**&#x20;
{% endstep %}

{% step %}
### 화면 호출

TreasureIsland screen launch
{% endstep %}
{% endstepper %}

***

## SDK 초기화 하기

{% hint style="warning" %}
프로젝트의 AppDelegate에서 **보물섬 iOS SDK 초기화가 진행 됩니다.**

***

초기화가 진행되지 않을경우 보물섬 서비스가 정상 동작하지 않습니다.

✓ [https://developer.apple.com/documentation/uikit/uiapplicationdelegate](https://developer.apple.com/documentation/uikit/uiapplicationdelegate)
{% endhint %}

보물섬 SDK 사용을 위한 초기화를 진행합니다.

`AppDelegate`(StoryBoardUI), `App`(SwiftUI) 클래스에서 `SceneKit.Builder`를 통해 SDK를 초기화 하세요.

### SceneKit.Builder

<table><thead><tr><th width="193">Name</th><th width="226">Type</th><th>Value</th></tr></thead><tbody><tr><td><code>appId</code></td><td>string</td><td>연동앱의 고유 식별자</td></tr><tr><td><code>appSecret</code></td><td>string</td><td>연동앱의 고유 식별자 검증키</td></tr><tr><td><code>membership</code></td><td>enum(basic, <strong>channeling</strong>)</td><td>연동앱의 회원 적용 방식(<strong>channeling</strong> 선택)</td></tr></tbody></table>

**✓ SceneKit.Builder 인스터스를 통해 옵션과 보물섬 SDK 초기화를 진행합니다.**

{% tabs %}
{% tab title="Swift UI(App)" %}
<pre class="language-swift" data-line-numbers><code class="lang-swift">import SwiftUI
import TreasureIslandFoundationKit
import TreasureIslandSceneKit

@main
struct PartnerApp: App {
    init() {
        // SceneKit
        let sceneKit = SceneKit.Builder(
            appId: "{APP-ID}", 
            appSecret: "{APP-SECRET}",
<strong>            membership: SceneKit.Membership.channeling
</strong>        )
        // option: 로그 출력 여부를 설정
<strong>        .withAllowLog(allow: true)
</strong>        // TreasureKit 인스턴스 생성
        .build()
        // 보물섬 SDK 초기화
        treasureKit.initialize()
    }
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
</code></pre>
{% endtab %}

{% tab title="StoryBoar(App Delegate)" %}
<pre class="language-swift" data-line-numbers><code class="lang-swift">import TreasureIslandFoundationKit
import TreasureIslandSceneKit

@main
class AppDelegate: UIResponder, UIApplicationDelegate {
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
         // SceneKit
        let sceneKit = SceneKit.Builder(
            appId: "{APP-ID}", 
            appSecret: "{APP-SECRET}"
<strong>            membership: SceneKit.Membership.channeling
</strong>        )
        // option: 로그 출력 여부를 설정
<strong>        .withAllowLog(allow: true)
</strong>        // TreasureKit 인스턴스 생성
        .build()
        // 보물섬 SDK 초기화
        treasureKit.initialize()        
        return true
    }
}

</code></pre>
{% endtab %}
{% endtabs %}

#### Options <a href="#options" id="options"></a>

**🎈withAllowLog(allowLog: boolean)**

SDK 로그 출력 여부를 설정 합니다.

**✓ 기본값** → **로그가 출력되지 않습니다.**

| Name       | Type    | Description            |
| ---------- | ------- | ---------------------- |
| `allowLog` | boolean | 로그 출력 여부 (`기본값 false`) |

***

***

## 프로필 설정하기

### 연동 순서

{% stepper %}
{% step %}
### SignKey 생성

HmacSHA256 방식을 통한 SignKey 생성
{% endstep %}

{% step %}
### Profile Builder 생성

SignKey를 통한 Builder 인스턴스 생성
{% endstep %}

{% step %}
### Profile Option 설정

✓ Gender → 성별 정보(enum)

✓ BirthYear → 태어난 연도 정보(Int)
{% endstep %}

{% step %}
### Profile 등록

Profile.Builder().register() 호출을 통한 프로필 등록
{% endstep %}
{% endstepper %}

***

### SignKey 생성 하기

{% hint style="danger" %}
**보안을 강화하기 위해 SignKey는 클라이언트가 아닌 서버에서 생성한 후 클라이언트로 전달해주세요.**

***

보물섬은 결제 서비스를 연동하고 있으므로, 유저 식별자 보안 관리가 필요합니다.
{% endhint %}

{% hint style="info" %}
**signature 생성 (**<mark style="color:red;">**HmacSHA256 생성에 필요한 Key는 영업팀을 통해 전달 됩니다.**</mark>**)**

***

**$timeStamp$nonce$암호화된User식별자**

위 값을 HmacSHA256 Hash -> Base64 Url Encodeing을 통해 Signature를 생성합니다.

***

* timeStamp → unix timestamp seconds
* nonce → 문자열 32자(임의로 생성된 문자열 32자)
* user 식별자 → 회원 구분이 가능한 식별자
{% endhint %}

<table data-full-width="false"><thead><tr><th width="127">Name</th><th width="141">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>sign</code></td><td>string</td><td><p><code>timestmap.nonce.encryptedUserId.signature</code></p><hr><p> <mark style="background-color:red;">timestamp, nonce, userid  값은 <strong>signature 생성에 사용된 값</strong>을 전달 합니다.</mark></p></td></tr></tbody></table>

### Profile.Builder

```swift
// SignKey를 이용하여 인스턴스를 생성합니다.
Profile.Builder(signKey: AccountUtils.accountTicket())
    // 성별을 설정합니다.(옵션)
    .withGender(gender: Profile.Gender.male 또는 Profile.Gender.female)
    // 태어난 연도를 설정합니다.(옵션)
    .withBirthYear(birthYear: 2000)
    .register { success, message in
        // success: 프로필 등록 여부
        // message: 프로필 등록과 관련된 메시지(오류 메시지)                
        print("Profile.Builder { success: \(success), message: \(message) }")
}
```

***

## 화면 호출 하기

### 연동 순서

{% stepper %}
{% step %}
### Builder 인스턴스 생성

Launch.Builder::Builder()
{% endstep %}

{% step %}
### Builder Option 설정

✓ advertising id

✓ header
{% endstep %}

{% step %}
### Launch 인스턴스 생성

Launch.Builder().build()
{% endstep %}

{% step %}
### Launch 호출

Launch.Builder().build()  생성된 Lauch 인스턴스의 launch() 실행

`launch(completionHandler: (_ success: Bool, _ message: String) → Void)`
{% endstep %}
{% endstepper %}

***

### Launcher.Builder

{% code lineNumbers="true" %}
```swift
// Builder 옵션과 함께 LaunchKit 인스턴스를 생성합니다.
let launchKit = LauncherKit.Builder()
    // Option: 광고 식별자를 설정합니다.
    .withAdvertisingId(advertisingId: "0000-0000-0000-0000-0000")
    .build()

// 보물섬을 시작합니다.
launchKit.launch { completed, message in
    // completed(bool) 성공여부
    // message(string) 성공여부 관련 메시지(오류메시지)
}
```
{% endcode %}

***

#### Options

🎈**withAdvertisingId(advertisingId: String)**

&#x20;ANDROID ADID를 설정합니다.

**✓ 설정이 없을 경우 SDK에서 별도 추출하여 사용합니다.**

| Name            | Type   | Description  |
| --------------- | ------ | ------------ |
| `advertisingId` | string | 안드로이드 광고 식별자 |

***

### Launcher.launch

보물섬을 실행합니다. 상황에 따라 보물섬 메인 화면 또는 약관 동의 화면이 노출 됩니다.

🎈**launch(completionHandler: (\_ success: Bool, \_ message: String) → Void)**

**✓ completionHandler의 success 값은 launch 실행 결과를 전달합니다.**

<table><thead><tr><th width="173">Name</th><th width="129">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>success</code></td><td>bool</td><td>success 실행 결과 <code>true: 성공 / false: 실패</code></td></tr><tr><td><code>message</code></td><td>string</td><td>실행 결과 메시지(오류시 오류 메시지 전달)</td></tr></tbody></table>


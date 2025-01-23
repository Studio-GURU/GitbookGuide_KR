---
icon: user
description: 보물섬 iOS SDK를 사용하여 보물섬 메인화면을 실행 방법에 대해 안내합니다.
---

# 채널회원 미연동

{% hint style="success" %}
파트너사의 회원이 존재하지 않거나, 보물섬에서 제공하는 자체 계정을 사용하고자 하는 경우

***

✔ **보물섬 자체 계정의 경우 파트너사에서 사용중인 계정과 연동되지 않습니다.**
{% endhint %}

<figure><img src="../.gitbook/assets/스크린샷 2024-08-22 오후 2.05.51.png" alt=""><figcaption></figcaption></figure>

***

## 준비 사항

보물섬 서비스 이용을 위해서는 [start.md](start.md "mention")의 기본 설정이 완료 되어야 합니다.

***

## 연동 순서

{% stepper %}
{% step %}
### SDK 초기화

iOS SDK initialize

**✓ Membership:Basic**
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

<table><thead><tr><th width="193">Name</th><th>Type</th><th>Value</th></tr></thead><tbody><tr><td><code>appId</code></td><td>string</td><td>연동앱의 고유 식별자</td></tr><tr><td><code>appSecret</code></td><td>string</td><td>연동앱의 고유 식별자 검증키</td></tr><tr><td><code>membership</code></td><td>enum(<strong>basic</strong>, channeling)</td><td>연동앱의 회원 적용 방식(<strong>basic</strong> 선택)</td></tr></tbody></table>

**✓** **SceneKit.Builder 인스터스를 통해 옵션과 보물섬 SDK 초기화를 진행합니다.**

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
<strong>            membership: SceneKit.Membership.basic
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
<strong>            membership: SceneKit.Membership.basic
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

**✓ 기본값 → 로그가 출력되지 않습니다.**

| Name       | Type    | Description            |
| ---------- | ------- | ---------------------- |
| `allowLog` | boolean | 로그 출력 여부 (`기본값 false`) |

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

Launch.Builder().build()  생성된 Launch 인스턴스의 launch() 실행

`launch(completionHandler: (_ success: Bool, _ message: String) → Void)`
{% endstep %}
{% endstepper %}

***

## Launcher.Builder

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

### Options

#### 🎈withAdvertisingId(advertisingId: String)

&#x20;ANDROID ADID를 설정합니다.

**✓ 설정이 없을 경우 SDK에서 별도 추출하여 사용합니다.**

| Name            | Type   | Description  |
| --------------- | ------ | ------------ |
| `advertisingId` | string | 안드로이드 광고 식별자 |

***

## Launcher.launch

보물섬을 실행합니다. 상황에 따라 보물섬 메인 화면 또는 약관 동의 화면이 노출 됩니다.

#### 🎈launch(completionHandler: (\_ success: Bool, \_ message: String) → Void)

**✓ completionHandler의 success 값은 launch 실행 결과를 전달합니다.**

<table><thead><tr><th width="173">Name</th><th width="129">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>success</code></td><td>bool</td><td>success 실행 결과 <code>true: 성공 / false: 실패</code></td></tr><tr><td><code>message</code></td><td>string</td><td>실행 결과 메시지(오류시 오류 메시지 전달)</td></tr></tbody></table>








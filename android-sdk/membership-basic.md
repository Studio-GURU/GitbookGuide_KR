---
description: 보물섬 ANDROID SDK를 사용하여 보물섬 메인화면을 실행 방법에 대해 안내합니다.
icon: user
---

# 채널회원 미연동 방식

{% hint style="success" %}
파트너사의 회원이 존재하지 않거나, 보물섬에서 제공하는 자체 계정을 사용하고자 하는 경우

***

**✓ 보물섬 자체 계정의 경우 파트너사에서 사용중인 계정과 연동되지 않습니다.**
{% endhint %}

<figure><img src="../.gitbook/assets/스크린샷 2024-08-22 오후 2.05.51.png" alt=""><figcaption><p>보물섬 회원 플로우</p></figcaption></figure>

***

## 준비 사항

보물섬 서비스 이용을 위해서는 :link:[start.md](start.md "mention")의 기본 설정이 완료 되어야 합니다.

***

## 연동 순서

{% stepper %}
{% step %}
### 기본 모듈 적용

Apply build.gradle dependencies
{% endstep %}

{% step %}
### SDK 초기화

**Android SDK initialize**

<mark style="color:red;">**✓**</mark> <mark style="color:red;">**Membership:Basic**</mark>
{% endstep %}

{% step %}
### 화면 호출

TreasureIsland screen launch
{% endstep %}
{% endstepper %}

***

## 기본 모듈 적용 하기

기본 블록을 **앱(모듈) 수준의 "build.gradle"** 파일에 설정하세요.

{% hint style="info" %}
최신 버전 사용을 권장하며, :link:[release.md](release.md "mention")를 통해 최신 버전을 확인 하세요.

***

**✓ 추가 기능 사용을 위해 보물섬X PLUG 모듈의 추가될 수 있습니다.**
{% endhint %}

{% code lineNumbers="true" %}
```gradle
dependencies {
  implementation 'com.treasurecomics.sdk:scene:{SDK-VERSION}'
}
```
{% endcode %}

***

## SDK 초기화 하기

{% hint style="warning" %}
**Application의 “onCreate()"에서 보물섬 ANDROID SDK 초기화가 진행 됩니다.**
{% endhint %}

사용중인 ":link:[Application Class](https://developer.android.com/reference/android/app/Application)"가 없다면, 신규로 생성후 초기화를 진행하시면 됩니다.

보물섬 SDK 사용을 위해 초기화를 진행 합니다.

`Application`의 `onCreate()`에서 `SceneConfig.Builder`를 통해 SDK를 초기화하세요.

### **TreasureConfig.Builder**

| Name         | Value                                                                |
| ------------ | -------------------------------------------------------------------- |
| `context`    | Android Context                                                      |
| `appId`      | 연동앱의 고유 식별자                                                          |
| `appSecret`  | 연동앱의 공유 식별자 검증키                                                      |
| `membership` | 연동앱의 회원 적용 방식(<mark style="color:red;">**Basic**</mark>**&#x20;선택**) |

**✓** **생성된 Builder 인스턴스를 통해 옵션과 SDK 초기화를 진행합니다.**

{% tabs %}
{% tab title="KOTLIN" %}
<pre class="language-kotlin" data-line-numbers><code class="lang-kotlin">class AppApplication : Application() {
    override fun onCreate() {
        super.onCreate()
        
        // ... other code ...
        // &#x3C;code>
        // ... other code ...
        
        SceneConfig.Builder(
            context = this, 
            appId = "{발급받은 appId}", 
            appSecret = "{발급받은 appSecret}",
<strong>            membership = SceneConfig.Membership.BASIC
</strong>        )
        // option 로그 출력 여부를 설정합니다.
        .withAllowLog(allowLog = true)
        // option 푸시 알림 설정
        .withNotificationOption(
            config = SceneConfig.NotificationOption(
                channelName = "알림 채널명",
                iconResourceId = R.drawable.ic_notification
            )
        )
        .build()?.initialize()
        
        // ... other code ...
        // &#x3C;code>
        // ... other code ...
    }
}
</code></pre>
{% endtab %}

{% tab title="JAVA" %}
<pre class="language-java" data-line-numbers><code class="lang-java">public class AppApplication extends Application {
    @Override
    public void onCreate() {
        super.onCreate();
        
        // ... other code ...
        // &#x3C;code>
        // ... other code ...
    
        SceneConfig.Builder builder = new SceneConfig.Builder(
            this,
            "testAppID",
            "testSecret",
<strong>            SceneConfig.Membership.BASIC
</strong>        );
        builder.withAllowLog(true);
        builder.withStatusBarOption(new SceneConfig.StatusBarOption(
            true,
            Color.parseColor("#FF6103"),
            false
        ));
        builder.withNotificationOption(new SceneConfig.NotificationOption(
            true,
            "보물섬",
            R.drawable.ic_notify
        ));
        SceneConfig SceneConfig = builder.build();
        if (SceneConfig != null) {
            SceneConfig.initialize();
        }
        
        // ... other code ...
        // &#x3C;code>
        // ... other code ...
    }
}
</code></pre>
{% endtab %}
{% endtabs %}

### Options

#### 🎈withAllowLog(allowLog: boolean)

SDK 로그 출력 여부를 설정 합니다.

**✓ 기본값** → **로그가 출력되지 않습니다.**

| Name       | Type    | Description            |
| ---------- | ------- | ---------------------- |
| `allowLog` | boolean | 로그 출력 여부 (`기본값 false`) |

#### 🎈withNotificationOption(config: TreasureConfig.NotificationOption)

{% hint style="info" %}
해당 옵션을 사용하기 위해서는 하다무 알림 서비스 SDK 적용이 필요합니다.

-> 하다무 알림 SDK 적용이 되어있지 않은 경우 정상 동작하지 않습니다.

***

알림 서비스 SDK 적용 방법에 대해서는 "[notification.md](plug/notification.md "mention")" 가이드를 참고 바랍니다.
{% endhint %}

기다무 푸시 알림을 설정합니다.

**✓ 기본값** → **보물섬의 기본값이 사용됩니다.**

⬇ TreasureConfig.NotificationOption

<table><thead><tr><th width="242">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td><code>channelName</code></td><td>string(<code>nullable</code>)</td><td>푸시 알림 채널명<br><code>기본값: '보물섬'</code></td></tr><tr><td><code>smallIconResourceId</code></td><td><strong>'@'DrawableRes</strong>(<code>nullable</code>)</td><td>푸시 알림 아이콘 리소스<br><code>기본값: 보물섬 아이콘</code></td></tr></tbody></table>

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
{% endstep %}
{% endstepper %}

***

### Launcher.Builder

{% tabs %}
{% tab title="KOTLIN" %}
<pre class="language-kotlin" data-line-numbers><code class="lang-kotlin">// 빌더 인스턴스를 생성합니다.
val builder = Launcher.StandardBuilder()

// ADID값을 설정합니다
builder.withAdvertisingId(advertisingId = "00000000-0000-0000-0000-000000000000")

// Header 스타일을 설정합니다.
val headerModel = SceneHeaderModel.Builder()
    // Header Title
    .withHeaderTitle(title = "보물섬")
    // Header Back Button
    .withUseBackButton(use = true)
    // Header Close Button
    .withUseCloseButton(use = true)
    .build()
builder.withHeader(headerModel = headerModel)
    
// Launcher 인스턴스를 생성합니다.
val launcher = builder.build()

// 보물섬을 실행 합니다.
launcher.launch(
    // 액티비티
    ownerActivity = {ACTIVITY}, 
    // 결과 리스너
    listener = object : Launcher.Listener {
<strong>        override fun onLaunched(success: Boolean, message: String) {
</strong>            // success: 성공 여부            
            // message: 성공/실패 관련 메시지
       }
    }
)
</code></pre>
{% endtab %}

{% tab title="JAVA" %}
<pre class="language-java" data-line-numbers><code class="lang-java">// 빌더 인스턴스를 생성합니다.
Launcher.StandardBuilder builder = new Launcher.StandardBuilder();

// ADID값을 설정합니다
builder.withAdvertisingId("00000000-0000-0000-0000-000000000000");

// Header 스타일을 설정합니다.
SceneHeaderModel.Builder headerBuilder = new SceneHeaderModel.Builder();
// Header Title(빈값 타이틀 노출 되지 않음)
headerBuilder.withHeaderTitle("보물섬");
// Header Use Back Button
headerBuilder.withUseBackButton(true);
// Header Use Close Button
headerBuilder.withUseCloseButton(true);
SceneHeaderModel headerModel = headerBuilder.build();
builder.withHeader(headerModel);

// Launcher 인스턴스를 생성합니다.
Launcher launcher = builder.build();

// 보물섬을 실행 합니다.
launcher.launch(
    // 액티비티
    this, 
    // 결과 리스너
    new Launcher.Listener() {
        @Override
<strong>        public void onLaunched(boolean success, String message) {
</strong>            // success: 성공 여부
            // message: 성공/실패 관련 메시지            
        }
    }
);
</code></pre>
{% endtab %}
{% endtabs %}

***

#### Options

🎈**withAdvertisingId(advertisingId: String)**

&#x20;ANDROID ADID를 설정합니다.

**✓ 설정이 없을 경우 SDK에서 별도 추출하여 사용합니다.**

| Name            | Type   | Description  |
| --------------- | ------ | ------------ |
| `advertisingId` | string | 안드로이드 광고 식별자 |

***

🎈**withHeader(headerModel: SceneHeaderModel)**

**✓ None, Back, Close, Custom 설정을 통해 원하는 해더를 설정 할 수 있습니다.**

| Name          | Type               | Description   |
| ------------- | ------------------ | ------------- |
| `headerModel` | `SceneHeaderModel` | 해덩 설정 데이타 클래스 |



{% hint style="success" %}
**설정에 대한 자세한 내용은** [options.md](options.md "mention") **가이드를 확인 바랍니다.**
{% endhint %}

***

### Launcher.launch

보물섬을 실행합니다. 상황에 따라 보물섬 메인 화면 또는 약관 동의 화면이 노출 됩니다.

🎈**launch(ownerActivity: Activity, listener: Launcher.Listener)**

| Name            | Type              | Description |
| --------------- | ----------------- | ----------- |
| `ownerActivity` | activity          | 안드로이드 액티비티  |
| `listener`      | Launcher.Listener | 실행 결과 리스너   |

⬇ Launcher.Listener

| Name                                                                                                                        | Description                                                         |
| --------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| <p><code>onLaunched(</code><br>    <code>success: Boolean,</code><br>    <code>message: String</code><br><code>)</code></p> | <p>실행 여부가 'success' 값으로 전달 됩니다.<br>실행 여부 관련 'message'값이 전달 됩니다.</p> |


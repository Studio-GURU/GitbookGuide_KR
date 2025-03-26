---
description: 보물섬 ANDROID SDK를 사용하여 보물섬 메인화면을 실행 방법에 대해 안내합니다.
icon: user-group
---

# 채널회원 연동 방식

{% hint style="success" %}
파트너사의 회원을 보물섬 계정과 연동하여 사용하고자 하는 경우

***

전달된 파트너사의 회원정보를 통해 보물섬 계정을 생성합니다.&#x20;

**✓** **파트너사의 앱의 운영 방식에 따라 로그인 여부 확인이 가능한 기능 구현이 필요 할 수 있습니다.**
{% endhint %}

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>채널링 서비스 플로우</p></figcaption></figure>

***

## 준비 사항

보물섬 채널링 서비스 이용을 위해서는 :link:[start.md](start.md "mention")의 기본 설정이 완료 되어야 합니다.

***

## 연동 순서

{% stepper %}
{% step %}
### 기본 모듈 적용

Apply build.gradle dependencies
{% endstep %}

{% step %}
### SDK 초기화

Android SDK initialize

**✓ Membership:Channeling**
{% endstep %}

{% step %}
### 프로필 설정

Profile with **SignKey & Register**
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

**✓** **추가 기능 사용을 위해 보물섬 PLUG 모듈의 추가될 수 있습니다.**
{% endhint %}

{% code lineNumbers="true" %}
```gradle
dependencies {
  implementation 'kr.co.studioguru.sdk:treasureislandx-scene:{SDK-VERSION}'
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

| Name         | Value                            |
| ------------ | -------------------------------- |
| `context`    | Android Context                  |
| `appId`      | 연동앱의 고유 식별자                      |
| `appSecret`  | 연동앱의 공유 식별자 검증키                  |
| `membership` | 연동앱의 회원 적용 방식(**Channeling 선택**) |

**✓** **생성된 Builder 인스턴스를 통해 옵션과 SDK 초기화를 진행합니다.**

{% tabs %}
{% tab title="KOTLIN" %}
<pre class="language-kotlin" data-line-numbers><code class="lang-kotlin">class AppApplication : Application() {
    override fun onCreate() {
        super.onCreate()
        SceneConfig.Builder(
            context = this, 
            appId = "{APP-ID}", 
            appSecret = "{APP-SECRET}",
<strong>            membership = SceneConfig.Membership.CHANNELING
</strong>        )
        // option 로그 출력 여부를 설정합니다.
        .withAllowLog(allowLog = true)
        // option 상태창의 색상을 설정 합니다.
        .withStatusBarOption(
            config = SceneConfig.StatusBarOption(
                statusBarColor = Color.parseColor("#FF6103"),
                isWindowLight = false
            )
        )
        // option 푸시 알림 설정
        .withNotificationOption(
            config = SceneConfig.NotificationOption(
                channelName = "알림 채널명",
                iconResourceId = R.drawable.ic_notification
            )
        )
        .build()?.initialize()
    }
}
</code></pre>
{% endtab %}

{% tab title="JAVA" %}
<pre class="language-java" data-line-numbers><code class="lang-java">public class AppApplication extends Application {
    @Override
    public void onCreate() {
        super.onCreate();
        SceneConfig.Builder builder = new SceneConfig.Builder(
            this,
            "testAppID",
            "testSecret",
<strong>            SceneConfig.Membership.CHANNELING
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
    }
}
</code></pre>
{% endtab %}
{% endtabs %}

### Options

#### 🎈withAllowLog(allowLog: boolean)

SDK 로그 출력 여부를 설정 합니다.

**✓ 기본값 → 로그가 출력되지 않습니다.**

| Name       | Type    | Description            |
| ---------- | ------- | ---------------------- |
| `allowLog` | boolean | 로그 출력 여부 (`기본값 false`) |

#### 🎈withStatusBarColor(config: TreasureConfig.StatusBarOption)

화면의 상단 상태창의 색상을 설정합니다.

**✓ 기본값 → 보물섬의 기본값이 사용됩니다.**

⬇ TreasureConfig.StatusBarOption

| Name             | Type                        | Description                                                                                                         |
| ---------------- | --------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `statusBarColor` | **'@'ColorInt**(`nullable`) | <p>상태창 배경 색상<br><code>기본값: Color.WHITE</code></p>                                                                   |
| `isWindowLight`  | boolean(`nullable`)         | <p>상태창 텍스트 색상 설정<br><code>기본값: false</code><br><code>true: 어두운 색상의 텍스트</code><br><code>false: 밝은 색상의 텍스트</code></p> |

#### 🎈withNotificationOption(config: TreasureConfig.NotificationOption)

{% hint style="info" %}
해당 옵션을 사용하기 위해서는 하다무 알림 서비스 SDK 적용이 필요합니다.

-> 하다무 알림 SDK 적용이 되어있지 않은 경우 정상 동작하지 않습니다.

***

알림 서비스 SDK 적용 방법에 대해서는 "[notification.md](plug/notification.md "mention")" 가이드를 참고 바랍니다.
{% endhint %}

기다무 푸시 알림을 설정합니다.

**✓ 기본값 → 보물섬의 기본값이 사용됩니다.**

⬇ TreasureConfig.NotificationOption

<table><thead><tr><th width="242">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td><code>channelName</code></td><td>string(<code>nullable</code>)</td><td>푸시 알림 채널명<br><code>기본값: '보물섬'</code></td></tr><tr><td><code>smallIconResourceId</code></td><td><strong>'@'DrawableRes</strong>(<code>nullable</code>)</td><td>푸시 알림 아이콘 리소스<br><code>기본값: 보물섬 아이콘</code></td></tr></tbody></table>

***

## 프로필 설정하기

### 연동 순서

{% stepper %}
{% step %}
### SignKey 생성

✓ **HmacSHA256** 방식을 통한 [**SignKey 생성 하기**](sign.md)

{% hint style="danger" %}
**보안을 강화하기 위해 SignKey는 클라이언트가 아닌 서버에서 생성한 후 클라이언트로 전달해주세요.**

***

보물섬은 결제 서비스를 연동하고 있으므로, 유저 식별자 보안 관리가 필요합니다.
{% endhint %}
{% endstep %}

{% step %}
### Profile Builder 생성

[**SignKey**](sign.md)를 통한 Builder 인스턴스 생성
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

### Profile.Builder

{% tabs %}
{% tab title="KOTLIN" %}
<pre class="language-kotlin"><code class="lang-kotlin">// 빌더 인스턴스를 생성합니다.(signKey 필수)
<strong>val builder = Profile.Builder(signKey = ${signKey})
</strong>// 성별을 설정합니다.(옵션)
builder.withGender(gender = Profile.Gender.MALE 또는 Profile.Gender.FEMALE)
// 태어난 연도를 설정합니다.(옵션)
builder.withBirthYear(birthYear = 2000)
// 프로필 인스턴스를 등록합니다.
<strong>builder.register { success, message ->
</strong>    // success: 프로필 등록 여부
    // message: 프로필 등록과 관련된 메시지(오류 메시지)
}
</code></pre>
{% endtab %}

{% tab title="JAVA" %}
```java
// 빌더 인스턴스를 생성합니다.(signKey 필수)
Profile.Builder builder = new Profile.Builder(${signKey});
// 성별을 설정합니다.(옵션)
builder.withGender(Profile.Gender.MALE 또는 Profile.Gender.FEMALE);
// 태어난 연도를 설정합니다.(옵션)
builder.withBirthYear(2000);
// 프로필 인스턴스를 등록합니다.
builder.register((successs, message) ->
    // success: 프로필 등록 여부
    // message: 프로필 등록과 관련된 메시지(오류 메시지)                
);
```
{% endtab %}
{% endtabs %}

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
val builder = Launcher.Builder()

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

| Name                                                                                                                         | Description                                                               |
| ---------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| <p><code>onLaunched(</code><br>    <code>success: Boolean,</code> <br>    <code>message: String</code><br><code>)</code></p> | <p>실행 여부가 'success' 값으로 전달 됩니다.<br>실행 여부와 관련 'message' 값이 전달 됩니다.<br></p> |


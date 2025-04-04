---
description: 보물섬 Flutter-Package을 사용하여 보물섬 메인화면을 실행 방법에 대해 안내합니다.
icon: user-group
---

# 채널회원 연동 방식

{% hint style="success" %}
전달된 파트너사의 회원정보를 통해 보물섬 계정을 생성합니다.&#x20;

**✓ 파트너사의 앱의 운영 방식에 따라 로그인 여부 확인이 가능한 기능 구현이 필요 할 수 있습니다.**
{% endhint %}

<figure><img src="../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption><p>채널링 서비스 플로우</p></figcaption></figure>

***

## 준비 사항

보물섬 서비스 이용을 위해서는 :link:[start.md](../unity/start.md "mention")의 기본 설정이 완료 되어야 합니다.

***

## 연동 순서

{% stepper %}
{% step %}
### Package 초기화

Package Initialize

<mark style="color:red;">**✓**</mark> <mark style="color:red;">**Membership:Channeling**</mark>
{% endstep %}

{% step %}
### 프로필 설정

Profile with **SignKey & Register**
{% endstep %}

{% step %}
### 화면 호출

**comicsLaunch ⇨ (success, message);**
{% endstep %}
{% endstepper %}

***

## Package 초기화 하기

보물섬 Flutter-Package 사용을 위해 초기화를 진행합니다.

{% hint style="success" %}
Application 시작시 초기화를 진행합니다.

***

최신 버전 사용을 권항하며, [release.md](release.md "mention")를 통해 최신 버전을 확인 하세요.

추가 기능 사용을 위해 추가 모듈의 설치가 필요할 수 있습니다.
{% endhint %}

### module import

{% code lineNumbers="true" %}
```dart
import 'package:flutter_treasureislandx_addon/flutter_treasureislandx_addon.dart';
import 'package:flutter_treasureislandx_addon/models/environment_config.dart';
import 'package:flutter_treasureislandx_addon/models/membership_config.dart';
import 'package:flutter_treasureislandx_addon/models/notification_config.dart';
import 'package:flutter_treasureislandx_addon/models/statusbar_config.dart';
```
{% endcode %}

<table><thead><tr><th width="300">Module Name</th><th width="122">Type</th><th width="147">Description</th><th>Etc</th></tr></thead><tbody><tr><td><code>environment_config.dart</code></td><td>enum</td><td>접속 환경 설정</td><td>default : Live</td></tr><tr><td><code>membership_config.dart</code></td><td>enum</td><td>회원 정책 설정</td><td>Basic / <mark style="color:red;"><strong>Channeling</strong></mark></td></tr><tr><td><code>statusbar_config.dart</code></td><td>data class</td><td>상태창 색상 설정 </td><td>Only Android</td></tr><tr><td><code>notification_config.datd</code></td><td>data class</td><td>푸시알림 설정</td><td>Only Android</td></tr></tbody></table>

### comicsWithInitialize

| Name                 | Value                                  |
| -------------------- | -------------------------------------- |
| `appId`              | 연동앱의 고유 식별자                            |
| `appSecret`          | 연동앱의 고유 식별자 검증키                        |
| `allowDebug`         | 로그 출력 여부 (optional / default: false)   |
| `statusBarConfig`    | 상태창 색상 설정(optional / only android)     |
| `notificationConfig` | 푸시 알림(기다무) 설정(optional / only android) |
| `environment`        | 접속 환경(optional / default: Live)        |

{% hint style="info" %}
고유 식별자 및 고유 식별자 검증키는 영업팀을 통해 별도 전달 됩니다.&#x20;
{% endhint %}

<pre class="language-dart" data-line-numbers><code class="lang-dart">import 'package:flutter_treasureislandx_addon/flutter_treasureislandx_addon.dart';
import 'package:flutter_treasureislandx_addon/models/environment_config.dart';
import 'package:flutter_treasureislandx_addon/models/membership_config.dart';
import 'package:flutter_treasureislandx_addon/models/notification_config.dart';
import 'package:flutter_treasureislandx_addon/models/statusbar_config.dart';

// 앱의 시작점에 아래 코드를 참고하여 초기화를 진행합니다.
Future&#x3C;void> initComics() async {
    final statusbarConfig = StatusbarConfig(statusBarColor: "#FFFF00", isWindowLight: false);
    final notificationConfig = NotificationConfig(channelName: "플러터", smallIconResourceName: "ic_flutter_notify");
    final result = await FlutterTreasureislandAddon().comicsInitialize(
        // AppID
        'harustory',
        // AppSecret
        'haruSecret',
        // Membership
<strong>        Membership.Channeling,
</strong>        // Log
        true,
        // Statusbar config
        statusbarConfig,
        // Notification config
        notificationConfig,
        // Environment
<strong>        Environment.Live,
</strong>    );
    print("comicsInitialize { success: ${result.success}, message: ${result.message} }");
  }
</code></pre>

### StatusBarConfig

{% code lineNumbers="true" %}
```dart
// define
class StatusbarConfig {
  // StatusBar 색상을 설정 합니다.색상 HEX값을 사용합니다. #FFFFFF
  final String statusBarColor;
  // true: StatusBar 요소의 색상이 밝게 표시 됩니다.(어두운 배경일 경우 사용)
  // false: StatusBar 요소의 색상이 어둡게 표시 됩니다.(밝은 배경일 경우 사용)
  final bool isWindowLight;
}

// usage
final statusbarConfig = StatusbarConfig(
  statusBarColor: "#FFFFFF", 
  isWindowLight: false
);
```
{% endcode %}

### NotificationConfig

{% code lineNumbers="true" %}
```dart
// define
class NotificationConfig {
  // 푸시알림의 채널명을 설정합니다.
  // 별도 설정이 없는 경우 기본값인 '보물섬'으로 표시됩니다.
  final String channelName;
  // 푸시알림에 표시되는 아이콘 리소스를 설정합니다.
  // 확장자를 제외한 파일명
  final String smallIconResourceName;
}

// usage
final notificationConfig = NotificationConfig(
  channelName: "보물섬", 
  smallIconResourceName: "ic_flutter_notify"
);
```
{% endcode %}

***

## 프로필 설정

### 연동 순서

{% stepper %}
{% step %}
### SignKey 생성

✓ HmacSHA256 방식을 통한 [**SignKey 생성 하기**](sign.md)

{% hint style="danger" %}
**보안을 강화하기 위해 SignKey는 클라이언트가 아닌 서버에서 생성한 후 클라이언트로 전달해주세요.**

***

보물섬은 결제 서비스를 연동하고 있으므로, 유저 식별자 보안 관리가 필요합니다.
{% endhint %}
{% endstep %}

{% step %}
### Profile Option

✓ Gender → 성별 정보(enum)

✓ BirthYear → 태어난 연도 정보(Int)
{% endstep %}

{% step %}
### Profile 등록

**comicsProfile($signkey, $gender, $birthYear);**
{% endstep %}
{% endstepper %}

***

### comicsProfile

<pre class="language-dart" data-line-numbers><code class="lang-dart">// define
Future&#x3C;AddOnResult> comicsWithProfile(
  // signkey(필수)
  String signKey, 
  // 성별(옵션)
  Gender? gender
  // 태어난 연도(옵셥)
  int? birthYear
)

// usage
<strong>import 'package:flutter_treasureislandx_addon/models/profile_gender_config.dart';
</strong>final result = await FlutterTreasureislandAddon().comicsProfile(
  // signkey
<strong>  signKey, 
</strong>  // 성별(옵션/없을 경우 null) 
<strong>  Gender.Male, 
</strong>  // 태어난 연도 정보(옵셥/없을 경우 null)
<strong>  2000
</strong>);
print("setProfile { success: ${result.success}, message: ${result.message} }");

</code></pre>

***

## 화면 호출 하기

### comicsLaunch

{% code lineNumbers="true" %}
```dart
// define
Future<AddOnResult> comicsLaunch(
    // 광고 아이디 (빈값 사용시 PlugIn에서 추출)
    String advertisingId, 
    // 해더 표시 여부
    bool allowHeader, 
    // 해더 타이틀
    String headerTitle,
    // 해더의 왼쪽에 표시되는 뒤로가기 버튼('<') 표시 여부 
    bool allowBackButton, 
    // 해더의 오른쪽에 표시되는 닫기('X') 표시 여부
    bool allowCloseButton
)

class AddOnResult {
    // 성공 여부
    final bool success;
    // 성공 및 실패 메시지
    final String? message;
}

// usage
import 'package:flutter_treasureislandx_addon/flutter_treasureisland_addon.dart';
..
..
Future<void> launch() async {
    final result = await FlutterTreasureislandAddon().comicsLaunch(
        // 광고 아이디
        '00000000-0000-0000-0000-000000000000',
        // 해더 표시 여부
        true,
        // 해더 타이틀
        '보물섬',
        // 해더의 왼쪽에 표시되는 뒤로가기 버튼('<') 표시 여부  
        false,
        // 해더의 오른쪽에 표시되는 닫기('X') 표시 여부
        true,
    );
    print("comicsLaunch { success: ${result.success}, message: ${result.message} }");
  }
..
..
```
{% endcode %}

***

#### Options

🎈**advertisingId: String(optional)**

&#x20;ANDROID/iOS ADID(IDFA)를 설정합니다.

**✓ 설정이 없을 경우 Package에서 별도 추출하여 사용합니다.**

| Name            | Type   | Description |
| --------------- | ------ | ----------- |
| `advertisingId` | string | 광고 식별자      |

***

**🎈allowHeader: boolean(optional)**

**✓ 해더 표시 여부를 설정합니다.**

| Name          | Type    | Description |
| ------------- | ------- | ----------- |
| `allowHeader` | boolean | 해더 노출 여부 설정 |

**🎈headerTitle: string(optional)**

**✓ 해더의 타이틀을 설정합니다.**

| Name          | Type   | Description |
| ------------- | ------ | ----------- |
| `headerTitle` | string | 해더 타이틀      |

**🎈allowBackButton: boolean**

**✓ 해더 왼쪽에 표시되는 뒤로가기('<') 버튼의 표시 여부를 설정합니다.**

| Name              | Type    | Description   |
| ----------------- | ------- | ------------- |
| `allowBackButton` | boolean | Back 버튼 노출 유무 |

**🎈allowCloseButton: boolean**

**✓ 해더 오른쪽에 표시되는 닫기('X')  버튼의 표시 여부를 설정합니다.**

| Name               | Type    | Description     |
| ------------------ | ------- | --------------- |
| `allowCloseButton` | boolean | Close  버튼 노출 여부 |




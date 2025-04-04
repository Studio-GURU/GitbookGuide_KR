---
description: 보물섬 ReactNative-PlugIn을 사용하여 보물섬 메인화면을 실행 방법에 대해 안내합니다.
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
### Package 초기화

Package Initialize

<mark style="color:red;">**✓**</mark> <mark style="color:red;">**Membership:Basic**</mark>
{% endstep %}

{% step %}
### 화면 호출

**comicsLaunch ⇨ callback(ITaskListener\<boo>);**
{% endstep %}
{% endstepper %}

***

## Namespace

iOS / Android 별도의 Namespace를 사용합니다.

**✓ iOS** → **TreasureIslandXPlugin.iOS**

**✓ Android** → **TreasureIslandXPlugin.Android**

{% code lineNumbers="true" %}
```csharp
#if UNITY_IOS
using TreasureIslandXPlugin.iOS;
#elif UNITY_ANDROID
using TreasureIslandXPlugin.Android;
#endif
```
{% endcode %}

## Callback

모든 함수는 ITaskListener\<T> 결과를 반환합니다.

**✓ ITaskListener\<T> callback**

{% code lineNumbers="true" %}
```csharp
// callback
public interface ITaskListener<T>
{
    void OnSuccess(T result);
    void OnFailure(string message);
}
```
{% endcode %}

## Package 초기화 하기

보물섬 Unity-Package 사용을 위해 초기화를 진행합니다.

{% hint style="success" %}
Pacake 구동 이전에 초기화가 진행되어야 합니다.

***

최신 버전 사용을 권항하며, [release.md](../flutter/release.md "mention")를 통해 최신 버전을 확인 하세요.

추가 기능 사용을 위해 추가 모듈의 설치가 필요할 수 있습니다.
{% endhint %}

### InitModel(entity) 설정

{% code lineNumbers="true" %}
```csharp
public InitModel(
    string appId,
    string appSecret,
    Membership membership,
    bool allowLog,
    Environment environment,
    NotificationOptionModel notificationOption,
    StatusbarOptionModel statusbarOption
)
```
{% endcode %}

<table><thead><tr><th width="300">Module Name</th><th width="122">Type</th><th width="147">Description</th><th>Etc</th></tr></thead><tbody><tr><td><code>Membership</code></td><td>enum</td><td>회원 정책 설정</td><td><mark style="color:red;"><strong>Basic</strong></mark> / Channeling</td></tr><tr><td><code>Environment</code></td><td>enum</td><td>접속 환경 설정</td><td>default : Live</td></tr><tr><td><code>NotificationOptionModel</code></td><td>data class</td><td>상태창 색상 설정 </td><td>Only Android</td></tr><tr><td><code>StatusbarOptionModel</code></td><td>data class</td><td>푸시알림 설정</td><td>Only Android</td></tr></tbody></table>

### StatusbarOptionModel

<pre class="language-csharp" data-line-numbers><code class="lang-csharp">// define
public class StatusbarOptionModel {
  // StatusBar 색상을 설정 합니다.색상 HEX값을 사용합니다. #FFFFFF
  public string statusbarColor;
  // true: StatusBar 요소의 색상이 밝게 표시 됩니다.(어두운 배경일 경우 사용)
  // false: StatusBar 요소의 색상이 어둡게 표시 됩니다.(밝은 배경일 경우 사용)
  public bool isWindwoLight = false;  
}

// usage
<strong>#if UNITY_IOS
</strong>TreasureIslandXPlugin.iOS.StatusbarOptionModel model = new(
  channelName: "보물섬",
  notificationIconName: "app_icon"
);
<strong>#elif UNITY_ANDROID
</strong>TreasureIslandXPlugin.Android.StatusbarOptionModel model = new(
  channelName: "보물섬",
  notificationIconName: "app_icon"
);
<strong>#endif
</strong></code></pre>

### NotificationOptionModel

<pre class="language-csharp" data-line-numbers><code class="lang-csharp">// define
public class NotificationOptionModel {
  // 푸시알림의 채널명을 설정합니다.
  // 별도 설정이 없는 경우 기본값인 '보물섬'으로 표시됩니다.
  public string channelName;
  // 푸시알림에 표시되는 아이콘 리소스를 설정합니다.
  // 확장자를 제외한 파일명
  public string notificationIconName;  
}

// usage
<strong>#if UNITY_IOS
</strong>TreasureIslandXPlugin.iOS.NotificationOptionModel model = new(
  channelName: "보물섬",
  notificationIconName: "app_icon"
);
<strong>#elif UNITY_ANDROID
</strong>TreasureIslandXPlugin.Android.NotificationOptionModel model = new(
  channelName: "보물섬",
  notificationIconName: "app_icon"
);
<strong>#endif
</strong></code></pre>

### ComicsScript.Initialize

| Name                 | Value                                                                 |
| -------------------- | --------------------------------------------------------------------- |
| `appId`              | 연동앱의 고유 식별자                                                           |
| `appSecret`          | 연동앱의 고유 식별자 검증키                                                       |
| `membership`         | 연동앱의 회원 정책 설정(<mark style="color:red;">**Basic**</mark> / Channeling) |
| `allowDebug`         | 로그 출력 여부 (optional / **default: false**)                              |
| `statusBarConfig`    | 상태창 색상 설정(optional / **only android**)                                |
| `notificationConfig` | 푸시 알림(기다무) 설정(optional / **only android**)                            |
| `environment`        | 접속 환경(optional / **default: Live**)                                   |

{% hint style="info" %}
고유 식별자 및 고유 식별자 검증키는 영업팀을 통해 별도 전달 됩니다.&#x20;
{% endhint %}

<pre class="language-csharp" data-line-numbers><code class="lang-csharp">using UnityEngine;
<strong>#if UNITY_IOS
</strong><strong>using TreasureIslandXPlugin.iOS;
</strong><strong>#elif UNITY_ANDROID
</strong><strong>using TreasureIslandXPlugin.Android;
</strong><strong>#endif
</strong>public class ButtonInitScript : MonoBehaviour
{
    public void OnClickButton() {        
        Membership membership = Membership.Basic;
        Environment environment = Environment.Live;
        InitModel entity = new(
            appId: "{발급받은 appId}",
            appSecret: "{발급받은 appSecret}",
            membership: membership,
            allowLog: true,
            environment: environment,
            notificationOption: new NotificationOptionModel(
                channelName: "보물섬",
                notificationIconName: "app_icon"                          
            ),
            statusbarOption: new StatusbarOptionModel(
                statusbarColor: "#FFFFFF",
                isWindwoLight: false
            )
        );
<strong>        TaskListenerImplementation taskImplementation = new();
</strong><strong>        ComicsScript.Initialize(entity: entity, callback: taskImplementation);
</strong>    }

<strong>    public class TaskListenerImplementation : ITaskListener&#x3C;bool>
</strong>    {
        public void OnSuccess(bool result)
        {
            Debug.Log("Initialization Successful: " + result);
        }

        public void OnFailure(string message)
        {
            Debug.Log("Initialization Failed: " + message);
        }
    }
}
</code></pre>

***

## 화면 호출 하기

### ComicsScript.Launch

<pre class="language-csharp" data-line-numbers><code class="lang-csharp">// define
public class LaunchModel{
    // 광고 아이디 (빈값 사용시 Package에서 추출)
    public string advertisingId;
    // 해더 표시 여부
    public bool allowHeader;
    // 해더 타이틀
    public string headerTitle;
    // 해더의 왼쪽에 표시되는 뒤로가기 버튼('&#x3C;') 표시 여부 
    public bool allowBackButton;
    // 해더의 오른쪽에 표시되는 닫기('X') 표시 여부
    public bool allowCloseButton;
}

// usage
<strong>using UnityEngine;
</strong><strong>#if UNITY_IOS
</strong><strong>using TreasureIslandXPlugin.iOS;
</strong><strong>#elif UNITY_ANDROID
</strong><strong>using TreasureIslandXPlugin.Android;
</strong><strong>#endif
</strong>public class ButtonLaunchScript : MonoBehaviour
{
    public void OnClickButton()
    {
<strong>        LaunchModel entity = new(
</strong>            advertisingId: "0000-0000-0000",
            allowHeader: false,
            headerTitle: "",
            allowBackButton: false,
            allowCloseButton: false
        );
<strong>        TaskListenerImplementation taskImplementation = new();
</strong><strong>        ComicsScript.Launch(entity: entity, callback: taskImplementation);
</strong>    }

<strong>    public class TaskListenerImplementation : ITaskListener&#x3C;bool>
</strong>    {
        public void OnSuccess(bool result)
        {
            Debug.Log("Launch Successful: " + result);
        }

        public void OnFailure(string message)
        {
            Debug.Log("Launch Failed: " + message);
        }
    }
}

</code></pre>

***

#### Options

🎈**advertisingId: String(optional)**

&#x20;ANDROID/iOS ADID(IDFA)를 설정합니다.

**✓ 설정이 없을 경우 PlugIn에서 별도 추출하여 사용합니다.**

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








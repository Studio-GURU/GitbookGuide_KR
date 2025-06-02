---
description: 보물섬 ReactNative-Package을 사용하여 보물섬 메인화면을 실행 방법에 대해 안내합니다.
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

보물섬 서비스 이용을 위해서는 :link:[start.md](start.md "mention")의 기본 설정이 완료 되어야 합니다.

***

## 연동 순서

{% stepper %}
{% step %}
### Package 초기화

**Package Initialize**

<mark style="color:red;">**✓**</mark> <mark style="color:red;">**Membership:Channeling**</mark>
{% endstep %}

{% step %}
### 프로필 설정

Profile with <mark style="color:red;">**SignKey & Register**</mark>
{% endstep %}

{% step %}
### 화면 호출

**comicsLaunch ⇨ (success, message);**
{% endstep %}
{% endstepper %}

***

## Package 초기화 하기

보물섬 ReactNative-Package 사용을 위해 초기화를 진행합니다.

{% hint style="success" %}
Application 시작시 초기화를 진행합니다.

***

최신 버전 사용을 권항하며, [release.md](release.md "mention")를 통해 최신 버전을 확인 하세요.

추가 기능 사용을 위해 추가 모듈의 설치가 필요할 수 있습니다.
{% endhint %}

### module import

```typescript
import {
  Environment,
  Membership,
  NotificationConfig,
  comicsInitialize,  
  comicsLaunch,
  comicsProfile,
} from 'treasurecomics-addon';
```

<table><thead><tr><th width="212">Module Name</th><th width="129">Type</th><th>Description</th><th>Etc</th></tr></thead><tbody><tr><td><code>Environment</code></td><td>enum</td><td>접속 환경 설정</td><td>default : Live</td></tr><tr><td><code>Membership</code></td><td>enum</td><td>회원 정책 설정</td><td>Basic / <mark style="color:red;"><strong>Channeling</strong></mark></td></tr><tr><td><code>NotificationConfig</code></td><td>data class</td><td>푸시알림 설정</td><td>Only Android</td></tr><tr><td><code>comicsWithInitialize</code></td><td>function</td><td>초기화 함수</td><td></td></tr></tbody></table>

### comicsInitialize

| Name                 | Value                                                                 |
| -------------------- | --------------------------------------------------------------------- |
| `appId`              | 연동앱의 고유 식별자                                                           |
| `appSecret`          | 연동앱의 고유 식별자 검증키                                                       |
| `membership`         | 연동앱의 회원 정책 설정(Basic / <mark style="color:red;">**Channeling**</mark>) |
| `allowDebug`         | 로그 출력 여부 (optional / default: false)                                  |
| `notificationConfig` | 푸시 알림(기다무) 설정(optional / only android)                                |
| `environment`        | 접속 환경(optional / default: Live)                                       |

{% hint style="info" %}
고유 식별자 및 고유 식별자 검증키는 영업팀을 통해 별도 전달 됩니다.&#x20;
{% endhint %}

<pre class="language-typescript" data-line-numbers><code class="lang-typescript">import {
  Environment,
  Membership,
  NotificationConfig,
  comicsInitialize,  
  comicsLaunch,
  comicsProfile,
} from 'treasurecomics-addon';

function App(): React.JSX.Element {
  useEffect(() => {
    const init = async () => {
      console.log('App mounted');
      const notificationConfig = new NotificationConfig(
        '보물섬X리액트', 
        require('./assets/icon/ic_notify.png')
      );
      comicsWithInitialize(
        // appId
        '{발급받은 appId}',
        // appSecret
        '{발급받은 appSecret}',
        // membership
<strong>        Membership.Channeling
</strong>        // allowDebug
        true,
        // NotificationConfig
        notificationConfig,
        // environment
<strong>        Environment.Live
</strong>      )
      .then((result: any) => console.log(`comicsWithInitialize::Result => ${result}`))
      .catch((error: any) => console.error('comicsWithInitialize::Failed:', error));
    };
    init();
  }, []);
</code></pre>

### NotificationConfig

```typescript
// define
class NotificationConfig {
  // 푸시알림의 채널명을 설정합니다.
  // 별도 설정이 없는 경우 기본값인 '보물섬'으로 표시됩니다.
  channelName: string;
  // 푸시알림에 표시되는 아이콘 리소스를 설정합니다.
  // require('ImagePath')
  smallIconResourceId: number;
}

// usage
const notificationConfig = new NotificationConfig(
  '보물섬', 
  require('./assets/icon/ic_notify.png')
);
```

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

```typescript
// define
function comicsProfile(
  // signkey(필수)
  signKey: string, 
  // 성별(옵션)
  gender: Gender | null | undefined = undefined,
  // 태어난 연도(옵셥)
  birthYear: number | null | undefined = undefined
)

// usage
comicsProfile(signKey, Gender.MALE, 2000)
    .then((result: any) => console.log(`comicsProfile => { success: ${result.isSuccess}, message: ${result.message} }`))
    .catch((error: any) => console.error('comicsProfile::Failed:', error.message));

```

***

## 화면 호출 하기

## comicsLaunch

{% code lineNumbers="true" %}
```typescript
// define
function comicsLaunch(
  // 광고 아이디(optional)
  advertisingId: string = '',
  // 해더 표시 여부(optional)
  allowHeader: boolean = false,
  // 해더의 타이틀(optional)
  headerTitle: string = '',
  // 해더의 왼쪽에 표시되는 뒤로가기 버튼('<') 표시 여부 
  allowBackButton: boolean = false,
  // 해더의 오른쪽에 표시되는 닫기('X') 표시 여부
  allowCloseButton: boolean = false
)

// usage
import { comicsLaunch } from 'treasurecomics-addon';
..
..
const handleButtonPress = () => {
    comicsLaunch()
        .then((result: any) => console.log(`comicsLaunch::Success => ${result}`))
        .catch((error: any) => console.error('comicsLaunch::Failed:', error));
};
..
..
```
{% endcode %}

***

### Options

#### 🎈advertisingId: String(optional)

&#x20;ANDROID/iOS ADID(IDFA)를 설정합니다.

**✓ 설정이 없을 경우 Package에서 별도 추출하여 사용합니다.**

| Name            | Type   | Description |
| --------------- | ------ | ----------- |
| `advertisingId` | string | 광고 식별자      |

***

#### 🎈allowHeader: boolean(optional)

**✓ 해더 표시 여부를 설정합니다.**

| Name          | Type    | Description |
| ------------- | ------- | ----------- |
| `allowHeader` | boolean | 해더 노출 여부 설정 |

#### 🎈headerTitle: string(optional)

**✓ 해더의 타이틀을 설정합니다.**

| Name          | Type   | Description |
| ------------- | ------ | ----------- |
| `headerTitle` | string | 해더 타이틀      |

#### 🎈allowBackButton: boolean

**✓ 해더 왼쪽에 표시되는 뒤로가기('<') 버튼의 표시 여부를 설정합니다.**

| Name              | Type    | Description   |
| ----------------- | ------- | ------------- |
| `allowBackButton` | boolean | Back 버튼 노출 유무 |

#### 🎈allowCloseButton: boolean

**✓ 해더 오른쪽에 표시되는 닫기('X')  버튼의 표시 여부를 설정합니다.**

| Name               | Type    | Description     |
| ------------------ | ------- | --------------- |
| `allowCloseButton` | boolean | Close  버튼 노출 여부 |








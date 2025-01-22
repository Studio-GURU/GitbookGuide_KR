---
icon: user-group
description: 보물섬 ReactNative-PlugIn을 사용하여 보물섬 메인화면을 실행 방법에 대해 안내합니다.
---

# 채널회원 연동

{% hint style="success" %}
전달된 파트너사의 회원정보를 통해 보물섬 계정을 생성합니다.&#x20;

:heavy\_check\_mark: **파트너사의 앱의 운영 방식에 따라 로그인 여부 확인이 가능한 기능 구현이 필요 할 수 있습니다.**
{% endhint %}

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>채널링 서비스 플로우</p></figcaption></figure>

***

## 준비 사항

보물섬 서비스 이용을 위해서는 :link:[start.md](start.md "mention")의 기본 설정이 완료 되어야 합니다.

***

## 연동 순서

1. Plugin(SDK) 초기화 하기(Initialize)
2. 프로필 설정하기(Profile)
3. 화면 호출 하기(Launch)

***

## PlugIn 초기화 하기

보물섬 ReactNative-PlugIn 사용을 위해 초기화를 진행합니다.

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
  StatusBarConfig,
  NotificationConfig,
  comicsInitialize,  
  comicsLaunch,
  comicsProfile,
} from 'react-treasureisland-addon';
```

<table><thead><tr><th width="248">Module Name</th><th width="129">Type</th><th>Description</th><th>Etc</th></tr></thead><tbody><tr><td><code>Environment</code></td><td>enum</td><td>접속 환경 설정</td><td>default : Live</td></tr><tr><td><code>Membership</code></td><td>enum</td><td>회원 정책 설정</td><td>Basic / <strong>Channeling</strong></td></tr><tr><td><code>StatusBarConfig</code></td><td>data class</td><td>상태창 색상 설정 </td><td>Only Android</td></tr><tr><td><code>NotificationConfig</code></td><td>data class</td><td>푸시알림 설정</td><td>Only Android</td></tr><tr><td><code>comicsWithInitialize</code></td><td>function</td><td>초기화 함수</td><td></td></tr></tbody></table>

### comicsInitialize

| Name                 | Value                                  |
| -------------------- | -------------------------------------- |
| `appId`              | 연동앱의 고유 식별자                            |
| `appSecret`          | 연동앱의 고유 식별자 검증키                        |
| `membership`         | 연동앱의 회원 정책 설정(Basic / **Channeling**)  |
| `allowDebug`         | 로그 출력 여부 (optional / default: false)   |
| `statusBarConfig`    | 상태창 색상 설정(optional / only android)     |
| `notificationConfig` | 푸시 알림(기다무) 설정(optional / only android) |
| `environment`        | 접속 환경(optional / default: Live)        |

{% hint style="info" %}
고유 식별자 및 고유 식별자 검증키는 영업팀을 통해 별도 전달 됩니다.&#x20;
{% endhint %}

<pre class="language-typescript" data-line-numbers><code class="lang-typescript">import {
  Environment,
  Membership,
  StatusBarConfig,
  NotificationConfig,
  comicsInitialize,  
  comicsLaunch,
  comicsProfile,
} from 'react-treasureisland-addon';

function App(): React.JSX.Element {
  useEffect(() => {
    const init = async () => {
      console.log('App mounted');
      const statusBarConfig = new StatusBarConfig('#FFFFFF', false);
      const notificationConfig = new NotificationConfig(
        '보물섬X리액트', 
        require('./assets/icon/ic_notify.png')
      );
      comicsWithInitialize(
        // appId
        'harustory',
        // appSecret
        'haruSecret',
        // membership
<strong>        Membership.Channeling
</strong>        // allowDebug
        true, 
        // StatusBarConfig
        statusBarConfig,
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

### StatusBarConfig

```typescript
// define
class StatusBarConfig {
  // StatusBar 색상을 설정 합니다.색상 HEX값을 사용합니다. #FFFFFF
  statusBarColor: string;
  // true: StatusBar 요소의 색상이 밝게 표시 됩니다.(어두운 배경일 경우 사용)
  // false: StatusBar 요소의 색상이 어둡게 표시 됩니다.(밝은 배경일 경우 사용)
  isWindowLight: boolean;
}

// usage
const statusBarConfig = new StatusBarConfig('#FFFFFF', false);
```

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

1. "**SignKey**" 생성
2. 생성된 **SignKey**를 **Profile** 정보를 "**comicsProfile**" 함수를 통해 전달

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

:heavy\_check\_mark: $timeStamp$nonce$암호화된User식별자

위 값을 HmacSHA256 Hash -> Base64 Url Encodeing을 통해 Signature를 생성합니다.

***

* timeStamp -> unix timestamp seconds
* nonce -> 문자열 32자(임의로 생성된 문자열 32자)
* user 식별자 -> 회원 구분이 가능한 식별자
{% endhint %}

<table data-full-width="false"><thead><tr><th width="127">Name</th><th width="141">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>sign</code></td><td>string</td><td><p><code>timestmap.nonce.encryptedUserId.signature</code></p><hr><p> <mark style="background-color:red;">timestamp, nonce, userid  값은 <strong>signature 생성에 사용된 값</strong>을 전달 합니다.</mark></p></td></tr></tbody></table>

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
import { comicsLaunch } from 'react-treasureisland-addon';
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

:heavy\_check\_mark: 설정이 없을 경우 PlugIn에서 별도 추출하여 사용합니다.

| Name            | Type   | Description |
| --------------- | ------ | ----------- |
| `advertisingId` | string | 광고 식별자      |

***

#### 🎈allowHeader: boolean(optional)

:heavy\_check\_mark: 해더 표시 여부를 설정합니다.

| Name          | Type    | Description |
| ------------- | ------- | ----------- |
| `allowHeader` | boolean | 해더 노출 여부 설정 |

#### 🎈headerTitle: string(optional)

:heavy\_check\_mark: 해더의 타이틀을 설정합니다.

| Name          | Type   | Description |
| ------------- | ------ | ----------- |
| `headerTitle` | string | 해더 타이틀      |

#### 🎈allowBackButton: boolean

:heavy\_check\_mark: 해더 왼쪽에 표시되는 뒤로가기('<') 버튼의 표시 여부를 설정합니다.

| Name              | Type    | Description   |
| ----------------- | ------- | ------------- |
| `allowBackButton` | boolean | Back 버튼 노출 유무 |

#### 🎈allowCloseButton: boolean

:heavy\_check\_mark: 해더 오른쪽에 표시되는 닫기('X')  버튼의 표시 여부를 설정합니다.

| Name               | Type    | Description     |
| ------------------ | ------- | --------------- |
| `allowCloseButton` | boolean | Close  버튼 노출 여부 |








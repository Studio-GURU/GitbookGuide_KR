---
icon: laptop-code
description: 보물섬 ReactNatvie-PlugIn 초기화 방법에 대해 안내합니다.
---

# 보물섬 서비스

{% hint style="success" %}
Application 시작시 초기화를 진행합니다.

***

최신 버전 사용을 권항하며, [release.md](../release.md "mention")를 통해 최신 버전을 확인 하세요.

추가 기능 사용을 위해 추가 모듈의 설치가 필요할 수 있습니다.
{% endhint %}

***

## PlugIn 초기화 하기

보물섬 ReactNative-PlugIn 사용을 위해 초기화를 진행합니다.

### module import

```typescript
import {
  Environment,
  StatusBarConfig,
  NotificationConfig,
  comicsWithInitialize,
} from 'react-treasureisland-addon';
```

<table><thead><tr><th width="248">Module Name</th><th width="129">Type</th><th>Description</th><th>Etc</th></tr></thead><tbody><tr><td><code>Enviroment</code></td><td>enum</td><td>접속 환경 설정</td><td>default : Live</td></tr><tr><td><code>StatusBarConfig</code></td><td>data class</td><td>상태창 색상 설정 </td><td>Only Android</td></tr><tr><td><code>NotificationConfig</code></td><td>data class</td><td>푸시알림 설정</td><td>Only Android</td></tr><tr><td><code>comicsWithInitialize</code></td><td>function</td><td>초기화 함수</td><td></td></tr></tbody></table>

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

```typescript
import {
  Environment,
  StatusBarConfig,
  NotificationConfig,
  comicsWithInitialize,
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
        // allowDebug
        true, 
        // StatusBarConfig
        statusBarConfig,
        // NotificationConfig
        notificationConfig,
        // environment
        Environment.Live
      )
      .then((result: any) => console.log(`comicsWithInitialize::Result => ${result}`))
      .catch((error: any) => console.error('comicsWithInitialize::Failed:', error));
    };
    init();
  }, []);
```

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




---
icon: laptop-code
description: 보물섬 Flutter-PlugIn 초기화 방법에 대해 안내합니다.
---

# 보물섬 서비스

{% hint style="success" %}
Application 시작시 초기화를 진행합니다.

***

최신 버전 사용을 권항하며, [undefined.md](../undefined.md "mention")를 통해 최신 버전을 확인 하세요.

추가 기능 사용을 위해 추가 모듈의 설치가 필요할 수 있습니다.
{% endhint %}

***

## PlugIn 초기화 하기

보물섬 Flutter-PlugIn 사용을 위해 초기화를 진행합니다.

### module import

```dart
import 'package:flutter_treasureisland_addon/flutter_treasureisland_addon.dart';
import 'package:flutter_treasureisland_addon/models/environment_config.dart';
import 'package:flutter_treasureisland_addon/models/statusbar_config.dart';
import 'package:flutter_treasureisland_addon/models/notification_config.dart';
```

<table><thead><tr><th width="300">Module Name</th><th width="129">Type</th><th>Description</th><th>Etc</th></tr></thead><tbody><tr><td><code>environment_config.dart</code></td><td>enum</td><td>접속 환경 설정</td><td>default : Live</td></tr><tr><td><code>statusbar_config.dart</code></td><td>data class</td><td>상태창 색상 설정 </td><td>Only Android</td></tr><tr><td><code>notification_config.datd</code></td><td>data class</td><td>푸시알림 설정</td><td>Only Android</td></tr></tbody></table>

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

```dart
import 'package:flutter_treasureisland_addon/flutter_treasureisland_addon.dart';
import 'package:flutter_treasureisland_addon/models/environment_config.dart';
import 'package:flutter_treasureisland_addon/models/statusbar_config.dart';
import 'package:flutter_treasureisland_addon/models/notification_config.dart';

// 앱의 시작점에 아래 코드를 참고하여 초기화를 진행합니다.
Future<void> initComics() async {
    final statusbarConfig = StatusbarConfig(statusBarColor: "#FFFF00", isWindowLight: false);
    final notificationConfig = NotificationConfig(channelName: "플러터", smallIconResourceName: "ic_flutter_notify");
    final result = await FlutterTreasureislandAddon().comicsWithInitialize(
        'harustory',
        'haruSecret',
        true,
        statusbarConfig,
        notificationConfig,
        Environment.Develop,
    );
    print("comicsWithInitialize { success: ${result.success}, message: ${result.message} }");
  }
```

### StatusBarConfig

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

### NotificationConfig

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




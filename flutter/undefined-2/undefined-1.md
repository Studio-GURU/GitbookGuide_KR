---
description: 보물섬 ReactNative-PlugIn을 사용하여 보물섬 메인화면을 실행 방법에 대해 안내합니다.
icon: user-group
---

# 채널회원 연동

{% hint style="success" %}
전달된 파트너사의 회원정보를 통해 보물섬 계정을 생성합니다.&#x20;

:heavy\_check\_mark: **파트너사의 앱의 운영 방식에 따라 로그인 여부 확인이 가능한 기능 구현이 필요 할 수 있습니다.**
{% endhint %}

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption><p>채널링 서비스 플로우</p></figcaption></figure>

***

## 준비 사항

보물섬 서비스 이용을 위해서는 :link:[undefined-1.md](../../react-native/undefined-1.md "mention") :arrow\_forward: :link:[undefined-2](../../react-native/undefined-2/ "mention")의 기본 설정이 완료 되어야 합니다.

***

## comicsLaunchWithStandard

```dart
// define
Future<AddOnResult> comicsLaunchWithStandard(
    // 연동 회원키(변경되지 않는 고유키값) *필수항목*
    String userId,
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
import 'package:flutter_treasureisland_addon/flutter_treasureisland_addon.dart';
..
..
Future<void> launchWithChanneling() async {
    final result = await FlutterTreasureislandAddon().comicsLaunchWithChanneling(
        // 연동 회원키(변경되지 않는 고유키값) *필수항목*
        'userId'        
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
    print("comicsLaunchStandard { success: ${result.success}, message: ${result.message} }");
  }
..
..

```

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










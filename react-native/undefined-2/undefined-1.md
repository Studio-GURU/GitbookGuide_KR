---
icon: user-group
description: 보물섬 ReactNative-PlugIn을 사용하여 보물섬 메인화면을 실행 방법에 대해 안내합니다.
---

# 채널회원 연동

{% hint style="success" %}
전달된 파트너사의 회원정보를 통해 보물섬 계정을 생성합니다.&#x20;

:heavy\_check\_mark: **파트너사의 앱의 운영 방식에 따라 로그인 여부 확인이 가능한 기능 구현이 필요 할 수 있습니다.**
{% endhint %}

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption><p>채널링 서비스 플로우</p></figcaption></figure>

***

## 준비 사항

보물섬 서비스 이용을 위해서는 :link:[undefined-1.md](../undefined-1.md "mention") :arrow\_forward: :link:[.](./ "mention")의 기본 설정이 완료 되어야 합니다.

***

## comicsLaunchWithStandard

```typescript
// define
function comicsLaunchWithChanneling(
  // 연동 회원키(변경되지 않는 고유키값) *필수항목*
  userId: string,
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
import { comicsLaunchWithChanneling } from 'react-treasureisland-addon';
..
..
const handleButtonPressWithChanneling = () => {
    comicsLaunchWithChanneling('고유한 유저 식별자')
    .then((result: any) => console.log(`comicsLaunchWithChanneling::Success => ${result}`))
    .catch((error: any) => console.error('comicsLaunchWithChanneling::Failed:', error));
};

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










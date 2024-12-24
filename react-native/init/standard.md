---
icon: user
description: 보물섬 ReactNative-PlugIn을 사용하여 보물섬 메인화면을 실행 방법에 대해 안내합니다.
---

# 채널회원 미연동

{% hint style="success" %}
파트너사의 회원이 존재하지 않거나, 보물섬에서 제공하는 자체 계정을 사용하고자 하는 경우

***

:heavy\_check\_mark: **보물섬 자체 계정의 경우 파트너사에서 사용중인 계정과 연동되지 않습니다.**
{% endhint %}

<figure><img src="../../.gitbook/assets/스크린샷 2024-08-22 오후 2.05.51.png" alt=""><figcaption><p>보물섬 회원 플로우</p></figcaption></figure>

***

## 준비 사항

보물섬 서비스 이용을 위해서는 :link:[start.md](../start.md "mention") :arrow\_forward: :link:[.](./ "mention")의 기본 설정이 완료 되어야 합니다.

***

## comicsLaunchWithStandard

```typescript
// define
function comicsLaunchWithStandard(
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
import { comicsLaunchWithStandard } from 'react-treasureisland-addon';
..
..
const handleButtonPressWithStandard = () => {
    comicsLaunchWithStandard()
        .then((result: any) => console.log(`comicsLaunchWithStandard::Success => ${result}`))
        .catch((error: any) => console.error('comicsLaunchWithStandard::Failed:', error));
};
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










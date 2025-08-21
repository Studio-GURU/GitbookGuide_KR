---
description: Android & iOS Javascript interface
icon: comments
---

# 자바스크립트 통신

## 공통 정보 <a href="#common" id="common"></a>

✓ 웹에서 네이티브로 요청하는 Javascript interface 정보입니다.

**✓ BridgeName → "treasureComics"**

✓ Javascript interface 호출은 "postMessage" 메서드만 사용하며, 미리 정의한 JSONObject 값으로 전달됩니다.

{% hint style="danger" %}
**iOS의 경우 대상 웹사이트가 "UTF-8" 인코딩을 사용해야 합니다.**
{% endhint %}

{% code lineNumbers="true" %}
```json
{
    "request": "$request-method",
    "parameter" : {
        $request-method-parameter-object
    },	
    "callback": "$callback-function-name"
}
```
{% endcode %}

<table><thead><tr><th width="170">name</th><th width="138">data</th><th>description</th></tr></thead><tbody><tr><td>request(필수)</td><td>String</td><td>호출할 함수명</td></tr><tr><td>parameter(옵션)</td><td>JSON Object</td><td>호출 함수에 전달되는 파라미터 정보</td></tr><tr><td>callback(옵션)</td><td>String</td><td>호출 결과 전달을 위한 콜백 함수명 → callback을 통해 전달되는 값은 기능별로 설정 됩니다.</td></tr></tbody></table>

***

### Require

{% content-ref url="../../../web-view/webview-config/javascript/undefined.md" %}
[undefined.md](../../../web-view/webview-config/javascript/undefined.md)
{% endcontent-ref %}

✓ 웹 브라우져를 새창으로 오픈해야 하는 경우 웹에서 네이티브에 전달하는 메시지입니다.

✓ 앱스토어 및 CP ( 웹툰, 웹소설 ) 제공자의 정책 변경에 유연하게 대응하기 위해, 보물섬에서 인앱 또는 아웃브라우저를 효과적으로 선택 · 운영하기 위해 필요한 작업입니다.

{% content-ref url="../../../web-view/webview-config/javascript/undefined-1.md" %}
[undefined-1.md](../../../web-view/webview-config/javascript/undefined-1.md)
{% endcontent-ref %}

✓ 보물섬 내부에서 기기 광고 식별값을 수집해야 하는 경우 웹에서 네이티브에 전달하는 메세지입니다.

✓ AOS의 경우 ADID, IOS일 경우 IDFA를 전달주시면 됩니다.



### Optional

{% content-ref url="../../../web-view/webview-config/javascript/undefined-2.md" %}
[undefined-2.md](../../../web-view/webview-config/javascript/undefined-2.md)
{% endcontent-ref %}

✓ 보물섬 내부에서 추가 정보를 수집해야 하는 경우 웹에서 네이티브에 전달하는 메세지입니다.

✓ 보물섬에서 추가 데이터가 필요할 시 요청하며, 협의된 데이터를 전달 주시면 됩니다.

{% content-ref url="../../../web-view/webview-config/javascript/text-to-speech-tts.md" %}
[text-to-speech-tts.md](../../../web-view/webview-config/javascript/text-to-speech-tts.md)
{% endcontent-ref %}

✓ 보물섬 웹소설의 TTS 기능을 사용하기 위한 가이드입니다.


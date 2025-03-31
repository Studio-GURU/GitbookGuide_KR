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


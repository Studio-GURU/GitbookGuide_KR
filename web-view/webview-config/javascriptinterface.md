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

## 외부 웹 브라우져 오픈 요청 ( Require ) <a href="#window.open" id="window.open"></a>

✓ 웹 브라우져를 새창으로 오픈해야 하는 경우 웹에서 네이티브에 전달하는 메시지입니다.

✓ 앱스토어 및 CP ( 웹툰, 웹소설 ) 제공자의 정책 변경에 유연하게 대응하기 위해, 보물섬에서 인앱 또는 아웃브라우저를 효과적으로 선택 · 운영하기 위해 필요한 작업입니다.

| request           |
| ----------------- |
| openOutWebBrowser |

| parameter | description           |
| --------- | --------------------- |
| openUrl   | 웹 브라우져를 통해 접근 하려는 주소값 |

### 웹에서의 호출 예제

{% tabs %}
{% tab title="ANDROID" %}
<pre class="language-javascript" data-line-numbers><code class="lang-javascript">&#x3C;script type="text/javascript">
// 외부 웹브라우져 열기
function openOuterWebBrowser() {
    let request = {
        request: "openOutWebBrowser",
        parameter: {
            openUrl: "https://www.naver.com"
        }
    }
    let message = JSON.stringify(request);
<strong>    treasureComics.postMessage(message.toString());
</strong>}
&#x3C;/script>
</code></pre>
{% endtab %}

{% tab title="iOS" %}
<pre class="language-javascript" data-line-numbers><code class="lang-javascript">&#x3C;script type="text/javascript">
// 외부 웹브라우져 열기
function openOuterWebBrowser() {
    let request = {
        request: "openOutWebBrowser",
        parameter: {
            openUrl: "https://www.naver.com"
        }
    }
    let message = JSON.stringify(request);
<strong>    window.webkit.messageHandlers.treasureComics.postMessage(message.toString());
</strong>}
&#x3C;/script>
</code></pre>
{% endtab %}
{% endtabs %}

***

### 호출 처리

{% hint style="warning" %}
**예제로 작성된 코드로 참고용으로 확인 부탁드립니다.**
{% endhint %}

{% tabs %}
{% tab title="ANDROID" %}
<pre class="language-kotlin" data-line-numbers><code class="lang-kotlin"><strong>WebView.addJavascriptInterface(TreasureKitJavascriptInterface(), "treasureComics")
</strong>
@JavascriptInterface
class TreasureKitJavascriptInterface {
    fun postMessage(message: String) {     
        // message를 JSON-Object로 변환
        // JSONObject -> request
        // JSONObject -> parameter.openUrl
        // requestType에 따라 실행
        JSONObject(contractMessage).let {
            val request = it.getString("request")
            val parameter = it.getJSONObject("parameter")
            val openUrl = parameter.getString("openUrl")
<strong>            if(request == "openOutWebBrowser") {
</strong><strong>                startActivity(Intent(Intent.ACTION_VIEW, Uri.parse(openUrl)))
</strong><strong>            }
</strong>        }
    }
}
</code></pre>
{% endtab %}

{% tab title="iOS" %}
<pre class="language-swift" data-line-numbers><code class="lang-swift">class ViewController: WKScriptMessageHandler {
    ...
    ...
    // userContentController 설정
<strong>    WKWebView.configuration.userContentController.add(self, name: "treasureComics")
</strong>    ...
    ...
    // MARK: - webview content javascript interface message handler
    func userContentController(_ userContentController: WKUserContentController, didReceive message: WKScriptMessage) {
        if message.name == "treasureComics", let messageBody = message.body as? String {
            do {
                // check data
                guard let withData = messageBody.data(using: .utf8) else {
                    return
                }
                // convert json
                guard let json = try JSONSerialization.jsonObject(with: withData, options: .allowFragments) as? [String: AnyObject] else {
                    return
                }
                // make contract
                let request = (json["request"] as? String) ?? ""
                let params = json["parameter"] as? [String: AnyObject]  
                let openUrl = params["openUrl"] as? String
                if request == "openOutWebBrowser" {
<strong>                    onOpenWebBrowser(openUrl: openUrl)
</strong><strong>                }
</strong>            } catch {
                self = WebContentBehavior()
            }
        }
    }
    
    func onOpenWebBrowser(openUrl: String) {
        if let openUri = URL(string: openUrl) {
<strong>            if UIApplication.shared.canOpenURL(openUri) {
</strong><strong>                UIApplication.shared.open(openUri, completionHandler: { (success) in
</strong>                    print("onOpenWebBrowser opened: \(success)")
                })
            }
        }
    }
    ...
    ...
}
</code></pre>


{% endtab %}
{% endtabs %}

***

## 기기 광고 식별값 수집 요청 ( Require ) <a href="#window.open" id="window.open"></a>

✓ 보물섬 내부에서 기기 광고 식별값을 수집해야 하는 경우 웹에서 네이티브에 전달하는 메세지입니다.

✓ AOS의 경우 ADID, IOS일 경우 IDFA를 전달주시면 됩니다.

| request       |
| ------------- |
| getDeviceADID |

### 웹에서의 호출 예제

{% tabs %}
{% tab title="ANDROID" %}
<pre class="language-javascript" data-line-numbers><code class="lang-javascript">&#x3C;script type="text/javascript">
// 광고 식별값 수집
function getDeviceADID() {
    let request = {
        request: "getDeviceADID",
        callback: "$callback-function-name"
    }
    let message = JSON.stringify(request);
<strong>    treasureComics.postMessage(message.toString());
</strong>}
&#x3C;/script>
</code></pre>
{% endtab %}

{% tab title="iOS" %}
<pre class="language-javascript" data-line-numbers><code class="lang-javascript">&#x3C;script type="text/javascript">
// 광고 식별값 수집
function openOuterWebBrowser() {
    let request = {
        request: "getDeviceADID"
    }
    let message = JSON.stringify(request);
<strong>    window.webkit.messageHandlers.treasureComics.postMessage(message.toString());
</strong>}
&#x3C;/script>
</code></pre>
{% endtab %}
{% endtabs %}

### 응답 예제

| parameter                                      | description                                                                                                         |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| <p>{<br>  "deviceADID": "$deviceADID"<br>}</p> | <p>callback으로 전달된 함수에 파라미터 값을 포함하여 호출합니다.<br>JSON 값을 stringfy하여 전달합니다.<br><br>AOS : deviceADID</p><p>IOS : IDFA</p> |

***



## 추가 정보 수집 요청 ( Optional ) <a href="#window.open" id="window.open"></a>

✓ 보물섬 내부에서 추가 정보를 수집해야 하는 경우 웹에서 네이티브에 전달하는 메세지입니다.

✓ 보물섬에서 추가 데이터가 필요할 시 요청하며, 협의된 데이터를 전달 주시면 됩니다.

| request      |
| ------------ |
| getExtraData |

### 웹에서의 호출 예제

{% tabs %}
{% tab title="ANDROID" %}
<pre class="language-javascript" data-line-numbers><code class="lang-javascript">&#x3C;script type="text/javascript">
// 광고 식별값 수집
function getExtraData() {
    let request = {
        request: "getExtraData",
        callback: "$callback-function-name"
    }
    let message = JSON.stringify(request);
<strong>    treasureComics.postMessage(message.toString());
</strong>}
&#x3C;/script>
</code></pre>
{% endtab %}

{% tab title="iOS" %}
<pre class="language-javascript" data-line-numbers><code class="lang-javascript">&#x3C;script type="text/javascript">
// 광고 식별값 수집
function openOuterWebBrowser() {
    let request = {
        request: "getExtraData"
    }
    let message = JSON.stringify(request);
<strong>    window.webkit.messageHandlers.treasureComics.postMessage(message.toString());
</strong>}
&#x3C;/script>
</code></pre>
{% endtab %}
{% endtabs %}

### 응답 예제

| parameter                                                 | description                                                                                                                       |
| --------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| <p>{<br>  "phone" : 01011111111,<br>  "age" : 30<br>}</p> | <p>callback으로 전달된 함수에 파라미터 값을 포함하여 호출합니다.<br>JSON 값을 stringfy하여 전달합니다.<br><br>예시로 작성된 데이터입니다. <br>키 및 데이터는 보물섬과 협의 후 반환해 주세요.</p> |


---
icon: comments
description: Android & iOS Javascript interface
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

<table><thead><tr><th width="170">name</th><th width="138">data</th><th width="144">Required</th><th>description</th></tr></thead><tbody><tr><td>request</td><td>String</td><td>true</td><td>호출할 함수명</td></tr><tr><td>parameter</td><td>JSON Object</td><td>false</td><td>호출 함수에 전달되는 파라미터 정보</td></tr><tr><td>callback</td><td>String</td><td>false</td><td>호출 결과 전달을 위한 콜백 함수명 → callback을 통해 전달되는 값은 기능별로 설정 됩니다.</td></tr></tbody></table>

***

## 외부 웹 브라우져 오픈 요청 <a href="#window.open" id="window.open"></a>

**✓ 웹 브라우져를 새창으로 오픈해야 하는 경우 웹에서 네이티브에 전달하는 메시지입니다.**

| request           |
| ----------------- |
| openOutWebBrowser |

| parameter | description           |
| --------- | --------------------- |
| openUrl   | 웹 브라우져를 통해 접근 하려는 주소값 |

***

### 호출 처리

{% hint style="success" %}
**앱에서 구현이 필요한 부분이며, 참고 가능한 예제 코드입니다.**
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

### 보물섬 웹에서의 호출 예제

{% hint style="danger" %}
**보물섬 웹에서 호출하는 예제입니다. 참고용으로 확인 부탁드립니다.**
{% endhint %}

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

## 기기 광고 식별값 수집 요청 <a href="#window.open" id="window.open"></a>

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
function openOuterWebBrowser() {
    let request = {
        request: "getDeviceADID"
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

| parameter  | description                              |
| ---------- | ---------------------------------------- |
| deviceADID | <p>AOS : deviceADID</p><p>IOS : IDFA</p> |


















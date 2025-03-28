---
hidden: true
icon: js
---

# 기기 광고 식별값 수집 요청(Require)

## 기기 광고 식별값 수집 요청 ( Require ) <a href="#window.open" id="window.open"></a>

✓ 보물섬 내부에서 기기 광고 식별값을 수집해야 하는 경우 웹에서 네이티브에 전달하는 메세지입니다.

✓ AOS의 경우 ADID, IOS일 경우 IDFA를 전달주시면 됩니다.

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

***

### 응답 예제

| parameter                                      | description                                                                                                         |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| <p>{<br>  "deviceADID": "$deviceADID"<br>}</p> | <p>callback으로 전달된 함수에 파라미터 값을 포함하여 호출합니다.<br>JSON 값을 stringfy하여 전달합니다.<br><br>AOS : deviceADID</p><p>IOS : IDFA</p> |

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
        // requestType에 따라 실행
        JSONObject(contractMessage).let {
            val request = it.getString("request")
<strong>            if(request == "getDeviceADID") {
</strong><strong>                
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

## &#x20;<a href="#window.open" id="window.open"></a>

***


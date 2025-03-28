---
hidden: true
icon: js
---

# 외부 웹 브라우져 오픈 요청(Require)

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

## &#x20;<a href="#window.open" id="window.open"></a>

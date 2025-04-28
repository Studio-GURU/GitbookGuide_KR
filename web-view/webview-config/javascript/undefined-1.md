---
icon: js
---

# 기기 광고 식별값 수집 요청

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

| parameter                                                                                            | description                                                                                                         |
| ---------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| <pre class="language-json"><code class="lang-json">{
  "deviceADID" : "$deviceADID",
}
</code></pre> | <p>callback으로 전달된 함수에 파라미터 값을 포함하여 호출합니다.<br>JSON 값을 stringfy하여 전달합니다.<br><br>AOS : deviceADID</p><p>IOS : IDFA</p> |

***

### 호출 처리

{% hint style="warning" %}
**예제로 작성된 코드로 참고용으로 확인 부탁드립니다.**
{% endhint %}

{% tabs %}
{% tab title="ANDROID" %}
{% tabs %}
{% tab title="KOTLIN" %}
{% code lineNumbers="true" %}
```kotlin
// ... import ...
class SampleActivity: AppCompatActivity() {

    // ... other code ...
    // <code>
    // ... other code ...
    
    WebView.addJavascriptInterface(TreasureKitJavascriptInterface(), "treasureComics")

    class TreasureKitJavascriptInterface {
        @JavascriptInterface
        class TreasureKitJavascriptInterface {
            fun postMessage(message: String) {     
                // message를 JSON-Object로 변환
                // JSONObject -> request
                // requestType에 따라 실행
                JSONObject(contractMessage).let {
                    val request = it.getString("request")
                    val callback = it.getString("callback")
                    if(request == "getDeviceADID") {
                        // 광고 아이디를 javascript를 통해 callback에 전달합니다.
                        val params = JSONObject().apply {
                            put("deviceADID", "${광고아이디}")
                        }
                        val paramString = if (params != null) "'${params.toString().replace("\"", "\\\"")}'" else ""
                        weakWebView.get()?.evaluateJavascript(
                            "(function(){$callback($paramString);})();", null
                        )
                    }
                }
            }
        }
    }
    
    // ... other code ...
    // <code>
    // ... other code ...
}
```
{% endcode %}
{% endtab %}

{% tab title="JAVA" %}
{% code lineNumbers="true" %}
```java
public class SampleActivity extends AppCompatActivity {
    
    // ... other code ...
    // <code>
    // ... other code ...
    
    webView.addJavascriptInterface(new TreasureKitJavascriptInterface(this), "treasureComics");

    public class TreasureKitJavascriptInterface {
        @JavascriptInterface
        public void postMessage(String message) {
            try {
                JSONObject jsonObject = new JSONObject(message);
                String request = jsonObject.getString("request");
                String callback = jsonObject.getString("callback");
    
                if ("getDeviceADID".equals(request)) {
                    JSONObject params = new JSONObject();
                    try {
                        params.put("deviceADID", "광고아이디"); // 실제 광고 ID로 변경 필요
                    } catch (JSONException e) {
                        e.printStackTrace();
                    }
    
                    String paramString = "'" + params.toString().replace("\"", "\\\"") + "'";
                    WebView webView = weakWebView.get();
                    if (webView != null) {
                        webView.post(() -> webView.evaluateJavascript(
                            "(function(){" + callback + "(" + paramString + ");})();", null
                        ));
                    }
                }
            } catch (JSONException e) {
                e.printStackTrace();
            }
        }
    }
    
    // ... other code ...
    // <code>
    // ... other code ...
}
```
{% endcode %}


{% endtab %}
{% endtabs %}
{% endtab %}

{% tab title="iOS" %}
<pre class="language-swift" data-line-numbers><code class="lang-swift">// ... import ...
class ViewController: WKScriptMessageHandler {
    
    // ... other code ...
    // &#x3C;code>
    // ... other code ...
    
    // userContentController 설정
    WKWebView.configuration.userContentController.add(self, name: "treasureComics")
    
    // ... other code ...
    // &#x3C;code>
    // ... other code ...
    
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
                let callback = (json["callback"] as? String) ?? ""
                if request == "getDeviceADID" {
                    var params: [String: Any] = [:]
                    params["deviceADID"] = "$광고아이디값$"
                    var paramString: String = ""
                    if params != nil {
                        guard let json = try? JSONSerialization.data(withJSONObject: params!, options: .fragmentsAllowed) else {
                            print("Something is wrong while converting dictionary to JSON data.")
                            return
                        }
                        guard let paramStringify = String(data: json, encoding: .utf8) else {
                            print("Something is wrong while converting JSON data to JSON string.")
                            return
                        }
                        paramString = paramStringify.replacingOccurrences(of: "\"", with: "\\\"")
                        paramString = "'\(paramString)'"
                        DispatchQueue.main.async {
<strong>                            $WebView.evaluateJavaScript("(function(){\(callback)(\(paramString));})();")
</strong>                        }
                    }                
                }
            } catch {
                print("error")
            }
        }
    }
    
    // ... other code ...
    // &#x3C;code>
    // ... other code ...
}
</code></pre>
{% endtab %}
{% endtabs %}




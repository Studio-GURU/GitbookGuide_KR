---
icon: js
---

# 추가 정보 수집 요청

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

| parameter                                                                                                  | description                                                                                                                       |
| ---------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| <pre class="language-json"><code class="lang-json">{
  "phone" : 01011111111,
  "age" : 30
}
</code></pre> | <p>callback으로 전달된 함수에 파라미터 값을 포함하여 호출합니다.<br>JSON 값을 stringfy하여 전달합니다.<br><br>예시로 작성된 데이터입니다. <br>키 및 데이터는 보물섬과 협의 후 반환해 주세요.</p> |

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
                    if(request == "getExtraData") {
                        // 광고 아이디를 javascript를 통해 callback에 전달합니다.
                        val params = JSONObject().apply {
                            put("phone", "${전화번호}")
                            put("age", "${나이}")
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
                if ("getExtraData".equals(request)) {
                    JSONObject params = new JSONObject();
                    try {
                        params.put("phone", "${전화번호}");
                        params.put("age", "${나이}");
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
{% code lineNumbers="true" %}
```swift
// ... import ...
class ViewController: WKScriptMessageHandler {

    // ... other code ...
    // <code>
    // ... other code ...

    // userContentController 설정
    WKWebView.configuration.userContentController.add(self, name: "treasureComics")
    
    // ... other code ...
    // <code>
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
                if request == "getExtraData" {
                    var params: [String: Any] = [:]
                    params["phone"] = "$전화번호$"
                    params["age"] = "$나이$"
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
                            $WebView.evaluateJavaScript("(function(){\(callback)(\(paramString));})();")
                        }
                    }                
                }
            } catch {
                print("error")
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


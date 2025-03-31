---
description: TTS 기능 구현을 위한 안내입니다.
hidden: true
icon: js
---

# Text To Speech(TTS)

## Text To Speech 기능 <a href="#window.open" id="window.open"></a>

✓ 보물섬 웹소설의 TTS 기능을 사용하기 위한 가이드입니다.

| request   |
| --------- |
| postSpeak |

### 웹에서의 호출 예제

{% tabs %}
{% tab title="ANDROID" %}
{% code lineNumbers="true" %}
```javascript
<script type="text/javascript">
// TTS Start
function postSpeakStart() {
	// speakid 값은 테스트를 위해 임시값 사용
	const rand_0_100 = Math.floor(Math.random() * 101);
  let request = {
      request: "postSpeak",
      action: "start",
      parameter: {
          speakId: "" + rand_0_100 + "",
          speakText: "스크린 캡처 방지를 통해 콘텐츠를 보호하는 방법을 알아보겠습니다. 이 과정은 콘텐츠의 무단 복제를 방지하고, 중요한 자료나 개인 정보를 안전하게 보호하는 데 도움이 됩니다",
          speechRate: 0.5, //0.1 ~ 1.0
          pitch: 1.0
      },
      callback: "postSpeakCallback"
  }
  let message = JSON.stringify(request);
  treasureComics.postMessage(message.toString());
}
// TTS Pause
function postSpeakPause() {
  let request = {
      request: "postSpeak",
      action: "pause",
      callback: "postSpeakCallback"
  }
  let message = JSON.stringify(request);
  treasureComics.postMessage(message.toString());
}
// TTS Resume
function postSpeakResume() {
  let request = {
      request: "postSpeak",
      action: "resume",
      callback: "postSpeakCallback"
  }
  let message = JSON.stringify(request);
  treasureComics.postMessage(message.toString());
}
// TTS Stop
function postSpeakStop() {
  let request = {
      request: "postSpeak",
      action: "stop",
      callback: "postSpeakCallback"
  }
  let message = JSON.stringify(request);
  treasureComics.postMessage(message.toString());
}
// TTS Response
function postSpeakCallback(response) {
  var obj = JSON.parse(response);
  let speakId = obj.speakId
  let speakStatus = obj.speakStatus
  alert('{ speakId: ' + speakId + ', speakStatus: ' + speakStatus + ' }');
}
</script>
```
{% endcode %}
{% endtab %}

{% tab title="iOS" %}
{% code lineNumbers="true" %}
```javascript
<script type="text/javascript">
// TTS Start
function postSpeakStart() {
    // speakid 값은 테스트를 위해 임시값 사용
    const rand_0_100 = Math.floor(Math.random() * 101);
    let request = {
      request: "postSpeak",
      action: "start",
      parameter: {
          speakId: "" + rand_0_100 + "",
          speakText: "스크린 캡처 방지를 통해 콘텐츠를 보호하는 방법을 알아보겠습니다. 이 과정은 콘텐츠의 무단 복제를 방지하고, 중요한 자료나 개인 정보를 안전하게 보호하는 데 도움이 됩니다",
          speechRate: 0.5, //0.1 ~ 1.0
          pitch: 1.0
      },
      callback: "postSpeakCallback"
  }
  let message = JSON.stringify(request);
  window.webkit.messageHandlers.treasureComics.postMessage(message.toString());
}
// TTS Pause
function postSpeakPause() {
  let request = {
      request: "postSpeak",
      action: "pause",
      callback: "postSpeakCallback"
  }
  let message = JSON.stringify(request);
  window.webkit.messageHandlers.treasureComics.postMessage(message.toString());
}
// TTS Resume
function postSpeakResume() {
    let request = {
        request: "postSpeak",
        action: "resume",
        callback: "postSpeakCallback"
    }
    let message = JSON.stringify(request);
    window.webkit.messageHandlers.treasureComics.postMessage(message.toString());
}
// TTS Stop
function postSpeakStop() {
    let request = {
        request: "postSpeak",
        action: "stop",
        callback: "postSpeakCallback"
    }
    let message = JSON.stringify(request);
    window.webkit.messageHandlers.treasureComics.postMessage(message.toString());
}
// TTS Response
function postSpeakCallback(response) {
    var obj = JSON.parse(response);
    let speakId = obj.speakId
    let speakStatus = obj.speakStatus
    alert('{ speakId: ' + speakId + ', speakStatus: ' + speakStatus + ' }');
}
</script>
```
{% endcode %}
{% endtab %}
{% endtabs %}

### 클라이언트 응답

<table><thead><tr><th width="302">parameter</th><th>description</th></tr></thead><tbody><tr><td><pre><code>{
  "speakId": "$deviceADID",
  "speakStatus": $speakStatus
}
</code></pre></td><td>callback으로 전달된 함수에 파라미터 값을 포함하여 호출합니다.<br>JSON 값을 stringify하여 전달합니다.</td></tr></tbody></table>

{% tabs %}
{% tab title="ANDROID" %}
{% tabs %}
{% tab title="KOTLIN" %}
{% code lineNumbers="true" %}
```kotlin
WebView.addJavascriptInterface(TreasureKitJavascriptInterface(), "treasureComics")

class TreasureKitJavascriptInterface {
    @JavascriptInterface
    class TreasureKitJavascriptInterface {
        fun postMessage(message: String) {     
            // message를 JSON-Object로 변환
            // JSONObject -> request
            // requestType에 따라 실행
            JSONObject(message).let {
                val request = it.getString("request")
                val action = it.getString("action")
                val callback = it.getStsring("callback")
                if (request == "postSpeak" && action == "start") {
                    val parameter = it.getJSONObject("parameter")
                    val spaekId = parameter.getString("speakId")
                    val speakText = parameter.getString("speakText")
                    val speechRate = parameter.getFloat("speechRate")
                    val pitch = parameter.getFloat("pitch")
                    // TTS Start
                    // Start 액션 이후 callback에 결과를 전달합니다.
                }
                if (request == "postSpeak" && action == "pause") {
                    // TTS Pause
                    // 액션 이후 callback에 결과를 전달합니다.
                }
                if (request == "postSpeak" && action == "resume") {
                    // TTS Resume
                    // 액션 이후 callback에 결과를 전달합니다.
                }
                if (request == "postSpeak" && action == "stop") {
                    // TTS Stop
                    // 액션 이후 callback에 결과를 전달합니다.
                }
            }
        }
    }
}
```
{% endcode %}
{% endtab %}

{% tab title="JAVA" %}
{% code lineNumbers="true" %}
```java
webView.addJavascriptInterface(new TreasureKitJavascriptInterface(this), "treasureComics");

public class TreasureKitJavascriptInterface {
    @JavascriptInterface
    public void postMessage(String message) {
        try {
            JSONObject jsonObject = new JSONObject(message);
            String request = jsonObject.getString("request");
            String action = jsonObject.getString("action");
            if ("postSpeak".equals(request)) {
                if ("start".equals(action)) {
                    JSONObject parameter = jsonObject.getJSONObject("parameter");
                    String speakId = parameter.getString("speakId");
                    String speakText = parameter.getString("speakText");
                    float speechRate = Float.parseFloat(parameter.getString("speechRate"));
                    float pitch = Float.parseFloat(parameter.getString("pitch"));
                    // TTS Start
                    // 액션 이후 callback에 결과를 전달합니다.
                } else if ("pause".equals(action)) {
                    // TTS Pause
                    // 액션 이후 callback에 결과를 전달합니다.
                } else if ("resume".equals(action)) {
                    // TTS Resume
                    // 액션 이후 callback에 결과를 전달합니다.
                } else if ("stop".equals(action)) {
                    // TTS STOP
                    // 액션 이후 callback에 결과를 전달합니다.
                }
            }
        } catch (JSONException e) {
            e.printStackTrace();
        }
    }
}
```
{% endcode %}


{% endtab %}
{% endtabs %}
{% endtab %}

{% tab title="iOS" %}
{% code lineNumbers="true" %}
```swift
class ViewController: WKScriptMessageHandler {
    ...
    ...
    innerWebView.configuration.userContentController.add(self, name: "treasureComics")
    ...
    ...    
    func userContentController(_ userContentController: WKUserContentController, didReceive message: WKScriptMessage) {
        if message.name == "treasureComics", let messageBody = message.body as? String {
            do {
                if let withData = messageBody.data(using: .utf8) {
                    if let json = try JSONSerialization.jsonObject(with: withData, options: .allowFragments) as? [String: AnyObject] {                        
                        let request = (json["request"] as? String) ?? ""
                        let action = (json["action"] as? String) ?? ""
                        let callbackName = json["callback"] as? String ?? ""
                        // TTS
                        if request == "postSpeak" && action == "start" {
                            let params = json["parameter"] as? [String: AnyObject]
                            let speakId = params?["speakId"] as? String ?? ""
                            let speakText = params?["speakText"] as? String ?? ""
                            let speechRate = params?["speechRate"] as? Float ?? 0.5
                            let pitch = params?["pitch"] as? Float ?? 1.0
                            // TTS Start
                            // 액션 이후 callback에 결과를 전달합니다.
                            return
                        }
                        if request == "postSpeak" && action == "stop" {
                            // TTS Stop
                            // 액션 이후 callback에 결과를 전달합니다.
                            return
                        }                            
                        if request == "postSpeak" && action == "pause" {
                            // TTS Pause
                            // 액션 이후 callback에 결과를 전달합니다.
                            return
                        }
                        if request == "postSpeak" && action == "resume" {
                            // TTS Resume
                            // 액션 이후 callback에 결과를 전달합니다.
                            return
                        }
                    }
                }
            } catch {
                print("error: \(error)")
            }
        }
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

***

## 예제 프로젝트

{% embed url="https://github.com/Studio-GURU/TreasureIslandX-Mockup-AOS-TTS" %}

{% embed url="https://github.com/Studio-GURU/TreasureIslandX-Mockup-iOS-TTS" %}

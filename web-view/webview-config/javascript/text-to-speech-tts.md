---
description: TTS 기능 구현을 위한 안내입니다.
hidden: true
icon: js
---

# Text To Speech(TTS)

## Text To Speech 기능 <a href="#window.open" id="window.open"></a>

✓ 보물섬 웹소설의 TTS 기능을 사용하지 위한 가이드입니다.

| request   |
| --------- |
| postSpeak |

### 웹에서의 호출 예제

{% tabs %}
{% tab title="ANDROID" %}
{% code lineNumbers="true" %}
```javascript
<script type="text/javascript">
function postSpeakStart() {
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
    treasureKit.postMessage(message.toString());
}
</script>
```
{% endcode %}
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

### 클라이언트 응답

<table><thead><tr><th width="302">parameter</th><th>description</th></tr></thead><tbody><tr><td><pre><code>{
  "speakId": "$deviceADID",
  "speakStatus": $speakStatus
}
</code></pre></td><td>callback으로 전달된 함수에 파라미터 값을 포함하여 호출합니다.<br>JSON 값을 stringfy하여 전달합니다.</td></tr></tbody></table>

{% tabs %}
{% tab title="ANDROID" %}
{% tabs %}
{% tab title="KOTLIN" %}

{% endtab %}

{% tab title="JAVA" %}

{% endtab %}
{% endtabs %}
{% endtab %}

{% tab title="iOS" %}

{% endtab %}
{% endtabs %}











***













{% embed url="https://github.com/Studio-GURU/TreasureIslandX-Mockup-AOS-TTS" %}

{% embed url="https://github.com/Studio-GURU/TreasureIslandX-Mockup-iOS-TTS" %}

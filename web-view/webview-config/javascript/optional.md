---
hidden: true
icon: js
---

# 추가 정보 수집 요청(Optional)

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


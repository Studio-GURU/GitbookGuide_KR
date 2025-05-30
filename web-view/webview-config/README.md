---
icon: window-flip
---

# 웹뷰 설정 가이드

유료 결제를 위한 Scheme 등록

TossPayments를 통한 유료 결제에 필요한 은행앱 패키지 등록

자세한 내용은 아래의 링크를 확인 하세요.

{% embed url="https://docs.tosspayments.com/guides/v2/webview" %}

***

## 웹뷰 셋팅 ( Require ) <a href="#config" id="config"></a>

**✓ 웹뷰 셋팅 값 설정에 대한 방법을 안내합니다.**

{% hint style="info" %}
WebView 구성에 필요한 **예제 코드**이며, 실 프로젝트에서는 **참고만 하시길 바랍니다**.

***

<mark style="color:red;">**✓ WebView(WKWebView) Javascript 및 DomStorage는 기본적으로 허용이 필수 입니다.**</mark>
{% endhint %}

{% tabs %}
{% tab title="ANDROID(WebView)" %}
{% tabs %}
{% tab title="KOTLIN" %}
<pre class="language-kotlin" data-line-numbers><code class="lang-kotlin">// ... import ...
class SampleActivity: AppCompatActivity() {

    // ... other code ...
    // &#x3C;code>
    // ... other code ...
    
    with(webView.settings) {
<strong>        // ---------- 필수 ---------- //
</strong><strong>        domStorageEnabled = true // DOM 스토리지 활성화
</strong><strong>        javaScriptEnabled = true // JavaScript 사용 가능
</strong><strong>        javaScriptCanOpenWindowsAutomatically = true // JavaScript에서 새 창 열기 허용
</strong><strong>        setSupportMultipleWindows(true) // 다중 창 지원
</strong><strong>        mediaPlaybackRequiresUserGesture = false // 사용자 제스처 없이 미디어 재생 허용
</strong>        // ---------- 옵션 ---------- //
        databaseEnabled = true // 데이터베이스 사용 가능
        cacheMode = WebSettings.LOAD_DEFAULT // 기본 캐시 모드 설정
        textZoom = 100 // 텍스트 확대/축소 비율 설정
        setSupportZoom(false) // 확대/축소 지원 비활성화
        displayZoomControls = false // 확대/축소 컨트롤 비활성화
        defaultTextEncodingName = "utf-8" // 기본 텍스트 인코딩 설정
        loadWithOverviewMode = true // 콘텐츠를 웹뷰에 맞게 축소하여 전체 내용을 한눈에 볼 수 있도록 설정 // 개요 모드로 로드 설정
        mixedContentMode = WebSettings.MIXED_CONTENT_ALWAYS_ALLOW // 혼합 컨텐츠 허용 (HTTPS 페이지에서 HTTP 컨텐츠 로드 가능)
        // WebSettings.MIXED_CONTENT_NEVER_ALLOW: 보안상의 이유로 HTTPS 페이지에서 HTTP 컨텐츠 로드를 차단
        // WebSettings.MIXED_CONTENT_ALWAYS_ALLOW: 모든 HTTP 및 HTTPS 컨텐츠 로드를 허용
        // WebSettings.MIXED_CONTENT_COMPATIBILITY_MODE: 기본적으로 HTTPS를 유지하지만 일부 HTTP 컨텐츠 로드를 허용 // 혼합 컨텐츠 허용
        if (Build.VERSION.SDK_INT &#x3C;= Build.VERSION_CODES.O) {
            // 콘텐츠를 단일 열로 정렬하여 화면 너비에 맞게 표시
            layoutAlgorithm = WebSettings.LayoutAlgorithm.SINGLE_COLUMN
        }
    }
<strong>    // 웹뷰의 오버스크롤을 제한합니다.
</strong><strong>    ${WebView}.overScrollMode = View.OVER_SCROLL_NEVER
</strong>    
    // ... other code ...
    // &#x3C;code>
    // ... other code ...
}
</code></pre>
{% endtab %}

{% tab title="JAVA" %}
<pre class="language-java" data-line-numbers><code class="lang-java">// ... import ...
public class SampleActivity extends AppCompatActivity {

    // ... other code ...
    // &#x3C;code>
    // ... other code ...   
    
    WebSettings webSettings = wView.getSettings();    
<strong>    // ---------- 필수 ---------- //
</strong><strong>    webSettings.setDomStorageEnabled(true); // DOM 스토리지 활성화
</strong><strong>    webSettings.setJavaScriptEnabled(true); // JavaScript 사용 가능
</strong><strong>    webSettings.setJavaScriptCanOpenWindowsAutomatically(true); // JavaScript에서 새 창 열기 허용
</strong><strong>    webSettings.setSupportMultipleWindows(true); // 다중 창 지원
</strong><strong>    webSettings.setMediaPlaybackRequiresUserGesture(false); // 사용자 제스처 없이 미디어 재생 허용
</strong>    // ---------- 옵션 ---------- //
    webSettings.setDatabaseEnabled(true); // 데이터베이스 사용 가능
    webSettings.setCacheMode(WebSettings.LOAD_DEFAULT); // 기본 캐시 모드 설정
    webSettings.setTextZoom(100); // 텍스트 확대/축소 비율 설정
    webSettings.setSupportZoom(false); // 확대/축소 지원 비활성화
    webSettings.setDisplayZoomControls(false); // 확대/축소 컨트롤 비활성화
    webSettings.setDefaultTextEncodingName("utf-8"); // 기본 텍스트 인코딩 설정
    webSettings.setLoadWithOverviewMode(true); // 콘텐츠를 웹뷰에 맞게 축소하여 전체 내용을 한눈에 볼 수 있도록 설정 // 개요 모드로 로드 설정
    webSettings.setMixedContentMode(WebSettings.MIXED_CONTENT_ALWAYS_ALLOW); // 혼합 컨텐츠 허용 (HTTPS 페이지에서 HTTP 컨텐츠 로드 가능)
    // WebSettings.MIXED_CONTENT_NEVER_ALLOW: 보안상의 이유로 HTTPS 페이지에서 HTTP 컨텐츠 로드를 차단
    // WebSettings.MIXED_CONTENT_ALWAYS_ALLOW: 모든 HTTP 및 HTTPS 컨텐츠 로드를 허용
    // WebSettings.MIXED_CONTENT_COMPATIBILITY_MODE: 기본적으로 HTTPS를 유지하지만 일부 HTTP 컨텐츠 로드를 허용 // 혼합 컨텐츠 허용
    if (Build.VERSION.SDK_INT &#x3C;= Build.VERSION_CODES.O) {
        // 콘텐츠를 단일 열로 정렬하여 화면 너비에 맞게 표시
        webSettings.setLayoutAlgorithm(WebSettings.LayoutAlgorithm.SINGLE_COLUMN); // 레이아웃 알고리즘 설정 (오래된 버전 지원)
    }    
<strong>    // 웹뷰의 오버스크롤을 제한합니다.
</strong><strong>    ${WebView}.setOverScrollMode(WebView.OVER_SCROLL_NEVER);
</strong>    
    // ... other code ...
    // &#x3C;code>
    // ... other code ...
}
</code></pre>
{% endtab %}
{% endtabs %}
{% endtab %}

{% tab title="iOS(WKWebView)" %}
<pre class="language-swift" data-line-numbers><code class="lang-swift">// ... import ...
class SampleViewController: UIViewController {
    
    // ... other code ...
    // &#x3C;code>
    // ... other code ...
    
    // ---------- 필수 ---------- //
    // WKWebView의 설정을 관리하는 객체를 생성합니다. 이를 통해 JavaScript 실행, 쿠키 저장, 콘텐츠 접근 정책 등을 설정할 수 있습니다.
    let configuration = WKWebViewConfiguration()
    // 비디오 재생이 자동으로 전체화면으로 전환되지 않도록 합니다.
<strong>    configuration.allowsInlineMediaPlayback = true
</strong>    // JavaScript에서 window.open()을 사용하여 새로운 창을 자동으로 열 수 있도록 허용합니다.
<strong>    configuration.preferences.javaScriptCanOpenWindowsAutomatically = true
</strong>    // 기본적인 웹사이트 데이터 저장소를 설정합니다.
    // 캐시, 쿠키, 세션 저장 등의 데이터를 관리하는 역할을 합니다.
<strong>    configuration.websiteDataStore = WKWebsiteDataStore.default()
</strong>    // Javascript 허용을 설정합니다.
    // 버전에 따라 분기 처리하여 Javascript를 허용합니다.
<strong>    if #available(iOS 14.0, *) {
</strong><strong>        configuration.defaultWebpagePreferences.allowsContentJavaScript = true
</strong><strong>    } else {
</strong><strong>        configuration.preferences.javaScriptEnabled = true
</strong><strong>    }
</strong>    // WebView History Back&#x26;Forward
    // 웹뷰의 스와이프 동작으로 앞으로가기 &#x26; 뒤로가기 동작을 설정합니다.
<strong>    ${WKWebView}.allowsBackForwardNavigationGestures = true
</strong>    // 웹뷰의 오버스크롤을 제한합니다.
<strong>    ${WKWebView}.scrollView.bounces = false
</strong>    
    // ... other code ...
    // &#x3C;code>
    // ... other code ...
}
</code></pre>
{% endtab %}
{% endtabs %}

***

## WebView History 관리 ( Require ) <a href="#config" id="config"></a>

{% hint style="info" %}
물리 키, 버튼 또는 제스처를 통해 WebView의 뒤로가기를 구현할 때는 웹 브라우저의 히스토리 상태를 확인한 후, 상황에 맞는 처리를 수행해야 합니다.
{% endhint %}

{% tabs %}
{% tab title="ANDROID(WebView)" %}
<pre class="language-kotlin" data-line-numbers><code class="lang-kotlin">// ... import ...
class SampleActivity: AppCompatActivity() {

    // ... other code ...
    // &#x3C;code>
    // ... other code ...
    
<strong>    // 뒤로가기가 가능할 경우 HistoryBack 처리
</strong><strong>    // 더이상 뒤로가기를 할 수 없는 경우 화면 종료 처리
</strong><strong>    if (${WebView}.canGoBack() &#x26;&#x26; ${WebView}.copyBackForwardList().size > 0) {
</strong><strong>        ${WebView}.goBack()
</strong><strong>    } else {
</strong><strong>        // Activity 종료 처리 또는 View 종료 처리 로직 추가
</strong><strong>    }
</strong>   
    // ... other code ...
    // &#x3C;code>
    // ... other code ...    
}    
</code></pre>
{% endtab %}

{% tab title="iOS(WKWebView)" %}
<pre class="language-swift" data-line-numbers><code class="lang-swift">// ... import ...
class SampleViewController: UIViewController {
    
    // ... other code ...
    // &#x3C;code>
    // ... other code ...
        
<strong>    // 뒤로가기가 가능할 경우 HistoryBack 처리
</strong><strong>    // 더이상 뒤로가기를 할 수 없는 경우 화면 종료 처리
</strong><strong>    if ${WKWebView}.canGoBack &#x26;&#x26; ${WKWebView}.backForwardList.backList.count > 0 {
</strong><strong>        ${WKWebView}.goBack()
</strong><strong>    } else {
</strong><strong>        // 화면 종료 처리
</strong><strong>    }
</strong>    
    // ... other code ...
    // &#x3C;code>
    // ... other code ...
}
</code></pre>
{% endtab %}
{% endtabs %}

***

## 웹뷰 네비게이션 바 ( Require ) <a href="#config" id="config"></a>

**✓ 웹뷰의 네비게이션 바는 우측에 닫기 버튼만 포함하도록 구성합니다.**

<figure><img src="../../.gitbook/assets/KakaoTalk_Photo_2025-04-02-15-02-29.jpeg" alt=""><figcaption></figcaption></figure>

***

## 웹뷰 컨텐츠 보호 ( Require ) <a href="#secure" id="secure"></a>

**✓ 스크린 캡쳐 방지를 통해 콘텐츠를 보호하는 방법을 안내합니다.**

{% tabs %}
{% tab title="ANDROID(WebView)" %}
보물섬을 감싸고 있는 Activity에 FLAG\_SECURE 적용을 통해 쉽게 스크린 캡쳐 방지를 할 수 있습니다.

{% tabs %}
{% tab title="KOTLIN" %}
<pre class="language-kotlin" data-line-numbers><code class="lang-kotlin">// ... import ...
class SampleActivity: AppCompatActivity() {

    // ... other code ...
    // &#x3C;code>
    // ... other code ...
    
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
<strong>        window.addFlags(WindowManager.LayoutParams.FLAG_SECURE)
</strong>        // ... other code ...
        // &#x3C;code>
        // ... other code ...
    }
    
    // ... other code ...
    // &#x3C;code>
    // ... other code ...
}
</code></pre>
{% endtab %}

{% tab title="JAVA" %}
<pre class="language-java" data-line-numbers><code class="lang-java">// ... import ...
public class SampleActivity extends AppCompatActivity {
    
    // ... other code ...
    // &#x3C;code>
    // ... other code ...
    
    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
<strong>        getWindow().addFlags(WindowManager.LayoutParams.FLAG_SECURE);
</strong>        // ... other code ...
        // &#x3C;code>
        // ... other code ...
    }
    
    // ... other code ...
    // &#x3C;code>
    // ... other code ...
}
</code></pre>
{% endtab %}
{% endtabs %}
{% endtab %}

{% tab title="iOS(WKWebView)" %}
`UITextField`의 isSecureTextEntry 속성을 통해 사용자가 스크린 캡쳐를 할 수 없도록 우회 처리해야 합니다.

{% hint style="info" %}
스크린 캡쳐 방지 기능은 실기기에서만 동작 합니다.
{% endhint %}

{% code lineNumbers="true" %}
```swift
// ... import ...
import Foundation
import UIKit
import WebKit

class SampleViewController: UIViewController {
    
    // ... other code ...
    // <code>
    // ... other code ...    
    
    private lazy var webView: WKWebView = {
        let view = WKWebView()
        view.translatesAutoresizingMaskIntoConstraints = false
        return view
    }()

    override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(animated)
        self.view.addSubview(self.webView)
        NSLayoutConstraint.activate([
            self.webView.topAnchor.constraint(equalTo: self.view.safeAreaLayoutGuide.topAnchor),
            self.webView.leadingAnchor.constraint(equalTo: self.view.leadingAnchor),
            self.webView.trailingAnchor.constraint(equalTo: self.view.trailingAnchor),
            self.webView.bottomAnchor.constraint(equalTo: self.view.bottomAnchor)
        ])
        self.webView.load(URLRequest(url: URL(string: "https://www.harustory.co.kr")!))
        self.applySecureContent()
    }

    func applySecureContent() {
        DispatchQueue.main.async {
            let secureField = UITextField()
            // secureField 크기를 웹뷰의 크기와 동일하게 설정합니다.
            secureField.frame = self.webview.bounds
            // secureField의 보안을 설정합니다.
            secureField.isSecureTextEntry = true
            // secureField의 상호작용을 비활성화합니다.
            secureField.isUserInteractionEnabled = false
            // secureField의 배경색을 투명하게 설정합니다.
            secureField.backgroundColor = .clear
            // 웹뷰에 secureField를 추가합니다.
            self.webview.addSubview(secureField)
            // 웹뷰 레이어에 secureField의 레이어를 추가합니다.
            self.webview.layer.superlayer?.addSublayer(secureField.layer)
            // secureField의 레이어를 웹뷰의 레이어 위에 추가합니다.
            secureField.layer.sublayers?.last?.addSublayer(self.webview.layer)
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

***

## Javascript Window 처리 ( Require ) <a href="#scheme" id="scheme"></a>

{% hint style="info" %}
웹뷰 구성에 필요한 **Scheme** 처리에 대한 **예제 코드**이며, 실 프로젝트에서는 **참고만 하시길 바랍니다**.
{% endhint %}

{% tabs %}
{% tab title="ANDROID(WebView)" %}
### Javascript window.open

WebView에서 `window.open()`을 처리하려면 **WebChromeClient**를 설정하고, `onCreateWindow()`를 오버라이드해야 합니다.

{% tabs %}
{% tab title="KOTLIN" %}
{% code lineNumbers="true" %}
```kotlin
// ... import ...
class SampleActivity: AppCompatActivity() {
    
    // ... other code ...
    // <code>
    // ... other code ...
    
    webView.webChromeClient = object : WebChromeClient() {
        override fun onCreateWindow(
            view: WebView?,
            isDialog: Boolean,
            isUserGesture: Boolean,
            resultMsg: Message?
        ): Boolean {
            val popupWebView = WebView(view?.context!!)
            popupWebView?.webViewClient = WebViewClient()
            popupWebView?.webChromeClient = WebChromeClient()
            // 새 창을 다룰 수 있도록 WebView를 포함하는 Dialog 생성
            val webViewDialog = Dialog(view.context)
            webViewDialog?.setContentView(newWebView)
            webViewDialog?.setOnDismissListener {
                popupWebView?.removeAllViews()
                popupWebView?.destroy()
            }
            webViewDialog?.show()
            val transport = resultMsg?.obj as? WebView.WebViewTransport
            transport?.webView = newWebView
            resultMsg?.sendToTarget()
            return true
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
// ... import ...
public class SampleActivity extends AppCompatActivity {
    
    // ... other code ...
    // <code>
    // ... other code ...
    
    webView.setWebChromeClient(new WebChromeClient() {
        @Override
        public boolean onCreateWindow(WebView view, boolean isDialog, boolean isUserGesture, Message resultMsg) {
            Context context = view.getContext();
            WebView popupWebView = new WebView(context);
            popupWebView.setWebViewClient(new WebViewClient());
            popupWebView.setWebChromeClient(new WebChromeClient());
            // 새 창을 다룰 수 있도록 Dialog에 WebView 추가
            Dialog webViewDialog = new Dialog(context);
            webViewDialog.setContentView(popupWebView);
            webViewDialog.setOnDismissListener(dialog -> {
                popupWebView.removeAllViews();
                popupWebView.destroy();
            });
            webViewDialog.show();
            WebView.WebViewTransport transport = (WebView.WebViewTransport) resultMsg.obj;
            transport.setWebView(popupWebView);
            resultMsg.sendToTarget();
            return true;
        }
    });
    
    // ... other code ...
    // <code>
    // ... other code ...
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

***

### Javascript Alert

`Android WebView`에서 `window.alert()`을 처리하려면 `WebChromeClient`의 `onJsAlert()` 메서드를 오버라이드해야 합니다. 이 메서드는 JavaScript의 `alert()` 창이 호출될 때 반응할 수 있게 해줍니다.

{% tabs %}
{% tab title="KOTLIN" %}
{% code lineNumbers="true" %}
```kotlin
// ... import ...
class SampleActivity: AppCompatActivity() {
    // ... other code ...
    // <code>
    // ... other code ...
    webView.webChromeClient = object : WebChromeClient() {
        override fun onJsAlert(view: WebView?, url: String?, message: String?, result: JsResult?): Boolean {
            val builder = AlertDialog.Builder(view?.context)
            builder.setMessage(message)
                .setCancelable(false)
                .setPositiveButton("OK") { _, _ ->
                    result?.confirm()
                }
            val alert = builder.create()
            alert.show()
            return true
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
// ... import ...
public class SampleActivity extends AppCompatActivity {
    // ... other code ...
    // <code>
    // ... other code ...
    webView.setWebChromeClient(new WebChromeClient() {
        @Override
        public boolean onJsAlert(WebView view, String url, String message, JsResult result) {
            AlertDialog.Builder builder = new AlertDialog.Builder(view.getContext());
            builder.setMessage(message)
                .setCancelable(false)
                .setPositiveButton("OK", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialog, int which) {
                        result.confirm();
                    }
                });
    
            AlertDialog alert = builder.create();
            alert.show();    
            return true; 
        }
    });
    // ... other code ...
    // <code>
    // ... other code ...
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

***

### Javascript Confirm

`Android WebView`에서 `window.confirm()`을 처리하려면 `WebChromeClient`의 `onJsConfirm()` 메서드를 오버라이드해야 합니다. 이 메서드는 JavaScript의 `confirm()` 창이 호출될 때 반응할 수 있게 해줍니다.

{% tabs %}
{% tab title="KOTLIN" %}
{% code lineNumbers="true" %}
```kotlin
// ... import ...
class SampleActivity: AppCompatActivity() {
    // ... other code ...
    // <code>
    // ... other code ...
    webView.webChromeClient = object : WebChromeClient() {
        override fun onJsConfirm(
            view: WebView?,
            url: String?,
            message: String?,
            result: JsResult?
        ): Boolean {
            val builder = AlertDialog.Builder(view?.context)
            builder.setMessage(message)
                .setCancelable(false)
                .setPositiveButton("OK") { _, _ -> 
                    result?.confirm()
                }
                .setNegativeButton("Cancel") { _, _ -> 
                    result?.cancel()
                }
            val alert = builder.create()
            alert.show()    
            return true // 대화상자를 직접 처리했음을 알림
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
// ... import ...
public class SampleActivity extends AppCompatActivity {
    // ... other code ...
    // <code>
    // ... other code ...
    webView.setWebChromeClient(new WebChromeClient() {
        @Override
        public boolean onJsConfirm(WebView view, String url, String message, JsResult result) {
            AlertDialog.Builder builder = new AlertDialog.Builder(view.getContext());
            builder.setMessage(message)
                .setCancelable(false)
                .setPositiveButton("OK", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialog, int which) {
                        result.confirm();
                    }
                })
                .setNegativeButton("Cancel", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialog, int which) {
                        result.cancel();
                    }
                });
    
            AlertDialog alert = builder.create();
            alert.show();    
            return true;
        }
    });
    // ... other code ...
    // <code>
    // ... other code ...
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

***

### Javascript Alert(Confirm) TextInput

JavaScript의 `window.prompt()`를 WebView에서 처리하려면, `WebChromeClient`의 `onJsPrompt()` 메서드를 오버라이드하여 사용자 입력을 받을 수 있는 맞춤형 다이얼로그를 생성할 수 있습니다.

{% tabs %}
{% tab title="KOTLIN" %}
{% code lineNumbers="true" %}
```kotlin
// ... import ...
class SampleActivity: AppCompatActivity() {
    
    // ... other code ...
    // <code>
    // ... other code ...
    
    webView.webChromeClient = object : WebChromeClient() {
        override fun onJsPrompt(view: WebView?, url: String?, message: String?, defaultValue: String?, result: JsPromptResult?): Boolean {
            // JavaScript prompt를 대체할 커스텀 입력 다이얼로그 생성
            val builder = AlertDialog.Builder(view?.context)
            builder.setTitle("Prompt")
                .setMessage(message) // JavaScript prompt에서 전달된 메시지
                .setCancelable(false)    
            // 입력 필드를 생성
            val input = EditText(view?.context)
            input.setText(defaultValue) // 기본값이 있다면 기본값을 미리 설정
            builder.setView(input)
    
            builder.setPositiveButton("OK") { _, _ ->
                val userInput = input.text.toString()
                result?.confirm(userInput) // 사용자가 입력한 값으로 JavaScript에 응답
            }
    
            builder.setNegativeButton("Cancel") { _, _ ->
                result?.cancel() // "Cancel" 클릭 시 null을 JavaScript로 반환
            }
    
            val alert = builder.create()
            alert.show()
    
            return true // prompt가 처리되었음을 WebView에 알림
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
// ... import ...
public class SampleActivity extends AppCompatActivity {
    
    // ... other code ...
    // <code>
    // ... other code ...
    
    webView.setWebChromeClient(new WebChromeClient() {
        @Override
        public boolean onJsPrompt(WebView view, String url, String message, String defaultValue, JsPromptResult result) {
            // JavaScript prompt를 대체할 커스텀 입력 다이얼로그 생성
            AlertDialog.Builder builder = new AlertDialog.Builder(view.getContext());
            builder.setTitle("Prompt")
                .setMessage(message) // JavaScript prompt에서 전달된 메시지
                .setCancelable(false);
    
            // 입력 필드를 생성
            final EditText input = new EditText(view.getContext());
            input.setText(defaultValue); // 기본값이 있다면 기본값을 미리 설정
            builder.setView(input);
    
            builder.setPositiveButton("OK", new DialogInterface.OnClickListener() {
                @Override
                public void onClick(DialogInterface dialog, int which) {
                    String userInput = input.getText().toString();
                    result.confirm(userInput); // 사용자가 입력한 값으로 JavaScript에 응답
                }
            });
    
            builder.setNegativeButton("Cancel", new DialogInterface.OnClickListener() {
                @Override
                public void onClick(DialogInterface dialog, int which) {
                    result.cancel(); // "Cancel" 클릭 시 null을 JavaScript로 반환
                }
            });
    
            AlertDialog alert = builder.create();
            alert.show();
    
            return true; // prompt가 처리되었음을 WebView에 알림
        }
    });
    
    // ... other code ...
    // <code>
    // ... other code ...
}    
```
{% endcode %}


{% endtab %}
{% endtabs %}
{% endtab %}

{% tab title="iOS(WKWebView)" %}
### Javascript window.open

WKWebView javascript window.open() 명령어 처리 방법에 대한 안내

{% hint style="success" %}
**public protocol UIWebViewDelegate, UIAdaptivePresentationControllerDelegate**

***

`func webView(_ webView: WKWebView, createWebViewWith configuration: WKWebViewConfiguration, for navigationAction: WKNavigationAction, windowFeatures: WKWindowFeatures) -> WKWebView?`

***

:white\_check\_mark: **여러개의 팝업이 열린 경우를 위해 해당 웹뷰에 대한 리소스 관리가 필요합니다.**

* 웹 뷰의 크기와 위치는 원하는 값을 넣어 사용합니다.
* 모달 윈도우의 옵션은 앱의 상황에 따라 변경 후 사용하세요.
{% endhint %}

<pre class="language-swift" data-line-numbers><code class="lang-swift"><strong>// ... import ...
</strong><strong>class SampleViewController: ..., ..., UIAdaptivePresentationControllerDelegate {
</strong>    
    // ... other code ...
    // &#x3C;code>
    // ... other code ...
    
    // MARK: - Javascript window.open { WKUIDelegate }
    func webView(_ webView: WKWebView, createWebViewWith configuration: WKWebViewConfiguration, for navigationAction: WKNavigationAction, windowFeatures: WKWindowFeatures) -> WKWebView? {    
        let viewControllerToPresent = UIViewController()
        viewControllerToPresent.view.backgroundColor = UIColor.white
        viewControllerToPresent.modalPresentationStyle = .automatic
        if let sheet = viewControllerToPresent.sheetPresentationController {
            sheet.prefersGrabberVisible = true
        }
        // 웹뷰를 생성하여 리턴하면 현재 웹뷰와 parent 관계가 형성됩니다.
        let modalView = WKWebView(frame: CGRect(x: 0, y: 12, width: self.bounds.width, height: self.bounds.height), configuration: configuration)
        // set delegate
        modalView.uiDelegate = self
        modalView.navigationDelegate = self
        // setup scrollview
        modalView.scrollView.bounces = false
        modalView.scrollView.isPagingEnabled = false
        modalView.scrollView.alwaysBounceVertical = false
        modalView.scrollView.showsVerticalScrollIndicator = false
        modalView.scrollView.showsHorizontalScrollIndicator = false
        modalView.scrollView.contentInsetAdjustmentBehavior = .never
        // addview
        viewControllerToPresent.view.addSubview(modalView)
        viewControllerToPresent.presentationController?.delegate = self
        // present
        self.viewController.present(viewControllerToPresent, animated: true);
        return modalView
    }

<strong>    func presentationControllerDidDismiss(_ presentationController: UIPresentationController) {
</strong><strong>        // 팝업 종료 처리
</strong><strong>    }
</strong>    
    // ... other code ...
    // &#x3C;code>
    // ... other code ...
}
</code></pre>

***

### javascript window.close

WKWebView javascript window.close() 명령어 처리 방법에 대한 안내

{% hint style="success" %}
**public protocol UIWebViewDelegate**

***

`func webViewDidClose(_ webView: WKWebView)`
{% endhint %}

{% code lineNumbers="true" %}
```swift
// ... import ...
class SampleViewController: UIViewController, UIWebViewDelegate {
    
    // ... other code ...
    // <code>
    // ... other code ...
    
    // MARK: - window.close { UIWebViewDelegate }    
    func webViewDidClose(_ webView: WKWebView) {
        webView.removeFromSuperView()
        //webView = nil
    }
    
    // ... other code ...
    // <code>
    // ... other code ...
}
```
{% endcode %}

***

### Javascript Alert

Javascript alert 팝업 윈도우 처리에 대한 가이드

{% hint style="success" %}
**public protocol UIWebViewDelegate**

***

`func webView(_ webView: WKWebView, runJavaScriptAlertPanelWithMessage message: String, initiatedByFrame frame: WKFrameInfo, completionHandler: @escaping @MainActor () -> Void)`
{% endhint %}

{% code lineNumbers="true" %}
```swift
// ... import ...
class SampleViewController: UIViewController, UIWebViewDelegate {
    
    // ... other code ...
    // <code>
    // ... other code ...
    
    // MARK: - Javascript Alert Controll { UIWebViewDelegate }
    func webView(_ webView: WKWebView, runJavaScriptAlertPanelWithMessage message: String, initiatedByFrame frame: WKFrameInfo, completionHandler: @escaping @MainActor () -> Void) {
        let alertController = UIAlertController(title: nil, message: message, preferredStyle: .actionSheet)
        alertController.addAction(UIAlertAction(title: "확인", style: .default, handler: { (action) in
            completionHandler()
        }))
        DispatchQueue.main.async{
            self.viewController?.present(alertController, animated: true, completion: nil)
        }
    }
    
    // ... other code ...
    // <code>
    // ... other code ...
}
```
{% endcode %}

***

### Javascript Confirm

javascript confirm 팝업 윈도우 처리에 대한 가이드

{% hint style="success" %}
**public protocol UIWebViewDelegate**

***

`func webView(_ webView: WKWebView, runJavaScriptConfirmPanelWithMessage message: String, initiatedByFrame frame: WKFrameInfo, completionHandler: @escaping @MainActor (Bool) -> Void)`
{% endhint %}

{% code lineNumbers="true" %}
```swift
// ... import ...
class SampleViewController: UIViewController, UIWebViewDelegate {
    
    // ... other code ...
    // <code>
    // ... other code ...
    
    // MARK: - Javascript Confirm Controll { UIWebViewDelegate }
    func webView(_ webView: WKWebView, runJavaScriptConfirmPanelWithMessage message: String, initiatedByFrame frame: WKFrameInfo, completionHandler: @escaping @MainActor (Bool) -> Void) {
        let alertController = UIAlertController(title: nil, message: message, preferredStyle: .actionSheet)
        alertController.addAction(UIAlertAction(title: "확인", style: .default, handler: { (action) in
            completionHandler(true)
        }))
        alertController.addAction(UIAlertAction(title: "취소", style: .default, handler: { (action) in
            completionHandler(false)
        }))
        self.viewController?.present(alertController, animated: true, completion: nil)
    }
    
    // ... other code ...
    // <code>
    // ... other code ...
}
```
{% endcode %}

***

### Javascript Alert(Confirm) TextInput

javascript 텍스트 입력이 필요한 팝업 윈도우 처리에 대한 가이드

{% hint style="success" %}
**public protocol UIWebViewDelegate**

***

`func webView(_ webView: WKWebView, runJavaScriptTextInputPanelWithPrompt prompt: String, defaultText: String?, initiatedByFrame frame: WKFrameInfo, completionHandler: @escaping @MainActor (String?) -> Void)`
{% endhint %}

<pre class="language-swift" data-line-numbers><code class="lang-swift">// ... import ...
class SampleViewController: UIViewController, UIWebViewDelegate {
    
    // ... other code ...
    // &#x3C;code>
    // ... other code ...
    
    // MARK: - Javascript InputText Controll { UIWebViewDelegate }
<strong>    func webView(_ webView: WKWebView, runJavaScriptTextInputPanelWithPrompt prompt: String, defaultText: String?, initiatedByFrame frame: WKFrameInfo, completionHandler: @escaping @MainActor (String?) -> Void) {
</strong>        let alertController = UIAlertController(title: nil, message: prompt, preferredStyle: .actionSheet)
        alertController.addTextField { (textField) in
            textField.text = defaultText
        }
        alertController.addAction(UIAlertAction(title: "확인", style: .default, handler: { (action) in
            if let text = alertController.textFields?.first?.text {
                completionHandler(text)
            } else {
                completionHandler(defaultText)
            }
        }))
        alertController.addAction(UIAlertAction(title: "취소", style: .default, handler: { (action) in
            completionHandler(nil)
        }))
        self.viewController?.present(alertController, animated: true, completion: nil)
    }
    
    // ... other code ...
    // &#x3C;code>
    // ... other code ...
}
</code></pre>
{% endtab %}
{% endtabs %}

***

## Scheme 처리 ( Require ) <a href="#scheme" id="scheme"></a>

{% hint style="info" %}
웹뷰 구성에 필요한 **Scheme** 처리에 대한 **예제 코드**이며, 실 프로젝트에서는 **참고만 하시길 바랍니다**.
{% endhint %}

{% tabs %}
{% tab title="ANDROID(WebView)" %}
✓ WebView::shouldOverrideUrlLoading을 통해 전달된 scheme 처리에 대한 방법을 가이드합니다.

### intent

{% tabs %}
{% tab title="KOTLIN" %}
<pre class="language-kotlin" data-line-numbers><code class="lang-kotlin">// ... import code ...
class SampleActivity: AppCompatActivity() {
    
    // ... other code ...
    // &#x3C;code>
    // ... other code ...    
    
    private fun actionIntentTask(viewContext: Context, webView: WebView?, url: String): Boolean {
        val actionWebView = webView ?: return false
        val actionActivity = viewContext as? Activity ?: return false
        val actionIntent = try {
            Intent.parseUri(url, Intent.URI_INTENT_SCHEME)
        } catch (e: Exception) {
            // error
            null        
        }
    
        // check intent
        if (actionIntent == null) {
            Log.e("TAG", "intent is null")
            return false
        }
    
        try {
            // Fallback URL -> Loading WebView For Kakao
            val fallbackUrl = actionIntent.getStringExtra("browser_fallback_url")
            if (fallbackUrl != null) {
                actionWebView.loadUrl(fallbackUrl)
                return true
            }
            
            // action
            val actionPackageName = actionIntent.`package` ?: ""
            if (actionPackageName.isNotEmpty()) {
                // launch activity
                val launchIntent = viewContext.packageManager.getLaunchIntentForPackage(actionPackageName)
                if (launchIntent != null) {
                    actionActivity.startActivity(launchIntent)
                    return true
                }
            }
            
            // market
            if (actionPackageName.isNotEmpty()) {
                try {
                    val marketIntent = Intent(Intent.ACTION_VIEW)
                    marketIntent.data = Uri.parse("market://details?id=$actionPackageName")
                    actionActivity.startActivity(marketIntent)
                    return true
                } catch (e: Exception) {
                    // error
                }
            }
        } catch (e: Exception) {
                // error
            }
        }
<strong>        return false
</strong>    }
    
    // ... other code ...
    // &#x3C;code>
    // ... other code ...
}
</code></pre>
{% endtab %}

{% tab title="JAVA" %}
{% code lineNumbers="true" %}
```java
// ... import code ...   
public class SampleActivity extends AppCompatActivity {
    
    // ... other code ...
    // <code>
    // ... other code ...
    
    private boolean actionIntentTask(Context viewContext, WebView webView, String url) {
        final WebView actionWebView = webView;
        if (actionWebView == null) {
            return false;
        }

        if (!(viewContext instanceof Activity)) {
            return false;
        }
        final Activity actionActivity = (Activity) viewContext;

        Intent actionIntent = null;
        try {
            actionIntent = Intent.parseUri(url, Intent.URI_INTENT_SCHEME);
        } catch (Exception e) {
            // error handling if needed, but the original code just catches and sets to null
             Log.e("TAG", "Error parsing URI: " + e.getMessage());
            actionIntent = null; // Explicitly set to null on error
        }

        // check intent
        if (actionIntent == null) {
            Log.e("TAG", "intent is null");
            return false;
        }

        try {
            // Fallback URL -> Loading WebView For Kakao
            String fallbackUrl = actionIntent.getStringExtra("browser_fallback_url");
            if (fallbackUrl != null) {
                actionWebView.loadUrl(fallbackUrl);
                return true;
            }

            // action
            String actionPackageName = actionIntent.getPackage(); // Use getPackage() in Java
            if (actionPackageName != null && !actionPackageName.isEmpty()) { // Check for null and empty
                // launch activity
                Intent launchIntent = viewContext.getPackageManager().getLaunchIntentForPackage(actionPackageName);
                if (launchIntent != null) {
                    actionActivity.startActivity(launchIntent);
                    return true;
                }
            }

            // market
            if (actionPackageName != null && !actionPackageName.isEmpty()) { // Check for null and empty
                try {
                    Intent marketIntent = new Intent(Intent.ACTION_VIEW);
                    marketIntent.setData(Uri.parse("market://details?id=" + actionPackageName)); // Use setData() in Java
                    actionActivity.startActivity(marketIntent);
                    return true;
                } catch (Exception e) {
                    // error handling if needed
                     Log.e("TAG", "Error opening Market: " + e.getMessage());
                }
            }
        } catch (Exception e) {
            // error handling for the outer try block
             Log.e("TAG", "Error during intent handling: " + e.getMessage());
        }
        return false;
    }
    
    // ... other code ...
    // </code>
    // ... other code ...
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

***

### Market

schem market 처리 방식을 안내합니다.

{% tabs %}
{% tab title="KOTLIN" %}
{% code lineNumbers="true" %}
```kotlin
// ... import ...
class SampleActivity: AppCompatActivity() {
    
    // ... other code ...
    // <code>
    // ... other code ...
    
    private fun actionMarketTask(viewContext: Context, url: String): Boolean {
        val activity = viewContext as? Activity ?: return false
        kotlin.runCatching {
            val id = Uri.parse(url).getQueryParameter("id")
            val marketIntent = Intent(Intent.ACTION_VIEW).apply {
                data = Uri.parse("market://details?id=$id")
            }
            if (marketIntent.resolveActivity(viewContext.packageManager) != null) {
                activity.startActivity(marketIntent)
            } else {
                val viewIntent = Intent(Intent.ACTION_VIEW).apply {
                    data = Uri.parse("https://play.google.com/store/apps/details?id=$id")
                }
                activity.startActivity(viewIntent)
            }
        }.onFailure {
            // error
        }
        return true
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
// ... import code ...
public class SampleActivity extends AppCompatActivity {
    
    // ... other code ...
    // <code>
    // ... other code ...
    
    private boolean actionMarketTask(Context viewContext, String url) {
        if (!(viewContext instanceof Activity)) {
            return false;
        }
        final Activity activity = (Activity) viewContext;

        try {
            Uri uri = Uri.parse(url);
            String id = uri.getQueryParameter("id");
            if (id == null || id.isEmpty()) {
                // Handle cases where id is missing in the URL
                Log.e("TAG", "App ID missing from URL: " + url);
                return false;
            }
            Intent marketIntent = new Intent(Intent.ACTION_VIEW);
            marketIntent.setData(Uri.parse("market://details?id=" + id));
            if (marketIntent.resolveActivity(viewContext.getPackageManager()) != null) {
                activity.startActivity(marketIntent);
            } else {
                Intent viewIntent = new Intent(Intent.ACTION_VIEW);
                viewIntent.setData(Uri.parse("https://play.google.com/store/apps/details?id=" + id));
                activity.startActivity(viewIntent);
            }
        } catch (Exception e) {
            Log.e("TAG", "Error handling market intent: " + e.getMessage());
        }
        return true;
    }
    
    // ... other code ...
    // </code>
    // ... other code ...
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

***

### Mailto

{% tabs %}
{% tab title="KOTLIN" %}
{% code lineNumbers="true" %}
```kotlin
// ... import ...
class SampleActivity: AppCompatActivity() {
    
    // ... other code ...
    // <code>
    // ... other code ...
    
    private fun actionMailToTask(viewContext: Context, uri: Uri): Boolean {
        val activity = viewContext as? Activity ?: return false
        kotlin.runCatching {
            activity.startActivity(Intent(Intent.ACTION_VIEW, uri))
        }.onFailure {
            tales.error(moduleName = moduleName, throwable = it, trace = { "actionMailToTask { uri: $uri }" })
            it.message?.produce { message -> ToastView.show(context = viewContext, message = message) }
        }
        return true
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
// ... import code ...
public class SampleActivity extends AppCompatActivity {
    
    // ... other code ...
    // <code>
    // ... other code ...
    
    private boolean actionMailToTask(Context viewContext, Uri uri) {
        if (!(viewContext instanceof Activity)) {
            return false;
        }
        final Activity activity = (Activity) viewContext;

        try {
            activity.startActivity(new Intent(Intent.ACTION_VIEW, uri));
        } catch (Exception e) {
            Log.e("TAG", "actionMailToTask { uri: " + uri.toString() + " }", e);
            String message = e.getMessage();
            if (message != null) {
                 Toast.makeText(viewContext, message, Toast.LENGTH_SHORT).show();
            } else {
                 Toast.makeText(viewContext, "Error handling mailto link", Toast.LENGTH_SHORT).show();
            }
        }
        return true;
    }
    
    // ... other code ...
    // </code>
    // ... other code ...
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
{% endtab %}

{% tab title="iOS(WKWebView)" %}
### Javascript window.open

WKWebView javascript window.open() 명령어 처리 방법에 대한 안내

{% hint style="success" %}
**public protocol UIWebViewDelegate**

***

`func webView(_ webView: WKWebView, createWebViewWith configuration: WKWebViewConfiguration, for navigationAction: WKNavigationAction, windowFeatures: WKWindowFeatures) -> WKWebView?`

***

:white\_check\_mark: **여러개의 팝업이 열린 경우를 위해 해당 웹뷰에 대한 리소스 관리가 필요합니다.**

* 웹 뷰의 크기와 위치는 원하는 값을 넣어 사용합니다.
* 모달 윈도우의 옵션은 앱의 상황에 따라 변경 후 사용하세요.
{% endhint %}

{% code lineNumbers="true" %}
```swift
// ... import ...
class SampleViewController: UIViewController, UIWebViewDelegate {
    
    // ... other code ...
    // <code>
    // ... other code ...
    
    // MARK: - Javascript window.open { WKUIDelegate }
    func webView(_ webView: WKWebView, createWebViewWith configuration: WKWebViewConfiguration, for navigationAction: WKNavigationAction, windowFeatures: WKWindowFeatures) -> WKWebView? {    
        let viewControllerToPresent = UIViewController()
        viewControllerToPresent.view.backgroundColor = UIColor.white
        viewControllerToPresent.modalPresentationStyle = .automatic
        if let sheet = viewControllerToPresent.sheetPresentationController {
            sheet.prefersGrabberVisible = true
        }
        // 웹뷰를 생성하여 리턴하면 현재 웹뷰와 parent 관계가 형성됩니다.
        let modalView = WKWebView(frame: CGRect(x: 0, y: 12, width: self.bounds.width, height: self.bounds.height), configuration: configuration)
        // set delegate
        modalView.uiDelegate = self
        modalView.navigationDelegate = self
        // setup scrollview
        modalView.scrollView.bounces = false
        modalView.scrollView.isPagingEnabled = false
        modalView.scrollView.alwaysBounceVertical = false
        modalView.scrollView.showsVerticalScrollIndicator = false
        modalView.scrollView.showsHorizontalScrollIndicator = false
        modalView.scrollView.contentInsetAdjustmentBehavior = .never
        // addview
        viewControllerToPresent.view.addSubview(modalView)
        viewControllerToPresent.presentationController?.delegate = self
        // present
        self.viewController.present(viewControllerToPresent, animated: true);
        return modalView
    }
    
    // ... other code ...
    // <code>
    // ... other code ...
}
```
{% endcode %}

***

### javascript window.close

WKWebView javascript window.close() 명령어 처리 방법에 대한 안내

{% hint style="success" %}
**public protocol UIWebViewDelegate**

***

`func webViewDidClose(_ webView: WKWebView)`
{% endhint %}

{% code lineNumbers="true" %}
```swift
// ... import ...
class SampleViewController: UIViewController, UIWebViewDelegate {
    
    // ... other code ...
    // <code>
    // ... other code ...
    
    // MARK: - window.close { UIWebViewDelegate }
    func webViewDidClose(_ webView: WKWebView) {
        webView.removeFromSuperView()
        //webView = nil
    }
    
    // ... other code ...
    // <code>
    // ... other code ...
}
```
{% endcode %}

***

### Javascript Alert

Javascript alert 팝업 윈도우 처리에 대한 가이드

{% hint style="success" %}
**public protocol UIWebViewDelegate**

***

`func webView(_ webView: WKWebView, runJavaScriptAlertPanelWithMessage message: String, initiatedByFrame frame: WKFrameInfo, completionHandler: @escaping @MainActor () -> Void)`
{% endhint %}

{% code lineNumbers="true" %}
```swift
// ... import ...
class SampleViewController: UIViewController, UIWebViewDelegate {
    
    // ... other code ...
    // <code>
    // ... other code ...
    
    // MARK: - Javascript Alert Controll { UIWebViewDelegate }
    func webView(_ webView: WKWebView, runJavaScriptAlertPanelWithMessage message: String, initiatedByFrame frame: WKFrameInfo, completionHandler: @escaping @MainActor () -> Void) {
        let alertController = UIAlertController(title: nil, message: message, preferredStyle: .actionSheet)
        alertController.addAction(UIAlertAction(title: "확인", style: .default, handler: { (action) in
            completionHandler()
        }))
        DispatchQueue.main.async{
            self.viewController?.present(alertController, animated: true, completion: nil)
        }
    }
    
    // ... other code ...
    // <code>
    // ... other code ...
}
```
{% endcode %}

***

### Javascript Confirm

javascript confirm 팝업 윈도우 처리에 대한 가이드

{% hint style="success" %}
**public protocol UIWebViewDelegate**

***

`func webView(_ webView: WKWebView, runJavaScriptConfirmPanelWithMessage message: String, initiatedByFrame frame: WKFrameInfo, completionHandler: @escaping @MainActor (Bool) -> Void)`
{% endhint %}

{% code lineNumbers="true" %}
```swift
// ... import ...
class SampleViewController: UIViewController, UIWebViewDelegate {
    // ... other code ...
    // <code>
    // ... other code ...
    
    // MARK: - Javascript Confirm Controll { UIWebViewDelegate }
    func webView(_ webView: WKWebView, runJavaScriptConfirmPanelWithMessage message: String, initiatedByFrame frame: WKFrameInfo, completionHandler: @escaping @MainActor (Bool) -> Void) {
        let alertController = UIAlertController(title: nil, message: message, preferredStyle: .actionSheet)
        alertController.addAction(UIAlertAction(title: "확인", style: .default, handler: { (action) in
            completionHandler(true)
        }))
        alertController.addAction(UIAlertAction(title: "취소", style: .default, handler: { (action) in
            completionHandler(false)
        }))
        self.viewController?.present(alertController, animated: true, completion: nil)
    }
    
    // ... other code ...
    // <code>
    // ... other code ...
}
```
{% endcode %}

***

### Javascript Alert(Confirm) TextInput

javascript 텍스트 입력이 필요한 팝업 윈도우 처리에 대한 가이드

{% hint style="success" %}
**public protocol UIWebViewDelegate**

***

`func webView(_ webView: WKWebView, runJavaScriptTextInputPanelWithPrompt prompt: String, defaultText: String?, initiatedByFrame frame: WKFrameInfo, completionHandler: @escaping @MainActor (String?) -> Void)`
{% endhint %}

{% code lineNumbers="true" %}
```swift
// ... import ...
class SampleViewController: UIViewController, UIWebViewDelegate {
    
    // ... other code ...
    // <code>
    // ... other code ...
    
    // MARK: - Javascript InputText Controll { UIWebViewDelegate }
    func webView(_ webView: WKWebView, runJavaScriptTextInputPanelWithPrompt prompt: String, defaultText: String?, initiatedByFrame frame: WKFrameInfo, completionHandler: @escaping @MainActor (String?) -> Void) {
        let alertController = UIAlertController(title: nil, message: prompt, preferredStyle: .actionSheet)
        alertController.addTextField { (textField) in
            textField.text = defaultText
        }
        alertController.addAction(UIAlertAction(title: "확인", style: .default, handler: { (action) in
            if let text = alertController.textFields?.first?.text {
                completionHandler(text)
            } else {
                completionHandler(defaultText)
            }
        }))
        alertController.addAction(UIAlertAction(title: "취소", style: .default, handler: { (action) in
            completionHandler(nil)
        }))
        self.viewController?.present(alertController, animated: true, completion: nil)
    }
    
    // ... other code ...
    // <code>
    // ... other code ...
}
```
{% endcode %}

***

### Mailto

mailto scheme 처리에 방법에 대한 안내

**✓ update** → **subject, messageBody**

{% hint style="success" %}
**public protocol UIWebViewDelegate, MFMailComposeViewControllerDelegate**\
**WebView를 포함한 ViewController에 "MFMailComposeViewControllerDelegate" 선언이 필요합니다.**

***

`func webView(_ webView: WKWebView, decidePolicyFor navigationAction: WKNavigationAction, decisionHandler: @escaping @MainActor (WKNavigationActionPolicy) -> Void)`
{% endhint %}

<pre class="language-swift" data-line-numbers><code class="lang-swift"><strong>// ... import ...
</strong><strong>import MessageUI
</strong><strong>
</strong><strong>class WebContentViewController:..., ..., MFMailComposeViewControllerDelegate {
</strong>    
    // ... other code ...
    // &#x3C;code>
    // ... other code ...
    
    // MARK: - mailto: { UIWebViewDelegate }
    func webView(_ webView: WKWebView, decidePolicyFor navigationAction: WKNavigationAction, decisionHandler: @escaping @MainActor (WKNavigationActionPolicy) -> Void) {
        // check url
        guard let url = navigationAction.request.url else {
            self.error(stackMessage: "scheme -> url is null")
            decisionHandler(.allow)
            return
        }
        // check sheme
        guard let scheme = url.scheme else {
            decisionHandler(.allow)
            return
        }
        // mailto
        if scheme == "mailto" {
<strong>            hadleMailtoLink(url: url)
</strong><strong>            decisionHandler(.cancel)
</strong>            return
        }
    }
    
<strong>    private func hadleMailtoLink(url: URL) {
</strong>        if MFMailComposeViewController.canSendMail() {
            let mailVC = MFMailComposeViewController()
            mailVC.mailComposeDelegate = self
            // 1. mailto:주소?subject=...&#x26;body=... 에서 주소와 쿼리 분리
            if let components = URLComponents(url: url, resolvingAgainstBaseURL: false) {
                // 받는 사람 설정
                if let toAddress = components.path.removingPercentEncoding {
                    mailVC.setToRecipients([toAddress])
                }
                // 쿼리 파라미터 처리
                if let queryItems = components.queryItems {
                    for item in queryItems {
                        switch item.name.lowercased() {
                        case "subject":
                            mailVC.setSubject(item.value ?? "")
                        case "body":
                            mailVC.setMessageBody(item.value ?? "", isHTML: false)
                        default:
                            break
                        }
                    }
                }
            }
            viewController?.present(mailVC, animated: true)
        } else {
            // 메일을 보낼 수 없는 경우: 사용자에게 안내
            let alert = UIAlertController(
                title: "메일 설정 오류",
                message: "메일 앱이 설정되어 있지 않거나 메일을 보낼 수 없습니다. 메일 계정을 설정해주세요.",
                preferredStyle: .alert
            )
            alert.addAction(UIAlertAction(title: "확인", style: .default, handler: nil))
            viewController?.present(alert, animated: true, completion: nil)
        }
    }
    
<strong>    // MARK: - MFMailComposeViewControllerDelegate
</strong><strong>    func mailComposeController(_ controller: MFMailComposeViewController, didFinishWith result: MFMailComposeResult, error: Error?) {
</strong>        // 필요시 구현
        switch result {
        case .cancelled:
            print("메일 전송 취소됨")
        case .saved:
            print("메일 임시 저장됨")
        case .sent:
            print("메일 전송 성공")
        case .failed:
            print("메일 전송 실패: \(error?.localizedDescription ?? "알 수 없는 오류")")
        @unknown default:
            print("알 수 없는 결과")
        }
        // 반드시 dismiss 해야 함!
<strong>        controller.dismiss(animated: true, completion: nil)
</strong>    }
    
    // ... other code ...
    // &#x3C;code>
    // ... other code ...
}
</code></pre>

***

### Tel

tel scheme 처리에 방법에 대한 안내

{% hint style="success" %}
**public protocol UIWebViewDelegate**

***

`func webView(_ webView: WKWebView, decidePolicyFor navigationAction: WKNavigationAction, decisionHandler: @escaping @MainActor (WKNavigationActionPolicy) -> Void)`
{% endhint %}

<pre class="language-swift" data-line-numbers><code class="lang-swift">// ... import ...
class SampleViewController: UIViewController, UIWebViewDelegate {
    
    // ... other code ...
    // &#x3C;code>
    // ... other code ...
    
    // MARK: - tel: { UIWebViewDelegate }
    func webView(_ webView: WKWebView, decidePolicyFor navigationAction: WKNavigationAction, decisionHandler: @escaping @MainActor (WKNavigationActionPolicy) -> Void) {
        // check url
        guard let url = navigationAction.request.url else {
            self.error(stackMessage: "scheme -> url is null")
            decisionHandler(.allow)
            return
        }
        // check sheme
        guard let scheme = url.scheme else {
            decisionHandler(.allow)
            return
        }
        // tel
        if scheme == "tel" {
<strong>            handleTelLink(url: url)
</strong><strong>            decisionHandler(.cancel)
</strong>            return
        }
    }
    
<strong>    private func handleTelLink(url: URL) {
</strong>        UIApplication.shared.open(url, options: [:], completionHandler: nil)
    }
    
    // ... other code ...
    // &#x3C;code>
    // ... other code ...
}    
</code></pre>
{% endtab %}
{% endtabs %}






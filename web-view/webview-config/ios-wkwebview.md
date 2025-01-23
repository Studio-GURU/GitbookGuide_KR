---
icon: apple
---

# iOS WKWebView

## 유료 결제를 위한 Scheme 등록

TossPayments를 통한 유료 결제에 필요한 은행앱 패키지 등록

자세한 내용은 아래의 링크를 확인 하세요.

{% embed url="https://docs.tosspayments.com/guides/webview#ios" %}

***

## 컨텐츠 보호

`UITextField`의 isSecureTextEntry 속성을 통해 사용자가 스크린 캡춰를 할 수 없도록 우회 처리해야 합니다.

{% code lineNumbers="true" %}
```swift
private let preventedView = UITextField()

func applySecureContent() {
    self.addSubview(self.preventedView)
    self.preventedView.backgroundColor = .clear
    self.preventedView.isSecureTextEntry = true
    self.preventedView.isUserInteractionEnabled = false
    self.preventedView.translatesAutoresizingMaskIntoConstraints = false
    self.preventedView.centerYAnchor.constraint(equalTo: self.centerYAnchor).isActive = true
    self.preventedView.centerXAnchor.constraint(equalTo: self.centerXAnchor).isActive = true
    self.preventedView.leftView = UIView(frame: CGRect(x: 0, y: 0, width: self.preventedView.frame.self.width, height: self.preventedView.frame.self.height))
    self.preventedView.leftViewMode = .always
    self.layer.superlayer?.addSublayer(self.preventedView.layer)
    self.preventedView.layer.sublayers?.last?.addSublayer(self.layer)
}

//..
//..
override func viewDidAppear(_ animated: Bool) {
    DispatchQueue.main.async {
        applySecureContent()
    }
}
```
{% endcode %}

***

## Scheme 처리 <a href="#scheme" id="scheme"></a>

{% hint style="info" %}
웹뷰 구성에 필요한 Scheme 처리에 대한 **예제 코드**이며, 실 프로젝트에서는 **참고만 하시길 바랍니다**.
{% endhint %}

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
// MARK: - window.close { UIWebViewDelegate }
func webViewDidClose(_ webView: WKWebView) {
    webView.removeFromSuperView()
    //webView = nil
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
```
{% endcode %}

***

### Mailto, Tel&#x20;

mailto, tel scheme 처리에 방법에 대한 안내

{% hint style="success" %}
**public protocol UIWebViewDelegate**

***

`func webView(_ webView: WKWebView, decidePolicyFor navigationAction: WKNavigationAction, decisionHandler: @escaping @MainActor (WKNavigationActionPolicy) -> Void)`
{% endhint %}

{% code lineNumbers="true" %}
```swift
// MARK: - mailto:, tel: { UIWebViewDelegate }
func webView(_ webView: WKWebView, decidePolicyFor navigationAction: WKNavigationAction, decisionHandler: @escaping @MainActor (WKNavigationActionPolicy) -> Void) {
    // check url
    guard let url = navigationAction.request.url else {
        self.error(stackMessage: "scheme -> url is null")
        decisionHandler(.allow)
        return
    }
    // check scheme
    guard let scheme = url.scheme else {
        self.error(stackMessage: "scheme -> protocol is null")
        decisionHandler(.allow)
        return
    }
    // check mailto, tel
    let schemeOpenUrl = switch scheme {
    case "mailto": url.absoluteString.replacingOccurrences(of: "mailto:", with: "")
    case "tel": url.absoluteString.replacingOccurrences(of: "tel:", with: "")
    default: ""
    }
    // check empty
    if schemeOpenUrl.isEmpty {
        decisionHandler(.allow)
        return
    }
    // create URLComponents
    var components = URLComponents()
    components.scheme = url.scheme
    components.path = schemeOpenUrl
    guard let componentUrl = components.url else {
        decisionHandler(.allow)
        return
    }
    // open application
    if UIApplication.shared.canOpenURL(componentUrl) {
        UIApplication.shared.open(componentUrl)
        decisionHandler(.cancel)
    } else {
        decisionHandler(.allow)
    }
}
```
{% endcode %}


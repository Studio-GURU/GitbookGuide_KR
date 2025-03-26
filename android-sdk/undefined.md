---
description: 보물섬이 제공하는 "오늘의추천" 페이지를 사용하지 않고, 별도 화면을 구성하려면 API 이용하시면 됩니다.
icon: list
---

# 추천 컨텐츠 목록 조회

## API

```
Contents.recommendationContentModel(
    signature, 
    adid, 
    isAdult, 
    response: IResponse<MutableList<RecommendationContentModel>>
)
```

<table><thead><tr><th width="146">Name</th><th width="143">Type</th><th width="118">Required</th><th>Description</th></tr></thead><tbody><tr><td>signature</td><td>string</td><td>required</td><td><a data-mention href="sign.md">sign.md</a></td></tr><tr><td>adid</td><td>string</td><td>option</td><td>광고 식별값(ADID, IDFA)</td></tr><tr><td>isAdult</td><td>boolean</td><td>option</td><td> 성인 여부</td></tr></tbody></table>

***

## Response(RecommendationContentModel)

<table><thead><tr><th width="239">Fields</th><th width="106">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>recommendationSN</code></td><td>number</td><td>sequence</td></tr><tr><td><code>title</code></td><td>string</td><td>제목</td></tr><tr><td><code>description</code></td><td>string</td><td>내용</td></tr><tr><td><code>thumbnail</code></td><td>string</td><td>썸네일 이미지 경로 ( 세로 )</td></tr><tr><td><code>subThumbnail</code></td><td>string</td><td>썸네일 이미지 경로 ( 가로 )</td></tr><tr><td><code>contentType</code></td><td>string</td><td>웹툰 | 웹소설</td></tr><tr><td><code>contentCName</code></td><td>string</td><td>작품 키</td></tr><tr><td><code>episodeNo</code></td><td>number</td><td>회차 번호</td></tr><tr><td><code>genre</code></td><td>string</td><td>장르</td></tr><tr><td><code>link</code></td><td>string</td><td><p>제공되는 링크 뒤에 sign 붙여서 전달</p><p>예)<code>&#x26;sign=1724328195.3da08653e6c1420aac89eecdf5c20063.OGMzYjUzYTUyYjE1YTJiNDAyZGM3MGJiZmMzMDI2YWE1NDg0YWY2ZTdjNjMyZTJlMTdjMjQyOGU1NjZhYjdhYQ</code></p></td></tr><tr><td><code>returnUrl</code></td><td>string</td><td>최종 이동 링크 ( 참고용 )</td></tr><tr><td><code>order</code></td><td>number</td><td>노출 우선 순위 ( 같은 값이 존재할 수 있습니다 )</td></tr><tr><td><code>recommendationDate</code></td><td>string</td><td>추천일 ( YYYY-MM-DD )</td></tr><tr><td><code>freeEpisode</code></td><td>number</td><td>무료 회차 수</td></tr><tr><td><code>isRewardAvailable</code></td><td>boolean</td><td>포인트 지급 가능 여부</td></tr><tr><td><code>minReward</code></td><td>number</td><td>지급 가능 최소 금액 ( 지급 불가능일 경우 0으로 반환 )</td></tr><tr><td><code>maxReward</code></td><td>number</td><td>지급 가능 최대 금액 ( 지급 불가능일 경우 0으로 반환 )</td></tr></tbody></table>

## Usage

{% tabs %}
{% tab title="KOTLIN" %}
```kotlin
Contents.recommendationContentModel(
    signature = ${signature}, 
    adid = ${adid}, 
    isAdult = ${isAdult}, 
    response = object : Contents.IResponse<MutableList<RecommendationContentModel>> {
        override fun onSuccess(success: MutableList<RecommendationContentModel>) {
        }

        override fun onError(errorCode: String, errorMessage: String) {
        }
    })
}
```
{% endtab %}

{% tab title="JAVA" %}
```java
Contents.recommendationContentModel(        
    ${signature}, // signature(sign값)
    ${adid}, // adid(광고아이디)
    ${isAdult}, // isAdult(성인여부)
    new Contents.IResponse<List<RecommendationContentModel>>() {
        @Override
        public void onSuccess(List<RecommendationContentModel> success) {
            
        }

        @Override
        public void onError(@NonNull String errorCode, @NonNull String errorMessage) {

        }
    }
);
```
{% endtab %}
{% endtabs %}






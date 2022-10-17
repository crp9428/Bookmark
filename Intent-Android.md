# 안드로이드에서 구글 크롬으로 URL 열기   

- 당시 개발하던 모바일(안드로이드) 웹앱이 기기 특성과 앱 구조 상 외부 URL로 진입이 불가능한데, 외부 링크를 반드시 열어야 하는 상황
- 안드로이드 기기는 구글 크롬이 모두 설치되어 있다는 점에 착안하여 intent를 이용, 크롬에서 링크가 열리도록 함
<br>

```javascript
var agent = navigator.userAgent.toLowerCase();
if (Number(agent.indexOf('android')) > -1) {
  location.href='intent://' + url.replace(/http:\/\/|https:\/\//g, '') + '#Intent;scheme=http;package=com.android.chrome;end';
}

```   

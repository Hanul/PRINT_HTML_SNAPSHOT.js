*이제 검색엔진들이 동적으로 생성된 DOM에 대해서도 검색 결과에 반영하기 때문에, 이 프로젝트는 더 이상 필요하지 않습니다.*

# PRINT_HTML_SNAPSHOT.js
검색엔진의 크롤러들이 Single Page 웹 애플리케이션을 방문할 때 HTML 스냅샷을 제공합니다.

이 기능을 사용하려면 [PhantomJS](http://phantomjs.org)가 서버에 설치되어 있어야 합니다.

```javascript
if (params._escaped_fragment_ !== undefined) {
	
	let content = '';
	
	let phantom = require('child_process').spawn('phantomjs', [__dirname + '/PRINT_HTML_SNAPSHOT.js', (CONFIG.webServerPort === undefined ? CONFIG.securedWebServerPort : CONFIG.webServerPort), uri === '' ? params._escaped_fragment_ : decodeURIComponent(uri)]);
    
    phantom.stdout.setEncoding('utf8');
    
    phantom.stdout.on('data', (data) => {
        content += data.toString();
    });
    
    phantom.on('exit', (code) => {
		response(content);
    });
    
    return false;
}
```
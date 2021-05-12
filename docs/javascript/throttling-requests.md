# 지나친 requests를 조절해보자

## throttling & debouncing

throttling 과 debouncing 개념이 있다.

둘 다 성능을 고의로 떨어뜨려 문제를 해결하는 기법이라고 볼 수 있다.

둘의 차이를 매우 간단하게 요약하면

- throttling 은 delay 내의 이벤트를 적당히 무시하고 처리
- debouncing 은 주어진 시간 내 이벤트를 적당히 그룹핑 처리

가 될 수 있는데 이렇게만 얘기하기엔 좀 나이브하긴 하지만..

debounce 같은 경우는 UI 상에서 검색 기능을 구현하는 경우에 많이 본 적이 있다.

요새는 더 즉각적인 UX를 위해 사용자가 검색 버튼이나 엔터키를 누르는 것 대신 문자열을 입력할 때마다 검색 결과를 필터링해서 보여주는 방식도 많이 쓰인다.

이 때 '한국'을 검색할 때 ㅎ,ㅏ,ㄴ,ㄱ,ㅜ,ㄱ 을 검색하는 동안 매번 검색 request를 날리게 되면 얻는 성능에 비해 비용이 큰 구현이 된다.

그래서 이를 디바운스를 적용해서 적당하게~ 1~2초 정도 여유를 두어 1~2초간 모여진 문자열에 대해 request를 날리면 성능과 사용자 경험 둘 다 잡을 수 있다!

## throttling requests

지나친 request 를 적당하게 스로틀링 해야되는 이슈를 마주하게 되었다.

나는 구글드라이브와 같은 웹 드라이브를 만들고 있는데

이를 테면 (이런 경우는 없겠지만 적절한 예시가 안 떠올라) node_modules 같이 내부에 수많은 폴더와 파일로 점칠된 그런 폴더를 하나 업로드 한다고 해보자

파일 업로드는 한 개씩 그 메타정보라던지 실제 파일이라던지 작업을 처리하게 되기 때문에 수십만 개의 request 가 필요하게 된다.

이런 경우에 loop 를 돌면서 동시에 수십만 개의 리퀘스트를 날려버리면 서버도 문제지만 웹 브라우저에서도 감당이 안되는 것 같았다..

그래서 의도적으로 일정한 시간동안 일정한 수의 파일 업로드만 허용하도록 구현하여 전체 업로드는 시간이 좀 걸릴지라도 가능하게 만드는 구현이 필요하다.

리액트에서 어떤식으로 throttling 하는지를 공부하기 위해 찾은 링크들

https://blog.logrocket.com/throttling-data-requests-with-react-hooks/

https://ncoughlin.com/posts/react-throttling-api-requests/

https://blog.bitsrc.io/improve-your-react-app-performance-by-using-throttling-and-debouncing-101afbe9055

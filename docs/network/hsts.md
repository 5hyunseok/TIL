# Arachni 사용 및 HSTS에 대한 내용

## Arachni 사용

Arachni 는 Web application security scanner 이다.

- 무료로 사용할 수 있고, 다른 유료 스캐너 라이브러리나 서비스에 비해도 꽤 괜찮은 벤치마크를 자랑함
- 서버를 띄워서 웹 ui 로 조작하는 방식이기 때문에 사용이 편리함

심지어 도커 이미지를 배포하고 있길래 간단하게 도커로 띄워보았다.

https://hub.docker.com/r/arachni/arachni/

도커로 띄우고 9494포트로(default) 접속해서 target url 만 넘기면 바로 스캔을 해 볼 수 있다.

## HSTS (HTTP Strict Transport Security)

아라크니로 몇몇 사이트를 돌려보니

```
Missing 'Strict-Transport-Security' header
```

라는 취약점 항목을 자주 볼 수 있었다.

이 항목은 웹서버에서 HSTS를 만족하지 않을 때 생기는 항목이다.

기본적으로 https 를 사용하는 웹서버는 http 요청에 대해서 https 로 리다이렉트 하는 방식으로 https 를 강제하곤 한다.

하지만 이 리다이렉트가 취약점으로 작용할 수 있다고 한다.

그래서 브라우저에서 https 를 강제하도록 만드는 방식이 있는데 이것이 HSTS 이다. 이 방식을 사용하면 클라이언트 (웹 브라우저)에서 http 연결 자체가 되지 않는다.

HSTS를 클라이언트 측인 웹 브라우저 사용자가 도메인 별로 사용하도록 할 수도 있다.

보통은 웹서버 response header에 Strict-Transport-Security 값을 내려주어 세팅하게 한다.

https 로 웹서버를 운영할 것이라면 무조건 세팅하는 게 좋겠다.

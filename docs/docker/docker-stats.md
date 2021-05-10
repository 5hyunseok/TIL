# 도커 리소스 사용량 모니터링하기

도커 컨테이너들은 띄울 때 따로 리소스 제한을 걸지 않는 이상 호스트의 리소스를 최대한 활용한다.

그래서 docker-compose 같이 여러 컨테이너를 한꺼번에 띄우다보면 컨테이너들이 현재 리소스를 얼마나 쓰고 있는건지 모니터링 해야할 때가 생기는 것 같다.

가장 간단하게 도커 리소스 사용량 모니터링 하는 방법은 다음과 같다.

```shell
$ docker stats
```

docker stats 를 이용하면

```shell
CONTAINER ID    NAME    CPU %   MEM USAGE / LIMIT   MEM %   NET I/O             BLOCK I/O       PIDS
7b4c5c69bd59    xxx     0.06%   696.6MiB / 31.34GiB 2.17%   6.19MB / 1.39MB     3.73MB / 401kB  232
e58b75d20ce1    yyy     0.11%   794.2MiB / 31.34GiB 2.47%   8.65MB / 6.03MB     5.19MB / 397kB  661
```

이런식으로 실시간으로 각 컨테이너별 cpu, memory, i/o 사용량을 알려준다.

```shell
$ docker stats --no-stream
```

복사하고 싶거나 여러 이유로 실시간이 아니라 현재 시점의 사용량만 포착하고 싶을때는 `--no-stream` 옵션을 주면 된다.

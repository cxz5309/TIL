# docker 오류 목록

## error during connect: Post http://%2F%2F.%2Fpipe%2Fdocker_engine/v1.40/containers/create: open //./pipe/docker_engine: The system cannot find the file specified. In the default daemon configuration on Windows, the docker client must be run elevated to connect. This error may also indicate that the docker daemon is not running. #1825

### 해결
[해결](https://github.com/docker/for-win/issues/1825#issuecomment-433719346)
- docker 연결시 daemon 설정이 window로 되어있지 않아서 생기는 문제인것 같다.
1. 도커 재설치 - 실패
2. 
```
cd "C:\Program Files\Docker\Docker"
./DockerCli.exe -SwitchDaemon
```
3. 해결 확인
```
실패
docker ps
//./pipe/docker_engine: The system cannot find the file specified
성공
docker ps
현재 가동중인 컨테이너 출력
```

- 예전에 docker 쓸 때 리눅스로 설정을 변경한 적이 있었는데 그 때문인 것 같다. 오랜만에 써서 까맣게 잊고 있었다.

---

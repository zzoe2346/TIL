# Docker교과서에서 익힌 명령어
## ch03 도커 이미지 만들기
`docker container run 8a8853903859` 
컨테이너에 이미지 올린다. 이미지 명칭은 이미지 이름 or 해시값

`docker container run -it 8a8853903859`
-it 플래그 사용하면 컨테이너를 대화식으로 실행 가능(터미널)

`docker container commit ch03lab newCh03`
commit =>     Create a new image from a container's changes
컨테이너의 변화가 있으면 커밋을해 새로운 이미지를 생성함

Docker 명령어에서 `-it`는 다음과 같은 두 가지 옵션을 결합한 것입니다:

1. `-i` 또는 `--interactive`: 컨테이너의 표준 입력(stdin)을 열어둡니다. 이를 통해 터미널 세션에서 입력을 받을 수 있게 됩니다.
2. `-t` 또는 `--tty`: 가상 터미널(tty)을 할당합니다. 이를 통해 컨테이너 내부의 쉘에서 명령을 실행하고 결과를 볼 수 있는 터미널 환경을 제공합니다.

이 두 옵션을 결합하여 사용하면, 컨테이너를 인터랙티브 모드로 실행할 수 있습니다. 즉, 사용자와 상호작용할 수 있는 쉘을 실행할 수 있게 됩니다. 다음은 예시입니다:

```bash
docker container run -it ubuntu /bin/bash
```

이 명령어는 `ubuntu` 이미지를 사용하여 컨테이너를 생성하고, `/bin/bash` 쉘을 실행합니다. 사용자는 해당 쉘에서 직접 명령을 입력하고 결과를 볼 수 있습니다.

## build
docker build -t {imageName} .

## run
docker run -p 8080:8080 {imageName}

## pull
docker image pull [OPTIONS] NAME[:TAG|@DIGEST]

개발중인 컴퓨터에서  build => push 하고
서버 컴퓨터에서 pull => run 하면 서버 환경 신경 안쓰고 배포 성공!  굳.
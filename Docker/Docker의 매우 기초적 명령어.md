## build
docker build -t {imageName} .

## run
docker run -p 8080:8080 {imageName}

## pull
docker image pull [OPTIONS] NAME[:TAG|@DIGEST]

개발중인 컴퓨터에서  build => push 하고
서버 컴퓨터에서 pull => run 하면 서버 환경 신경 안쓰고 배포 성공!  굳.
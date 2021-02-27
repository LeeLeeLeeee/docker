
# 도커 컴포즈 설정을 위한 파이썬/Django 샘플 프로젝트

참고 사이트 : https://www.44bits.io/ko/post/almost-perfect-development-environment-with-docker-and-docker-compose

### 샘플 프로젝트 실행 요약

```
$ git clone https://github.com/raccoonyy/django-sample-for-docker-compose.git
$ cd django-sample-for-docker-compose
$ docker-compose up
```

## Docker Image, Container

### Image 
 - 하나의 구성 환경의 스냅샷을 찍는 것. 찰칵! 🎞
 - docker build
 #### docker build 옵션 정리
 ```
    -t : 저장소 이름, 이미지 이름등 태그 설정
    --force-rm : 이미지 생성에 실패했을 때도 임시 컨테이너를 삭제
    --no-cache : 이전 빌드에서 생성된 캐시 미사용
    --q : DockerFile의 RUN이 실행한 출력 결과를 표시하지 않습니다.
    --rm : 이미지 생성에 성공했을 떄 임시 컨테이너를 삭제합니다.

 ```
### 컨테이너
 - 독립적으로 실행 환경을 구성해주는 것 독립성 확보
 - docker run
#### docker run 옵션 정리
 ```bash
   docker run [OPtions] [Image] [COMMAND]
    --rm
    -i : 사용자가 입출력할 수 있는 상태
    -t : tty 가상 터미널 환경
    -e
    --name : 컨테이너 이름
    -p : 포트 연결 (호스트 포트:컨테이너 포트)
    --link : 컨테이너간 연동을 자동으로 제어 해주는 것
    --volume, -v : 도커가 특정 볼륨를 지속적으로 마운트하게 해줌. <마운트할 볼륨:컨테이너의 경로>
    * 바인드 마운트 : 생성한 볼륨 대신 특정 경로를 지정하는 것 명령어는 -v로 동일하다. <마운트 할 폴더 경로:컨테이너 경로>
 ```
 > Docker Network 구조 <https://bluese05.tistory.com/15>
 > Docker Link <https://bluese05.tistory.com/54>
 > Docker Volumne <https://www.daleseo.com/docker-volumes-bind-mounts/>
 ## Docker 명령어 정리
 #### `search` Docker hub에 있는 Image 검색
 #### `pull` Docker hub로 부터 image를 다운받는 명령어
 #### `images` Host PC의 Image를 출력
 #### `run` Container를 생성과 동시에 컨테이너로 접속
##### ** option( -i : , -t ,  -d : 컨테이너를 데몬 프로세스 형태로 끝나도 유지)
 #### `exec` 외부에서 컨테이너 안의 명령을 실행하는 명령어
 ##### ** option( -d : 명령을 백그라운드로 실행, -i : 표준 입력 활성화, -t : TTY 모드 사용 bash사용하려면 이 설정을 해야함)
 #### => docker exec -it <Container-name> <command>
 #### `ps` Docker 컨테이너 확인
 #### `start` Docker 컨테이너 실행
 #### `attach` 컨테이너 접속하기
 #### `stop` 컨테이너 종료하기
 #### `rm` 컨테이너 삭제 
 #### `inspect` 도커에서 필요한 것의 상세정보를 보기 위한 것
 #### `history` 이미지가 만들어지기 까지의 과정 전체를 보여주는 명령어.

 ## DockerFile 내용 정리.
 #### DockerFile이란?
 - Docker Image를 만들기 위한 설정 파일. 설정되어 있는 내용을 Docker가 읽어 Docker 이미지를 구성합니다.

 ```python

#FROM => 기반이 되는 이미지 레이어 <이미지 이름>:<태그> 형식으로 작성
FROM ubuntu:14.04

# RUN =>도커 이미지가 생성되기 전에 수행할 쉘 명령어
# app 디렉토리 생성
RUN mkdir -p /app

#Docker 이미지 내부에서 RUN, CMD, ENTRYPOINT의 명령이 실행될 디렉터리를 설정합니다.
WORKDIR /app

# 현재 디렉터리에 있는 파일들을 이미지 내부 /app 디렉터리에 추가함
ADD     . /app

RUN apt-get update

RUN apt-get install apache2

RUN service apache2 start

# VOLUMNE => 디렉터리 내용을 컨테이너에 저장하지 않고 호스트에 저장하도록 설정.
VOLUME ["/data", "/var/log/httpd"]

# EXPOSE 호스트와 연결할 포트 번호.
# 하기 포트를 외부로 노출합니다.
EXPOSE 80

# CMD => 컨테이너가 시작되었을 때 실행할 실행 파일 또는 셸 스크립트. DockerFile내 1회만 쓸 수 있음.    
# 쉘을 사용하지 않고 컨테이너가 시작되었을 때 logbackup 스크립트를 실행
CMD ["/app/log.backup.sh"]

 ```
## dockerignore
- Docker 이미지 생성 시 이미지안에 들어가지 않을 파일을 지정 할 수 있음.

 ## Docker-compose 란?


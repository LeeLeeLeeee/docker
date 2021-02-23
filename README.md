
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
    -t
 ```
### 컨테이너
 - 독립적으로 실행 환경을 구성해주는 것 독립성 확보
 - docker run
#### docker run 옵션 정리
 ```
    --rm
    -it
    -e
    --name
    -p
    --link
    --volume
 ```

 ## Docker File 이란?


 ## Docker-compose 란?


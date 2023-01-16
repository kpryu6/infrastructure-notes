# Introduction

## 도커의 비유적인 개념

### 앱스토어 비유

|App store|$\leftrightarrow$|[Docker Hub](https://hub.docker.com)|
|---|---|---|
|$\downarrow$ download| |$\downarrow$ [pull](https://docs.docker.com/engine/reference/commandline/pull/)|
|program|$\leftrightarrow$|image|
|$\downarrow$ run| |$\downarrow$ run|
|process|$\leftrightarrow$|container|

#
</br>

## 실습 예제

## **Apache Web server**을 Container 위에서 실행

### pull

- httpd를 검색하여 image 확인
```
docker pull httpd
```

- pull 후 images 확인
```
docker images
```
  
### run

- httpd 기반의 Container 생성 및 실행
```
docker run httpd
```

- ws2라는 이름 지정 후 생성 및 실행
```
docker run --name ws2 httpd
```

- List Containers
```
docker ps
```

- Stop or Start Container
```
docker stop ws2
docker start ws2
```

- Log or Log watching
```
docker logs ws2
docker logs -f ws2
```

- Delete Container or Image
```
(Stop 후 삭제) docker rm ws2
(실행 중 강제 삭제) docker rm --force ws2
(이미지 삭제) docker rmi httpd
```

---

## Network

### 도커 없이 Web Server 구축

- 2대 컴퓨터 필요
  - Web browser 설치된 1대
  - Web Server 설치된 1대
    - Web Page를 파일로 만들어서 저장장치 특정 디렉토리에 위치시켜야함 (/usr/local/apache2/htdocs/ 안에 있는 index.html)
    - 데이터가 저장된 공간 = File System

- Apache Web Server은 `80번 포트`에서 접속을 대기하고 있도록 설정되어 있음
- Web Server가 설치된 컴퓨터의 주소 = example.com

<p align="center"><img src="https://user-images.githubusercontent.com/113777043/212723381-0db9733e-e9e4-41bf-95e6-a139ab716078.png" ></p>


### 도커로 Web Server 구축

- Web Server가 Container에 설치됨
- Container가 설치된 OS는 Host
  - Host와 Container 각각 독립적인 실행 환경
    - 독립적인 포트 & File System

- ws3 Container / 8081 -> 80
```
docker run --name ws3 -p 8081:80 httpd
```

- web browser과 Container가 같은 컴퓨터이기에 localhost
  - localhost:8081/index.html => it works!

<p align="center"><img src="https://user-images.githubusercontent.com/113777043/212723395-838935ca-7a9f-4f82-b4ca-a3550077c13d.png"></p>

</br>

### index.html 편집

- `index.html`은 `/usr/local/apache2/htdocs` 안에 존재

- Container 안에 들어가기 $\Rightarrow$ 앞에 # 붙음
```
docker exec -it ws3 /bin/sh (기본)
docker exec -it ws3 /bin/bash (기능이 좀 더 많음)
```
`-it` = Container와 지속적으로 연결 (-i + -t)

- 현재 디렉토리
```
# pwd
```

- 편집하기 위해 apt나 yum을 이용해 nano나 vim 설치 필수
```
# apt update
# apt install nano
# nano index.html
```

- index.html 진입 후 `^O` 키를 이용해 수정 후 `^X` Y Enter 로 저장

---

## Host와 Container의 디렉토리 연결

- Host의 디렉토리에 index.html 생성
```html
<html>
  <body>
    Hello, Docker!
  </body>
</html>
```

- 8888 -> 80연결, 디렉토리 연결
```
docker run -p 8888:80 -v ~/Desktop/htdocs:/usr/local/apache2/htdocs/ httpd
```

<p align="center"><img src="https://user-images.githubusercontent.com/113777043/212722645-4d06aaff-600d-4bcf-a446-ae806f06340b.png"></p>












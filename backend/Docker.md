# Docker

## Docker란?

**컨테이너 기반의 오픈소스 가상화 플랫폼**

다양한 프로그램, 실행환경을 컨테이너로 추상화하고 동일한 인터페이스를 제공하여 프로그램의 배포 및 관리를 단순하게 해준다. 백엔드 프로그램, DB, 서버, 메시지 큐 등 어떤 프로그램도 컨테이너로 추상화할 수 있고 AWS, Azure, Google cloud 등 어디에서든 실행할 수 있다.



#### 컨테이너(Container)

기존의 방식은 OS를 가상화하는 것인 반면, 컨테이너는 **프로세스를 격리**하는 방식이다. 

전체 OS를 가상화하는 방식은 사용법은 간단하지만 무겁고 느리다. 프로세스를 격리하는 방식은 프로세스가 필요한 만큼만 CPU나 메모리를 사용하기 때문에 가볍고 빠르게 동작한다. 새로운 컨테이너를 만드는데는 1-2초 남짓이다. 도커는 자체적인 libcontainer 기술을 활용하여 이러한 컨테이너 기술을 구현했다.



#### 이미지(Image)

도커 이미지는 **컨테이너 실행에 필요한 파일과 설정값 등을 포함하고 있는 것**으로 상태값을 가지지 않고 immutable하다. 컨테이너는 이미지를 실행한 상태라고 볼 수 있으며 추가되거나 변하는 값들은 컨테이너에 저장된다. 

같은 이미지에서 여러개의 컨테이너를 생성할 수 있으며, 컨테이너의 상태를 바꾸거나 삭제해도 이미지는 변하지 않고 남아있다.

ubuntu 이미지, MySQL 이미지, node 이미지 등 여러개의 등록된 이미지가 있으며 도커 이미지는 Docker hub에 등록하거나 Docker Registry를 만들어 관리할 수 있다.

도커는 이미지 생성을 위해 ``Dockerfile``이라는 파일에 DSL(Domain-specific language)라는 언어를 이용하여 이미지 생성 과정을 적는다.



## Docker 설치 및 배포

#### Docker 설치

ncloud로 띄운 ubuntu 서버에서 docker를 설치한다.

``` bash
curl -fsSL https://get.docker.com/ | sudo sh
```

docker는 기본적으로 root권한이 필요하기 때문에 ``sudo`` 없이 사용하려면 docker 그룹에 현재 사용자를 추가해줘야 한다. 이때 로그아웃하고 다시 로그인해야 권한이 적용된다

``` shell
sudo usermod -aG docker $USER # 현재 접속중인 사용자에게 권한 부여
```

정상적으로 설치되었는지 아래 명령어를 통해 확인한다.

```shell
docker version
```

``docker run ${image}``를 하면 이미지로 컨테이너를 생성한다. 이미지가 없으면 pull한 후에 생성한다. 

```bash
docker run ubuntu
```

``docker images``를 통해 도커가 다운받은 이미지 목록을 확인할 수 있다.

``docker ps``를 통해 컨테이너 목록을 볼 수 있다.



#### Docker를 통한 node js 배포

실행할 app.js가 있는 디렉토리 위치에 Dockerfile을 만든다.

```bash
touch Dockerfile
```

아래와 같이 각자 환경에 맞게 ``Dockerfile``을 작성한다.

```dockerfile
FROM node:14

WORKDIR ./

COPY ./package*.json ./

RUN npm install --production ## dev-dependencies 제외하고 설치

COPY . . # Docker 이미지 안에 앱 소스코드를 넣는다

EXPOSE 3000 # 포트 바인딩

CMD ["npm", "start"] # 실행 명령
```

 docker image에 로컬모듈을 복사하는 것을 막기 위해 ``.dockerignore``파일을 만든다.

```이dockerfile
node_modules
npm-debug.log
```

이제 ``Dockerfile``이 있는 디렉토리에서 이미지를 빌드한다. ``Dockerfile``에 있는 명령어대로 실행된다.

```dockerfile
docker build -t <username>/tagname ## -t 옵션으로 이미지에 태그를 추가
```

빌드한 이미지를 실행한다.

```dockerfile
docker run -p 3000:3000 -d <username>/tagname
```

도커가 컨테이너 내의 3000포트(뒤)를 머신의 3000포트(앞)로 매핑한 것이다.

 

#### reference

* https://subicura.com/2017/01/19/docker-guide-for-beginners-2.html

* https://nodejs.org/ko/docs/guides/nodejs-docker-webapp/
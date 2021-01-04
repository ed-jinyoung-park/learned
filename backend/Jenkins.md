# Jenkins

### Jenkins란?

SW 빌드, 테스트, 배포 등의 태스크를 자동화할 수 있는 오픈소스 자동화 서버.

대표적인 **CI(Continuous Integration)** 툴 중의 하나.

정기적인 빌드에서 나아가 Git과 연동하여 커밋을 감지하면 자동적으로 테스트가 포함된 빌드가 작동하도록 설정할 수 있다.

#### Jenkins 설치

```bash
sudo apt install openjdk-8-jre # java 설치
sudo wget -q -O - https://pkg.jenkins.io/debian/jenkins-ci.org.key | sudo apt-key add - # repository key 추가
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
sudo apt-get install jenkins # jenkins 설치
```

cloud에서 기본포트인 8080을 열어주거나 포트를 아래와 같이 변경해야 한다.

```bash
sudo vi /etc/default/jenkins

HTTP_PORT = 8080
```

웹에서 ip주소:(jenkins 포트)에 접속하면 jenkins에 접속할 수 있다.

![image-20201101204702892](C:\Users\pjy20\AppData\Roaming\Typora\typora-user-images\image-20201101204702892.png)

(현재는 로그인된 상태)

adminPassword를 입력하고 유저를 생성한 뒤 로그인할 수 있다.

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```



#### 플러그인 설치

Jenkins는 각 서비스와 연동할 수 있는 플러그인을 제공한다.

[Jenkins 관리] - [플러그인 관리]를 들어가 필요한 플러그인을 설치한다.

Nodejs Plugin, Public Over SSH Plugin을 설치했다.

![image-20201101205204652](C:\Users\pjy20\AppData\Roaming\Typora\typora-user-images\image-20201101205204652.png)

![image-20201101205224801](C:\Users\pjy20\AppData\Roaming\Typora\typora-user-images\image-20201101205224801.png)



#### 프로젝트 생성

[새로운 item]을 통해 프로젝트를 생성한다.

Freestyle Project를 클릭
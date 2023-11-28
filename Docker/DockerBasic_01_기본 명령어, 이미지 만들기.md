Date: 2023.11.08
>Udemy의 [초보자를 위한 Docker 실습 - 데브옵스(DevOps)](https://www.udemy.com/course/docker-hands-on-devops/) 강의 내용 정리
## Docker 란?
- 리눅스(Linux) **컨테이너** 기반의 오픈소스 가상화 플랫폼으로, 컨테이너는 각자의 의존성(dependency)에 따라 라이브러리, 시스템 도구 등등 소프트웨어를 실행하는데 필요한 모든 것이 포함되어 있다.
- Docker를 사용하면 환경에 구애받지 않고 애플리케이션을 실행할 수 있다.

<details>
<summary>💡심화과정 - Docker 가상화에 대해</summary>
<ul>
	<li>Linux 계열의 운영체제들은 "Kernel + Softwere"로 이루어져 있다.</li>
	<ul>
		<li>Kernel 은 하드웨어와 상호작용하는 역할을 한다.</li>
		<li>Softwere에 따라 ubuntu, centos, debian 등등 다양한 운영체제로 나뉘게 된다.</li>
	</ul>
	<li>Docker는 docker host 기반으로 커널을 공유해 애플리케이션을 컨테이너화해서 실행하기 때문에 운영체제의 가상화를 필요로 하지 않는다.</li>
	<ul>
		<li>Docker host와 같이 단일 컨트롤 호스트 상에서 여러 컨테이너를 실행하는 시스템 레벨의 가상화 방법을 <strong>LXC(LinuX Containers)</strong>라고 한다.</li>
	</ul>
	<li>Window의 경우 호스트 위에 Hypervisor 가 실행되어 가상 머신을 만드는 방법으로 머신은 운영 체제의 가상화를 필요로하며 하드웨어 자원을 나눠서 할당 받는다.</li>
	<li>컨테이너 기반의 가상화는 가상 머신에 비해 더 적은 리소스를 사용하며 실행 속도가 빠르다.</li>
	<li>필요에 따라 가상 머신과 컨테이너를 조합해 활용한다.</li>
</ul>
</details>

## Docker 의 기본적인 사용방법
1. Dockerfile 작성
	- `Dockerfile` 안에 운영체제, 라이브러리 등등 애플리케이션 실행을 위해 필요한 설정 및 명령어를 기술한다.
2. `Dockerfile`로 image를 생성한다.
3. Image를 기반으로 컨테이너를 생성한다.
4. [Dockerhub](https://hub.docker.com/)에 사용자들이 미리 만들어 놓은 이미지들이 있으며 소프트웨어들의 공식버전도 존재하니 직접 만들기 전에 찾아보자.

## Docker 기본 명령어
- 컨테이너 생성 및 실행: `docker run [이미지명]`
	- 해당 이미지가 없다면 도커허브에서 이미지를 내려받은 후 컨테이너를 실행한다.
	- 컨테이너는 호스팅의 목적이 아닌 프로세스의 실행을 목적으로 하기 때문에 프로세스가 종료되면 컨테이너도 자동으로 종료된다. (운영 체제 기본 이미지 컨테이너를 실행하면 프로세스가 없기 때문에 컨테이너 생성 후 바로 종료되는 것을 확인할 수 있다.)
	- `-d` 옵션을 통해 백그라운드에서 실행시킬 수 있다.
	- 백그라운드에서 실행중인 컨테이너에 다시 연결하기 위해선 `docker attach [컨테이너ID]` 명령어를 사용한다.
	- `-i` 옵션을 사용해 컨테이너와 상호작용 할 수 있다. 옵션을 주지 않으면 컨테이너는 사용자의 입력을 받지 않는다.
	- `-t` 옵션을 사용해 컨테이너의 터미널에 연결 할 수 있다.
	- `-p` 컨테이너에 접근할 수 있도록 도커호스트의 포트를 컨테이너 포트에 포워딩 해주는 옵션이다.
		- ex) `docker run -p 80:5000 sample-webapp` -> "도커호스트IP:80" 으로 접속 시 컨테이너로 포워딩됨
	- `-v`옵션을 사용해 외부 디렉토리를 컨테이너와 연결해 삭제 이후에도 데이터를 유지 할 수 있다.
		- ex) `docker run -v /user/my/data:/opt/data mysql`
	- `-e` 옵션을 사용하면 컨테이너를 생성하며 환경변수를 전달할 수 있다.
		- ex) `docker run -e APP_COLOR=blue simple-webapp-color`
- 컨테이너 목록 확인: `docker ps`
- 컨테이너 종료: `docker stop [컨테이너명 or 컨테이너ID]`
- 컨테이너 삭제: `docker rm [컨테이너명 or 컨테이너ID]`
- 이미지 목록 확인: `docker images`
- 이미지 삭제: `docker rmi [이미지명 or 이미지ID]`
	- 이미지 삭제를 위해서는 해당 이미지로 생성된 모든 컨테이너가 없어야(삭제된 상태여야) 한다.
- 이미지 다운로드: `docker pull [이미지명]`
- 컨테이너에 특정 동작 실행하기: `docker exec [컨테이너명] [동작명령어]`
	- ex) `docker exec my_container cat /etc/hosts`
- 컨테이너 세부 정보 확인: `docker inspect [컨테이너명 or 컨테이너ID]`
	- 컨테이너의 내부 IP, 환경변수 등을 확인할 수 있다.
- 컨테이너 로그 확인: `docker logs [컨테이너명 or 컨테이너ID]`

## Docker image 생성하기 (`docker build`)
**Image를 만드는 과정**
1. `Dockerfile` 작성하기
	- `Dockerfile`에 작성할 내용 예시 - Flask 로 구현된 애플리케이션을 배포시 동작 순서
		1. 운영체제 선택(Ubuntu)
		2. 소스 레포지토리 업데이트
		3. 의존성(dependencies) 설치
		4. Python 모듈 설치 (pip)
		5. 소스코드 복사 (/opt/source-code)
		6. Flask 명령어를 사용해 웹 서버 가동

	- 예시 내용을 바탕으로 `Dockerfile`로 작성 ("명령어 + 인수" 형식)
		```Dockerfile
		# 1. 운영체제 선택
		FROM ubuntu
		# 2. 소스 레포지토리 업데이트 & 3. 의존성 설치
		RUN apt-get update && apt-get -y install python
		# 4. Python 모듈 설치
		RUN pip install flask flask-mysql
		# 5. 소스코드 복사
		COPY . /opt/source-code
		# 6. Flask 웹 서버 가동
		ENTRYPOINT FLASK_APP=/opt/source-code/app.py flask run
		```
2. Image 생성: `docker build . -t [이미지명=레포지토리]`
	- 현재 디렉토리를 이름으로 하여 이미지가 생성된다.
3. (선택사항) Dokerhub에 이미지 올리기
	1. Dockerhub에 이미지를 올리기 위해서는 도커로부터 인정 받은 공식 레포지토리가 아닌이상 태그를 붙여 이미지를 생성해야 한다.  ex) `docker build . -t [레포지토리]:[태그명]` 
	2. 도커허브에 로그인하기: `docker login`
	3. 이미지 올리기: `docker push [레포지토리]:[태그명]`

**Image의 동작원리**
- `Dockerfile`에 기술된 명령어에 따라 순차적으로 layer을 쌓아가는 방식이다.
- 단계별로 캐시에 저장하기 때문에 중간에 오류가 발생해 멈추거나 소스 코드 업데이트시, 오류가 나거나 변경된 계층부터 다시 실행되기 때문에 작업속도의 이점이 있다.
- 이미지의 상세 정보 확인: `docker history [이미지명]`
	- Layer 별 크기 등을 확인할 수 있다.

Date: 2023.11.09
>Udemy의 [초보자를 위한 Docker 실습 - 데브옵스(DevOps)](https://www.udemy.com/course/docker-hands-on-devops/) 강의 내용 정리

#### Container에 명령하기(CMD)와  진입점(ENTRYPOINT)
**Container에 명령하기**
- Container에 원하는 명령어를 내리기 위해서는 컨테이너를 생성할 때 명령어를 입력하는 방법과 `Dockerfile`에 명령어를 기술하는 두가지 방법이 있다.
	- 생성할 때 원하는 명령어를 입력 예시:  `docker run ubuntu sleep 5`
	- `Dockerfile`에 명령어 작성 예시
		```Dockerfile
		FROM ubuntu
		# 명령어 작성
		CMD sleep 5
		# 명령어는 JSON 형태로 작성할 수도 있다.
		# CMD ["sleep", "5"]
		```
	- `docker run` 할 때 명령어를 함께 입력하게 되면 `Dockerfile`에 명령어를 무시하고 생성 시 입력한 명령어를 수행한다.
- 위의 두 경우에는 명령어 사용을 위해서는 container를 생성하거나 명령어의 파라미터를 수정하고 싶은 경우, 명령어와 파라미터를 항상 다시 입력해줘야 한다.

**진입점(Entrypoint)**
- Container 생성시 사용자의 입력 또는 동작이 개입 가능하도록 진입점을 만들 수 있다.
	```Dockerfile
	FROM ubuntu
	# 진입점과 명령어를 동시에 작성하면 sleep 명령에 대한 파라미터의 기본값으 5를 가지며,
	# 사용자 입력이 있을 경우 5를 무시하고 사용자 입력값을 파라미터로 취한다.
	ENTRYPOINT ["sleep"] # 파라미터를 한 번에 작성하는 경우 변경이 불가능해짐
	CMD ["5"]
	```
- `Dockerfile`의 진입점(entrypoint)에 명령어를 작성한 경우 CMD와 명령어를 변경 할 수 없으며, 추가적인 파라미터 전달만 가능하다.
- 진입점(Entrypoint)에 명령어만 작성하고, 파라미터에 대한 내용을 작성하지 않고 도커 생성시에도 전달하지 않는 경우 에러가 발생한다.
- `--entrypoint` 옵션으로 `Dockerfile`의 진입점을 무시하고 새롭게 설정할 수 있음
	- 예시) `docker run --entrypoint=="cat" ubuntu /etc/hostname`
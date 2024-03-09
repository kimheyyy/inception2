# 'all' 타겟은 프로젝트를 초기화하고, Docker 컨테이너를 빌드 및 실행합니다.
all:
# WordPress 데이터를 저장할 디렉토리 생성
		sudo mkdir -p /home/hwankim/data/wordpress 
# 데이터베이스 데이터를 저장할 디렉토리 생성
		sudo mkdir -p /home/hwankim/data/database
 # /etc/hosts 파일에 대한 권한 변경	 
		sudo chmod 777 /etc/hosts
# 로컬 DNS( 도메인 이름을 IP 주소의 매핑과 관련된 정보)에 hwankim.42.fr - 127.0.0.1을 연결
		echo "127.0.0.1 hwankim.42.fr" >> /etc/hosts 
 # Docker Compose를 사용하여 컨테이너 빌드 및 백그라운드에서 실행
		sudo docker-compose -f srcs/docker-compose.yml up --build -d

# 'up' 타겟은 Docker 컨테이너를 빌드 및 실행합니다. 'all' 타겟과 유사하지만, 데이터 디렉토리 생성은 포함하지 않습니다.
up:
		sudo docker-compose -f srcs/docker-compose.yml up --build -d # Docker Compose를 사용하여 컨테이너 빌드 및 백그라운드에서 실행

# 'fclean' 타겟은 모든 Docker 컨테이너, 이미지, 볼륨을 정리합니다.
fclean:
		sudo docker-compose -f srcs/docker-compose.yml down --rmi all --volumes # Docker Compose를 사용하여 모든 컨테이너를 중지하고, 이미지 및 볼륨 삭제
		if [ -n "$(sudo docker images -q debian:buster)" ]; then sudo docker rmi debian:buster; fi # debian:buster 이미지가 있으면 삭제
		sudo rm -rf /home/hwankim/data # 데이터 디렉토리 삭제

.PHONY:	all up fclean # Make가 파일 이름으로 인식하지 않도록 .PHONY를 사용하여 가짜 타겟을 선언
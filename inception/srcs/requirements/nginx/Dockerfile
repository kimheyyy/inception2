# 베이스 이미지 가져오기
FROM debian:buster

# 패키지 목록 업데이트 및 패키지들 최신버전으로 nginx설치 및 openssl설치
RUN     apt-get update -y
RUN     apt-get upgrade -y
RUN     apt-get install -y nginx
RUN     apt-get install -y openssl

# 로컬시스템의 파일 및 디렉토리를 이미지로 이동
COPY    conf/default /
RUN     mv default /etc/nginx/sites-available/default
# 개인키 생성 -> CSR생성 -> 새로운 인증서 생성 -> 각 요소들 이동
RUN     openssl genrsa -out server.key 4096
RUN     openssl req -new -key server.key -subj "/C=KR/ST=Seoul/O=42Seoul/OU=GAM" -out server.csr
RUN     openssl req -x509 -in server.csr -key server.key -out server.crt
RUN     mv server.crt /etc/ssl/certs/
RUN     mv server.csr server.key /etc/ssl/private
# 443 포트로 노출
EXPOSE 443

# 컨테이너로 올라갈때 실행하는 명령어 nginx 를 포그라운드 모드로 실행
ENTRYPOINT     ["nginx", "-g", "daemon off;"]


# 명령어 가이드 #
# RUN: 이미지를 빌드 할때 쉘 명령어를 실행
# COPY: 로컬시스템의 파일 및 디렉토리를 이미재 내부로 복사
# ENTRYPOINT: 컨테이너가 시작 될 떄 실행할 명령어를 설정 
# FROM: 베이스 이미지를 설정합니다. 이 이미지 위에 추가적인 설정이 적용됩니다.
# WORKDIR: 작업 디렉토리를 설정합니다. 이후의 RUN, CMD, ENTRYPOINT, COPY, ADD 명령어들이 이 디렉토리 내에서 실행됩니다.
# ENV: 환경 변수를 설정합니다. 이 환경 변수는 이미지 내에서 사용될 수 있습니다.
# ADD: COPY와 비슷하지만, 로컬의 tar 파일을 추가하면 자동으로 압축을 해제합니다. 또한 URL을 통해 원격 파일을 추가할 수 있습니다.
# CMD: 컨테이너가 시작될 때 실행할 기본 명령어를 설정합니다. ENTRYPOINT와 함께 사용되며, ENTRYPOINT에 의해 오버라이드 될 수 있습니다.
# EXPOSE: 컨테이너에서 열어둘 네트워크 포트를 지정합니다.
# VOLUME: 호스트와 공유할 디렉토리를 설정합니다. 이 디렉토리는 데이터를 저장하거나 공유하는 데 사용될 수 있습니다.
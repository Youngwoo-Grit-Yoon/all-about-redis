# Docker를 이용한 Redis 설치
## 1. Docker Hub에서 Redis 공식 이미지를 가져온다.
```text
$ docker pull redis
```
## 2. Redis 공식 홈페이지에서 redis.conf 샘플 파일을 가져온다.
https://redis.io/docs/management/config-file/
## 3. redis.conf 파일을 수정하여 외부 접속을 허용한다.
```text
# You will also need to set a password unless you explicitly disable protected
# mode.
# ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
# bind 127.0.0.1 -::1
bind 0.0.0.0
```
## 4. redis.conf 파일을 수정하여 패스워드를 설정할 수도 있다.
```text
# The requirepass is not compatible with aclfile option and the ACL LOAD
# command, these will cause requirepass to be ignored.
#
# requirepass foobared
```
## 5. redis.conf 파일을 수정하여 리스닝 포트를 수정할 수도 있다.
```text
# Accept connections on the specified port, default is 6379 (IANA #815344).
# If port 0 is specified Redis will not listen on a TCP socket.
port 6379
```
## 6. redis.conf 파일을 수정하여 보호 모드를 해제한다.
만약에 패스워드를 사용하지 않는다면, 하기와 같이 보호 모드를 해제하여 외부에서 접속할 수 있게 한다.
```text
# By default protected mode is enabled. You should disable it only if
# you are sure you want clients from other hosts to connect to Redis
# even if no authentication is configured.
# protected-mode yes
protected-mode no
```
## 7. Redis를 Docker 컨테이너로 배포한다.
```text
$ docker run -v /Users/youngwooyoon/YYW/Docker/redis:/usr/local/etc/redis \
-d \
-p 6379:6379 \
--name redis \
redis redis-server /usr/local/etc/redis/redis.conf
```

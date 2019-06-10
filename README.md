# 인수 인계

## 1. 도커 파일 생성

- Dockerfile 생성

## 2. 스크립트 작성

```
FROM centos:6

USER root

RUN yum update -y
RUN yum install -y wget

RUN yum install -y epel-release
RUN yum install -y gcc libxml2-devel openssl-devel libcurl-devel libjpeg-devel libpng-devel php-mcrypt libmcrypt-devel

RUN yum install -y http://opensource.wandisco.com/centos/6/git/x86_64/wandisco-git-release-6-1.noarch.rpm
RUN yum install -y git

RUN wget http://jp2.php.net/get/php-5.3.29.tar.gz/from/this/mirror

RUN mv mirror php-5.3.29.tar.gz

RUN tar -xvf php-5.3.29.tar.gz

RUN cd ./php-5.3.29 && ./configure --prefix=/usr/local/php55 --bindir=/usr/bin  --disable-debug --enable-sigchild --enable-inline-optimization --enable-sysvsem --enable-sysvshm --enable-bcmath --enable-ftp --enable-sockets --enable-exif --enable-soap --with-zlib-dir=/usr --with-zlib --with-gd --with-jpeg-dir=/usr --with-png-dir=/usr  --with-iconv --enable-mbstring --with-mcrypt --with-curl --with-openssl --enable-zip

RUN cd ./php-5.3.29 && make && make install

RUN rm -rf ./php-5.3.29.tar.gz ./php-5.3.29

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === '48e3236262b34d30969dca3c37281b3b4bbe3221bda826ac6a9a62d6444cdb0dcd0615698a5cbe587c3f0fe57a54d8f5') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php --install-dir=/usr/bin --filename=composer
RUN php -r "unlink('composer-setup.php');"

RUN yum install -y svn sshpass

RUN yum clean all
```

## 3. hub.docker.com

- 계정 생성
- github 연동
- Repository 생성 (github repository 연동)

## 4. build 확인

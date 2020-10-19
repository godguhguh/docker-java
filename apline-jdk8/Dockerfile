FROM alpine:3.10.2
MAINTAINER yanpp@nfky.com
ADD jdk-8u261-linux-x64.tar.gz /usr/local

##******************更换Alpine源为mirrors.ustc.edu.cn******************
RUN echo http://mirrors.ustc.edu.cn/alpine/v3.10/main > /etc/apk/repositories && \
    echo http://mirrors.ustc.edu.cn/alpine/v3.10/community >> /etc/apk/repositories
RUN apk update && apk upgrade

##******************Alpine安装 Glibc https://github.com/sgerrand/alpine-pkg-glibc *****************
RUN apk --no-cache add ca-certificates wget \
    && wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub \
    && apk add glibc-2.29-r0.apk glibc-bin-2.29-r0.apk glibc-i18n-2.29-r0.apk \
    && rm -rf /var/cache/apk/* glibc-2.29-r0.apk glibc-bin-2.29-r0.apk glibc-i18n-2.29-r0.apk

RUN apk update \
    && apk add tzdata \
    && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone

ENV JAVA_HOME=/usr/local/jdk1.8.0_261
ENV CLASSPATH=$JAVA_HOME/bin
ENV PATH=.:$JAVA_HOME/bin:$PATH
CMD ["java","-version"]
# alpine linux with swagger-ui
FROM youske/alpine-nodejs:latest
MAINTAINER youske miyakoshi <youske@gmail.com>

ENV PORT=8080 \
    WORKER_CONNECTION=512 \
    WORKER_RLIMIT_NOFILE=8192 \
    CHARSET=ja_JP.UTF-8 \
    WORKDIR=/swaggerwork

ENV PACKAGE='nginx git ' \
    BUILDPACKAGE="build-base musl-dev nodejs-dev python-dev linux-headers"

WORKDIR /
USER root

# swagger-ui dependencies package install
RUN apk add ${PACKAGE} --no-cache && apk add ${BUILDPACKAGE} --no-cache -t buildpackage

COPY nginx.conf.tmpl /etc/nginx/nginx.conf.tmpl

RUN git clone https://github.com/swagger-api/swagger-ui.git && \
    cd swagger-ui && \
#    npm install && npm run build && \
    cp -r ./dist/* /usr/share/nginx/html

RUN apk del buildpackage --no-cache && rm -rf /tmp/* /var/cache/apk/*

EXPOSE ${PORT}

#USER admin
#WORKDIR /home/admin
ENTRYPOINT ["render","/etc/nginx/nginx.conf", "--", "switch","shell=/bin/bash","--","nginx"]

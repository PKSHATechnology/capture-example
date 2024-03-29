FROM debian:buster-slim

RUN apt-get update
RUN apt-get install -y build-essential libpcre3 libpcre3-dev libssl-dev
RUN apt-get install -y ffmpeg
RUN apt-get install -y curl vim glances
RUN curl -OL https://nginx.org/download/nginx-1.25.2.tar.gz
RUN tar -zxf nginx-1.25.2.tar.gz

RUN curl -OL "https://github.com/sergey-dryabzhinsky/nginx-rtmp-module/archive/dev.tar.gz"
RUN tar -xvz -f "dev.tar.gz" && \
    cd nginx-1.25.2 && \
    ./configure \
        --prefix=/usr/local/nginx \
        --conf-path=/usr/local/nginx/conf/nginx.conf \
        --without-http_gzip_module \
        --with-http_ssl_module \
        --with-http_v2_module \
        --with-debug \
        --with-threads \
        --with-ipv6 \
        --add-module=../nginx-rtmp-module-dev && \
    make -j$(nproc) && \
    make install

RUN rm -rf /var/lib/apt/lists/*
RUN mv /nginx-rtmp-module-dev/stat.xsl /usr/local/nginx/html/stat.xsl

ADD nginx.conf /usr/local/nginx/conf/nginx.conf

STOPSIGNAL SIGQUIT

CMD [ "/usr/local/nginx/sbin/nginx", "-g", "daemon off;" ]

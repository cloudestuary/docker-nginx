FROM nginx:mainline

RUN apt-get update && apt-get install -y wget

ENV DOCKERIZE_VERSION v0.3.0
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz

ADD conf/default.tmpl /opt/default.tmpl

RUN echo "daemon off;" >> /etc/nginx/nginx.conf

CMD envsubst '$$DOCUMENT_ROOT $$INDEX_FILE $$CLIENT_MAX_BODY_SIZE $$PHP_FPM' < /opt/default.tmpl > /etc/nginx/conf.d/default.conf && nginx
